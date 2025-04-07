# Module 02 - Regulatory Compliance

## 목표
Microsoft Defender for Cloud의 규정 준수 대시보드를 통해 특정 표준에 대한 리소스의 상태를 평가하여 고객이 이러한 요구 사항을 충족할 수 있도록 지원합니다

### Regulatory Compliance란? <br>
규정 준수 기능은 클라우드 환경이 다양한 규정 준수 표준을 충족하는지 평가하고 모니터링하는 데 중점을 둡니다. 이 기능은 클라우드 환경의 보안 상태를 평가하고, 다양한 규정 준수 표준에 대한 준수 여부를 모니터링합니다.

* 기능:
  * 보안 표준 할당 및 평가.
  * 규정 준수 상태 모니터링.
  * 규정 준수 대시보드 제공.

### Lab 1: Adding new standards in Azure and multicloud

1.	MDC Console에서 Cloud Security >  Regulatory Compliance > 상단에 Manage compliance policies > 테스트 대상인 Subscription > Security policies로 이동합니다.

> ⭐ Tips: <br>
AWS 또는 GCP에서 표준을 할당하려면 AWS 또는 GCP 연결을 선택한 다음 **Security Policy**로 직접 이동합니다. 세 클라우드 모두에서 사용 가능한 규정 준수 표준은 [여기](https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-regulatory-compliance-standards#available-compliance-standards) 에 문서화되어 있습니다.

3. *CIS Microsoft Azure Foundations Benchmark v2.0.0*를 찾아 클릭합니다. 
5. Effect항목에서 **audit** 과 **manual**로 설정된 내용을 확인합니다. 
<img src="https://github.com/user-attachments/assets/1b5f7e6b-014f-42cc-abd2-5b76072814ed" alt="image" width="700" height="300">

> ⭐ Tips: <br>
> * **Audit effect**: 리소스가 특정 정책 정의를 준수하지 않을 경우, 정책은 해당 리소스를 비준수(non-compliant)로 표시하고 활동 로그에 경고를 생성하지만 실제 리소스에 대해서는 조치를 취하지 않습니다. 감사 효과에 대한 자세한 내용은 이 [페이지](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/effect-audit)를 방문하세요.
> * **Manual effect**: 일부 작업이나 작업을 자동화할 수 없거나 리소스의 규정 준수 상태를 업데이트해야 하는 경우 수동 인증이 필요할 수 있습니다. 이에 대해 자세히 알아보려면 이 [페이지](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/effect-manual) 를 확인하세요.

4. **rotation** 을 검색하여 **Keys should have a rotation policy ensuring that their rotation is scheduled within the specified number of days after creation.** 를 확인해보면, **Additional parameters** 항목값이 **Configured**로 설정되어있음을 확인할 수 있습니다.
5. 우측의 점 3개를 클릭해서 **view policy definition**를 확인합니다.
<img src="https://github.com/user-attachments/assets/027ea85e-5303-4966-aec6-2a5b03d53b0e" alt="image" width="700" height="150">
   
When assigning this standard to your scope (subscription or management group), you will be asked to input a value of the maximum days to rotate keys, per this policy definition. 
10.  Navigate back to the **Standards** page and click toggle **On** for *CIS Microsoft Azure Foundations Benchmark v2.0.0*. 
11.  Input the value that adheres to your organization's policy or, for this lab purpose only, input **30**. 
12.  In a few hours, this new standard will display in the **Regulatory Compliance** dashbard, next to the default MCSB. 
