---
title: ALTER DATABASE 호환성 수준(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COMPATIBILITY_LEVEL_TSQL
- COMPATIBILITY_LEVEL
dev_langs:
- TSQL
helpviewer_keywords:
- 80 compatibility level
- ALTER DATABASE statement, compatibility levels
- 90 compatibility level
- compatibility levels [SQL Server]
- 100 compatibility level
- db compatibility level
- db compat level
ms.assetid: ca5fd220-d5ea-4182-8950-55d4101a86f6
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1980e9c96e568352fe616b6de8a6c7320c3d6c86
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79288667"
---
# <a name="alter-database-transact-sql-compatibility-level"></a>ALTER DATABASE(Transact-SQL) 호환성 수준

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

지정된 버전의 SQL 엔진과 호환되도록 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 쿼리 처리 동작을 설정합니다. 다른 ALTER DATABASE 옵션은 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  

구문 표기 규칙에 대한 자세한 내용은 [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)을 참조하십시오.

## <a name="syntax"></a>구문

```
ALTER DATABASE database_name
SET COMPATIBILITY_LEVEL = { 150 | 140 | 130 | 120 | 110 | 100 | 90 }
```

## <a name="arguments"></a>인수

*database_name* 수정할 데이터베이스의 이름입니다.

COMPATIBILITY_LEVEL { 150 | 140 | 130 | 120 | 110 | 100 | 90 | 80 } 데이터베이스가 호환되도록 설정할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전입니다. 다음 호환성 수준 값을 구성할 수 있습니다(모든 버전이 위의 나열된 호환성 수준을 모두 지원하지는 않음).

<a name="supported-dbcompats"></a>

|Product|데이터베이스 엔진 버전|기본 호환성 수준 지정|지원되는 호환성 수준 값|
|-------------|-----------------------------|-------------------------------------|------------------------------------------|
|[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]|15|150|150, 140, 130, 120, 110, 100|
|[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|14|140|140, 130, 120, 110, 100|
|[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 단일 데이터베이스/탄력적 풀|12|150|150, 140, 130, 120, 110, 100|
|[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 관리되는 인스턴스|12|150|150, 140, 130, 120, 110, 100|
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|13|130|130, 120, 110, 100|
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|12|120|120, 110, 100|
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|11|110|110, 100, 90|
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|10.5|100|100, 90, 80|
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|10|100|100, 90, 80|
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|9|90|90, 80|
|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]|8|80|80|

> [!IMPORTANT]
> SQL Server 및 Azure SQL Database의 데이터베이스 엔진 버전 번호는 서로 비교할 수 없으며 이러한 개별 제품에 대한 내부 빌드 번호에 해당합니다. Azure SQL Database용 데이터베이스 엔진은 SQL Server 데이터베이스 엔진과 동일한 코드 베이스를 기준으로 합니다. 가장 중요한 사실은 Azure SQL Database의 데이터베이스 엔진에 항상 최신 SQL 데이터베이스 엔진 비트가 있다는 것입니다. Azure SQL Database 버전 12는 SQL Server 버전 15보다 최신 버전입니다.

## <a name="remarks"></a>설명
모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 경우 기본 호환성 수준은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 버전과 관련됩니다. 새로운 데이터베이스는 **model** 데이터베이스의 호환성 수준이 이보다 낮지 않은 한 이 수준으로 설정됩니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 첨부되거나 복구된 데이터베이스를 업그레이드할 때 데이터베이스의 호환성 수준이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 해당 인스턴스에 대해 허용된 최소 이상이면 기존 호환성 수준이 유지됩니다. [!INCLUDE[ssde_md](../../includes/ssde_md.md)]에 의해 허용된 수준보다 낮은 호환성 수준으로 데이터베이스를 이동하면 데이터베이스를 허용된 가장 낮은 호환성 수준으로 자동 설정합니다. 이는 시스템 및 사용자 데이터베이스 모두에 적용됩니다.

데이터베이스가 연결 또는 복원된 경우, 그리고 현재 위치 업그레이드 이후에 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]에서 아래 동작이 예상됩니다.

- 사용자 데이터베이스의 호환성 수준이 업그레이드 이전에 100 이상이었다면 업그레이드 후에도 동일하게 유지됩니다.
- 업그레이드 이전에 사용자데 이터베이스의 호환성 수준이 90이었다면 업그레이드된 데이터베이스에서는 호환성 수준이 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]에서 지원되는 가장 낮은 호환성 수준인 100으로 설정됩니다.
- tempdb, 모델, msdb 및 리소스 데이터베이스의 호환성 수준이 제공된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 버전의 기본 호환성 수준으로 설정됩니다. 
- master 시스템 데이터베이스는 업그레이드 이전의 호환성 수준으로 유지됩니다.

데이터베이스의 호환성 수준을 변경하려면 `ALTER DATABASE`를 사용합니다. 데이터베이스에 대한 새로운 호환성 수준 설정은 `USE <database>` 명령이 실행되거나 기본 데이터베이스로 해당 데이터베이스 컨텍스트를 사용하여 새 로그인이 처리될 때 적용됩니다.
데이터베이스의 현재 호환성 수준을 보려면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰에서 `compatibility_level` 열을 쿼리합니다.

> [!NOTE]
> 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 만들어져 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] RTM 또는 서비스 팩 1로 업그레이드되는 [배포 데이터베이스](../../relational-databases/replication/distribution-database.md)는 호환성 수준이 90이며 다른 데이터베이스에서 지원되지 않습니다. 복제 기능에는 영향을 미치지 않습니다. 이후의 서비스 팩 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전으로 업그레이드하면 **master** 데이터베이스의 수준에 맞게 배포 데이터베이스의 호환성 수준이 높아집니다.

> [!NOTE]
> **2019년 11월** 기준으로 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 새로 만들어진 데이터베이스에 대한 기본 호환성 수준은 150입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)]는 기존 데이터베이스에 대해서는 데이터베이스 호환성 수준을 업데이트하지 않습니다. 이것은 고객의 판단할 문제입니다.        
> [!INCLUDE[msCoName](../../includes/msconame-md.md)]는 최신 쿼리 최적화 기능 향상을 활용할 수 있도록 최신 호환성 수준으로 업그레이드할 것을 권장합니다.        

데이터베이스 전체에 데이터베이스 호환성 수준 120 이상을 활용하지만 데이터베이스 호환성 수준 110에 매핑되는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]의 [**카디널리티 추정**](../../relational-databases/performance/cardinality-estimation-sql-server.md) 모델을 옵트인하려면, [ALTER DATABASE SCOPED CONFIGURATION](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md), 특히 `LEGACY_CARDINALITY_ESTIMATION = ON` 키워드를 참조하세요.

[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 두 가지 다른 호환성 수준 간의 가장 중요한 쿼리의 성능 차이를 평가하는 방법에 대한 내용은 [Azure SQL Database에서 호환성 수준 130으로 향상된 쿼리 성능](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)을 참조하세요. 이 문서에서는 호환성 수준 130 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조하지만, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 140 이상으로 업그레이드하는 경우에도 같은 방법론이 적용됩니다.

연결된 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 버전을 확인하려면 다음 쿼리를 실행합니다.

```sql
SELECT SERVERPROPERTY('ProductVersion');
```

> [!NOTE]
> 호환성 수준에 따라 달라지는 일부 기능은 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 지원되지 않습니다.

현재 호환성 수준을 확인하려면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)의 **compatibility_level** 열을 쿼리합니다.

```sql
SELECT name, compatibility_level FROM sys.databases;
```

## <a name="compatibility-levels-and-database-engine-upgrades"></a>호환성 수준 및 업그레이드 데이터베이스 엔진
데이터베이스 호환성 수준은 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]를 업그레이드하도록 하여 데이터베이스 현대화를 지원하고, 동일한 사전 업그레이드 데이터베이스 호환성 수준을 유지하여 애플리케이션 기능 상태를 계속 연결하는 유용한 도구입니다. 즉, 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](예: [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)])에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)](Managed Instance 포함)으로 애플리케이션 변경 사항(데이터베이스 연결 제외) 없이 업그레이드할 수 있습니다. 자세한 내용은 [호환성 인증](../../database-engine/install-windows/compatibility-certification.md)을 참조하세요.

