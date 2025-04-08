# Module – Onboarding Azure DevOps to Defender for Cloud

## 목표
이번 연습에서는 Azure DevOps 저장소를 Defender for Cloud에 연결하는 방법을 배우게 됩니다.

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


