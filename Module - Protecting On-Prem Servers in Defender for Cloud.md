# Module - Protecting On-Prem Servers in Defender for Cloud 

## 목표
이 연습에서는 Hyper-V("온프레미스 서버" 역할)를 사용하여 개인 클라이언트 컴퓨터에 서버를 배포한 후, Microsoft Defender for Cloud를 사용하여 서버를 보호하기위해 Azure Arc를 배포하는 방법을 배우게 됩니다.

## 전제 조건
On-premises 컴퓨터의 서버 보호를 위해 Defender for Servers(플랜 1 또는 플랜 2)를 활성화해야 합니다.

## Lab 1: 컴퓨터에 서버를 만드는 데 사용할 Hyper-V 설치하기

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

## Lab 2: Hyper-V를 사용하여 데스크톱에 이미 가상 스위치가 설치되어 있는지 확인합니다.
1. Windows에서 **Hyper-v 관리자**를 클릭한 후, 오른쪽의 작업 창에서 "가상 스위치 관리자"를 선택하여 가상 스위치가 설치되어 있는지 확인해야 합니다.
![image](https://github.com/user-attachments/assets/aaad747e-3cbd-4a36-8132-c616107991f1)

2. 가상 스위치 아래에 가상 스위치가 설치되었음을 확인하는 "Default Switch"가 표시됩니다.
![image](https://github.com/user-attachments/assets/d338eae1-8b11-45f5-a595-996a18d4ac2c)

3. 기본 스위치(Default Switch)가 이미 설치되어 있지 않은 경우 [여기](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/get-started/create-a-virtual-switch-for-hyper-v-virtual-machines?tabs=hyper-v-manager) 의 안내에 따라 설치하세요.

## Lab 3: Hyper-V를 사용하여 Defender for DevOps를 통해 보호할 가상 온프레미스 서버 역할을 하는 VM(가상 머신)을 생성합니다.

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

1. 오른쪽의 **액션** 창 아래에 있는 **하이퍼-V 매니저**의 **아크-서버** VM으로 이동합니다.