애플리케이션이 상위 데이터베이스 호환성 수준에서만 사용 가능한 향상 기능을 사용할 필요가 없는 한, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]를 업그레이드하고 이전 데이터베이스 호환성 수준을 유지하는 것이 유효한 접근법입니다. 이전 버전과의 호환성을 위해 호환성 수준을 사용하는 방법에 대한 자세한 내용은 [호환성 인증](../../database-engine/install-windows/compatibility-certification.md)을 참조하세요.

## <a name="best-practices-for-upgrading-database-compatibility-level"></a>데이터베이스 호환성 수준 업그레이드 모범 사례
호환성 수준 업그레이드를 위해 권장되는 워크플로는 [데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)을 참조하세요. 또한 데이터베이스 호환성 수준 업그레이드를 지원하는 환경에 대해서는 [쿼리 튜닝 길잡이를 사용하여 데이터베이스 업그레이드](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)를 참조하세요.

## <a name="compatibility-levels-and-stored-procedures"></a>호환성 수준 및 저장 프로시저
저장 프로시저가 실행될 때 저장 프로시저는 정의된 데이터베이스의 현재 호환성 수준을 사용합니다. 데이터베이스의 호환성 설정이 변경되면 모든 저장 프로시저도 그에 맞게 자동으로 다시 컴파일됩니다.

