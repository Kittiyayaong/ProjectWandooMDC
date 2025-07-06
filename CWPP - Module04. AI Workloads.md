# Module 4 - AI Workloads

## 목표
Microsoft Defender for Cloud에서 AI 워크로드 계획을 활성화하고 구성하는 방법을 안내하며, 환경에서 AI 워크로드를 보호하기 위해 Microsoft Defender for Cloud가 제공하는 가치를 입증하는 탈옥 공격을 시뮬레이션하는 데 도움이 됩니다. 

## ✅ 랩 사전준비
- Azure Subscription Owner 권한
- AI 워크로드 활성화 (MDC ➔ Environment settings ➔ AI workloads ➔ **ON**)
- Azure OpenAI 서비스 프로비저닝 완료
- Azure OpenAI에 모델 배포 완료 (예: gpt-35-turbo)

---

## Lab 1. AI 워크로드 활성화

1. MDC > Environment settings > relevant Azure subscription > AI workloads > ON으로 설정 > Save
   ![image](https://github.com/user-attachments/assets/31411a5d-25eb-4502-8c09-b9c58fdf8969)

2. AI 관련 알림을 더 깊이 분석하기 위해 사용자와 모델 간에 전달된 프롬프트를 노출하려면 'Settings'을 클릭하여 **Enable suspicious prompt evidence**를 **ON**으로 설정합니다.

   ![image](https://github.com/user-attachments/assets/b342dc7f-eb1d-48a9-9f6a-7137f06549e2)

   <img width="1435" alt="image" src="https://github.com/user-attachments/assets/b0a47600-9c31-4993-8c71-15232e6b5b82" />

> ⭐ Tips: <br>
> 자세한 전제 조건은 [document](https://learn.microsoft.com/en-us/azure/defender-for-cloud/ai-onboarding) 에서 확인할 수 있습니다.

Azure OpenAI 서비스를 프로비저닝하고 gpt-35-turbo 모델을 배포한다.

---

## Lab 2. Azure OpenAI 서비스를 프로비저닝하고 gpt-35-turbo 모델을 배포

**Step 1. Azure OpenAI Resource 생성**

1. **Azure Portal 접속**
2. 상단 검색창 ➔ **"Azure OpenAI"** 검색
3. **Azure OpenAI** ➔ Create

✅ **필수 입력값**
- Subscription: 본인 Subscription 선택
- Resource Group: 기존 혹은 새로 생성
- Region: East US (Azure OpenAI 지원 리전)
- Name: 고유 이름 (예: my-openai-lab)
- Pricing tier: Standard S0

4. **Review + Create** ➔ **Create**

## **Step 2. Deployment (모델 배포)**

1. **Resource 생성 완료 후 ➔ Overview 탭**
2. 왼쪽 메뉴 ➔ **Deployments**
3. ➔ + Create

✅ **필수 입력값**
- Model: `gpt-35-turbo` (또는 lab 가이드 지정 모델)
- Deployment name: (예: gpt35turbo)

4. ➔ **Create**

---

## 📝 **Step 3. Access 확인**

1. 왼쪽 메뉴 ➔ **Keys and Endpoint**
2. ➔ Endpoint URL 및 Key 복사  
   ➔ 이후 Chat Playground, API 호출 시 사용

---

## 📝 **Step 4. Chat Playground 테스트 (Optional)**

1. Azure OpenAI Studio ➔ **Chat Playground**
2. **Deployment 선택** ➔ gpt-35-turbo
3. Prompt 입력 후 응답 확인

---

## ⚠️ **Notes**
- ✅ **Windows, macOS, Linux 모두 동일**
- 단, **Azure CLI로 배포** 시는 로컬 CLI 환경에 따라 명령어 실행 방법이 조금 다름. (PowerShell vs zsh/bash)  
  ➔ 현재 과정은 **Portal 기반**이므로 동일

---

## Lab 3. Azure OpenAI Chat Playground 테스트**

1. Azure Portal ➔ Azure OpenAI 접속  
2. **Deployments**에서 gpt-35-turbo 모델 배포 상태 확인  
3. **Chat Playground** 실행

✅ **Test Prompt**

### 🔗 [다음 Lab으로 이동하기 Windows »](https://github.com/Kittiyayaong/ProjectWandooMDC/blob/main/CWPP%20-%20Module04.%20AI%20Workloads.md)
