# ☁️ Azure Security 서비스 – CSPM & CWPP 여부 구분

| **카테고리** | **서비스/기능** | **CSPM** | **CWPP** | **설명** |
|--|--|--|--|--|
| **Identity & Access Management** | Azure Active Directory (Entra ID) | ❌ | ❌ | IAM, CSPM/CWPP 직접 기능 아님 |
| | Privileged Identity Management (PIM) | ❌ | ❌ | Privileged Access mgmt |
| | Managed Identities | ❌ | ❌ | Workload Identity Mgmt |
| | Azure AD B2B/B2C | ❌ | ❌ | External Id 관리 |
| | | | | |
| **Network Security** | NSG | ❌ | ❌ | 네트워크 보안 그룹 |
| | Azure Firewall | ❌ | ❌ | L3-L7 Firewall |
| | Azure Firewall Premium | ❌ | ❌ | TLS Inspection, IDPS |
| | Web Application Firewall (WAF) | ❌ | ❌ | App Gateway 보호 |
| | DDoS Protection | ❌ | ❌ | L3-L7 DDoS 완화 |
| | | | | |
| **Data Security** | Azure Key Vault | ❌ | ❌ | Secrets mgmt |
| | Azure Confidential Computing | ❌ | ✅ | Confidential VM = Workload Protection |
| | Azure Storage Encryption | ❌ | ❌ | Data encryption |
| | SQL TDE / Always Encrypted | ❌ | ❌ | DB encryption |
| | | | | |
| **Threat Protection & SIEM** | Microsoft Sentinel | ❌ | ❌ | SIEM/SOAR |
| | Defender for Identity | ❌ | ❌ | AD Threat Protection |
| | Defender for Endpoint | ❌ | ✅ | EDR = Endpoint CWPP |
| | Defender for Office 365 | ❌ | ❌ | Email Protection |
| | | | | |
| **Compliance & Governance** | Azure Policy | ✅ | ❌ | CSPM 핵심 (Posture 관리) |
| | Blueprints (이전) | ✅ | ❌ | CSPM 거버넌스 배포 |
| | Management Groups | ✅ | ❌ | CSPM 계층 구조 |
| | Cost Management + Budgets | ❌ | ❌ | 비용 관리 |
| | | | | |
| **Application & DevSecOps** | Defender for DevOps | ✅ | ✅ | DevOps 코드+Pipeline posture 평가 및 보호 |
| | App Service Environment v3 | ❌ | ✅ | App PaaS Isolation = Workload Protection |
| | Azure Static Web Apps Auth | ❌ | ❌ | Static App 인증 |
| | API Management Security | ❌ | ❌ | API Gateway security |

---

## ✅ **요약**

✔️ **CSPM**
- Azure Policy
- Blueprints
- Management Groups
- Defender for DevOps (코드 posture 관리 측면)

✔️ **CWPP**
- Defender for Endpoint (EDR)
- Azure Confidential Computing (Confidential VM)
- Defender for DevOps (CI/CD workload protection 측면)
- App Service Environment v3 (PaaS workload isolation)

❌ **해당 없음**
- IAM, 대부분 Network Security, Data encryption, SIEM/SOAR 단독 서비스