## <a name="using-compatibility-level-for-backward-compatibility"></a><a name="backwardCompat"></a> 이전 버전과의 호환을 위해 호환성 수준 사용
[데이터베이스 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 설정은 전체 서버가 아닌 지정된 데이터베이스에 대해서만 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 쿼리 최적화 동작과 관련된 사항에서 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전과의 호환성을 제공합니다.  

호환성 모드 130부터 수정 내용 및 기능에 영향을 주는 새로운 쿼리 계획이 새 호환성 수준에만 의도적으로 추가되었습니다. 새 쿼리 최적화 동작을 통해 도입된 잠재적 쿼리 계획 변경으로 인해 업그레이드 중에 성능 저하가 발생하는 위험을 최소화하기 위한 것입니다.      

애플리케이션 관점에서 더 안전한 마이그레이션 경로로 하위 호환성 수준을 사용하여 관련 호환성 수준 설정에서 제어하는 동작의 버전 차이를 해결할 수 있습니다. [지능형 쿼리 처리](../../relational-databases/performance/intelligent-query-processing.md)와 같은 새로운 기능 중 일부를 제어된 방식으로 상속하려면, 일정 시점에는 최신 호환성 수준으로 업그레이드하는 것을 계속 목표로 해야 합니다. 

데이터베이스 호환성 수준 업그레이드에 권장되는 워크플로를 비롯한 자세한 내용은 [데이터베이스 호환성 수준 업그레이드에 대한 모범 사례](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#best-practices-for-upgrading-database-compatibility-level)를 참조하세요.

> [!IMPORTANT]
> 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 도입된 **지원되지 않는** 기능은 호환성 수준으로 보호되지 **않습니다**. 이는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 제거된 기능을 나타냅니다.
> 예를 들어 `FASTFIRSTROW` 힌트는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 더 이상 사용되지 않으며 `OPTION (FAST n )` 힌트로 대체되었습니다. 데이터베이스 호환성 수준을 110으로 설정하면 지원되지 않는 힌트를 복원하지 않습니다.  
>  
> 지원되지 않는 기능에 대한 자세한 내용은 [SQL Server 2016에서 지원되지 않는 데이터베이스 엔진 기능](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md), [SQL Server 2014에서 지원되지 않는 데이터베이스 엔진 기능](https://docs.microsoft.com/sql/database-engine/discontinued-database-engine-functionality-in-sql-server-2016?view=sql-server-2014) 및 [SQL Server 2012에서 지원되지 않는 데이터베이스 엔진 기능](https://docs.microsoft.com/sql/database-engine/discontinued-database-engine-functionality-in-sql-server-2016?view=sql-server-2014#Denali)을 참조하세요.    

> [!IMPORTANT]
> 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 도입된 **주요 변경 사항**은 호환성 수준으로 보호되지 **않을 수 있습니다**. 이는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 버전 간 동작 변경을 나타냅니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 동작은 일반적으로 호환성 수준으로 보호됩니다. 그러나 변경되거나 제거된 시스템 개체는 호환성 수준으로 보호되지 **않습니다**.
>
> 호환성 수준으로 **보호되는** 주요 변경 내용의 예는 datetime에서 datetime2 데이터 형식으로의 암시적 변환입니다. 데이터베이스 호환성 수준 130에서 밀리초의 소수 부분을 고려하여 향상된 정확도를 보여 주므로 다르게 변환된 값을 생성합니다. 이전 변환 동작을 복원하려면 데이터베이스 호환성 수준을 120 이하로 설정합니다.
>
> 호환성 수준으로 **보호되지 않는** 주요 변경 내용의 예는 다음과 같습니다.
>
> - 시스템 개체의 변경된 열 이름입니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 sys.dm_os_sys_info의 *single_pages_kb* 열 이름은 *pages_kb*로 변경되었습니다. 호환성 수준에 관계 없이 쿼리 `SELECT single_pages_kb FROM sys.dm_os_sys_info`는 오류 207(잘못된 열 이름)을 생성합니다.
> - 제거된 시스템 개체입니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 `sp_dboption`이 제거되었습니다. 호환성 수준에 관계 없이 `EXEC sp_dboption 'AdventureWorks2016', 'autoshrink', 'FALSE';` 문은 오류 2812(저장된 프로시저 'sp_dboption'을 찾을 수 없음)를 생성합니다.
>
> 주요 변경 내용에 대한 자세한 내용은 [SQL Server 2017에서 데이터베이스 엔진 기능에 대한 주요 변경 내용](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2017.md), [SQL Server 2016에서 데이터베이스 엔진 기능에 대한 주요 변경 내용](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md), [SQL Server 2014에서 데이터베이스 엔진 기능에 대한 주요 변경 내용](https://docs.microsoft.com/sql/database-engine/discontinued-database-engine-functionality-in-sql-server-2016?view=sql-server-2014) 및 [SQL Server 2012에서 데이터베이스 엔진 기능에 대한 주요 변경 내용](https://docs.microsoft.com/sql/database-engine/discontinued-database-engine-functionality-in-sql-server-2016?view=sql-server-2014#Denali)을 참조하세요.

## <a name="differences-between-compatibility-levels"></a>호환성 수준 간 차이
모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 경우 [이 표](#supported-dbcompats)에 표시된 것처럼 기본 호환성 수준은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 버전과 관련됩니다. 새 개발 작업의 경우 항상 최신 데이터베이스 호환성 수준에서 애플리케이션을 인증하도록 계획합니다.

새 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문은 사용자 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드와의 충돌을 생성하여 기존 애플리케이션을 중단할 수 있는 경우를 제외하고 데이터베이스 호환성 수준으로 제어되지 않습니다. 관련 예외는 특정 호환성 수준 간의 차이점을 간략하게 설명하는 이 아티클의 다음 섹션에 나와 있습니다.

이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 연결되거나 복원된 데이터베이스는 기존 호환성 수준을 유지하므로 데이터베이스 호환성 수준은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와의 호환성도 제공합니다(허용되는 최소 호환성 수준보다 높거나 같은 경우). 이 내용은 이 문서의 [이전 버전과의 호환을 위해 호환성 수준 사용y](#backwardCompat) 섹션에 설명되어 있습니다.

데이터베이스 호환성 수준 130부터 쿼리 계획에 영향을 주는 새로운 수정 내용 및 기능은 기본 호환성 수준이라고도 하는 사용 가능한 최신 호환성 수준에만 추가되었습니다. 새 쿼리 최적화 동작을 통해 도입된 잠재적 쿼리 계획 변경으로 인해 업그레이드 중에 성능 저하가 발생하는 위험을 최소화하기 위한 것입니다. 

새 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 버전의 기본 호환성 수준에만 추가되는 계획에 영향을 주는 기본 변경 내용은 다음과 같습니다.

1.  **추적 플래그 4199 아래의 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 대해 릴리스된 쿼리 최적화 프로그램 수정 사항은 최신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전**의 기본 호환성 수준에서 자동으로 사용하도록 설정됩니다. **적용 대상:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 시작) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

    예를 들어, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]가 릴리스되었을 때 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전(및 해당 호환성 수준 100 ~ 120)용으로 릴리스된 모든 쿼리 최적화 프로그램은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 기본 호환성 수준(130)을 사용하는 데이터베이스에 대해 자동으로 사용하도록 설정되었습니다. RTM 이후 쿼리 최적화 프로그램 수정 사항만 명시적으로 사용하도록 설정해야 합니다.
    
    > [!NOTE]
    > 쿼리 최적화 프로그램 수정 사항을 사용하도록 설정하려면 다음 방법을 사용할 수 있습니다.    
    >
    > - 서버 수준에서 [추적 플래그 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199)를 사용합니다.
    > - 데이터베이스 수준에서 [ALTER DATABASE SCOPED CONFIGURATION(Transact-SQL)](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)의 `QUERY_OPTIMIZER_HOTFIXES` 옵션을 사용합니다.
    > - 쿼리 수준에서 `USE HINT 'ENABLE_QUERY_OPTIMIZER_HOTFIXES'` [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md#use_hint)를 사용합니다.
    
    이후에 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]이 릴리스되었을 때 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] RTM 이후에 릴리스된 모든 쿼리 최적화 프로그램 수정 사항은 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 기본 호환성 수준(140)을 사용하여 데이터베이스에 대해 자동으로 사용하도록 설정되었습니다. 이것은 이전 버전의 수정 사항도 모두 포함하는 누적 동작입니다. 다시 말하지만, RTM 이후 쿼리 최적화 프로그램 수정 사항만 명시적으로 사용하도록 설정해야 합니다.  
    
    다음 표에서는 이러한 동작을 요약해서 보여 줍니다.
    
    |DE(데이터베이스 엔진) 버전|데이터베이스 호환성 수준|TF 4199|모든 이전 데이터베이스 호환성 수준의 QO 변경 내용|RTM 이후 DE 버전에 대한 QO 변경 내용|
    |----------|----------|---|------------|--------|
    |13([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])|100 ~ 120<br /><br /><br />130|꺼짐<br />설정<br /><br />꺼짐<br />설정|**사용 안 함**<br />사용<br /><br />**Enabled**<br />사용|사용 안 함<br />사용<br /><br />사용 안 함<br />사용|
    |14([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)])|100 ~ 120<br /><br /><br />130<br /><br /><br />140|꺼짐<br />설정<br /><br />꺼짐<br />설정<br /><br />꺼짐<br />설정|**사용 안 함**<br />사용<br /><br />**Enabled**<br />사용<br /><br />**Enabled**<br />사용|사용 안 함<br />사용<br /><br />사용 안 함<br />사용<br /><br />사용 안 함<br />사용|
    |15([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) 및 12([!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)])|100 ~ 120<br /><br /><br />130 ~ 140<br /><br /><br />150|꺼짐<br />설정<br /><br />꺼짐<br />설정<br /><br />꺼짐<br />설정|**사용 안 함**<br />사용<br /><br />**Enabled**<br />사용<br /><br />**Enabled**<br />사용|사용 안 함<br />사용<br /><br />사용 안 함<br />사용<br /><br />사용 안 함<br />사용|
    
    > [!IMPORTANT]
    > 잘못된 결과 또는 액세스 위반 오류를 해결하는 쿼리 최적화 프로그램 수정 내용은 추적 플래그 4199로 보호되지 않습니다. 이러한 수정 사항은 선택 사항으로 간주되지 않습니다.
 
2.  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 릴리스된 [카디널리티 추정기](../../relational-databases/performance/cardinality-estimation-sql-server.md)에 대한 변경 내용은 새 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 버전**의 기본 호환성 수준에서만 사용할 수 있으며 이전 호환성 수준에서는 사용할 수 없습니다. 

    예를 들어, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]가 릴리스되었을 때 카디널리티 예측 프로세스의 변경 내용은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 기본 호환성 수준(130)을 사용하는 데이터베이스에 대해서만 사용할 수 있었습니다. 이전 호환성 수준에서는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 전에 사용할 수 있었던 카디널리티 예측 동작이 유지되었습니다. 
    
    이후에 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]이 릴리스되었을 때 카디널리티 예측 프로세스의 최신 변경 내용은 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 기본 호환성 수준(140)을 사용하는 데이터베이스에 대해서만 사용할 수 있었습니다. 데이터베이스 호환성 수준 130은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 카디널리티 예측 동작을 유지했습니다.
    
    다음 표에서는 이러한 동작을 요약해서 보여 줍니다.
    
    |데이터베이스 엔진 버전|데이터베이스 호환성 수준|새 버전 CE 변경 내용|
    |----------|--------|-------------|
    |13([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])|< 130<br />130|사용 안 함<br />사용|
    |14([!INCLUDE[ssSQL17](../../includes/sssql17-md.md)])<sup>1</sup>|< 140<br />140|사용 안 함<br />사용|
    |15 ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)])<sup>1</sup>|< 150<br />150|사용 안 함<br />사용|
    
    <sup>1</sup>[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에도 적용됩니다.
    
> [!IMPORTANT]
> 특정 호환성 수준 간의 다른 차이점은 이 문서의 다음 섹션에 제공됩니다.

## <a name="differences-between-compatibility-level-140-and-level-150"></a>호환성 수준 140과 수준 150 사이의 차이
이 섹션에서는 호환성 수준 150으로 정의된 새로운 동작에 대해 설명합니다.

|호환성 수준 설정 140 이하|호환성 수준 설정 150|
|--------------------------------------------------|-----------------------------------------|
|관계형 데이터 웨어하우스 및 분석 워크로드는 OLTP 오버헤드, 공급업체 지원 부족 또는 기타 제한 때문에 columnstore 인덱스를 사용하지 못할 수 있습니다.  columnstore 인덱스가 없으면 이러한 워크로드는 일괄 처리 실행 모드를 활용할 수 없습니다.|이제 columnstore 인덱스가 없어도 분석 워크로드에 일괄 처리 실행 모드를 사용할 수 있습니다. 자세한 내용은 [Rowstore의 일괄 처리 모드](../../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore)를 참조하세요.|
|디스크에 대한 분산이 발생하는 부족한 메모리 부여 크기를 요청하는 행 모드 쿼리는 연속 실행에 대한 문제가 지속될 수 있습니다.|디스크에 대한 분산이 발생하는 부족한 메모리 부여 크기를 요청하는 행 처리 모드 쿼리는 연속 실행에 대한 성능을 향상시킬 수 있습니다. 자세한 내용은 [행 모드 메모리 부여 피드백](../../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback)을 참조하세요.|
|동시성 문제가 발생하는 과도한 메모리 부여 크기를 요청하는 행 모드 쿼리는 연속 실행에 대한 문제가 지속될 수 있습니다.|동시성 문제가 발생하는 과도한 메모리 부여 크기를 요청하는 행 모드 쿼리는 연속 실행에 대한 동시성을 향상시킬 수 있습니다. 자세한 내용은 [행 모드 메모리 부여 피드백](../../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback)을 참조하세요.|
|T-SQL 스칼라 UDF를 참조하는 쿼리는 반복 호출, 비용 부족 및 강제 직렬 실행을 사용합니다. |T-SQL 스칼라 UDF는 호출 쿼리로 "인라인"되는 해당 관계형 식으로 변환되어 성능이 크게 향상됩니다. 자세한 내용은 [T-SQL UDF 인라인 처리](../../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining)를 참조하세요.|
|테이블 변수는 카디널리티 추정에 고정 추측을 사용합니다.  실제 행 수가 추측된 값보다 훨씬 높은 경우 다운스트립 작업의 성능이 저하될 수 있습니다. |새 플랜은 고정 추측 대신 첫 번째 컴파일에서 발생한 테이블의 변수의 실제 카디널리티를 사용합니다. 자세한 내용은 [테이블 변수 지연 컴파일](../../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation)을 참조하세요.|

데이터베이스 호환성 수준 150에서 사용하도록 설정된 쿼리 처리 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../../sql-server/what-s-new-in-sql-server-ver15.md) 및 [SQL 데이터베이스의 지능형 쿼리 처리](../../relational-databases/performance/intelligent-query-processing.md)를 참조하세요.

