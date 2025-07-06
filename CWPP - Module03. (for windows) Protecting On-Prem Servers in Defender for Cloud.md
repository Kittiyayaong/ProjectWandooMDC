# Module 3 - Protecting On-Prem Servers in Defender for Cloud 

## MDC Hybrid 환경 지원
Microsoft Defender for Cloud (MDC)의 Cloud Workload Protection Platform (CWPP)는 클라우드뿐만 아니라 온프레미스 서버도 보호합니다. 이는 하이브리드 환경에서의 보안 요구를 충족시키기 위해 설계된 기능입니다.

## 전제 조건
On-premises 컴퓨터의 서버 보호를 위해 Defender for Servers(플랜 1 또는 플랜 2)를 활성화해야 합니다.

--- 

## Lab 1:(Windows) 디바이스에 서버를 만드는 데 사용할 Hyper-V 설치하기 

* 전제 조건: Windows 10/11
Windows 10 Hyper-V 시스템. 이 가이드는 Windows 11에서도 작동합니다. 자세한 내용은 [여기](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/reference/hyper-v-requirements)) 를 참조하세요

1. 윈도우 키를 눌러 'Hyper-v'를 검색하여, **Windows 기능 켜기/끄지**창으로 들어갑니다. 
2. Hyper-V 박스를 눌러서 **Hyper-V Management Tools**와 **Hyper-V Platform** 두개를 활성화합니다.
  ![Windows Features](../Images/windowsfeatures.png?raw=true)

3. 설정 이후에 PC가 재시작됩니다. 
5. 윈도우에서 **Hyper-V**를 검색한 후 클릭합니다.  
6. Windows Server 2022와 같은 운영 체제를 설치할 ISO 이미지를 다운로드합니다 [here](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022).
7. PC 환경에 가장 적합한 이미지를 선택하고 다운로드하세요(참고: 이 과정은 몇 분 정도 걸릴 수 있습니다).

> ⭐ Notes <br>
> 본 모듈은 Windows Server 2022 64비트 버전 ISO를 기반으로 작성되었습니다.

