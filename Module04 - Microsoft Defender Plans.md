# Module 04 - Microsoft Defender Plans

### Lab 1: 경고 검증(Alert validation)

1.	Microsoft Defender for Cloud > General > Security Alerts으로 이동합니다. 
2.	Container에 대한 경고 시뮬레이션 생성:
    - 우측 상단에 **Sample alerts** 클릭합니다. 
    - 테스트 할 Subscription과 Defender for cloud plan에서 **Container**을 선택합니다. 

![Create sample virtual machine security alerts](../Images/asc-create-sample-security-alerts-vm.gif?raw=true)

3. 샘플 알림 생성이 진행 중이며 프로세스가 완료될 때까지 기다립니다. 알림 센터를 열거나 활동 로그에서 진행 상황을 추적할 수 있습니다(이 프로세스는 보통 완료하는 데 2분이 걸립니다)
4. 이제 알림 페이지에서 샘플 이벤트를 볼 수 있습니다. 
![image](https://github.com/user-attachments/assets/dc39e9a5-5651-458d-94cf-124926ef38eb)

### Lab 2: 경고 억제(Alert suppression)

하나의 경고가 흥미롭거나 관련성이 없을 때, 해제 옵션을 사용하여 단일 알림을 수동으로 해제가 가능합니다. 더 나아가, 이번 랩에서는 억제 규칙 기능을 사용하여 향후 유사한 알림을 자동으로 해제할 수 있습니다.

1.	Microsoft Defender for Cloud > General > Security Alerts으로 이동합니다. 
2.	**Container with a sensitive volume mount detected** alert을 클릭 > **Take action** 탭으로 이동 > **Create Suppression Rule**을 클릭합니다. 
3.	![image](https://github.com/user-attachments/assets/67a36b56-1198-401e-8548-532b770f37b5)

4.	Rule name: *Wandoo-MDC-mod4-test*.
6.	reason field: Other
7.	rule expiration: Lab 하루 이후로 설정합니다.
8.	**Apply** 클릭하고 새 규칙이 적용될 때까지 최대 10분 소요됩니다. 
9.	Microsoft Defender for Cloud > General > Security Alerts > 상단의 supression rules를 클릭하여 들어가면, 생성한 rule이 리스트업 된 것을 확인 할 수 있습니다. 

> ⭐ Tips: <br>
>  Azure 정책에서 Microsoft Defender for Cloud 알림에 대한 억제 규칙을 구성하려면 Deploy-라는 기본 정책 정의를 사용하여 관리 그룹 수준에서 억제 규칙을 만들 수 있습니다. 구독 수준에서 알림을 억제하려면 Azure 포털 또는 REST API를 사용할 수 있습니다.