## <a name="differences-between-compatibility-level-130-and-level-140"></a>호환성 수준 130과 수준 140 사이의 차이

이 섹션에서는 호환성 수준 140으로 도입된 새로운 동작에 대해 설명합니다.

|호환성 수준 설정 130 이하|호환성 수준 설정 140|
|--------------------------------------------------|-----------------------------------------|
|다중 문 테이블 반환 함수를 참조하는 문에 대한 카디널리티 예상치는 고정된 행 추측을 사용합니다.|다중 문 테이블 반환 함수를 참조하는 적절한 명령문에 대한 카디널리티 예상치는 함수 출력의 실제 카디널리티를 사용합니다. 다중 문 테이블 반환 함수에 대한 **인터리브 실행**을 통해 활성화됩니다.|
|디스크에 대한 분산이 발생하는 부족한 메모리 부여 크기를 요청하는 일괄 처리 모드 쿼리는 연속 실행에 대한 문제가 지속될 수 있습니다.|디스크에 대한 분산이 발생하는 부족한 메모리 부여 크기를 요청하는 일괄 처리 모드 쿼리는 연속 실행에 대한 성능을 향상시킬 수 있습니다. 일괄 처리 모드 연산자에 대해 분산이 발생한 경우 캐시 계획의 메모리 부여 크기를 업데이트하는 **일괄 처리 모드 메모리 부여 피드백**을 통해 활성화됩니다. |
|동시성 문제가 발생하는 과도한 메모리 부여 크기를 요청하는 일괄 처리 모드 쿼리는 연속 실행에 대한 문제가 지속될 수 있습니다.|동시성 문제가 발생하는 과도한 메모리 부여 크기를 요청하는 일괄 처리 모드 쿼리는 연속 실행에 대한 동시성을 향상시킬 수 있습니다. 과도한 양이 요청된 경우 캐시 계획의 메모리 부여 크기를 업데이트하는 **일괄 처리 모드 메모리 부여 피드백**을 통해 활성화됩니다.|
|조인 연산자를 포함하는 일괄 처리 모드 쿼리는 중첩된 루프, 해시 조인 및 병합 조인을 포함하는 세 개의 물리적 조인 알고리즘에 적합합니다. 카디널리티 예측치가 조인 입력에 대해 잘못된 경우 부적절한 조인 알고리즘이 선택될 수 있습니다. 이 문제가 발생하는 경우 성능이 저하되고 부적절한 조인 알고리즘이 캐시 계획이 다시 컴파일될 때까지 사용 중으로 남아 있습니다.|**적응형 조인**이라는 추가 조인 연산자가 있습니다. 카디널리티 예측치가 외부 빌드 조인 입력에 대해 잘못된 경우 부적절한 조인 알고리즘이 선택될 수 있습니다. 이 문제가 발생하고 명령문이 적응형 조인에 대해 적합한 경우 더 작은 조인 입력에 중첩된 루프가 사용되고 다시 컴파일할 필요 없이 더 큰 조인 입력에 해시 조인이 동적으로 사용됩니다. |
|Columnstore 인덱스를 참조하는 간단한 계획은 일괄 처리 모드 실행에 적합하지 않습니다. |Columnstore 인덱스를 참조하는 간단한 계획은 일괄 처리 모드 실행에 적합한 계획을 위해 무시됩니다.|
|`sp_execute_external_script` UDX 연산자는 행 모드에서만 실행할 수 있습니다.|`sp_execute_external_script` UDX 연산자는 일괄 처리 모드 실행에 적합합니다.|
|다중 문 TVF(테이블 반환 함수)는 인터리브 실행이 없습니다. |계획 품질을 개선하기 위한 다중 명령문 TVF에 대한 인터리브 실행입니다.|

SQL Server 2017 이전의 SQL Server 이전 버전에서 추적 플래그 4199의 수정 사항이 이제 기본적으로 활성화됩니다. 호환성 모드 140 사용 추적 플래그 4199는 SQL Server 2017 이후에 릴리스되는 새로운 쿼리 최적화 프로그램 수정에 적용됩니다. 추적 플래그 4199에 대한 자세한 내용은 [추적 플래그 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199)를 참조하세요.

## <a name="differences-between-compatibility-level-120-and-level-130"></a>호환성 수준 120과 수준 130 사이의 차이

이 섹션에서는 호환성 수준 130으로 정의된 새로운 동작에 대해 설명합니다.

