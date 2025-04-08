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
![Uploading image.png…]()

![Windows Features](../Images/windowsfeatures.png?raw=true)
4. You will need to re-start your PC to let the changes take effect.
5. Search for **Hyper-V** in the Windows search bar and open it.
6. Download an ISO image which will install an operating system, such as Windows Server 2022, by going [here](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022).
Select the image most suitable to your PC environment and download it (Note: This process may take a few minutes). 

Take note of where this ISO downloaded, as you'll need it later.
