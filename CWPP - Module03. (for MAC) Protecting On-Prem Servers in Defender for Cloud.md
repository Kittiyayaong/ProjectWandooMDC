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

## Lab 1: macOS에 Hypervisor 설치하기

### ✅ 1. UTM 설치 (예시, 무료)

🔗 [UTM 공식 다운로드](https://mac.getutm.app)

1. UTM dmg 파일 다운로드 후 Applications 폴더에 복사
2. UTM 실행 ➔ 상단 메뉴에서 **Create a New Virtual Machine** 클릭

---

## Lab 2: Windows Server VM 생성

1. **Virtualize ➔ Windows** 선택
2. Windows Server ISO 파일 선택 (예: Windows Server 2022)
3. CPU 코어 ➔ 최소 2개, 메모리 ➔ 최소 2048MB (권장 4096MB)
4. 네트워크 ➔ Shared Network (NAT)
5. 저장소 ➔ 64GB 이상 생성
6. VM 생성 후 **Start** 클릭 ➔ Windows Server 설치 진행

> ⚠️ Windows 라이선스가 없다면, Windows Server Evaluation ISO를 사용 가능  
> 🔗 [Windows Server Evaluation 다운로드](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022)

---

## Lab 3: Azure Arc RP (Resource Provider) 등록

1. Azure Portal ➔ **Cloud Shell (Bash)** 실행
2. 아래 명령어를 순서대로 실행

```bash
az login
az provider register --namespace Microsoft.HybridCompute
az provider register --namespace Microsoft.GuestConfiguration
az provider register --namespace Microsoft.HybridConnectivity
```
결과값에 나온 코드를 [https://microsoft.com/devicelogin](https://microsoft.com/devicelogin)에 등록하여 인증 

> ⭐ Tips.
>
> 이 3개의 Provider는 **Azure Arc를 통해 온프레미스 서버를 Azure에 연결(등록)하기 위한 전제 조건**임.
>
| 명령어 | 목적 |
|--|--|
| `az provider register --namespace Microsoft.HybridCompute` | Azure Arc를 통해 온프레미스 VM, 서버를 **Azure Resource Manager 리소스로 등록**할 수 있도록 Hybrid Compute 리소스 프로바이더를 활성화 |
| `az provider register --namespace Microsoft.GuestConfiguration` | Guest Configuration 정책(예: Arc로 연결된 서버의 OS 보안 설정 및 규정 준수 관리)을 적용하기 위한 프로바이더 |
| `az provider register --namespace Microsoft.HybridConnectivity` | 온프레미스 서버와 Azure 간 **하이브리드 연결 기능**(예: Arc Agent 연결, Private Link 등)을 지원 |

---

## Lab 4: Windows Server VM 초기 세팅 (macOS + UTM)

Windows Server 설치가 완료되면, VM을 Azure Arc에 연결하기 전에 기본 세팅을 진행해야 합니다.

### ✅ 1. 관리자 비밀번호 설정

1. 설치가 완료되면 첫 로그인 시 **Administrator** 계정 비밀번호 설정 화면이 나타납니다.
2. 복잡성 규칙을 만족하는 비밀번호를 입력합니다.

### ✅ 2. 네트워크 연결 확인

VM이 Azure Arc에 연결되려면 인터넷 접속이 필요합니다.

1. Windows Server VM에 로그인합니다.
2. **Start ➔ Windows PowerShell**을 열어 아래 명령어로 인터넷 연결을 확인합니다.

```powershell
ping www.google.com
```

---

## Lab 5: Azure Arc Agent 설치 (Onboarding)
1. Azure Portal ➔ Azure Arc ➔ add resource > add machine > 

   <img width="1440" alt="스크린샷 2025-07-06 오후 2 36 12" src="https://github.com/user-attachments/assets/8091dc81-dffd-451e-a86b-7b27c9a5a8e2" />

3. Add a single server ➔ Generate script: Subscription, Resource Group, Region, OS 등 정보 입력 후 스크립트 생성

   <img width="1192" alt="image" src="https://github.com/user-attachments/assets/437b632c-e710-4912-a182-bd76118cbc73" />

   <img width="1434" alt="image" src="https://github.com/user-attachments/assets/e06c2120-5b82-4d70-98b0-9fafca3db6fc" />


5. VM 내 PowerShell 관리자 권한으로 접속 후 스크립트 실행
6. https://microsoft.com/devicelogin에서 코드 입력 ➔ 인증 완료