|호환성 수준 설정 120 이하|호환성 수준 설정 130|
|--------------------------------------------------|-----------------------------------------|
|INSERT-SELECT 문의 INSERT는 단일 스레드입니다.|INSERT-SELECT 문의 INSERT는 다중 스레드 형식이거나, 병렬 계획일 수 있습니다.|
|메모리 최적화 테이블에 대한 쿼리는 단일 스레드를 실행합니다.|메모리 최적화 테이블에 대한 쿼리는 이제 병렬 계획을 가질 수 있습니다.|
|SQL 2014 카디널리티 평가기 **CardinalityEstimationModelVersion="120"** 을 도입했습니다.|카디널리티 추정 모델 130을 통한 자세한 CE(카디널리티 추정) 개선 사항은 쿼리 계획에서 볼 수 있습니다. **CardinalityEstimationModelVersion="130"**|
|Columnstore 인덱스를 사용한 일괄 처리 모드와 행 모드 비교 변경 내용입니다.<br /><ul><li>Columnstore 인덱스가 있는 테이블에 대한 정렬은 행 모드에 있습니다. <li>Windowing 함수 집계는 `LAG` 또는 `LEAD`와 같은 행 모드에서 작동합니다. <li>여러 고유 절이 있는 Columnstore 테이블에 대한 쿼리는 행 모드에서 작동했습니다. <li>MAXDOP 1에서 실행되거나 직렬 계획을 사용하는 쿼리는 행 모드에서 실행되었습니다.</li></ul>| Columnstore 인덱스를 사용한 일괄 처리 모드와 행 모드 비교 변경 내용입니다.<br /><ul><li>Columnstore 인덱스가 있는 테이블에 대한 정렬은 이제 일괄 처리 모드에 있습니다. <li>Windowing 집계는 이제 `LAG` 또는 `LEAD`와 같은 일괄 처리 모드에서 작동합니다. <li>여러 고유 절이 있는 Columnstore 테이블에 대한 쿼리는 일괄 처리 모드에서 작동합니다. <li>MAXDOP 1에서 실행되거나 직렬 계획을 사용하는 쿼리는 일괄 처리 모드에서 실행</li></ul>|
|통계는 자동으로 업데이트될 수 있습니다. | 자동으로 통계를 업데이트하는 논리는 대형 테이블에 더 적극적입니다. 실제로 고객이 새로 삽입된 행이 빈번하게 쿼리되지만 통계가 해당 값을 포함하도록 업데이트되지 않는 쿼리에 대한 성능 문제를 발견하는 사례를 줄여야 합니다. |
|추적 2371은 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 기본적으로 OFF입니다. | [추적 2371](https://blogs.msdn.microsoft.com/psssql/2016/10/04/default-auto-statistics-update-threshold-change-for-sql-server-2016/)은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 기본적으로 ON입니다. 추적 플래그 2371은 자동 통계 업데이트 도구에 매우 많은 행이 있는 테이블에서 더 작지만 현명한 행의 하위 집합을 샘플링하도록 알려 줍니다. <br/> <br/> 하나의 개선 사항은 최근에 삽입된 더 많은 행을 샘플에 포함하는 것입니다. <br/> <br/> 또 다른 개선 사항은 업데이트 통계 프로세스가 실행되는 동안 쿼리를 차단하기 보다는 쿼리가 실행되도록 두는 것입니다. |
|수준 120의 경우 통계는 단일 스레드 프로세스를 통해 샘플링됩니다.|수준 130의 경우 통계는 다중 스레드 프로세스(병렬 프로세스)를 통해 샘플링됩니다. |
|253 들어오는 외래 키는 제한입니다.| 최대 10,000개의 들어오는 외래 키 또는 유사한 참조로 지정된 테이블을 참조할 수 있습니다. 제한 사항에 대해서는 [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md)를 참조하세요. |
|사용되지 않는 MD2, MD4, MD5, SHA 및 SHA1 해시 알고리즘이 허용됩니다.|SHA2_256 및 SHA2_512 해시 알고리즘만 허용됩니다.|
||[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]는 일부 데이터 형식 변환 및 일부(주로 드문) 작업에서 향상된 기능을 포함합니다. 자세한 내용은 [일부 데이터 형식 및 일반적이지 않은 작업 처리 시 SQL Server 2016의 향상된 기능](https://support.microsoft.com/help/4010261/sql-server-2016-improvements-in-handling-some-data-types-and-uncommon)을 참조하세요.|
|`STRING_SPLIT` 함수를 사용할 수 없습니다.|`STRING_SPLIT` 함수는 호환성 수준 130 이상에서 사용할 수 있습니다. 데이터베이스 호환성 수준이 130보다 낮으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 `STRING_SPLIT` 함수를 찾아 실행할 수 없습니다.|

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이전 버전에서 추적 플래그 4199의 수정 사항이 이제 기본적으로 활성화됩니다. 호환성 모드 130 사용 추적 플래그 4199는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이후에 릴리스되는 새로운 쿼리 최적화 프로그램 수정에 적용됩니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 이전 쿼리 최적화 프로그램을 사용하려면 호환성 수준 110을 선택해야 합니다. 추적 플래그 4199에 대한 자세한 내용은 [추적 플래그 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199)를 참조하세요.

## <a name="differences-between-lower-compatibility-levels-and-level-120"></a>낮은 호환성 수준과 수준 120 사이의 차이

이 섹션에서는 호환성 수준 120으로 정의된 새로운 동작에 대해 설명합니다.

|호환성 수준 설정 110 이하|호환성 수준 설정 120|
|--------------------------------------------------|-----------------------------------------|
|이전 쿼리 최적화 프로그램이 사용됩니다.|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]는 쿼리 계획을 만들고 최적화하는 구성 요소에 대한 향상된 기능을 포함합니다. 이러한 새로운 쿼리 최적화 프로그램 기능은 데이터베이스 호환성 수준 120의 사용에 따라 달라집니다. 이러한 향상된 기능을 활용하려면 데이터베이스 호환성 수준 120을 사용하여 새 데이터베이스 애플리케이션을 개발해야 합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 마이그레이션된 애플리케이션의 경우 좋은 성능이 유지되거나 향상되었는지 확인하려면 신중하게 테스트해야 합니다. 성능이 저하되면 데이터베이스 호환성 수준을 110 이하로 설정하여 이전 쿼리 최적화 프로그램 방법을 사용할 수 있습니다.<br /><br /> 데이터베이스 호환성 수준 120은 최신 데이터 웨어하우징 및 OLTP 작업에 대해 조정된 새로운 카디널리티 추정기를 사용합니다. 성능 문제 때문에 데이터베이스 호환성 수준을 110으로 설정하려면 먼저 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [데이터베이스 엔진의 새로운 기능](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md) 항목의 *쿼리 계획* 섹션에서 권장 사항을 참조하세요.|
|120 미만의 호환성 수준에서는 **date** 값을 문자열 값으로 변환할 때 언어 설정이 무시됩니다. 이 동작은 **date** 유형에만 한정됩니다. 아래에 있는 예제 섹션에서 예제 B를 참조하세요.|**date** 값을 문자열 값으로 변환할 때 언어 설정이 무시되지 않습니다.|
|`EXCEPT` 절의 오른쪽에 있는 재귀 참조는 무한 루프를 만듭니다. 아래 예제 섹션의 예제 C는 이 동작을 보여 줍니다.|`EXCEPT` 절에 있는 재귀 참조는 ANSI SQL 표준에 따라 오류를 생성합니다.|
|재귀 CTE(공통 테이블 식)는 중복된 열 이름을 허용합니다.|재귀적 CTE에서 중복 열 이름을 허용하지 않습니다.|
|해제된 트리거는 트리거가 변경되는 경우 설정됩니다.|트리거를 변경하는 경우 트리거의 상태(설정 또는 해제)가 변경되지 않습니다.|
|OUTPUT INTO 테이블 절은 `IDENTITY_INSERT SETTING = OFF`를 무시하고 명시적 값이 삽입될 수 있도록 합니다.|`IDENTITY_INSERT`가 OFF로 설정되면 테이블의 ID 열에 명시적 값을 삽입할 수 없습니다.|
|데이터베이스 포함이 부분으로 설정된 경우 `MERGE` 문의 `OUTPUT` 절에서 `$action` 필드의 유효성을 검사하면 데이터 정렬 오류가 반환될 수 있습니다.|`MERGE` 문의 `$action` 절에서 반환되는 값의 데이터 정렬은 서버 데이터 정렬 대신 데이터베이스 데이터 정렬이며 데이터 정렬 충돌 오류가 반환되지 않습니다.|
|`SELECT INTO` 문은 항상 단일 스레드 삽입 작업을 만듭니다.|`SELECT INTO` 문은 병렬 삽입 작업을 만들 수 있습니다. 많은 수의 행을 삽입하는 경우 병렬 작업은 성능을 향상시킬 수 있습니다.|

## <a name="differences-between-lower-compatibility-levels-and-levels-100-and-110"></a>낮은 호환성 수준과 수준 100 및 110 사이의 차이

이 섹션에서는 호환성 수준 110으로 정의된 새로운 동작에 대해 설명합니다. 이 섹션에서는 호환성 수준 110 이상도 적용됩니다.

|호환성 수준 설정 100 이하|호환성 수준 설정 110 이상|
|--------------------------------------------------|--------------------------------------------------|
|CLR(공용 언어 런타임) 데이터베이스 개체는 CLR 버전 4를 사용하여 실행됩니다. 그러나 CLR 버전 4에 도입된 일부 동작 변경은 발생하지 않습니다. 자세한 내용은 [CLR 통합의 새로운 기능](../../relational-databases/clr-integration/clr-integration-what-s-new.md)을 참조하세요.|CLR 데이터베이스 개체는 CLR 버전 4를 사용하여 실행됩니다.|
|XQuery 함수 **string-length** 및 **substring**에서 각 서로게이트를 두 개의 문자로 계산합니다.|XQuery 함수 **string-length** 및 **substring**에서 각 서로게이트를 한 개의 문자로 계산합니다.|
|`PIVOT`이 재귀 CTE(공통 테이블 식) 쿼리에서 허용됩니다. 그러나 그룹화당 여러 행이 있는 경우에는 쿼리에서 잘못된 결과가 반환됩니다.|`PIVOT`이 재귀 CTE(공통 테이블 식) 쿼리에서 허용되지 않습니다. 오류가 반환됩니다.|
|RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.|RC4 또는 RC4_128를 사용하여 새 자료를 암호화할 수 없습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.|
|**time** 및 **datetime2** 데이터 형식 중 하나가 계산 열 식에서 사용되는 경우를 제외하고 이러한 데이터 형식에 대한 `CAST` 및 `CONVERT` 연산의 기본 스타일이 121입니다. 계산 열의 경우 기본 스타일은 0입니다. 이 동작은 자동 매개 변수화와 관련된 쿼리에서 이러한 연산이 만들어지고 사용될 때 또는 제약 조건 정의에 사용될 때 계산 열에 영향을 줍니다.<br /><br /> 아래 예제 섹션의 예제 D는 스타일 0과 121의 차이점을 보여 줍니다. 위에서 설명한 동작은 보여 주지 않습니다. 날 짜 및 시간 스타일에 대한 자세한 내용은 [CAST 및 CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요.|호환성 수준 110에서 **time** 및 **datetime2** 데이터 형식의 `CAST` 및 `CONVERT` 연산에 대한 기본 스타일은 항상 121입니다. 쿼리에 이전 동작이 적용되는 경우 110보다 낮은 호환성 수준을 사용하거나, 해당 쿼리에서 스타일 0을 명시적으로 지정해야 합니다.<br /><br /> 데이터베이스를 호환성 수준 110으로 업그레이드할 경우 디스크에 저장된 사용자 데이터는 변경되지 않습니다. 수동으로 이 데이터를 적절하게 수정해야 합니다. 예를 들어 `SELECT INTO`를 사용하여 위에서 설명한 계산 열 식이 포함된 원본에서 테이블을 만든 경우 계산 열 정의 자체가 아니라 스타일 0을 사용하는 데이터가 저장됩니다. 스타일 121과 일치하도록 이 데이터를 수동으로 업데이트해야 합니다.|
|분할 뷰에서 참조되는 **smalldatetime** 형식의 원격 테이블 열은 **datetime**으로 매핑됩니다. 로컬 테이블의 해당 열(SELECT 목록의 동일한 서수 위치에 있는 열)은 **datetime** 형식이어야 합니다.|분할 뷰에서 참조되는 **smalldatetime** 형식의 원격 테이블 열은 **smalldatetime**으로 매핑됩니다. 로컬 테이블의 해당 열(SELECT 목록의 동일한 서수 위치에 있는 열)은 **smalldatetime** 형식이어야 합니다.<br /><br /> 110으로 업그레이드한 후에는 데이터 형식이 일치하지 않으므로 분산형 분할 뷰가 실패합니다. 원격 테이블의 데이터 형식을 **datetime**으로 변경하거나 로컬 데이터베이스의 호환성 수준을 100 이하로 설정하여 이 문제를 해결할 수 있습니다.|
|`SOUNDEX` 함수는 다음 규칙을 구현합니다.<br /><br /> 1) `SOUNDEX` 코드에 동일한 숫자가 있는 두 개의 자음을 구분하는 경우 대문자 H 또는 대문자 W가 무시됩니다.<br /><br /> 2) `SOUNDEX` 코드에서 *character_expression*의 처음 2자에 같은 숫자가 있으면 두 문자 모두 포함됩니다. 위의 경우에 해당되지 않고 `SOUNDEX` 코드에서 나란히 있는 자음에 같은 값이 있으면 첫 번째 문자를 제외한 모든 문자가 제외됩니다.|`SOUNDEX` 함수는 다음 규칙을 구현합니다.<br /><br /> 1) 대문자 H 또는 대문자 W가 동일한 `SOUNDEX` 코드 숫자를 갖는 두 개의 자음을 구분하는 경우 오른쪽의 자음은 무시됩니다.<br /><br /> 2) `SOUNDEX` 코드에서 나란히 있는 자음에 같은 값이 있으면 첫 번째 문자를 제외한 모든 문자가 제외됩니다.<br /><br /> <br /><br /> 추가 규칙으로 인해 `SOUNDEX` 함수에서 계산된 값이 이전 호환성 수준에서 계산된 값과 다를 수 있습니다. 호환성 수준 110으로 업그레이드한 후 `SOUNDEX` 함수를 사용하는 인덱스, 힙 또는 CHECK 제약 조건을 다시 작성해야 할 수 있습니다. 자세한 내용은 [SOUNDEX](../../t-sql/functions/soundex-transact-sql.md)를 참조하세요.|

