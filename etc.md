# ☁️ Azure Security 서비스 – CSPM 여부 구분

| **카테고리** | **서비스/기능** | **CSPM 여부** | **설명** |
|--|--|--|--|
| **Identity & Access Management** | Azure Active Directory (Entra ID) | ❌ | IAM, CSPM 직접 기능 아님 |
| | Privileged Identity Management (PIM) | ❌ | IAM, CSPM 직접 기능 아님 |
| | Managed Identities | ❌ | Workload identity, CSPM 아님 |
| | Azure AD B2B/B2C | ❌ | External Id 관리, CSPM 아님 |
| | | | |
| **Network Security** | NSG | ❌ | 네트워크 보안 그룹, CSPM 아님 |
| | Azure Firewall | ❌ | 네트워크 보안, CSPM 아님 |
| | Azure Firewall Premium | ❌ | 네트워크 보안, CSPM 아님 |
| | Web Application Firewall (WAF) | ❌ | L7 Protection, CSPM 아님 |
| | DDoS Protection | ❌ | 네트워크 보호, CSPM 아님 |
| | | | |
| **Data Security** | Azure Key Vault | ❌ | Secrets mgmt, CSPM 아님 |
| | Azure Confidential Computing | ❌ | Confidentiality, CSPM 아님 |
| | Azure Storage Encryption | ❌ | Data encryption, CSPM 아님 |
| | SQL TDE / Always Encrypted | ❌ | DB encryption, CSPM 아님 |
| | | | |
| **Threat Protection & SIEM** | Microsoft Sentinel | ❌ | SIEM/SOAR, CSPM 아님 |
| | Defender for Identity | ❌ | ID Threat Protection, CSPM 아님 |
| | Defender for Endpoint | ❌ | EDR, CSPM 아님 |
| | Defender for Office 365 | ❌ | Email Protection, CSPM 아님 |
| | | | |
| **Compliance & Governance** | Azure Policy | ✅ | **CSPM 핵심 기능 (보안 posture 관리)** |
| | Blueprints (이전) | ✅ | CSPM 거버넌스 배포 도구 |
| | Management Groups | ✅ | CSPM 거버넌스 계층 구조 |
| | Cost Management + Budgets | ❌ | 비용 관리, CSPM 아님 |
| | | | |
| **Application & DevSecOps** | Defender for DevOps | ✅ | CSPM+CNAPP DevOps posture 평가 |
| | App Service Environment v3 | ❌ | PaaS isolation, CSPM 아님 |
| | Azure Static Web Apps Auth | ❌ | Static App Auth, CSPM 아님 |
| | API Management Security | ❌ | API Gateway security, CSPM 아님 |

---

## ✅ **요약**

✔️ **CSPM 범주**
- **Azure Policy**
- **Blueprints (Template Spec)**
- **Management Groups**
- **Defender for DevOps (코드 & 파이프라인 posture)**

❌ **CSPM이 아닌 항목**
- IAM, Network Security, Threat Protection, Data Security 서비스는 CSPM이 아닌 **별도 보안 컨트롤**.

---

필요하면 각 CSPM 기능별 **실습 Lab 설계**도 이어서 만들어드리겠습니다.
