# Module 17 – Defender CSPM  

## 목표
이 연습에서는 Defender for CSPM를 활성화하고 CSPM 기능을 활용하는 방법을 배우게 됩니다.

## CSPM이란? 
CSPM(Cloud Security Posture Management)은 클라우드 환경에서 보안 태세를 관리하는 솔루션입니다. CSPM은 클라우드 인프라의 보안 상태를 지속적으로 모니터링하고, 잘못된 구성이나 보안 위험을 식별하여 이를 해결하는 데 도움을 줍니다. Microsoft Defender for Cloud는 CSPM 기능을 제공하여 Azure, AWS, GCP와 같은 멀티 클라우드 환경에서 보안 태세를 관리할 수 있습니다

## Lab 1: Defender CSPM 계획 활성화
Defender CSPM에서 제공하는 기능에 액세스하려면 구독에서 <a href="https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-enhanced-security ">디펜더 클라우드 보안 자세 관리(CSPM) 계획을 활성화해야 합니다

1. MDC > Environment Settings > 하단에 테스트 대상 subscription > Defender plan > Defender CSPM > On 확인
   ![image](https://github.com/user-attachments/assets/4b644216-ae1d-4d2c-ab6b-c8391a03b747)

2. Defender CSPM의 Setting을 클릭하여 **Agentless scanning for machines**를 enable합니다.
   > ⭐ Tips: <br>
   > Agentless Scanning for machines: 취약점 평가 및 소프트웨어 인벤토리를 가능하게 합니다.

3. Save합니다.


## Lab 2: 공격 경로 분석 및 완화 확인하기 

1. MDC > general > Attach Path Analysis
   ![이미지](../이미지/모듈17Img01.png?raw=true)

2. 아래와 같이 공격 경로 보기를 찾을 수 있습니다:
   ![이미지](../이미지/모듈17Img02.png?raw=true)
 
3. **"심각도가 높은 인터넷 노출 Azure VM은 Azure 키 볼트로 측면 이동을 허용합니다"**라는 이름으로 공격 경로를 찾아 클릭하여 엽니다
   ![이미지](../이미지/모듈17Img03.png?raw=true)
   ![이미지](../이미지/모듈17Img04.png?raw=true)
 
4. 여기에서 공격 경로와 공격 벡터에 관련된 리소스를 관찰할 수 있습니다. 공격 경로의 각 노드/요소를 클릭하면 오른쪽 패널에서 자세한 정보를 검토할 수 있습니다. 이 패널은 관련 인사이트와 귀중한 정보를 제공하여 공격이 어떻게 발생할 수 있는지, 관련 리소스를 통해 측면 움직임에 어떤 요인이 기여하는지 이해하는 데 도움이 됩니다.
   ![이미지](../이미지/모듈17Img05.png?raw=true)

5. 권장 사항에 업데이트를 적용하여 공격 경로를 해결합니다. 기본 공격 경로 보기에서 **수정** 탭을 찾아 클릭합니다. 이 작업은 공격 벡터를 완화하는 데 필요한 특정 보안 권장 사항을 표시하는 수정 섹션을 엽니다.
   ![이미지](../이미지/모듈17Img06.png?raw=true)

6. 환경에서 발견된 나머지 공격 경로를 탐색하고 완료합니다.

## Lab 4: Cloud Security Explorer를 위한 Build Query

1. 