## <a name="differences-between-compatibility-level-90-and-level-100"></a>호환성 수준 90과 수준 100 사이의 차이

이 섹션에서는 호환성 수준 100으로 정의된 새로운 동작에 대해 설명합니다.

|호환성 수준 설정 90|호환성 수준 설정 100|영향력|
|----------------------------------------|-----------------------------------------|---------------------------|
|세션 수준 설정과 상관없이 다중 문 테이블 반환 함수를 만든 경우 이 함수에 대해 QUOTED_IDENTIFER 설정은 항상 ON으로 설정됩니다.|다중 문 테이블 반환 함수를 만든 경우 QUOTED IDENTIFIER 세션 설정이 적용됩니다.|중간|
|파티션 함수를 만들거나 바꾸면 언어 설정을 US_English로 가정하고 함수의 **datetime** 및 **smalldatetime** 리터럴을 평가합니다.|현재 언어 설정은 파티션 함수에서 **datetime** 및 **smalldatetime** 리터럴을 평가하는 데 사용됩니다.|중간|
|`FOR BROWSE` 절이 `INSERT` 및 `SELECT INTO` 문에서 허용되고 무시됩니다.|`FOR BROWSE` 절이 `INSERT` 및 `SELECT INTO` 문에서 허용되지 않습니다.|중간|
|전체 텍스트 조건자는 `OUTPUT` 절에서 허용됩니다.|전체 텍스트 조건자는 `OUTPUT` 절에서 허용되지 않습니다.|낮음|
|`CREATE FULLTEXT STOPLIST`, `ALTER FULLTEXT STOPLIST` 및 `DROP FULLTEXT STOPLIST`는 지원되지 않습니다. 시스템 중지 목록은 자동으로 새로운 전체 텍스트 인덱스와 연결됩니다.|`CREATE FULLTEXT STOPLIST`, `ALTER FULLTEXT STOPLIST` 및 `DROP FULLTEXT STOPLIST`는 지원됩니다.|낮음|
|`MERGE`는 예약 키워드가 아닙니다.|MERGE는 완전 예약 키워드입니다. `MERGE` 문은 호환성 수준 100 및 90 모두에서 지원됩니다.|낮음|
|INSERT 문에서 \<dml_table_source> 인수를 사용하면 구문 오류가 발생합니다.|중첩된 INSERT, UPDATE, DELETE 또는 MERGE 문에서 OUTPUT 절의 결과를 캡처하고 그 결과를 대상 테이블이나 뷰에 삽입할 수 있습니다. 이 작업은 INSERT 문의 \<dml_table_source> 인수를 사용하여 수행됩니다.|낮음|
|`NOINDEX`가 지정되지 않으면 `DBCC CHECKDB` 또는 `DBCC CHECKTABLE`은 단일 테이블이나 인덱싱된 뷰 및 해당하는 모든 비클러스터형 XML 인덱스에 대해 물리적 일관성 검사와 논리적 일관성 검사를 모두 수행합니다. 공간 인덱스는 지원되지 않습니다.|`NOINDEX`가 지정되지 않으면 `DBCC CHECKDB` 또는 `DBCC CHECKTABLE`은 단일 테이블 및 해당하는 모든 비클러스터형 인덱스에 대해 물리적 일관성 검사와 논리적 일관성 검사를 모두 수행합니다. 그러나 XML 인덱스, 공간 인덱스 및 인덱싱된 뷰에 대해서는 기본적으로 물리적 일관성 검사만 수행됩니다.<br /><br /> `WITH EXTENDED_LOGICAL_CHECKS`를 지정하면 인덱싱된 뷰, XML 인덱스 및 공간 인덱스에 대해 논리적 검사가 수행됩니다. 기본적으로 물리적 일관성 검사는 논리적 일관성 검사 전에 수행됩니다. `NOINDEX`도 지정할 경우 논리적 검사만 수행됩니다.|낮음|
|DML(데이터 조작 언어)로 OUTPUT 절을 사용하는 경우 문 실행 중에 런타임 오류가 발생하면 전체 트랜잭션이 종료되고 롤백됩니다.|DML(데이터 조작 언어) 문으로 `OUTPUT` 절을 사용하는 경우 명령문 실행 중에 런타임 오류가 발생하면 `SET XACT_ABORT` 설정에 따라 동작이 결정됩니다. `SET XACT_ABORT`가 OFF로 설정된 경우 `OUTPUT` 절을 사용하는 DML 문에서 문 중단 오류가 발생하면 해당 문은 종료되지만 일괄 처리의 실행이 계속되고 트랜잭션이 롤백되지 않습니다. `SET XACT_ABORT`가 ON으로 설정된 경우 OUTPUT 절을 사용하는 DML 문에서 런타임 오류가 발생하면 항상 일괄 처리가 종료되고 트랜잭션이 롤백됩니다.|낮음|
|CUBE 및 ROLLUP은 예약 키워드가 아닙니다.|`CUBE` 및 `ROLLUP`은 GROUP BY 절에서 예약 키워드입니다.|낮음|
|XML **anyType** 형식의 요소에는 엄격한 유효성 검사가 적용됩니다.|**anyType** 형식의 요소에는 엄격하지 않은 유효성 검사가 적용됩니다. 자세한 내용은 [와일드카드 구성 요소 및 콘텐츠 유효성 검사](../../relational-databases/xml/wildcard-components-and-content-validation.md)를 참조하세요.|낮음|
|특수 특성 **xsi:nil** 및 **xsi:type**은 데이터 조작 언어 문으로 쿼리하거나 수정할 수 없습니다.<br /><br /> 즉, `/e/@*`에서 **xsi:nil** 및 **xsi:type** 특성을 무시하고 `/e/@xsi:nil`이 실패합니다. 그러나 `xsi:nil = "false"`인 경우에도 `SELECT xmlCol`과의 일관성을 위해 `/e`에서 **xsi:nil** 및 **xsi:type** 특성을 반환합니다.|특수 특성 **xsi:nil** 및 **xsi:type**은 일반 특성으로 저장되므로 쿼리 및 수정이 가능합니다.<br /><br /> 예를 들어 쿼리 `SELECT x.query('a/b/@*')`를 실행하면 **xsi:nil** 및 **xsi:type**을 포함하는 모든 특성이 반환됩니다. 쿼리에서 이러한 유형을 제외하려면 `@*`를 `@*[namespace-uri(.) != "`*insert xsi namespace uri*`"`로 바꿉니다. `(local-name(.) = "type"` 또는 `local-name(.) ="nil".`로는 바꾸지 마십시오.|낮음|
|XML 상수 문자열 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datetime 형식으로 변환하는 사용자 정의 함수를 결정적 함수로 표시합니다.|XML 상수 문자열 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datetime 형식으로 변환하는 사용자 정의 함수를 비결정적 함수로 표시합니다.|낮음|
|XML union 및 list 형식 중 일부는 지원되지 않습니다.|다음 기능을 포함하여 union 및 list 형식은 모두 지원됩니다.<br /><br /> 목록의 합집합<br /><br /> 합집합의 합집합<br /><br /> 원자성 유형의 목록<br /><br /> 합집합의 목록|낮음|
|인라인 테이블 반환 함수 또는 뷰에 xQuery 메서드가 포함된 경우 이 메서드에 필요한 SET 옵션의 유효성을 검사하지 않습니다.|인라인 테이블 반환 함수 또는 뷰에 xQuery 메서드가 포함된 경우 이 메서드에 필요한 SET 옵션의 유효성을 검사합니다. 메서드의 SET 옵션을 잘못 설정하면 오류가 발생합니다.|낮음|
|줄 끝 문자(캐리지 리턴 및 줄 바꿈)를 포함하는 XML 특성 값은 XML 표준에 따라 정규화되지 않습니다. 즉, 하나의 줄 바꿈 문자 대신 두 문자 모두 반환됩니다.|줄 끝 문자(캐리지 리턴 및 줄 바꿈)를 포함하는 XML 특성 값은 XML 표준에 따라 정규화됩니다. 즉, 문서 엔터티를 포함하여 구문 분석된 외부 엔터티의 모든 줄 바꿈은 2자 시퀀스 #xD #xA 및 뒤에 #xA가 오지 않는 #xD 모두를 하나의 #xA 문자로 변환하여 입력에서 정규화됩니다.<br /><br /> 특성을 사용하여 줄 끝 문자를 포함하는 문자열 값을 변환하는 애플리케이션은 이러한 제출된 문자를 다시 수신하지 않습니다. 정규화 프로세스를 방지하려면 XML 숫자 문자 엔터티를 사용하여 모든 줄 끝 문자를 인코딩합니다.|낮음|
|열 속성 `ROWGUIDCOL` 및 `IDENTITY`는 제약 조건으로 잘못 이름이 지정될 수 있습니다. 예를 들어 `CREATE TABLE T (C1 int CONSTRAINT MyConstraint IDENTITY)` 문은 실행되긴 하지만 제약 조건 이름이 보존되지 않으며 이를 통해 사용자에게 액세스할 수 없습니다.|열 속성 `ROWGUIDCOL` 및 `IDENTITY`는 제약 조건으로 이름을 지정할 수 없습니다. 오류 156이 반환됩니다.|낮음|
|`UPDATE T1 SET @v = column_name = <expression>`과 같은 양방향 할당을 사용하여 열을 업데이트하면 명령문 실행 중에 `WHERE` 및 `ON` 절과 같은 다른 절에서 명령문의 시작 값 대신 변수의 현재 값을 사용할 수 있으므로 예상치 못한 결과가 발생할 수 있습니다. 그 결과 각 행에서 조건자의 의미가 예기치 않게 변경될 수 있습니다.<br /><br /> 이 동작은 호환성 수준이 90으로 설정된 경우에만 발생합니다.|양방향 할당을 사용하여 열을 업데이트하면 문 실행 중에 열의 문 시작 값만 액세스되므로 예상대로 결과가 나타납니다.|낮음|
|아래 예제 섹션의 예제 E를 참조하세요.|아래 예제 섹션의 예제 F를 참조하세요.|낮음|
|ODBC 함수 {fn CONVERT()}는 언어의 기본 날짜 형식을 사용합니다. 일부 언어에서 기본 형식은 YDM입니다. 이 경우 CONVERT()가 YMD 형식을 사용하는 `{fn CURDATE()}`와 같은 다른 함수와 결합되면 변환 오류가 발생합니다.|ODBC 함수 `{fn CONVERT()}`는 ODBC 데이터 형식 SQL_TIMESTAMP, SQL_DATE, SQL_TIME, SQLDATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP로 변환할 때 스타일 121(언어와 상관없는 YMD 형식)을 사용합니다.|낮음|
|DATEPART와 같은 datetime 내장 함수에서 문자열 입력 값은 유효한 datetime 리터럴이 아니어도 됩니다. 예를 들어 `SELECT DATEPART (year, '2007/05-30')`는 성공적으로 컴파일됩니다.|`DATEPART`와 같은 datetime 내장 함수에서 문자열 입력 값은 유효한 datetime 리터럴이어야 합니다. 유효하지 않은 datetime 리터럴을 사용하면 오류 241이 반환됩니다.|낮음|
|REPLACE 함수의 첫 번째 입력 매개 변수가 char 형식인 경우 이 매개 변수에 지정된 후행 공백이 잘립니다. 예를 들어 SELECT '<' + REPLACE(CONVERT(char(6), 'ABC '), ' ', 'L') + '>' 문에서 'ABC ' 값은 'ABC'로 잘못 평가됩니다.|후행 공백이 항상 유지됩니다. 이 함수의 이전 동작에 의존하는 애플리케이션의 경우 이 함수의 첫 번째 입력 매개 변수를 지정할 때 RTRIM 함수를 사용합니다. 예를 들어 다음 구문은 SQL Server 2005 동작 SELECT '<' + REPLACE(RTRIM(CONVERT(char(6), 'ABC ')), ' ', 'L') + '>'을 재현합니다.|낮음|

