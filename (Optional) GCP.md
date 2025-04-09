# Module 9 - Connecting a GCP project

### Lab 1: Create a GCP project

먼저 GCP 프로젝트를 만들어야 합니다.

1.	[Create free GCP](https://www.google.com/aclk?sa=l&ai=DChcSEwiA7K7Gubn3AhUJuu0KHbACBZkYABAAGgJkZw&sig=AOD64_0Cc0zndLvPEu7wV4blEFwWvjOWag&q&adurl&ved=2ahUKEwihk6nGubn3AhVFZcAKHWP5BYkQ0Qx6BAgDEAE)로 이동합니다.
  ![image](https://github.com/user-attachments/assets/74fe6bb0-4d75-4137-93a2-c8767d9248d2)

2. **무료로 시작하기**를 클릭합니다.
3. 이제 기존 Google 계정을 선택하거나 새 계정을 만드세요.
4. 화면의 지시에 따라 GCP 프로젝트를 만듭니다.
5. [Google Cloud Console](console.cloud.google.com)에 로그인 후 대시보드를 확인가능합니다.
  ![image](https://github.com/user-attachments/assets/e579c4a1-b800-4675-83ed-fe9adb8f816e)

6. 프로젝트 번호와 프로젝트 ID를 복사하여 기록해둡니다.

### Lab 2: Create the GCP connector in Microsoft Defender for Cloud
Microsoft Defender for Cloud에서 GCP 리소스를 보호하려면 다음 연습에서 수행할 Microsoft Defender for Cloud에서 GCP 커넥터를 만들어야 합니다.

1. MDC > Environment Settings > + Add environment** > Google Cloud Platform
  ![image](https://github.com/user-attachments/assets/906b2d1a-c2ff-45db-9e3e-bb8b9bc0a7aa)

4.  **Create GCP connector**페이지에서 detail한 정보를 기입합니다. 
하기 기재된 정보 외에는 default값을 유지합니다. 
* **Onboard**: Single project
* **Location**: Select the location nearest you.
* **GCP project number**: Lab 1-6 내용을 붙여넣거나 [Google Cloud Console](console.cloud.google.com) 으로 이동하여 대시보드에서 프로젝트 번호를 복사합니다.
* **GCP project id**: Lab 1-6 내용을 붙여넣거나 [Google Cloud Console](console.cloud.google.com) 으로 이동하여 대시보드에서 프로젝트 번호를 복사합니다.d.

  ![image](https://github.com/user-attachments/assets/bf19f11b-e6e1-4932-8607-24863ff63282)


5. **Next: Select plans** 에서 Defender CSPM, 서버, 컨테이너 및 데이터베이스 계획이 **On**으로 설정되어 있는지 확인합니다.
  ![image](https://github.com/user-attachments/assets/dbceb075-a293-4704-9ead-65e0c01a2b77)

6. **Next: Configure access**에서 GCP 클라우드 셸 스크립트를 복사합니다.
  ![image](https://github.com/user-attachments/assets/dbe129b4-c594-437f-b83b-edeb38638f02)

7. **GCP 클라우드 쉘** 버튼을 클릭하면 클라우드 쉘이 있는 GCP 콘솔이 열립니다.
8. 스크립트를 클라우드 셸에 붙여넣습니다.
  ![image](https://github.com/user-attachments/assets/34dcc055-9a0a-4795-8800-01e7e1fc1ff6)

8. 스크립트를 실행한 후 성공적으로 완료되면 Defender for Cloud로 돌아갑니다. 
9. review and generate 후 **Create**로 완료합니다. 

이제 Microsoft Defender for Cloud에서 GCP 커넥터를 성공적으로 만들었습니다. 이제 GCP 권장 사항과 알림을 받을 수 있습니다.

### Lab 3: Investigate the GCP recommendations 
취약한 이미지가 Azure 컨테이너 레지스트리로 푸시되면 Microsoft Defender for Containers가 이미지에 취약성이 있는지 스캔하기 시작합니다. 이제 Microsoft Defender for Cloud의 권장 사항을 살펴보겠습니다.

> [!NOTE]
> Microsoft Defender for Cloud에서 GCP에 대한 권장 사항을 보려면 GCP 리소스를 생성해야 합니다.
 
 1.MDC > Recommendation > Scope > GCP만 선택합니다. 
  ![image](https://github.com/user-attachments/assets/c8aa6ad8-e5db-4155-9459-659f5ce952ba)

기존 GCP 리소스가 있는 경우 해당 리소스와 관련된 권장 사항을 확인할 수 있습니다.
