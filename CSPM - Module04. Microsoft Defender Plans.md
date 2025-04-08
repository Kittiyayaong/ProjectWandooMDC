# Module 04 - Microsoft Defender Plans

## Defender Plan이란? 
Defender Plan은 MDC의 다양한 보안 기능을 활성화하여 클라우드 환경의 보안 태세를 강화하는 계획입니다. 각 Defender Plan은 특정 유형의 리소스에 대한 보안 기능을 제공하며, 이를 통해 클라우드 리소스를 보호하고 관리할 수 있습니다. 예를 들어, Defender for Servers는 Windows 및 Linux 서버에 대한 예방적 보호, 침해 후 탐지, 자동화된 조사 및 대응 기능을 제공합니다

* Defender Plan에는 다음이 포함됩니다:
    * Defender for Servers: Windows 및 Linux 서버에 대한 예방적 보호, 침해 후 탐지, 자동화된 조사 및 대응 기능을 제공합니다
    * Defender for Containers: 컨테이너 이미지의 취약성 평가 및 보안 권장 사항을 제공합니다.
    * Defender for SQL: SQL 데이터베이스에 대한 보안 평가 및 권장 사항을 제공합니다.
    * Defender for Storage: 스토리지 계정에 대한 악성 코드 스캔 및 민감한 데이터 발견 기능을 포함합니다.
    * Defender for Key Vault: Key Vault 리소스에 대한 보안 평가 및 권장 사항을 제공합니다

## 경고검증과 억제 
두 기능은 Microsoft Defender Plans의 일부로, 클라우드 환경의 보안을 강화하고 보안 팀의 효율성을 높이는 데 중요한 역할을 합니다. 
* 경고 검증: Microsoft Defender Plans에서 생성된 보안 경고의 유효성을 확인하여 실제 위협인지 판단합니다. 이를 통해 보안 팀은 경고를 분석하고 필요한 조치를 취할 수 있습니다 
* 경고 억제: 반복적으로 발생하는 오탐이나 불필요한 경고를 자동으로 억제하여 보안 팀이 중요한 경고에 집중할 수 있도록 합니다. 경고 억제 규칙을 설정하면 특정 유형의 경고가 자동으로 억제됩니다.

> ⭐ Tips: <br>
> * **경고 검증**은 경고의 유효성을 확인하고 실제 위협인지 판단하는 데 중점을 두며, **경고 억제**는 반복적으로 발생하는 오탐이나 불필요한 경고를 자동으로 억제하는 데 중점을 둡니다.
> * **경고 검증**은 보안 팀이 경고의 신뢰성을 평가하고, 필요한 경우 추가 조치를 취할 수 있도록 도와줍니다. **경고 억제**는 보안 팀이 중요한 경고에 집중할 수 있도록 하여, 경고 관리의 효율성을 높입니다.

### Lab 1: 경고 검증(Alert validation)

1.	Microsoft Defender for Cloud > General > Security Alerts으로 이동합니다. 
2.	Container에 대한 경고 시뮬레이션 생성:
    - 우측 상단에 **Sample alerts** 클릭합니다. 
    - 테스트 할 Subscription과 Defender for cloud plan에서 **Container**을 선택합니다.
    
    ![image](https://github.com/user-attachments/assets/bc36ca91-0687-459a-879a-5d6aa13f15ef)

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
