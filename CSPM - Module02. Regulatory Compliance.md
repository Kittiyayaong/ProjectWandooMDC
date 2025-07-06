# Module 02 - Regulatory Compliance

## Wandoo-KT는 이번 랩에서는 Lab 3~5만 진행합니다.

## 목표
Microsoft Defender for Cloud의 규정 준수 대시보드를 통해 특정 표준에 대한 리소스의 상태를 평가하여 고객이 이러한 요구 사항을 충족할 수 있도록 지원합니다

### Regulatory Compliance란? <br>
규정 준수 기능은 클라우드 환경이 다양한 규정 준수 표준을 충족하는지 평가하고 모니터링하는 데 중점을 둡니다. 이 기능은 클라우드 환경의 보안 상태를 평가하고, 다양한 규정 준수 표준에 대한 준수 여부를 모니터링합니다.

* 기능:
  * 보안 표준 할당 및 평가.
  * 규정 준수 상태 모니터링.
  * 규정 준수 대시보드 제공.

### Lab 요약

| **Lab 번호** | **제목**               | **목표**                                         | **주요 내용**                                                                                                                                 | **실무 가치**                                 |
| ---------- | -------------------- | ---------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| **Lab 1**  | Adding new standards | Subscription에 **새 규정 준수 표준(CIS Benchmark)** 추가 | - Cloud Security ➔ Regulatory Compliance ➔ Manage compliance policies<br>- CIS Benchmark v2.0.0 할당<br>- Parameter 설정(예: Key rotation 30일) | 클라우드 자산을 **글로벌 보안 표준에 매핑**                |
| **Lab 2**  | 벤치마크 보고서 다운로드        | 규정 준수 상태를 **CSV/PDF 보고서**로 내보내기                | - CIS Benchmark 페이지 ➔ Download CSV 선택<br>- 평가된 상태 요약 확인                                                                                   | **감사 대응**, 경영진/보안팀 보고                     |
| **Lab 3**  | Custom Standard 생성   | 조직 자체 **커스텀 규정 준수 표준 생성**                      | - +Create ➔ Custom Standard 생성<br>- EDR Recommendations 추가 ➔ Review + Create                                                              | **고객사 맞춤 규정 준수 프레임워크** 구축                 |
| **Lab 4**  | 감사 보고서 다운로드          | Microsoft 감사 보고서 **(Audit Report)** 다운로드       | - Regulatory Compliance ➔ Audit Report 클릭<br>- 예: IRS Safeguards Notification Form                                                        | **감사 증빙 문서 확보**                           |
| **Lab 5**  | 시간에 따른 규정 준수 통합 문서   | 규정 준수 상태를 **시간 경과별로 추적**                       | - Continuous Export ➔ Log Analytics로 내보내기 설정<br>- Regulatory compliance 데이터 선택 ➔ Streaming + Snapshots 활성화                                | 규정 준수 **추세 분석, Power BI, Sentinel 연계** 가능 |


---

### Lab 1: Adding new standards in Azure and multicloud

1.	MDC Console에서 Cloud Security >  Regulatory Compliance > 상단에 Manage compliance policies > 테스트 대상인 Subscription > Security policies로 이동합니다.

