# Module 6 – Integration with Microsoft Defender for Endpoint

### Lab 1: Microsoft Defender for Endpoint의 자동 배포 및 통합 활성화

> ⭐ Tips: <br>
> * [서버용 Defender Plan 1 및 Plan 2](https://learn.microsoft.com/en-gb/azure/defender-for-cloud/plan-defender-for-servers-select-plan) 에는 [Microsoft Defender for Endpoint](https://www.microsoft.com/microsoft-365/security/endpoint-defender) 에 대한 통합 및 라이선스 커버리지가 포함되어 있습니다. 이들은 [Microsoft Defender Vulnerability Management](https://learn.microsoft.com/en-gb/azure/defender-for-cloud/deploy-vulnerability-assessment-defender-vulnerability-management) 을 활용하여 종합적인 엔드포인트 탐지 및 응답(EDR) 기능, 소프트웨어 인벤토리 및 취약점 평가를 제공합니다.
Defender for Endpoint는 위협을 감지하자마자 Microsoft Defender for Cloud와 Microsoft 365 Defender에 표시되는 보안 경고를 트리거합니다. Microsoft Defender for Cloud에서 Defender for Endpoint 콘솔로 이동하여 자세한 조사를 수행하여 공격 범위를 파악할 수도 있습니다.
> * 두 개의 서버용 Defender 요금제 중 하나를 활성화하면 Microsoft Defender for Endpoint 및 Microsoft Defender 취약성 관리와의 통합이 기본적으로 활성화됩니다.

1. MDC > Environment settings > 하단에 테스트 대상 subscription > Servers > Setting > **Endpoint protection**과 **Vulnerability assessment for machines** 모두 **On**으로 설정합니다.
   [image](https://github.com/user-attachments/assets/8889989c-0eb9-4bea-b69a-0a112772cce5)

2. Save

> ⭐ Tips: <br>
> * Microsoft Defender for Endpoint와의 통합을 활성화하면 Microsoft Defender for Cloud는 Windows 및 Linux Azure VM과 Azure Arc 지원 서버를 실행하는 비Azure 머신에 MDE.Windows 및 MDE.Linux 확장을 자동으로 배포합니다. 확장이 배포되는 즉시 온보딩 패키지가 머신을 분석하고, Defender for Endpoint를 감지하고 Microsoft Defender for Cloud와 통합되도록 재구성합니다.

> ⭐ Tips: <br>
> MDE 에이전트의 온보딩은 한 시간 이내에 시작지만, **Machines should have vulnerability findings resolved** 권장 사항에 취약점 평가 결과가 표시되기까지 최대 12시간이 소요될 수 있습니다. 


### Lab 2: Direct 온보딩을 통해 on-premises server를 연결

Lab 1의 온보딩 시나리오에서는 Defender for Cloud의 백엔드 프로세스가 Microsoft Defender for Endpoint를 non-Azure 컴퓨터에 배포할 수 있도록 Azure Arc를 먼저 설치해야 하지만, Defender for Cloud는 Defender for Endpoint의 백엔드 서버를 감지하여 두 서비스 간의 백엔드 통합을 통해 Defender for Cloud에 연결할 수 있는 또 다른 기능인 직접 온보딩을 제공합니다.

1. MDC > Environment settings > Direct onboarding 클릭
   ![image](https://github.com/user-attachments/assets/79c4b500-e056-4d59-94fd-484f67d3b61a)

2. Direct Onboarding **ON**으로 설정하고, 테스트 Subscription을 설정합니다.
   ![image](https://github.com/user-attachments/assets/62efaed5-a951-45e5-b1f3-ca1692dcac6e)

#### Lab 2-1. 지정된 구독에서 직접 온보딩을 활성화하기 전에 Defender for Servers가 아직 활성화되지 않은 경우 

Defender for Cloud는 이 구독에서 Defender for Servers Plan 1을 자동으로 활성화합니다. 다음 단계로 Defender for Cloud는 이제 [Defender for Endpoint backend](https://security.microsoft.com 의 모든 서버를 감지하여 Defender for Cloud에 연결합니다. 

1. Security.microsoft.com (Defender Console)에 로그인 > Settings > Endpoints > Device Management > Onboarding 를 통해서 진행합니다.
   ![image](https://github.com/user-attachments/assets/9dffc738-dfcf-476b-8e4c-42e679db289b)

3. 서버의 운영 체제를 선택하고 설치 지침을 따릅니다.

> ⭐ Tips: <br>
> 디바이스가 Microsoft Defender for Endpoint에 성공적으로 온보딩되는 즉시 Defender for Cloud에 연결됩니다. 이제 Defender for Cloud 및 Microsoft 365 Defender에서 보안 경고, 소프트웨어 인벤토리 및 취약점 평가 결과를 확인할 수 있습니다.

