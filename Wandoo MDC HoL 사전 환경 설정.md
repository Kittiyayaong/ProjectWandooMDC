# Wandoo MDC HoL 사전 환경 설정 

#### 전제 조건
이 실험을 시작하기 전에 다음과 같은 전제 조건이 있는지 확인하세요:
- **지원되는 웹 브라우저** (Microsoft Edge, Google Chrome, Safari, Firefox Mozilla)
- 이러한 실험실을 사용할 때는 **이미 사용 중인 기존 Azure 구독/환경과의 충돌을 방지하기 위해 기기에서 비밀/비공개 브라우저 세션**을 열고 Azure Portal에 로그인하는 것이 좋습니다.
- **Microsoft 계정** - 기존 계정이 없는 경우 무료 계정을 만들기 위해 가입하세요: https://signup.live.com

#### Azure Free trial Instruction:
1. 웹 브라우저에서 in-private 세션을 열고 [here](https://azure.microsoft.com/en-us/free)으로 이동합니다
2. 이 페이지의 주요 부분에서 **무료 시작**을 클릭하고 Microsoft 계정 자격 증명을 사용하여 Azure 포털에 로그인합니다.
중요 - 회사 사용자와 로그인하지 않았는지 확인합니다.
3. Microsoft 계정 이메일 주소를 입력한 다음 **다음**을 클릭합니다.
4. **로그인 유지** 메시지에서 **예**를 클릭합니다.
5. **Azure 무료 사용** 페이지에서 4단계(프로필, 전화 본인 확인, 카드 본인 확인, 동의)에 따라 세부 정보를 입력하세요. 모든 단계를 완료한 후 **가입** 버튼을 클릭하여 구독 생성 프로세스를 완료하세요.
6. **Azure**부터 시작할 준비가 되었습니다** 페이지에서 **포털**로 이동** 버튼을 클릭하세요. 이제 소유자 권한을 포함하여 **Azure 구독 1**이라는 이름의 Azure 구독이 있어야 합니다.

### Lab 2: 리소스 프로비저닝

> ❗ Important: <br>
> 동일하게 In-private 창에서 MDC에 엑세스해야합니다.

이 실험 가이드에서 언급된 연습의 일환으로, ARM 템플릿을 기반으로 한 자동 배포 환경을 조성할 것입니다.
ARM 템플릿은 프로젝트의 인프라와 구성을 정의하는 JavaScript Object Notation(JSON) 파일입니다. 이 템플릿은 선언 구문을 사용하여 프로그래밍 명령어 시퀀스를 작성하지 않고도 배포하려는 내용을 명시할 수 있습니다.
다음 리소스 목록은 프로비저닝 과정에서 배포될 예정입니다(디스크, 네트워크 인터페이스, 공용 IP 주소 등과 같은 종속성 포함):

Name | Resource Type | Purpose
-----| ------------- | -------
asclab-win | Virtual machine | Windows Server
asclab-linux | Virtual machine | Linux Server
asclab-as | Availability set | Availability set for the 2-VMs
asclab-aks | Kubernetes service | Testing container services capabilities
asclab-app-[uniqestring] | App Service | App service to be used for web app, function app
asclab-sql-[uniqestring] | SQL server | To be using for the sample database
asclab-as | SQL database | Sample database based on AdventureWorks template
asclab-kv-[uniqestring] | Key vault | Demonstrating Key Vault related recommendations and security alerts
asclab-fa-[uniqestring] | Function App | Demonstrating related built-in and custom security recommendations
asclab-la-[uniqestring]	| Log Analytics workspace | Log Analytics workspace used for data collection and analysis, storing logs and continuous export data
asclab-nsg | Network security group | Required for Just-in-Time access and security recommendations
asclab-splan | App Service plan | Demonstrating related security recommendations
asclab-vnet | Virtual network | Default virtual network for both Azure VM and for network related recommendations
asclabcr[uniqestring] | Container registry | Demonstrating related security recommendations
asclabsa[uniqestring] | Storage account | Demonstrating related security recommendations
SecurityCenterFree | Solution | Default workspace solution used for Microsoft Defender for Cloud free tier

1. 아래의 파란색 **Azure에 배포** 버튼을 클릭하여 실험실 환경을 준비하세요:

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Security-Center%2Fmaster%2FLabs%2FFiles%2Flabdeploy.json" target="_blank"><img src="https://aka.ms/deploytoazurebutton"/></a>

2. Azure Portal > custom deployment 리디렉션되며, 배포를 위해 필수 필드를 지정해야 합니다.
   * Subscription은 테스트 대상 Subscription을 선택합니다.
   * Resource group: 새로만들기 (Create new)를 클릭하여 **Wandoo_MDC_tes**로 생성합니다.
   * Parameter: 현 위치에서 가장 가까운 DC **region**을 선택합니다.
   * Password: 서비스 전반에서 사용할 비밀번호(예: 가상 머신 및 SQL 데이터베이스의 자격 증명) 선택
     > ❗ Important: <br>
     > 비밀번호는 12자에서 72자 사이여야 하며, 소문자 1개, 소문자 1개, 숫자 1개, 특수 문자 1개 중 3개를 사용해야 합니다. 그렇게 하지 않으면 배포에 실패하게 됩니다.

3. **Review + create**로 생성을 완료합니다. 10분정도 소요됩니다.
  > ⭐ Tips: <br>
  > *배포가 진행 중입니다* 페이지는 배포가 성공했다고 가정하여 환경에 업로드되는 리소스를 계속 업데이트하고 표시합니다.
배포하는 동안 Kubernetes 리소스에 대한 추가 리소스 그룹이 자동으로 생성됩니다.<br>

