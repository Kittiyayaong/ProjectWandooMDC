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

