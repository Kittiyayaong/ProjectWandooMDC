# Module - Microsoft Defender for Cloud database protection

## Objectives

이 연습은 MDC의 데이터베이스 보호 계획을 안내합니다. Defender for Cloud의 데이터베이스 보호에는 보호하려는 데이터베이스 유형에 따라 네 가지 종류가 있습니다.
1. Defender for SQL PaaS (SQL on Azure VM): 이 계획에 대한 취약성 평가 및 위협 보호가 제공됩니다. 자세한 내용은 [여기](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-sql-introduction) 에서 확인하세요.
2. Defender for SQL on machines (SQL servers hosted on premise, in Azure, AWS or GCP): 이 요금제에는 Microsoft 모니터링 에이전트(MMA) 대신 Azure 모니터링 에이전트(AMA)가 필요합니다. 이에 대한 자세한 내용은 [여기](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-sql-usage) 에서 확인할 수 있습니다. Iasa SQL 서버를 보호하기 위해 취약점 평가 및 이상 활동 탐지가 가능합니다.
3. Defendr for Open-source relational database: 비정상적인 활동을 감지하여 PostgreSQL, MySQL 및 MariaDB 리소스를 보호하세요. 이러한 보안 경고에 대한 자세한 내용은 [여기](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-databases-introduction) 에서 확인하세요.
4. Defender for Cosmos DB (NoSQL): SQL 주입, 손상된 신원 또는 잠재적 악용과 같은 잠재적인 Cosmos DB 계정에 대한 위협을 감지합니다. CosmosDB 보호에 대한 자세한 내용은 [여기](https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-defender-for-cosmos) 에서 확인하세요.
   
### Lab 1. Azure VM에 SQL 서버를 생성하고 경고 검증 및 알림을 검증하고 알림을 검증합니다.

특정 구독에 대한 Defender Plan을 사용하기

1. MDC > Environment Settings > 관련 테스트 Subscription > Database > Setesc types > **SQL servers on machines** 가 `On` 상태인지 확인합니다.
6. 모니터링 범위 열에서 **Settings**을 클릭합니다:
    > 기존 It is *strongly* recommended to use the new Azure Monitoring Agent for SQL server on machines experience over the legacy Log Analytics/MMA option.
    1. Ensure that `Azure Monitoring Agent for SQL server on machines` is toggled to `On`  
    2. (Optional): In the `Configuration` column, you have the option of configuring which Log Analytic Workspace to use as well as the ability to register Azure SQL server instances by enabling SQL IaaS extension automatic registration.  
7. Click **Continue** and **Save**.

Now all your existing and upcoming Azure SQL servers on machines are protected.

