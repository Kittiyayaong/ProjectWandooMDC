# ☁️ Module 3 - Protecting On-Prem Servers in Defender for Cloud (macOS 버전)

---

## ✅ MDC Hybrid 환경 지원

Microsoft Defender for Cloud (MDC)의 Cloud Workload Protection Platform (CWPP)는 클라우드뿐만 아니라 **온프레미스 서버 및 macOS, Linux VM**도 보호합니다. 하이브리드 보안 요구를 충족하기 위해 Azure Arc를 사용합니다.

---

## ⚠️ macOS 전제 조건

- macOS Ventura/Sonoma 이상
- 가상화 지원 Hypervisor 설치:
  - UTM (무료)
  - Parallels Desktop (유료)
  - VMware Fusion (유료, 개인 무료 버전 있음)
- Windows Server ISO 또는 Linux 배포판 ISO (테스트용 VM용)

---

# 📝 Lab 1: macOS에 Hypervisor 설치하기

## ✅ 1. UTM 설치 (예시, 무료)

🔗 [UTM 공식 다운로드](https://mac.getutm.app)

1. UTM dmg 파일 다운로드 후 Applications 폴더에 복사
2. UTM 실행 ➔ 상단 메뉴에서 **Create a New Virtual Machine** 클릭

---

# 📝 Lab 2: Windows Server VM 생성

1. **Virtualize ➔ Windows** 선택
2. Windows Server ISO 파일 선택 (예: Windows Server 2022)
3. CPU 코어 ➔ 최소 2개, 메모리 ➔ 최소 2048MB (권장 4096MB)
4. 네트워크 ➔ Shared Network (NAT)
5. 저장소 ➔ 64GB 이상 생성
6. VM 생성 후 **Start** 클릭 ➔ Windows Server 설치 진행

> ⚠️ Windows 라이선스가 없다면, Windows Server Evaluation ISO를 사용 가능  
> 🔗 [Windows Server Evaluation 다운로드](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022)

---

# 📝 Lab 3: Azure Arc RP (Resource Provider) 등록

1. Azure Portal ➔ **Cloud Shell (Bash)** 실행
2. 아래 명령어를 순서대로 실행

```bash
az login
az provider register --namespace Microsoft.HybridCompute
az provider register --namespace Microsoft.GuestConfiguration
az provider register --namespace Microsoft.HybridConnectivity
