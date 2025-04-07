# Module 01 - 01. Security Policy 

## 목표
이 연습에서는 현재 클라우드용 Microsoft Defender의 보안 정책을 안내합니다. 이러한 보안 정책은 클라우드 보안 태세를 개선하는 데 도움이 되는 보안 표준 및 권장 사항으로 구성되어 있습니다. 보안 표준은 [Microsoft 클라우드 보안 벤치마크(MCSB)](https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-regulatory-compliance), 규정 준수 표준 및 사용자 지정 표준으로 구성됩니다. 
이 연습을 마치면 예외, 정책 적용 및 사용자 지정 정책을 만드는 방법을 알 수 있습니다.  

#### 사전 요구 사항
클라우드용 Microsoft Defender를 시작하려면 Microsoft Azure를 구독해야 합니다. 

### Lab 1: Microsoft Defender for cloud 정책 개요

1. Portal.azure.com에 접속하여 microsoft defender for cloud를 검색하여 클릭합니다.
2. Microsoft Defender for cloud의 왼쪽 탐색 화면에서 **Management > Environment Settings**을 클릭합니다. 
3. 그런 다음 하단 Tenant 목록에서 **Subscription**을 선택하고 왼쪽 탐색에서 **Security Policies**을 선택합니다.
4. **Standards** 탭에서 MCSB 및 241 권장 사항을 확인할 수 있습니다. **Type**은 **Default**입니다. 

참고: MCSB는 Microsoft Defender for Cloud에 온보딩할 때 자동으로 할당됩니다(Default). 기본 할당에는 감사 정책만 포함되어 있습니다. 자세한 내용은 [Security policies in Defender for Cloud]([https://aka.ms/ascpolicies](https://learn.microsoft.com/en-us/azure/defender-for-cloud/security-policy-concept))을 참조하세요. MCSB는 Azure뿐만 아니라 멀티 클라우드 환경의 보안 권장 사항 및 모범 사례의 기준이 됩니다. 

4.	**Microsoft Cloud Security Benchmark**를 클릭합니다. **Effect**가 **Audit**임을 확인합니다. 클라우드용 Microsoft Defender가 사용자 환경을 평가하고 데이터를 감사합니다. 사용자의 승인 없이는 적용되지 않습니다.

### Lab 2: Azure Policy 살펴보
1.	Azure Portal에서 **Policy**를 검색한 후, **Authoring > Definitions**를 클릭합니다.
2.	관련 azure policy를 모두 확인 가능합니다.

### Lab 3: 권장 사항에 대한 리소스 면제 만들기
리소스 면제를 사용하면 특정 리소스를 평가에서 면제할 수 있는 기능을 제공하여 권장 사항을 더욱 세밀하게 조정할 수 있습니다. 

> ⭐ Tips: <br>
> 면제는 추가 비용 없이 MDC 이용 고객에게 제공되는 프리미엄 Azure 정책 기능입니다. 다른 사용자의 경우 향후 요금이 부과될 수 있습니다.

1. Azure Portal에서 Microsoft Defender for Cloud 검색 후 클릭
2. **Recommendation** 클릭 후 리스트의 recommendation 중 한개 클릭 
3. 상단이ㅡ **view recommendation for all resources** 클릭
![image](https://github.com/user-attachments/assets/973a7ebe-3723-4c72-98c4-7fe4cc71b9ba)

4. Affected resources에서 **사용자 or 디바이스(리소스)** 클릭 후 **Exempt** 클릭
![image](https://github.com/user-attachments/assets/523d67cc-7ec5-4a37-ad20-8cd4c39e10e4)

5. The create **exemption pane** opens:
   *	Exemption name: ACS - recommendation name 
*	**expiration date** 박스 클릭으로 활성화 후, Date 설정 

    - Exemption Category: **Waiver** 
    - Provide a description: **Testing exemption capability – module 1**.
    - **Save** 클릭으로 저장 
<img src="https://github.com/user-attachments/assets/3d90973d-0ab0-42ca-a356-64bbba4e1be5" alt="image" width="500" height="800">

> ⭐ Tips: <br>
*  **Mitigated** - 이 문제는 제안된 리소스와 다른 도구 또는 프로세스에서 처리되었으므로 리소스와 관련이 없습니다.
* **Waiver** - 이 리소스에 대한 위험을 수락합니다.
* 예외를 설정하면 이 추천 사항이 포함된 모든 관리 표준에 대해 예외가 생성됩니다. 이는 특정 추천 사항에 대해 예외를 설정할 때, 해당 추천 사항이 적용되는 모든 관리 표준에 대해 동일한 예외가 적용된다는 것을 의미합니다. 예를 들어, Azure CSPM 표준에 포함된 추천 사항에 대해 예외를 설정하면, Azure CSPM 표준의 모든 관련 부분에 대해 예외가 생성됩니다.

6. 설정을 적용되려면 최대 30분이 소요될 수 있습니다. 설정 이후에는 아래와 같은 효과가 나타납니다. 
    - 해당 리소스는 보안 점수에 영향을 미치지 않습니다.
    - 리소스가 권장 사항 세부 정보 페이지의 해당 없음 탭에 나열됩니다.
    - 추천 세부정보 페이지 상단의 정보 스트립에 면제된 리소스 수가 나열됩니다

7. 5번 step과 동일한 tab으로 이동 후 **Not Applicable resources** 탭을 열어 면제된 리소스를 검토합니다. 리소스를 이유/설명 값과 함께 확인할 수 있습니다.
8. Azure portal에서 **policy** 검색 후 클릭 > Authoring > Exemptions로 이동합니다. 새로 생성한 **Exemption**이 리스트에 포함된 것을 확인합니다.

### Lab 4: Create a custom recommendation - Create a custom initiative using KQL Query
