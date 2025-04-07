# Module 02 - Regulatory Compliance

## 목표
Microsoft Defender for Cloud의 규정 준수 대시보드를 통해 특정 표준에 대한 리소스의 상태를 평가하여 고객이 이러한 요구 사항을 충족할 수 있도록 지원합니다

> ⭐ Tips: <br>
> 규정 준수 기능은 클라우드 환경이 다양한 규정 준수 표준을 충족하는지 평가하고 모니터링하는 데 중점을 둡니다. 이 기능은 클라우드 환경의 보안 상태를 평가하고, 다양한 규정 준수 표준에 대한 준수 여부를 모니터링합니다.

> 기능:
> * 보안 표준 할당 및 평가.
> * 규정 준수 상태 모니터링.
> * 규정 준수 대시보드 제공.

### Lab 1: Adding new standards in Azure and multicloud


1.	MDC Console에서 Cloud Security >  Regulatory Compliance로 이동합니다. 상단에 **Manage compliance policies** 를 클릭하여 테스트 대상인 Subscription을 클릭합니다. 
<br> Note: <br>
If you want to assign a standard in AWS or GCP, choose an AWS or GCP connection and then go directly to **Security policies** on the left. Available compliance standards in all three clouds are documented [here](https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-regulatory-compliance-standards#available-compliance-standards). 
<br> Another note: <br>
Modules [10](https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Labs/Modules/Module-10-GCP.md) and [11](https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Labs/Modules/Module-11-AWS.md) will walk through creating those multicloud connectors. Feel free to skip to those modules and then come back. 
3.  Select **Security policies**. 
4.	Under the **Standards** tab, look for *CIS Microsoft Azure Foundations Benchmark v2.0.0*.
5.  Select the standard. 
6.  Notice the number of **audit** and **manual** policy definitions. 
**Audit effect**: When a resource does not adhere to the specific policy definition, Policy will mark said resource as **non-compliant** and create a warning in the activity log but it won't take action on the actual resource. Visit this[page](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/effect-audit) to learn more about the audit effect. 
**Manual effect**: Sometimes, when some operations or tasks cannot be automated or requires updating of resource's compliance state, manual attestation is required. To learn more about this, check out this [page](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/effect-manual). 
7.  Search for **rotation** in the search box. **Keys should have a rotation policy ensuring that their rotation is scheduled within the specified number of days after creation.** should come up. Notice **Additional parameters** is set to **Configured**. 
8.  Click on the ellipses to **view policy definition**. 
When assigning this standard to your scope (subscription or management group), you will be asked to input a value of the maximum days to rotate keys, per this policy definition. 
9.  Navigate back to the **Standards** page and click toggle **On** for *CIS Microsoft Azure Foundations Benchmark v2.0.0*. 
10.  Input the value that adheres to your organization's policy or, for this lab purpose only, input **30**. 
11.  In a few hours, this new standard will display in the **Regulatory Compliance** dashbard, next to the default MCSB. 