## <a name="reserved-keywords"></a>예약 키워드

호환성 설정은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 예약되는 키워드도 결정합니다. 다음 표에서는 각 호환성 수준에 의해 정의된 예약 키워드를 보여 줍니다.

|호환성 수준 설정|예약 키워드|
|----------------------------------|-----------------------|
|130|결정될 예정입니다.|
|120|없음|
|110|`WITHIN GROUP`, `TRY_CONVERT`, `SEMANTICKEYPHRASETABLE`, `SEMANTICSIMILARITYDETAILSTABLE`, `SEMANTICSIMILARITYTABLE`|
|100|`CUBE`, `MERGE`, `ROLLUP`|
|90|`EXTERNAL`, `PIVOT`, `UNPIVOT`, `REVERT`, `TABLESAMPLE`|

지정된 호환성 수준의 예약 키워드에는 해당 수준 또는 그 아래 수준에서 정의된 모든 키워드가 포함됩니다. 따라서 수준이 110인 애플리케이션의 경우에는 위 표에 나열된 모든 키워드가 예약되어 있습니다. 더 낮은 호환성 수준에서 수준이 100인 키워드는 유효한 개체 이름으로 유지되지만 해당 키워드에 대한 수준이 110인 언어 기능은 사용할 수 없습니다.

