# Module 2 – Onboarding Azure DevOps to Defender for Cloud

## 목표
이번 연습에서는 Azure DevOps 저장소를 Defender for Cloud에 연결하는 방법을 배우게 됩니다.

## Azure DevOps
Azure DevOps는 소프트웨어 개발, 배포, 그리고 협업을 위한 종합적인 도구와 서비스를 제공하는 플랫폼입니다. 이 플랫폼은 개발자, 프로젝트 관리자가 협력하여 소프트웨어를 개발하고, 더 빠르게 제품을 개선할 수 있도록 지원합니다

* 주요 기능
  * Azure Boards: 작업을 계획하고 추적하며, 팀 간의 협업을 돕는 Kanban 보드, 백로그, 그리고 강력한 계획 도구를 제공합니다
  * Azure Pipelines: 모든 언어와 플랫폼에서 CI/CD(지속적 통합 및 지속적 배포)를 지원하여, 코드를 빌드, 테스트, 배포할 수 있습니다
  * Azure Repos: 무제한의 클라우드 호스팅 프라이빗 Git 리포지토리를 제공하여, 코드 협업과 파일 관리를 지원합니다
  * Azure Test Plans: 수동 및 탐색적 테스트 도구를 사용하여, 코드 품질을 개선하고 자신 있게 배포할 수 있습니다
  * Azure Artifacts: 팀과 패키지를 생성, 호스팅, 공유하며, CI/CD 파이프라인에 아티팩트를 추가할 수 있습니다

### Lab 1: Onboarding an Azure DevOps Connector

1.	MDC > Environment settings > 왼쪽 상단에서 + Add environment > Azure DevOps >  **Create Azure DevOps connection** 아래 샘플과 같이 페이지가 나타납니다.
![image](https://github.com/user-attachments/assets/8ed8cce0-b635-4ded-aad0-54fca78513c2)

2. Account Detail에 대한 정보를 기입한 후, Next를 클릭해서 **Configure access**로 들어갑니다. **Authorize**를 클릭합니다. 
<img width="625" alt="image" src="https://github.com/user-attachments/assets/f85b2051-39ae-4dd3-be28-ac3643a1fbeb">

3.DevOps 연결을 처음 승인하는 경우, 승인 권한을 요청하는 팝업 화면이 표시됩니다. 팝업 창 화면을 아래로 스크롤하고 아래 샘플에 표시된 **Access** 버튼을 클릭합니다:
<img width="1040" alt="image" src="https://github.com/user-attachments/assets/1794e5b1-ddd9-4a7d-9be2-d3a6e3f6c537">

> ⭐ Tips: <br>
> Azure DevOps에서 **Access**를 클릭하면 **Microsoft Security DevOps** 앱에 대한 인증 증명을 확인할 수 있습니다. 이 인증은 Azure ADO 조직의 **개인 액세스 토큰** / **사용자 설정** / **Authorizatons** 아래에서 확인할 수 있습니다.

4. **Review and generate** 버튼 클릭하여 진행완료합니다. 

> ⭐ Tips: <br>
> 이 프로세스를 완료하려면 Azure DevOps 조직에서 **Project Collection Admin**가 되어야 합니다. 이 역할에 대해 자세히 알아보세요 [여기](https://learn.microsoft.com/en-us/azure/devops/organizations/settings/about-settings?view=azure-devops&WT.mc_id=Portal-Microsoft_Azure_Security_DevOps#project-collection-administrator-pca-role-and-managing-collections-of-projects)

5. 몇 분 후 **Environment Settings** 페이지에 Azure DevOps 커넥터가 표시되고 약 15분 후에는 총 리소스 수가 채워지는 것을 확인할 수 있습니다.


### (Optional) Lab 2: Microsoft Security DevOps Azure DevOps 확장 구성

1.	dev.auzre.com에서 생성한 DevOps 계정으로 로그인합니다.
  ![image](https://github.com/user-attachments/assets/e0287583-cca9-4919-8545-bb976390f54b)

2. Organization을 새로 생성합니다.
  ![image](https://github.com/user-attachments/assets/f97a6857-cae0-4396-8cd2-2f1eb8d9ae50)

3.	생성 완료 후, 우측 상단에서 shopping bag 아이콘을 선택 후 **Browse marketplace** 을 클릭합니다.
  ![image](https://github.com/user-attachments/assets/2d12d2a4-2302-499c-8956-d5d4f5707e67)

4. **Azure DevOps extension** 검색 후 클릭하여 Free로 설정합니다. 
  ![image](https://github.com/user-attachments/assets/caf6f0df-e0e3-47d9-a81b-d94dcf4396d3)

5.	Azure DevOps Organization 선택 후, Install합니다. 
  ![image](https://github.com/user-attachments/assets/167a9980-afac-43a5-9c35-3daa8fd1d46a)

6. 설치가 완료됩니다. 



### 🔗 [다음 Lab으로 이동하기 Windows »](https://github.com/Kittiyayaong/ProjectWandooMDC/blob/main/CWPP%20-%20Module03.%20(for%20windows)%20Protecting%20On-Prem%20Servers%20in%20Defender%20for%20Cloud.md)
### 🔗 [다음 Lab으로 이동하기 MAC »](https://github.com/Kittiyayaong/ProjectWandooMDC/blob/main/CWPP%20-%20Module03.%20(for%20MAC)%20Protecting%20On-Prem%20Servers%20in%20Defender%20for%20Cloud.md)
