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
리소스 면제를 사용하면 특정 리소스를 평가에서 면제할 수 있는 기능을 제공하여 권장 사항을 더욱 세밀하게 조정할 수 있습니다. 권장 사항으로 작업할 때 오른쪽에 있는 줄임표 메뉴를 클릭한 다음 면제 만들기를 선택하여 면제를 만들 수 있습니다.

Tips. 면제는 추가 비용 없이 클라우드용 Microsoft Defender 고객에게 제공되는 프리미엄 Azure 정책 기능입니다. 다른 사용자의 경우 향후 요금이 부과될 수 있습니다.

1. Azure Portal에서 Microsoft Defender for Cloud 검색 후 클릭
2. **Recommendation** 클릭 후 리스트의 recommendation 중 한개 클릭 
3. 
