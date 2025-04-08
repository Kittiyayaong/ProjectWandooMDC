# Module 11 - Connecting an AWS  project

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

6. 스택 생성 클릭 후, 4번에서 다운로드 받은 **CloudFOrmation 템플릿**파일을 업로드합니다.
   ![image](https://github.com/user-attachments/assets/77ae6b74-c0df-495a-84c0-cfd5a7615151)

7. Stack 이름을 지정하고, 나머지는 Default 값으로 지정합니다. 
   ![image](https://github.com/user-attachments/assets/11dcaba2-218d-40c8-8bea-c99d45fb8a11)

8. 검토 후 생성하여 AWS Stack 생성을 완료합니다.

9. Azure로 돌아와, StackSet name을 입력 후 Create하여 완료합니다. 
    ![image](https://github.com/user-attachments/assets/4a4c5a0d-68cf-4eb4-a79f-c400a43044b4)
