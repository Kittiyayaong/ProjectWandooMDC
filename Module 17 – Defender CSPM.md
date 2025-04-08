# Module 17 – Defender CSPM  

## 목표
이 연습에서는 Defender for CSPM를 활성화하고 CSPM 기능을 활용하는 방법을 배우게 됩니다.

## CSPM이란? 
CSPM(Cloud Security Posture Management)은 클라우드 환경에서 보안 태세를 관리하는 솔루션입니다. CSPM은 클라우드 인프라의 보안 상태를 지속적으로 모니터링하고, 잘못된 구성이나 보안 위험을 식별하여 이를 해결하는 데 도움을 줍니다. Microsoft Defender for Cloud는 CSPM 기능을 제공하여 Azure, AWS, GCP와 같은 멀티 클라우드 환경에서 보안 태세를 관리할 수 있습니다

## Lab 1: DCSPM 계획을 위한 환경 준비하기

* 리소스 목록은 프로비저닝 과정에서 배포될 예정입니다(디스크, 네트워크 인터페이스, 공용 IP 주소 등과 같은 종속성 포함):

  Name | Resource Type | Purpose
  -----| ------------- | -------
  dcspmlab-winsrv | Virtual machine | Windows Server
  dcspmlab-nix | Virtual machine | Linux Server

1. 아래의 파란색 **Azure에 배포** 버튼을 클릭하여 실험실 환경을 준비하세요:
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMicrosoft-Defender-for-Cloud%2Fmaster%2FLabs%2FFiles%2Fdcspmlabdeploy.json" target="_blank"><img src="https://aka.ms/deploytoazurebutton"/></a>
  
2. 배포를 위해 필수 필드를 지정해야 하는 **Azure Portal > custom deployment** 페이지로 리디렉션됩니다. 설정값을 기입한 후, 
