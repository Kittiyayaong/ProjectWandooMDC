# Module 3 - Secure Posture

## ✅ Secure Posture란?

**보안 태세 (Security Posture)**  
- 클라우드 리소스의 보안 상태를 평가  
- **보안 점수(Secure Score)** 로 현재 상태를 시각화  
- Microsoft Cloud Security Benchmark(MCSB) 등 표준 기반 평가  
- 조직은 이를 통해 **Remediation(시정 조치) 우선순위**를 결정

## ✅ Lab 핵심요소 
| **항목**       | **내용**                                                                                                                                  |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| **랩 목적**     | **컨테이너 이미지의 취약점 평가**                                                                                                                    |
| **무엇을 배우나?** | Microsoft Defender for Cloud가 \*\*Azure Container Registry (ACR)\*\*에 저장된 컨테이너 이미지를 자동으로 스캔하여 **취약점을 탐지**하고, 보안 상태를 관리하는 방법             |
| **핵심 절차**    | 1. ACR (Container Registry) 생성<br>2. 테스트용 Linux 컨테이너 이미지(`hello-world`) 빌드 및 ACR에 푸시<br>3. Defender for Cloud가 자동 스캔하여 **취약점 결과 표시** 확인 |
| **기술 포인트**   | - **Qualys 엔진**을 사용하여 이미지 취약점 분석<br>- Defender for Cloud가 이미지 푸시 후 자동 스캔<br>- 실습 완료 후 \*\*Recommendation(권장 사항)\*\*에 취약점 결과 표시          |
| **실무 적용 가치** | - DevOps 파이프라인에 ACR 취약점 평가를 통합 가능<br>- 이미지 배포 전 **보안 검증**으로 공급망 리스크 최소화<br>- 관리자는 Defender for Cloud Dashboard에서 전체 취약점 현황을 시각화 가능      |
| **결론 문장**    | **“ACR에 푸시된 이미지가 Defender for Cloud를 통해 자동 스캔되고, 취약점 결과가 관리 콘솔에 표시되어 보안 태세를 강화할 수 있음을 이해하는 실습”**                                        |


---

### Lab 1: 컨테이너의 취약성 평가

Microsoft Defender for Cloud는 ACR에 푸시되거나 가져온 이미지, 또는 지난 30일 이내에 가져온 이미지를 자동으로 스캔합니다. 이 스캔 과정에서 각 이미지에 대한 보안 취약점을 탐지하고, 그 결과를 이미지별로 자세히 표시합니다. 이 과정에서 발견된 모든 취약점은 "Azure 컨테이너 레지스트리 이미지의 취약점은 Qualys에서 해결해야 합니다"라는 권장 사항에 따라 처리됩니다. Qualys는 앞서 설명한 것처럼 클라우드 기반 보안 솔루션을 제공하는 회사로, 취약점 관리 솔루션을 제공합니다.


#### Lab 1-1. Azure에서 Container Registry 생성하기

1. Portal.azure.com으로 로그인 후 상단에 **Create Resoure (리소스만들기)** 클릭
2. 검색 창에 "Container Registry"를 입력하고, 컨테이너 레지스트리를 선택합니다.
  ![image](https://github.com/user-attachments/assets/81d5c086-eb68-46cf-9768-5c429dfc41af)

3. Create 클릭
4. Create container registry에서 detail한 정보 기입 후 Review + Create
> ✅ **실습 Lab 기준**
  > - Subscription: 본인 Subscription
  > - Resource group: 새로 생성 (ex. wandoo-mdc)  
  > - Registry name: 고유한 이름 (ex. wandootestcontainer1 (user number))
  > - Location: Korea Central
  > - Domain name label scope: Unsecure
  > - Pricing plan: Standard
  > - Role assignment permissions mode: RBAC Registry Permissions

#### Lab 1-2. 취약점이 있는 컨테이너 레지스트리 이미지를 시뮬레이션하기 위해 ACR 작업 명령어와 샘플 이미지를 사용합니다. (Azure trial의 경우 이미지 업로드 불가) 

1. Portal.azure.com 에서 Container registries를 검색하여 들어갑니다. 
2. Lab 1-1에서 생성한 Container가 리스트에 있음을 확인한 후, 이름이나 컨테이너 레지스트리를 복사합니다.
3. bash 환경을 사용하여 [Azure Cloud Shell](https://shell.azure.com/)을 엽니다. 
![image](https://github.com/user-attachments/assets/7cfef76a-f1f1-4d7e-b64e-2078b3ce3903)
4. Microsoft 컨테이너 레지스트리에서 호스팅하는 hello-world 이미지에서 Linux 컨테이너 이미지를 빌드하고 이를 구독의 기존 Azure 컨테이너 레지스트리 인스턴스로 푸시합니다:

다음 두 스크립트 블록 실행합니다. :

```
echo FROM mcr.microsoft.com/azuredocs/aci-helloworld > Dockerfile
```

컨테이너 레지스트리 이름을 포함하도록 다음 스크립트를 수정합니다. :

```
az acr build --image sample/hello-world:v1 --registry <your container registry name> --file Dockerfile .
```

![image](https://github.com/user-attachments/assets/846beec8-1625-4a55-8e8c-5cf0092ff886)

5. 성공 메시지가 나타날 때까지 기다립니다.
   
![image](https://github.com/user-attachments/assets/77cdb543-527a-42e4-89fe-80c86f2f03ce)

7. Recommendatino에서 항목이 나타나기 위해, 스캔은 일반적으로 몇 분 이내에 완료되지만, 취약점/보안 결과가 권장 사항에 나타나려면 최대 15분이 걸릴 수 있습니다.
![image](https://github.com/user-attachments/assets/69540ca7-700f-4106-a28c-e0122dee9310)


### 🔗 [다음 Lab으로 이동하기 »](https://github.com/Kittiyayaong/ProjectWandooMDC/blob/main/CSPM%20-%20Module04.%20Microsoft%20Defender%20Plans.md)








