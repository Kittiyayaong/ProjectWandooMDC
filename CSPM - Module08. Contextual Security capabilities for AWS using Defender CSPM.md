# Module 8 - Contextual Security capabilities for AWS using Defender CSPM  

### Lab 1: AWS 계정 만들기

먼저 AWS 계정 프로젝트를 만들어야 합니다.

1. [무료 AWS 만들기](https://portal.aws.amazon.com/billing/signup?refid=em_127222&redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation #/start/email)로 이동합니다 
2. **무료 계정 만들기**를 클릭합니다.
3. AWS의 지침을 따라 무료 계정을 만드세요.

### Lab 2: Microsoft Defender for Cloud에서 새 AWS 계정을 위한 AWS 커넥터 만들기

1. MDC > Environment Settings > Add environment > Amazon Web Services
   ![image](https://github.com/user-attachments/assets/cff5208a-02e0-46ca-bce6-cb171bf17913)

2. 설정값 입력하기 (AWS Account ID는 아래 이미지와 같이 확인 가능합니다.) 
   ![image](https://github.com/user-attachments/assets/73098e66-305d-473d-abd1-9ee5bd834600)

3. Defender CSPM, Servers, Container의 Database plans 모두 **On**으로 설정합니다. 
   ![image](https://github.com/user-attachments/assets/2bee9998-38d0-4e43-8739-c14c5086faca)

4. **Configure access**으로 이동합니다. CloudFormation 템플릿 다운로드를 클릭합니다. CloudFormation 템플릿을 다운로드한 후 AWS에서 스택을 생성할 수 있습니다.
   ![image](https://github.com/user-attachments/assets/f40eba88-b520-46f5-9eda-9a6f3a76c9ab)

5. AWS Console로 이동해서 **View all services**를 클릭하여 CloudFormation을 찾아 클릭합니다.
   ![image](https://github.com/user-attachments/assets/8991c9f0-74df-4362-ae03-b8eeb6efc3f0)
   ![image](https://github.com/user-attachments/assets/63542f84-731d-400f-a259-d8b3ae69e26e)

6. [StackSet](https://eu-north-1.console.aws.amazon.com/cloudformation/home?region=eu-north-1#/stacksets) 클릭 후, 우측상단에 **StackSet 만들기**를 클릭해 생성을 시합니다. 4번에서 다운로드 받은 **CloudFOrmation 템플릿**파일을 업로드합니다.
   ![image](https://github.com/user-attachments/assets/7b95767f-d139-468c-a8bd-fa13429706b3)

7. StackSet 이름을 지정하고, 나머지는 Default 값으로 지정합니다. 
   ![image](https://github.com/user-attachments/assets/11dcaba2-218d-40c8-8bea-c99d45fb8a11)

8. 검토 후 생성하여 AWS Stack 생성을 완료합니다.

> ⭐ AWS Stack이란? : <br>
> AWS Stack은 AWS CloudFormation을 사용하여 여러 AWS 리소스를 단일 단위로 관리하는 기능입니다. 스택을 생성, 업데이트 및 삭제할 수 있으며, 이를 통해 인프라를 코드로 정의하고 자동화된 방식으로 배포할 수 있습니다. AWS Stack은 Azure의 Azure Resource Manager (ARM) 템플릿과 매우 유사한 개념입니다. 두 서비스 모두 인프라를 코드로 정의하고, 이를 통해 클라우드 리소스를 자동화된 방식으로 배포하고 관리할 수 있게 해줍니다.

> ⭐ AWS StackSet이란? : <br>
> AWS StackSet은 AWS CloudFormation의 기능을 확장하여 여러 계정과 리전에 걸쳐 스택을 생성, 업데이트 및 삭제할 수 있게 해주는 기능입니다. 이를 통해 단일 작업으로 여러 계정과 리전에 걸쳐 스택을 관리할 수 있습니다

9. Azure로 돌아와, StackSet name을 입력 후 Create하여 완료합니다. 
    ![image](https://github.com/user-attachments/assets/4a4c5a0d-68cf-4eb4-a79f-c400a43044b4)

10. Environment Setting에서 새롭게 추가된 AWS account 정보를 볼 수 있습니다.
    ![image](https://github.com/user-attachments/assets/8055e8b0-6547-4668-b1aa-a675d8d27598)



### Lab 3: Defender CSPM 계획을 위한 AWS 환경 준비하기
1. MDC > Environment setting > Lab 2에서 생성한 AWS Connector 클릭
   ![image](https://github.com/user-attachments/assets/b2cb7cac-56e7-45dc-9297-f21eaecf6a14)

2. Defender CSPM 토글 **ON**으로 변경 후 **Settings**로 이동 
    ![image](https://github.com/user-attachments/assets/1842cddf-5fd7-42de-a39b-e10b4a268183)

3. **Agentless Scanning** 와 **Sensitive Data Discovery**를 **ON**으로 변경 후 저장 
    ![image](https://github.com/user-attachments/assets/473060fb-3d2d-43a5-97fc-eb793d1a3628)

4. **Next: Configure access** 클릭
    ![image](https://github.com/user-attachments/assets/f77a88ff-4937-4940-8616-f03338ffc648)

5.  AWS CloudFormaion 하단에 **Download** 클릭해서 template 다운로드
6.  AWS의 업데이트 스택에서 AWS 환경에서 CloudFormation 템플릿이 업데이트되었음을 선택하고 검토 및 생성을 클릭합니다
     ![image](https://github.com/user-attachments/assets/78967dce-5c60-4101-be35-583db4429e67)

7. 다음페이지에서 **update**클릭 후 완료

8. [AWS Console](https://eu-north-1.console.aws.amazon.com/console/home?region=eu-north-1#)에서 스택을 사용하여 CloudFormation 템플릿 배포 
    ![image](https://github.com/user-attachments/assets/8ce7110c-071d-4d82-b1e9-ae5041da8444)

9. CloudFormation에서 Template기반으로 Stack 생성하기 
    ![image](https://github.com/user-attachments/assets/fea7a34c-670c-42cb-9f4e-aaee7298b4e8)

10. Stack Name 작성 후 Submit
    ![image](https://github.com/user-attachments/assets/38e74329-f198-40d2-8472-6a289183841b)

11. Stack Deployment 완료
    ![image](https://github.com/user-attachments/assets/7c78d52a-41e6-4e50-9499-30e4f207f209)

12. AWS console Serach bar에서 **S3** 검색 후 **S3 console**로 이동
13. **이 계정의 퍼블릭 액세스 차단 설정**항목으로 이동 > 우측 상단 **편집** 클
    ![image](https://github.com/user-attachments/assets/53e6ed5b-69a3-46bd-b44b-b62f03e11a03)

14. **모든 퍼블릭 엑세스 차단** 박스 활성화 후 변경사항 저장 
    ![image](https://github.com/user-attachments/assets/ba1eac96-07e8-4320-becf-18e80762e644)

14. 변경사항 저장 이후에 S3 Console bucket에 올라오기까지 24시간이 소요됩니다. (계정 스냅샷 24h마다 업데이트)


 