> ⭐ Tips: <br>
AWS 또는 GCP에서 표준을 할당하려면 AWS 또는 GCP 연결을 선택한 다음 **Security Policy**로 직접 이동합니다. 세 클라우드 모두에서 사용 가능한 규정 준수 표준은 [여기](https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-regulatory-compliance-standards#available-compliance-standards) 에 문서화되어 있습니다.

3. *CIS Microsoft Azure Foundations Benchmark v2.0.0*를 찾아 클릭합니다. 

> ⭐ Tips: <br>
> * **Audit effect**: 리소스가 특정 정책 정의를 준수하지 않을 경우, 정책은 해당 리소스를 비준수(non-compliant)로 표시하고 활동 로그에 경고를 생성하지만 실제 리소스에 대해서는 조치를 취하지 않습니다. 감사 효과에 대한 자세한 내용은 이 [페이지](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/effect-audit)를 방문하세요.
> * **Manual effect**: 일부 작업이나 작업을 자동화할 수 없거나 리소스의 규정 준수 상태를 업데이트해야 하는 경우 수동 인증이 필요할 수 있습니다. 이에 대해 자세히 알아보려면 이 [페이지](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/effect-manual) 를 확인하세요.

4. **rotation** 을 검색하여 **Keys should have a rotation policy ensuring that their rotation is scheduled within the specified number of days after creation.** 를 확인해보면, **Additional parameters** 항목값이 **Configured**로 설정되어있음을 확인할 수 있습니다.
5. 우측의 점 3개를 클릭해서 **view policy definition**를 확인합니다.
<img src="https://github.com/user-attachments/assets/027ea85e-5303-4966-aec6-2a5b03d53b0e" alt="image" width="700" height="150">
   
6. Assign policy를 클릭하여, Scope와 definition을 설정합니다. 
<img src="https://github.com/user-attachments/assets/eaa2038d-395d-4ccd-a6bf-c537f4824c4d" alt="image" width="700" height="300">

7. Standard를 Scope(구독 또는 관리 그룹)에 할당할 때, 이 정책 정의에 따라 키를 회전할 최대 일수를 입력하라는 Parameter설정에 30으로 기입합니다. 기입 후 review + Create를 클릭하여 설정을 완료합니다.
<img src="https://github.com/user-attachments/assets/d26c0d15-35cc-4763-859e-9dfb6bfb38c5" alt="image" width="400" height="150">
9.  전 페이지로 돌아가서 **CIS Microsoft Azure Foundations Benchmark v2.0.0** 의 토글 **On**으로 클릭합니다.
10. 몇 시간 후, 이 새로운 표준은 기본 MCSB 옆에 있는 **Regulatory Compliance** 대시보드에 표시됩니다.

> ❗ Important: <br>
> 변경 사항이 적용될 때까지 2-3시간 소요됩니다. 

---

### Lab 2: 벤치마크 보고서 
1. Lab 1의 Standard 페이지로 이동하여, *CIS Microsoft Azure Foundations Benchmark v2.0.0*를 선택합니다. 
2. 규제 표준 준수 상태를 PDF 보고서 또는 CSV 파일로 내보낼 수 있습니다. 상단 메뉴 모음에서 **Downloaded CSV file**를 선택합니다.
3. 파일이름 및 파일형식을 지정하여 컴퓨터에 저장됩니다. **CIS Microsoft Azure Foundations Benchmark v2.0.0**을 열고 규정 준수 보고서를 살펴보세요 - 이 보고서는 해당 평가가 관련된 제어 장치에 매핑될 때의 상태를 요약합니다.

--- 

### Lab 3: Custom Standard 생성하기 
별도의 "벤치마크"를 생성할 수 있으며, "Standard"이라는 용어로 사용됩니다. Standard는 하나 이상의 권장 사항으로 구성될 수 있습니다.
사용자 지정 표준을 만들면 Defender for Cloud를 사용하여 보안 정책으로 추가할 수 있으며, 이는 두 가지 주요 이점을 제공합니다:
* 보안 요구 사항이 있는 경우 추천 목록에 맞춤형 추천으로 표시
* 규정 준수 대시보드를 사용하여 규정 준수 상태를 추적하는 방법을 제시

1.	MDC Console에서 Cloud Security >  Regulatory Compliance > 상단에 Manage compliance policies > 테스트 대상인 Subscription > Security policies로 이동합니다.
2.	상단에 + Create를 클릭하여 **Custom Standard**를 생성합니다. 
<img src="https://github.com/user-attachments/assets/c08a09e7-5f87-4742-9b6a-6c33a519a8e3" alt="image" width="400" height="200">

3. EDR 관련된 Recommendations를 추가 후 Review + Create를 합니다. 
<img src="https://github.com/user-attachments/assets/899b8d12-dc00-4dbe-a45c-e59078d1a3ad3" alt="image" width="700" height="150">

4. 새로 생성된 표준이 구독에 적용되는지 확인하려면 Regulatory Compliance 대쉬보드에서 **Status**로 정렬하세요.
![module4_customstandard](https://github.com/Azure/Microsoft-Defender-for-Cloud/assets/45104504/aba2680c-9d1e-4fae-bb98-63ea3627c9a4)

---

### Lab 4: Azure 감사 보고서 
Microsoft Defender for Cloud에서는 규정 준수 표준에 대한 감사 보고서를 쉽게 작성하고 다운로드할 수 있습니다.

1.	MDC Console에서 Cloud Security >  Regulatory Compliance > 상단에 Audit Report 클릭
![image](https://github.com/user-attachments/assets/ead116ef-aed5-436d-b3ab-01065e61901f)

3.	필요한 내용을 다운로드받습니다. ex) Azure 2021 IRS Safeguards Cloud Computing Notification Form

---

### Lab 5: 시간에 따른 규정 준수 통합 문서

시간 경과에 따른 준수 통합 문서는 대시보드에 추가하는 다양한 표준을 사용하여 시간 경과에 따른 준수 상태를 추적합니다. 자세한 내용은 [여기](https://learn.microsoft.com/en-us/azure/defender-for-cloud/custom-dashboards-azure-workbooks#compliance-over-time-workbook). 이 워크북을 활용하려면 먼저 연속 내보내기를 구성하여 Log Analytics 워크스페이스로 데이터를 내보내야 합니다.

1.	MDC Console에서 Management > Environment Settings > 하단에 테스트에 사용할 subscription클릭
![image](https://github.com/user-attachments/assets/e5b9d439-a603-4a69-afb6-dc1b0c2502fc)

2. 왼쪽에서 **Continuous Export** 클릭 후 **Log Analytics workspace**으로 이동 
![image](https://github.com/user-attachments/assets/e858eec8-1d7a-4050-afca-8bcc159a4bd2)

3. Export enabled 토글을 **On**으로 설정 후, 하단의 Exported data type에서 **Regulatory compliance** 클릭 후 **Select All**
![image](https://github.com/user-attachments/assets/7281e452-20fc-42d0-b39f-55c54dc54a3b)

4. Export Frequency는 **Streaming updates**와 **Snapshots** 모두 박스를 클릭하여 활성화합니다.
5. Export Configuration에서 이전에 생성한 리소스 그룹을 선택합니다.
6. 저장 시 Sentinel 알림 커넥터가 활성화가 필요하므로, 이번 Lab에서는 저장하지 않습니다.  

### 🔗 [다음 Lab으로 이동하기 »](https://github.com/Kittiyayaong/ProjectWandooMDC/blob/main/CSPM%20-%20Module03.%20Secure%20Posture.md)
