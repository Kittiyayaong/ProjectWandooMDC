Module-13-Defender for APIs.md


# Module - Defender for APIs
## Objectives

이번 연습에서는 Azure API 관리를 통해 Defender for API를 활성화하고, Defender for API 기능을 활용하는 방법을 배우게 됩니다.

[Official Defender for API announcement](https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/microsoft-bolsters-cloud-native-security-in-defender-for-cloud/ba-p/3801818) 를 참조하세요.

[Defender for API documentation](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-apis-introduction) 를 참조하세요.
   
### Lab 1. AZURE API 관리 서비스 만들기

참고: 새로운 Azure API 관리 서비스의 배포 시간은 약 1시간입니다.

1. Azure portal > + Create a resource > API Management
   ![image](https://github.com/user-attachments/assets/2a8654d6-db62-4d8b-8970-d66b90fad2c9)

2. Setting 값을 설정합니다.  
   ![image](https://github.com/user-attachments/assets/943cd13c-3310-4d30-b800-ac9ae510c3ce)

### Lab 2. API 관리 내에서 API 게시하기

1. Azure portal > API management Services 검색 > 생성한 API Management service 클릭
   ![image](https://github.com/user-attachments/assets/94d3dae8-c55a-4c82-b13c-39342e02adbd)

2. APIs > APIs > Open API 클릭
   ![image](https://github.com/user-attachments/assets/aa275590-eafa-4ecb-a90b-1bdc93b637f9)

3. 설정값
   ![image](https://github.com/user-attachments/assets/f3d38b9c-848b-4364-83fd-fb47d82053a3)
   * **OpenAPI specification**		https://petstore3.swagger.io/api/v3/openapi.json
   * **Display name**	After you enter the OpenAPI specification URL, API Management fills out this field based on the JSON.
   * **Name**	After you enter the preceding Display Name, API Management fills out this field based on the JSON.
   * **API URL suffix**	petstore	
4. Create 후 완료

### API 테스트
Azure 포털에서 직접 API 작업을 호출할 수 있으므로 작업을 보고 테스트하는 데 편리한 방법이 있습니다. 포털의 테스트 콘솔에서는 기본적으로 내장된 올 액세스 구독의 키를 사용하여 API를 호출합니다. 또한 제품에 적용된 구독 키를 사용하여 API 호출을 테스트할 수도 있습니다.

1. **APIs > Swagger Petstore > Test** tab으로 이동해서, **Finds Pets by status**를 선택합니다. 페이지에는 **Query parameter**가 표시됩니다. 

 ![image](https://github.com/user-attachments/assets/85e31727-ca59-41f6-a910-a01e12166f98)


### Lab 3: DEFENDER FOR API 활성화

1. MDC > Environment settings > subscription > Defender plans > APIs 토글 **On**으로 설정
   ![image](https://github.com/user-attachments/assets/5c9d07c3-d54a-4f72-a352-41c6d46d738a)

2. Plan 설정
   ![image](https://github.com/user-attachments/assets/42e5b629-d9f5-4865-8489-8ba67aa5aec3)

3. 왼쪽 상단의 **Save** 클릭하여 완료

   
### Lab 4: ONBOARD APIS TO DEFENDER FOR APIS
해당 API를 Defender for API에 의해 보호되도록 온보딩합니다.

1. MDC > Recommendations > Defender for APIs 
