# Module 7 - External Attack Surface Management

### 외부 공격 표면 관리 (External Attack Surface Mgmt)?
외부 공격 표면(External Attack Surface)은 조직의 인터넷에 노출된 자산과 관련된 공격 포인트를 의미합니다. 이는 조직이 소유하거나 관리하는 모든 인터넷 연결 자산을 포함하며, 공격자가 악용할 수 있는 취약점과 노출을 포함합니다
* 인터넷에 노출된 자산: 웹 애플리케이션, 서드파티 종속성, 웹 인프라 등 조직이 소유한 모든 인터넷 연결 자산을 포함
* Shadow IT 및 레거시 서비스: 조직의 IT 부서가 모르는 자산과 여전히 온라인에서 운영되고 있는 레거시 서비스
   ![image](https://github.com/user-attachments/assets/ba6421b9-9aa9-41bf-8dab-51b014112921)

### EASM 동작 과정 및 원리
Microsoft Defender EASM은 Azure의 일부로, Azure에 앱으로 추가할 수 있습니다. 구독을 설정하고 앱을 실행하면, 자동화된 시스템이 조직과 관련된 자산을 식별합니다. 사용자는 도메인, ASM, IP 블록 등 “시드＂를 시스템에 입력할 수 있으며, 시스템은 며칠 동안 이 시드와 연결된 모든 자산을 식별합니다. 이를 통해 전체 공격 표면의 그림을 그릴 수 있습니다. 
   ![image](https://github.com/user-attachments/assets/1bac10c6-c180-4e8b-b4c6-0ab2a05051e0)

### 주요 개념 및 용어
* 발견 (Discovery): 공격 표면은 지속적으로 변화합니다. EASM은 지속적으로 새로운 자산을 식별하여 인벤토리에 추가하고 관리합니다.
* 인벤토리 (Inventory): 모든 자산을 검색할 수 있는 영역으로, 필터를 사용하여 자산을 검색할 수 있습니다.
* 자산 (Assets): IP 주소, IP 블록, 호스트, 도메인, 페이지, SSL 인증서, 자율 시스템 번호(ASN), Whois 연락처 등을 포함합니다.
* 필터 (Filter): 인벤토리에서 정의된 기준에 맞는 자산을 반환하는 검색 기능입니다.

### Lab 1: 리소스 생성하기
1. Azure portal > Defender EASM 검색 후 클릭 > + create
   ![image](https://github.com/user-attachments/assets/51d16f46-d335-4c4c-8840-dc9e9ef3712e)

2. 리소스 정보 기입 이후 Review + create 버튼 클릭
   ![image](https://github.com/user-attachments/assets/71fc7ed9-01f5-407e-a2e6-c4b2f65b22cb)

3. Go to Resoure 버튼 클릭
   ![image](https://github.com/user-attachments/assets/ac9f7f23-f2dd-4cd0-b17f-0c7e4e8f7d2b)

4. Create a custom attack surface 버튼 클릭
  ![image](https://github.com/user-attachments/assets/189d50ca-40e2-4858-ae81-29bb1ade8b9e)

5. Domains 항목에 우리 회사의 홈페이지 주소 www 제외하고 입력 > Next 버튼 클릭 > Confirm 버튼 클릭
  ![image](https://github.com/user-attachments/assets/9fe94270-669f-4d38-b692-3f306a2cfb2c)

6. 공격 표면을 형성하고 있으며 30일 Trial 기간이 시작되었다는 메시지 확인 (최대 48시간 이내에 공격 표면 스캔 완료)
  ![image](https://github.com/user-attachments/assets/59198b4d-6456-4a4b-82b6-431dc171e420)


### Lab 2: Discovery 그룹생성 및 실행 주기 설정
1. 왼쪽 창의 관리 아래에서 검색을 선택합니다.
  ![image](https://github.com/user-attachments/assets/c55f3d87-01bd-42a6-ae2f-0b530200f67b)

2. 이 검색 페이지에는 기본적으로 검색 그룹 목록이 표시됩니다. 이 목록은 플랫폼에 처음 액세스할 때 비어 있습니다. 첫 번째 검색을 실행하려면 검색 그룹 추가를 선택합니다.
  ![image](https://github.com/user-attachments/assets/7309bcfb-8d7a-4057-b010-71322c2dcf20)

3. 새 검색 그룹의 이름을 지정하고 설명을 추가합니다.
   ![image](https://github.com/user-attachments/assets/91fc346c-a548-4253-a901-4035a46d1060)

> ⭐ Tips: <br>
> Recurring frequeny 필드를 사용하면 지정된 시드와 관련된 새 자산을 지속적으로 스캔하여 이 그룹에 대한 검색 실행을 예약할 수 있습니다. Default값은 주간입니다. 조직의 자산이 정기적으로 모니터링 및 업데이트되도록 하려면 이 주기를 권장합니다.

> ⭐ Tips: <br>
> 일회성 검색 실행의 경우 ‘Never’을 선택합니다. 검색은 알려진 인프라와 관련된 새 자산을 지속적으로 검색하도록 설계되므로 기본 주기를 주간으로 유지하는 것이 좋습니다. 나중에 검색 그룹 세부 정보 페이지에서 "편집" 옵션을 선택하여 recurring frequency를 편집할 수 있습니다.

4-1. Quick Start를 통해 Seed 설정하기 (Option 1) 

이 Discovery group에 사용할 시드를 선택합니다. 빠른 시작 옵션을 사용하면 미리 채워진 공격 표면 목록에서 조직을 검색할 수 있습니다. 조직에 속한 알려진 자산을 기반으로 검색 그룹을 빠르게 만들 수 있습니다.
  ![image](https://github.com/user-attachments/assets/77c4e1a0-2e37-4dc5-bfa3-764d1fe750c6)
  ![image](https://github.com/user-attachments/assets/b9d084f1-c4d4-4663-97b1-a64a442dc3be)

4-2. 시드 수동 설정하기 (Option 2)

Defender EASM은 조직 이름, 도메인, IP 블록, 호스트, 메일 연락처, ASN 및 WhoIs 조직을 시드 값으로 허용합니다.
또한 자산 검색에서 제외할 엔터티를 지정하여 검색된 경우 인벤토리에 추가되지 않도록 할 수도 있습니다. 예를 들어 제외는 중앙 인프라에 연결될 가능성이 높지만 조직에 속하지 않는 자회사가 있는 조직에 유용합니다. 시드 선택 후  Review + Create 클릭합니다. 
  ![image](https://github.com/user-attachments/assets/3fe0a14f-0f2b-407c-832f-332fccc8a55a)

5. 그룹 정보 및 시드 목록을 검토 후, create+run을 클릭합니다.
  ![image](https://github.com/user-attachments/assets/da54f3a1-fdbe-41b8-8445-2a2efa88b2af)

6. Discovery group이 새롭게 생성된 것을 확인 할 수 있습니다. 
  ![image](https://github.com/user-attachments/assets/0160f3a4-cd87-4428-9b18-59885eaf8906)


### Lab 3: 정책엔진 자동화

#### 정책 엔진?
EASM 사용자가 사전 정의된 매개변수에 따라 특정 작업을 자동화할 수 있도록 합니다. 이를 통해 자산에 레이블을 적용하거나 상태를 변경하는 등의 작업을 자동화하여 공격 표면을 관리할 수 있습니다.

* 주요 기능
  * 레이블 추가 또는 제거: 자산에 레이블을 추가하거나 제거할 수 있습니다.
  * 외부 ID 설정: 자산에 외부 ID를 설정하여 더 쉽게 추적하고 관리할 수 있습니다.
  * 자산 상태 설정: 자산의 상태를 설정하여 현재 상태를 반영합니다.
  * 인벤토리에서 제거: 필요에 따라 자산을 인벤토리에서 제거할 수 있습니다.
  * 정책이 정의되면 자동으로 실행되어 인벤토리가 사용자의 특정 요구에 따라 분류되도록 합니다. 이를 통해 최소한의 수작업으로 비즈니스 컨텍스트를 대량으로 인벤토리에 적용할 수 있습니다


1. 정책 추가하기

Defender EASM 리소스 내 왼쪽 탐색 창의 관리 섹션에서 정책을 선택하여 정책 페이지로 이동합니다. + 정책 추가를 선택합니다. 팝업된 오른쪽 창에서 Query가 없는 상태이므로, query를 생성합니다.
  ![image](https://github.com/user-attachments/assets/f91be512-8530-4862-82f0-8ee9a5f63362)

2. Query 생성하기

자산 상태가 "Requires Investigation"인 자산을 필터링하고, 해당 자산을 인벤토리에서 제거하는 작업을 수행합니다. 이를 통해 추가 조사가 필요한 자산을 효과적으로 관리하고, 인벤토리를 최신 상태로 유지할 수 있습니다.
  ![image](https://github.com/user-attachments/assets/680954a8-667a-412c-b490-7f98926c9752)

3. 생성한 query와 action 값을 넣고 생성합니다.
   ![image](https://github.com/user-attachments/assets/375d2196-2e1e-4613-b7da-964d52513a33)

4. 생성된 정책엔진 확인
  ![image](https://github.com/user-attachments/assets/82b470cb-def3-4501-98c5-133b290a757d)

