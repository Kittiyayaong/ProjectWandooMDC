# Module 9 - Azure Policy Lab

# 🎯 **목표**
Azure Policy를 활용해 조직의 클라우드 리소스 거버넌스를 강화한다.  
특히,
* ✔**Allowed Locations 정책** ➔ **배포 지역 규정 준수(Data Residency Compliance)**
* **Owner 태그 정책** ➔ **비용 책임 관리(Chargeback), 운영 거버넌스**

을 동시에 구현한다.

## ✅ **전제 조건**
- Azure Subscription Owner/Contributor 권한
- Azure Policy Resource Provider 등록 완료

## 📌 **시나리오 배경**

### 🎯 **조직 요구사항**

> ✅ **보안 & 컴플라이언스 팀 요구**
> - 모든 리소스는 **Korea Central 지역**에만 배포해야 한다. (데이터 주권 준수)

> ✅ **IT 운영 & 재무팀 요구**
> - **Owner 태그가 없는 리소스는 비용 책임자가 불명확**하여 Chargeback(비용 배분 청구) 불가 ➔ **Owner 태그 필수화** 필요.

---

## **Lab 1. Built-in Policy 할당**

1. Azure Portal 접속 > **Policy** 클릭 > Authoring > Definitions 클릭 > **“Allowed locations”** 정책 선택 > 정책 할당 (Assign policy) 클릭
2. 정보 기입 후 생성

* Policy 설정: Allowed locations ➔ Korea Central
* Scope: 내 Azure Subscription 전체 (또는 특정 Resource Group)
* ✔️ 즉, Allowed locations 정책은 “지정된 지역 외 배포는 허용하지 않음” 정책으로, Scope 안의 리소스 배포 위치를 모니터링하고 허용된 지역 외에는 Non-compliant으로 평가 합니다.

    <img width="903" alt="image" src="https://github.com/user-attachments/assets/a1c42c8a-3606-4d91-ada3-905b691ac9ac" />
   <img width="1180" alt="스크린샷 2025-07-06 오후 4 19 20" src="https://github.com/user-attachments/assets/c6052125-5746-4ab7-b236-66e0db9357ed" />

| 상황                                                                     | 결과                                                                        |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| **내가 VM, Storage 계정, Key Vault 등 Azure 리소스를 Korea Central에 배포**        | ✔️ **Compliant (정책 준수)**                                                  |
| **내가 Japan East, East US, Southeast Asia 같은 Korea Central 이외의 리전에 배포** | ❌ **Non-compliant (정책 위반)**<br>Policy Compliance에서 Non-compliant 리소스로 표시됨 |

3. Review + Create ➔ **Create**

✅ **결과**
- 지정된 Scope 내 리소스 배포가 **Korea Central 이외 지역일 경우 Non-compliant** 로 평가됨

---

## **Lab 2. 정책 평가 및 Remediation**
Azure Policy를 할당한 뒤, 실제 리소스들이 정책을 준수하고 있는지(Compliant), 아니면 위반 중인지(Non-compliant) 를 평가/확인하는 단계입니다.

1. Compliance 확인
   1. Policy 메뉴 ➔ **Compliance**
   2. 방금 할당한 **Allowed locations 정책** 확인
   3. Non-compliant 리소스가 있으면 표시됨

    <img width="1434" alt="image" src="https://github.com/user-attachments/assets/1409e364-1c86-477c-8d4d-3aa65041a8ee" />

---

## **Lab 3. Owner Tag Custom Policy 정의 ➔ Assignment ➔ Remediation**

### **1. Custom Policy 정의**

1. Policy ➔ **Definitions ➔ + Policy definition**
2. 아래 정보 입력:

| 항목 | 값 |
|--|--|
| **Definition location** | Subscription |
| **Name** | Enforce tag: Owner |
| **Description** | 모든 리소스에 Owner 태그 필수 |
| **Category** | Tags |


### **2. Policy Rule 작성**

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
```

### 🔗 [다음 Lab으로 이동하기 »](https://github.com/Kittiyayaong/ProjectWandooMDC/blob/main/CWPP%20-%20Module01.%20Agentless%20container%20vulnerability%20assessment%20scanning.md)
