# Module 9 - Azure Policy Lab

## 🎯 **목표**
Azure Policy를 활용해 조직의 클라우드 리소스 규정 준수(Posture)를 관리하고, Built-in 및 Custom Policy를 할당/평가/Remediation하는 방법을 익힌다.

## ✅ **전제 조건**
- Azure Subscription Owner/Contributor 권한
- Azure Policy 리소스 Provider 등록 완료 상태 (기본적으로 활성화됨)

---

## **Lab 1. Built-in Policy 할당**

1. Azure Portal 접속 > **Policy** 클릭 >  Definitions 클릭 > Built-in 정책 목록을 확인
3. 예제: **“Allowed locations”** 정책 선택

---

### 🔷 **3. 정책 할당 (Assign)**

1. 상단 메뉴 ➔ **Assign**
2. Scope:
   - Subscription 또는 Resource Group 선택
3. Parameters:
   - Allowed locations ➔ 예: Korea Central
4. Review + Create ➔ **Create**

✅ **결과**
- 지정된 Scope 내 리소스 배포가 **Korea Central 이외 지역일 경우 Non-compliant** 로 평가됨

---

## 📝 **Lab 2. 정책 평가 및 Remediation**

### 🔷 **1. Compliance 확인**

1. Policy 메뉴 ➔ **Compliance**
2. 방금 할당한 **Allowed locations 정책** 확인
3. Non-compliant 리소스가 있으면 표시됨

---

### 🔷 **2. Remediation Task 생성**

1. Non-compliant 항목 클릭
2. 상단 ➔ **Create remediation task**
3. Remediation 실행 ➔ 정책에 따라 지원되지 않는 경우도 있음 (위 정책은 location 변경 불가)

---

## 📝 **Lab 3. Custom Policy 정의 ➔ Assignment ➔ Remediation**

### 🔷 **1. Custom Policy 정의**

1. **Definitions ➔ + Policy definition** 클릭
2. 아래 예시 정보 입력:

| 항목 | 값 |
|--|--|
| **Definition location** | Subscription 선택 |
| **Name** | Enforce tag: Owner |
| **Description** | 모든 리소스에 Owner 태그 필수 |
| **Category** | Tags |

---

### 🔷 **2. Policy Rule 작성**

```json
{
  "if": {
    "field": "[concat('tags[', parameters('tagName'), ']')]",
    "exists": "false"
  },
  "then": {
    "effect": "modify",
    "details": {
      "roleDefinitionIds": [
        "/providers/microsoft.authorization/roleDefinitions/<Contributor Role GUID>"
      ],
      "operations": [
        {
          "operation": "add",
          "field": "[concat('tags[', parameters('tagName'), ']')]",
          "value": "[parameters('tagValue')]"
        }
      ]
    }
  }
}
