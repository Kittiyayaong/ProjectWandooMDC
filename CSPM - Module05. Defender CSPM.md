# Module 5 – Defender CSPM  

## 목표
이 연습에서는 Defender for CSPM를 활성화하고 CSPM 기능을 활용하는 방법을 배우게 됩니다.

---

Wandoo-kt에서는 Lab 2번만 진행합니다.

---

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

1. MDC > general > Attach Path Analysis로 이동합니다. 

   ![image](https://github.com/user-attachments/assets/9ceff19c-142a-4873-ad33-47c8376c5f3b)

2. **"심각도가 높은 인터넷 노출 Azure VM은 Azure 키 볼트로 측면 이동을 허용합니다"**라는 이름으로 공격 경로를 찾아 클릭하여 엽니다

   ![image](https://github.com/user-attachments/assets/ecf8c76a-766e-4865-a704-472edfecab51)

   ![image](https://github.com/user-attachments/assets/a6db3b99-ccae-4a23-8c1f-e52b37087bfb)

 
3. 공격 경로와 관련된 리소스를 확인할 수 있습니다. 공격 경로의 각 노드/요소를 클릭하면 오른쪽 패널에서 자세한 정보를 검토할 수 있습니다. 이 패널은 관련 인사이트와 정보를 제공하여 공격이 어떻게 발생할 수 있는지, 관련 리소스를 통해 이해하는 데 도움이 됩니다.


   ![image](https://github.com/user-attachments/assets/7bf07c4c-f5f0-4c40-a3ce-5f365eb16d7f)


5. 권장 사항에 업데이트를 적용하여 공격 경로를 해결합니다. 기본 공격 경로 보기에서 **수정** 탭을 찾아 클릭합니다. 이 작업은 공격 벡터를 완화하는 데 필요한 특정 보안 권장 사항을 표시하는 수정 섹션을 엽니다.

   ![image](https://github.com/user-attachments/assets/431b075e-15a6-4b5e-a100-37d8b9023799)


7. 발견된 나머지 공격 경로를 탐색하고 완료합니다.

## Lab 3: Cloud Security Explorer를 위한 Build Query

1. MDC > Cloud Security Explorer로 이동
2. “Internet exposed VMs with high severity vulnerabilities” 템플릿을 찾아 클릭하면, 심각도가 높은 취약성을 가진 VM 목록을 찾을 수 있습니다. 
   ![image](https://github.com/user-attachments/assets/a2aae948-0a25-4d55-82cd-6b3e1a6a9edc)

   ![image](https://github.com/user-attachments/assets/a3e2bb0e-ddd8-4d49-a5ca-ed0fccdf3339)


4. 쿼리 빌더를 사용하여 자신만의 쿼리를 탐색하고 구축할 수도 있습니다: 드롭다운에서 계산 > 가상 머신 > Azure 가상 머신을 선택합니다.

   ![image](https://github.com/user-attachments/assets/b12fa514-9065-4076-a3eb-8a63a2254ba6)

5. +를 클릭하고 선택 조건에서 Security > **vulnerable to remote code execution** 을 선택합니다.

   ![image](https://github.com/user-attachments/assets/714affa6-28f0-47d6-a50c-adc2edfef5d5)

6. 특정 취약점이 있는 가상 머신의 환경을 살펴봅니다.

   ![image](https://github.com/user-attachments/assets/18b82c97-e169-45f7-b5ec-3580a1222c00)

   ![image](https://github.com/user-attachments/assets/27818199-34d8-445c-95d4-7c6db382c53f)

7. 인터넷에 노출된 스토리지 계정 환경을 살펴봅니다.

   ![image](https://github.com/user-attachments/assets/6ab575e1-81af-4eba-bd30-b2b1bce930d9)

   ![image](https://github.com/user-attachments/assets/3558ad07-a951-4967-b0d4-f255aca58389)


### 🔗 [다음 Lab으로 이동하기 »](https://github.com/Kittiyayaong/ProjectWandooMDC/blob/main/CSPM%20-%20Module06.%20Data%20security%20posture%20management.md)