## Lab 2: Hyper-V를 사용하여 데스크톱에 가상 스위치가 설치 확인
1. Windows에서 **Hyper-v 관리자**를 클릭한 후, 오른쪽의 작업 창에서 "가상 스위치 관리자"를 선택하여 가상 스위치가 설치되어 있는지 확인해야 합니다.
![image](https://github.com/user-attachments/assets/aaad747e-3cbd-4a36-8132-c616107991f1)

2. 가상 스위치 아래에 가상 스위치가 설치되었음을 확인하는 "Default Switch"가 표시됩니다.
![image](https://github.com/user-attachments/assets/d338eae1-8b11-45f5-a595-996a18d4ac2c)

3. 기본 스위치(Default Switch)가 이미 설치되어 있지 않은 경우 [여기](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/get-started/create-a-virtual-switch-for-hyper-v-virtual-machines?tabs=hyper-v-manager) 의 안내에 따라 설치하세요.

## Lab 3: Hyper-V를 사용하여 Defender for DevOps를 통해 보호할 가상 온프레미스 서버 역할을 하는 VM(가상 머신)을 생성

1. Hyper-V에서 **새로만들기 > Virtual Machine**을 클릭합니다.
  ![image](https://github.com/user-attachments/assets/af252b06-136a-49ff-9fdd-c19ee0bd173e)

2. **New Virtual Machine Wizard**에서 Next를 클릭합니다.
 ![image](https://github.com/user-attachments/assets/1781f739-64c6-48a5-89ea-4cb2cb679931)

3. VM에 **Arc Server Wandoo**로 이름을 설정하고, 기본 위치를 선택한 상태로 둡니다. 
  ![image](https://github.com/user-attachments/assets/7fe617e5-32d1-4ea6-b551-e83374fb73f6)

4. **세대 2**로 설정합니다.
  ![image](https://github.com/user-attachments/assets/bb422820-1e91-476b-9237-8297e4fa13c4)

5. 시작 메모리 할당 - 최소 메모리는 2048MB여야 하며, 권장 메모리는 4096MB입니다. 2048MB를 선택합니다.
  ![image](https://github.com/user-attachments/assets/cf4e2b8c-626a-4dcd-8a38-59dd006dd3a5)

6. **네트워크 구성**에서 **기본 스위치**를 선택합니다.
   ![image](https://github.com/user-attachments/assets/dc862ffb-f34a-4c68-98a0-d050d159c694)

7. **가상 하드 디스크 연결**에서 모든 기본값을 그대로 두고 **다음**을 클릭합니다.
    ![image](https://github.com/user-attachments/assets/1f2ed205-b89e-4a6a-8f16-6bf7ff310f31)

8. 사전에 다운로드 받은 ISO 이미지 파일을 올린 후 완료합니다. 
   ![image](https://github.com/user-attachments/assets/a12ab94c-15e6-4501-8503-4d8bf3261429)


## Lab 4: VM에 운영 체제 설치

1. Hyper-V 관리자의 우측 하단에서 **연결**을 클릭합니다.
   ![image](https://github.com/user-attachments/assets/6bf2910f-328d-4ba6-8f46-850314799c65)
2. 가상 머신 연결 팝업이 나타나면 **시작**을 클릭합니다.
  ![image](https://github.com/user-attachments/assets/bd69a616-ed96-42d6-95cc-5195452a56ce)
3. 이제 스페이스 바와 같은 키보드의 아무 키나 누르고 약 1분 정도 기다린 후, Boot manager가 뜨면 **Enter**을 누릅니다. 그런 다음 **Microsoft Server 운영 체제 설정**이 나타나면 기본값을 그대로 두고 **다음**을 클릭합니다.
   ![image](https://github.com/user-attachments/assets/4bf6f3dc-ebb3-41e1-b684-bc4a1d7b0687)

5. 모든 설정을 Default로 Install 합니다.
   ![image](https://github.com/user-attachments/assets/c4a9b596-9476-4e42-9793-ad69374ebe60)

6. Windwos Server 2022 Standard Evaluation (Desktop Experience)를 클릭합니다. 
  ![image](https://github.com/user-attachments/assets/a1bae6c4-277c-45d3-81c3-a096985f0a86)

7. Terms and COndition을 Accept하고, **Custom**으로 설정합니다. 
   ![image](https://github.com/user-attachments/assets/fc63da6e-c0bb-46b5-88d7-c1a33891e617)

8. Default Drive 상태로 유지하고 넘어갑니다.
   ![image](https://github.com/user-attachments/assets/9674b05f-fddb-46ba-bcda-6139012e4562)

9. OS설치가 포함된 VM이 설치되고 있습니다.
   ![image](https://github.com/user-attachments/assets/27d31085-f0a0-4bb6-9f87-b14c30f092aa)

10. VM의 password를 설정합니다.
   ![image](https://github.com/user-attachments/assets/0dfc53f1-7222-41c0-85e8-0aaca14974e9)

2. 디스플레이 구성은 환경에 맞게 설정한 후 연결합니다. 
 ![image](https://github.com/user-attachments/assets/5f681a1b-e3d6-49f1-86a8-dd6187b3f2cb)

## Lab 5: Azure Arc RP Setup하기 

> ⭐ Azure ARC란? <br>
> Azure Arc는 온프레미스, 멀티 클라우드, 엣지 환경을 포함한 모든 인프라에 Azure 관리 및 서비스를 확장하는 종합 솔루션입니다. 이를 통해 기존 non-Azure 및/또는 온프레미스 리소스를 Azure Resource Manager에 투영하여 전체 환경을 함께 관리할 수 있습니다. 여기에는 가상 머신, Kubernetes 클러스터 및 데이터베이스를 Azure에서 실행되는 것처럼 관리하는 것이 포함됩니다.

> ⭐ Azure Arc RP (Resource Provider)란? <br>
> Azure Arc Resource Provider (RP)는 Azure Resource Manager를 사용하여 Azure 외부에서 실행되는 서버를 관리할 수 있게 해줍니다. 각 서버는 Azure에서 하이브리드 컴퓨트 머신 리소스로 표현됩니다. 서버가 Azure Arc로 관리되면 확장을 사용하여 에이전트, 스크립트 또는 구성을 머신에 배포할 수 있습니다.

> Azure Arc RP의 주요 기능:
>  * 하이브리드 컴퓨트 API: Azure Arc 지원 서버 및 관련 확장을 생성, 목록화, 업데이트 및 삭제할 수 있습니다.
>  * 사용자 정의 위치: Azure Arc 지원 데이터 서비스 RP는 kubeconfig를 사용하여 클러스터와 통신하고 사용자 정의 위치에 매핑된 네임스페이스에 Azure Arc 지원 데이터 서비스 유형의 사용자 정의 리소스를 생성합니다.

1. Cloud shell을 Powershell로 엽니다. [Cloud Shell](https://portal.azure.com/#cloudshell/)
2. [여기](https://learn.microsoft.com/en-us/azure/azure-arc/servers/prerequisites#azure-resource-providers) 로 이동하여 Powershell 명령을 복사하여 Azure Resource Provider를 등록합니다.
![image](https://github.com/user-attachments/assets/826e5fd5-d263-42c2-99bb-bcb8468b875e)


## Lab 6: Defender for Cloud가 VM을 보호할 수 있도록 VM에 Azure Arc를 설치

* 전제 조건: Arc 설치를 위한 전제 조건을 확인하세요 [여기](https://learn.microsoft.com/en-us/azure/azure-arc/servers/learn/quick-enable-hybrid-vm#prerequisites)

1. Azure portal에서 **Azure Arc**를 검색 > Azure Arc REsources > Machines > + Add/Create > Add a machine
   ![image](https://github.com/user-attachments/assets/fc378e2f-2f81-4f3a-a75e-eca2b099ccb8)

2. **Add a single server** 옵션에서 **Generate Script**를 클릭합니다.
   ![image](https://github.com/user-attachments/assets/07e77e60-f9df-438f-8fa3-a74be26d9c58)

3. Server Detail 정보를 기입합니다.
   ![image](https://github.com/user-attachments/assets/38a95d54-b799-40e4-91b4-89d9abdc4d92)

> ⭐ Tips: <br>
> 연결 방법(connectivity method)의 경우 환경에 가장 적합한 방법을 선택하세요. 제 경우 테스트 서버이므로 퍼블릭 엔드포인트로 남겨두겠습니다.

4. tag는 필요시 진행하며, 이번 랩에서는 skip합니다.
5. 스크립트 다운로드 및 실행 페이지에서 스크립트를 클립보드에 복사합니다.
   ![image](https://github.com/user-attachments/assets/fba2840c-b100-415f-8776-5cad29d40207)
   
7. Lab 4에서 생성한 VM으로 돌아가서 **PowerShell ISE**를 관리자 권한으로 실행합니다.
   ![image](https://github.com/user-attachments/assets/262d3670-2443-4032-b7bd-32a4bdabc7eb)

8. 이제 Powershell이 열렸으니 새 파일을 만들고 이전에 복사한 Arc 스크립트를 이 파일에 직접 붙여넣은 다음 실행을 누릅니다.

9. 스크립트가 실행되면 VM의 기본 브라우저에 Azure 구독 인증을 요청하는 메시지가 표시됩니다(이 서버를 연결할 위치) Azure 구독에 로그인합니다.

10. 스크립트가 완료되면 Azure Arc 에이전트가 서버에 배포되고 구성됩니다.

> ⭐ Tips: <br>
> Azure Subscription은 약 24시간 후에 이 서버를 감지할 수 있습니다. 이 VM은 Azure에서 온프레미스 서버 역할을 하며, Microsoft Defender for Cloud의 보호를 받게 됩니다.

### 🔗 [다음 Lab으로 이동하기 Windows »](https://github.com/Kittiyayaong/ProjectWandooMDC/blob/main/CWPP%20-%20Module04.%20AI%20Workloads.md)
