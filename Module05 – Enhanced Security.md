# Module 05 - Enhanced Security

## 목표
Defender for Servers는 컴퓨팅 워크로드에 대한 위협 감지 및 고급 클라우드 방어 기능을 제공합니다. 여기에는 컴퓨터의 관리 포트를 보호하는 Just In Time (JIT) VM Access, 컴퓨터에서 변경 사항을 추적하고 실행 중인 애플리케이션을 추적하는 파일 무결성 모니터링(FIM) 및 적응형 애플리케이션 제어뿐만 아니라 Microsoft Defender for Endpoint에서 제공하는 OS 수준의 위협 감지, DNS 및 네트워크 기반 공격을 포함한 Azure VM에 대한 네트워크 계층 위협 감지도 포함됩니다. 이 연습에서는 Defender for Servers Plan 2의 이러한 향상된 기능 중 일부가 클라우드 환경에서 컴퓨팅 워크로드를 보호하는 데 어떻게 도움이 되는지 이해할 수 있습니다.

### Lab 1: Microsoft Defender for Servers Plan 2 활성
특정 구독에서 Defender 요금제를 활성화하려면:
1.	Azure portal > Microsoft Defender for Cloud > Environment settings > 하단에서 테스트 대상 subscription > 
2.  Server 토글을 **On**으로 설정합니다. 
3.	왼쪽 상단에 **Save**로 저장 후 완료합니다.

### Lab 2-1: test용 VM 생성하기 
1.	Azure portal > Create a resource > Virtual machine > Create
2.	detail한 정보 기입 후 create 

### Lab 2-2: JIT(Just-in-time)를 사용하여 공격 표면 줄이기
1.	Azure portal > Microsoft Defender for Cloud > Cloud security > Workload Protectinos > **Just-in-time VM access** 클
![image](https://github.com/user-attachments/assets/1807135f-537a-4a02-86cf-fdf0e09b2756)

2. 