정의된 키워드는 예약된 상태로 유지됩니다. 예를 들어 호환성 수준 90에서 정의된 예약 키워드 PIVOT은 수준 100, 110 및 120에서도 예약되어 있습니다.

애플리케이션이 호환성 수준에 대한 키워드로 예약되어 있는 식별자를 사용할 경우 제대로 실행되지 않습니다. 이러한 문제를 해결하려면 식별자를 대괄호( **[]** )나 따옴표( **""** )로 묶으십시오. 예를 들어 식별자`EXTERNAL`을 사용하는 애플리케이션을 호환성 수준 90으로 업그레이드하려면 식별자를 `[EXTERNAL]`이나 `"EXTERNAL"`로 변경할 수 있습니다.

자세한 내용은 [예약 키워드](../../t-sql/language-elements/reserved-keywords-transact-sql.md)를 참조하세요.

## <a name="permissions"></a>사용 권한

데이터베이스에 대한 `ALTER` 권한이 필요합니다.

## <a name="examples"></a>예

### <a name="a-changing-the-compatibility-level"></a>A. 호환성 수준 변경

다음 예제에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 호환성 수준을 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]의 기본값인 110으로 변경합니다.

```sql
ALTER DATABASE AdventureWorks2012
SET COMPATIBILITY_LEVEL = 110;
GO
```

다음 예에서는 현재 데이터베이스의 호환성 수준을 반환합니다.

```sql
SELECT name, compatibility_level
FROM sys.databases
WHERE name = db_name();
```

### <a name="b-ignoring-the-set-language-statement-except-under-compatibility-level-120"></a>B. 호환성 수준이 120 미만일 때를 제외하고 SET LANGUAGE 문을 무시합니다.

다음 쿼리에서는 호환성 수준이 120 미만일 때를 제외하고 `SET LANGUAGE` 문을 무시합니다.

```sql
SET DATEFORMAT dmy;
DECLARE @t2 date = '12/5/2011' ;
SET LANGUAGE dutch;
SELECT CONVERT(varchar(11), @t2, 106);

-- Results when the compatibility level is less than 120.
12 May 2011

-- Results when the compatibility level is set to 120).
12 mei 2011
```

### <a name="c-for-compatibility-level-setting-of-110-or-lower-recursive-references-on-the-right-hand-side-of-an-except-clause-create-an-infinite-loop"></a>C. 110 이하의 호환성 수준 설정의 경우 EXCEPT 절의 오른쪽에 있는 재귀 참조는 무한 루프를 만듭니다.

```sql
WITH
cte AS (SELECT * FROM (VALUES (1),(2),(3)) v (a)),
r
AS (SELECT a FROM Table1
UNION ALL
(SELECT a FROM Table1 EXCEPT SELECT a FROM r) )
SELECT a
FROM r;

```

### <a name="d-the-difference-between-styles-0-and-121"></a>D. 스타일 0과 스타일 121의 차이입니다.

날 짜 및 시간 스타일에 대한 자세한 내용은 [CAST 및 CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요.

```sql
CREATE TABLE t1 (c1 time(7), c2 datetime2);

INSERT t1 (c1,c2) VALUES (GETDATE(), GETDATE());

SELECT CONVERT(nvarchar(16),c1,0) AS TimeStyle0
       ,CONVERT(nvarchar(16),c1,121)AS TimeStyle121
       ,CONVERT(nvarchar(32),c2,0) AS Datetime2Style0
       ,CONVERT(nvarchar(32),c2,121)AS Datetime2Style121
FROM t1;

-- Returns values such as the following.
TimeStyle0       TimeStyle121
Datetime2Style0      Datetime2Style121
---------------- ----------------
-------------------- --------------------------
3:15PM           15:15:35.8100000
Jun  7 2011  3:15PM  2011-06-07 15:15:35.8130000
```

### <a name="e-variable-assignment---top-level-union-operator"></a>E. 변수 할당 - 최상위 UNION 연산자
최상위 UNION 연산자가 포함된 문에 변수를 할당할 수 있지만 예상치 않은 결과가 반환됩니다. 예를 들어 다음 문에서 지역 변수 `@v`에는 두 테이블의 합집합의 열 `BusinessEntityID` 값이 할당됩니다. 원래 SELECT 문에서 둘 이상의 값을 반환하면 반환된 값 중 마지막 값이 변수에 할당됩니다. 이 경우 변수에 마지막 값이 올바르게 할당되지만 SELECT UNION 문의 결과 집합도 함께 반환됩니다.

```sql
ALTER DATABASE AdventureWorks2012
SET compatibility_level = 110;
GO
USE AdventureWorks2012;
GO
DECLARE @v int;
SELECT @v = BusinessEntityID FROM HumanResources.Employee
UNION ALL
SELECT @v = BusinessEntityID FROM HumanResources.EmployeeAddress;
SELECT @v;
```

최상위 UNION 연산자가 포함된 문에는 변수를 할당할 수 없습니다. 오류 10734가 반환됩니다. 오류를 해결하려면 다음 예와 같이 쿼리를 다시 작성합니다.

```sql
DECLARE @v int;
SELECT @v = BusinessEntityID FROM
    (SELECT BusinessEntityID FROM HumanResources.Employee
     UNION ALL
     SELECT BusinessEntityID FROM HumanResources.EmployeeAddress) AS Test;
SELECT @v;
```

## <a name="see-also"></a>참고 항목 
[호환성 인증](../../database-engine/install-windows/compatibility-certification.md)       
[데이터베이스 변경](../../t-sql/statements/alter-database-transact-sql.md)       
[예약 키워드](../../t-sql/language-elements/reserved-keywords-transact-sql.md)       
[CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md)       
[DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)       
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)       
[sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)       
[데이터베이스의 호환성 수준 보기 또는 변경](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)       
[데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)       
[쿼리 튜닝 도우미를 사용하여 데이터베이스 업그레이드](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)
