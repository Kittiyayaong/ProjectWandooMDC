# Module 6 - Data security posture management

## 목표
이 연습은 Microsoft Defender for Cloud에서 민감한 데이터 검색을 활성화하고 구성하는 방법을 안내하며, Defender CSPM 및 Defender for Storage 플랜에서 제공하는 추가 민감도 컨텍스트를 활용하는 다양한 방법을 보여줍니다.

## Lab 1: 민감한 데이터 검색 활성화

민감한 데이터 검색을 활성화하려면 특정 구독에서 Defender CSPM 또는 Defender for Storage 플랜을 활성화해야 합니다:

1. MDC > Environment settings > 하단에 테스트 대상 Subscription > Defender CSPM, Storage plan이 **ON**상태로 변경합니다.

> ⭐ Tips: <br>
> 민감한 데이터 검색을 실행할 수 있는 자세한 권한은 [document](https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-data-security-posture-prepare#whats-supported) 에 설명되어 있습니다.

> ⭐ Tips: <br>
> Storage plan만 활성화된 경우 민감한 데이터 검색은 이 Plan에서 지원하는 리소스에 대해서만 사용할 수 있습니다. Defender CSPM Plan을 활성화하면 데이터베이스 및 멀티클라우드 리소스를 포함하여 모든 지원되는 리소스가 Scanning에 포함됩니다.

2. Settings & monitoring에서 **Sensitive data discovery**도 **ON**상태로 변경합니다.
   ![image](https://github.com/user-attachments/assets/0615c179-c4b3-4831-bb8f-94d4b3dffd5a)

> ⭐ Tips: <br>
> Plan을 활성화한 후 처음 발견한 경우 결과를 확인하는 데 최대 24시간이 걸립니다.


## Lab 2: Configure sensitive data categories

1. MDC > Environment settings > Data sensitivity 를 클릭합니다. 
   ![image](https://github.com/user-attachments/assets/4fe7143e-858e-4a2b-a8b7-d257c33cf243)

2. **Other**를 클릭 후, **South Korea Resident Registration Number** 항목을 적용합니다. 
   ![image](https://github.com/user-attachments/assets/04c7fbf1-0673-48a9-ad83-660505418d3b)

> ⭐ Tips: <br>
> 기본적으로 **Other** 카테고리의 정보 유형은 민감한 데이터 검색에서 제외됩니다.



### 🔗 [다음 Lab으로 이동하기 »](https://github.com/Kittiyayaong/ProjectWandooMDC/blob/main/CSPM%20-%20Module07.%20EASM.md)

