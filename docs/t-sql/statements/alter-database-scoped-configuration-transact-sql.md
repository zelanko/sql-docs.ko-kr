---
title: ALTER DATABASE SCOPED CONFIGURATION (Transact SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- ALTER_DATABASE_SCOPED_CONFIGURATION
- ALTER_DATABASE_SCOPED_CONFIGURATION_TSQL
- DATABASE_SCOPED_CONFIGURATION_TSQL
- SCOPED_CONFIGURATION_TSQL
- SCOPED_TSQL
- ALTER_DATABASE_SCOPED_TSQL
- DATABASE_SCOPED_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CONFIGURATION statement
- configuration [SQL Server], ALTER DATABASE SCOPED CONFIGURATION statement
ms.assetid: 63373c2f-9a0b-431b-b9d2-6fa35641571a
caps.latest.revision: 32
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: fce97e74e2b4bbc5ae0fbdadf596734677734155
ms.contentlocale: ko-kr
ms.lasthandoff: 10/17/2017

---
# <a name="alter-database-scoped-configuration-transact-sql"></a>ALTER DATABASE SCOPED CONFIGURATION (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 문을에서 다양 한 데이터베이스 구성 설정을 사용 하면는 **개별 데이터베이스** 수준입니다. 이 문을 모두에서 사용할 수 있는지 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 및 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]합니다. 이러한 설정은 다음과 같습니다.  
  
- 프로시저 캐시를 지웁니다.  
  
- 주 데이터베이스의 경우 MAXDOP 매개 변수를 해당 데이터베이스에 가장 적합한 임의 값(1,2, ...)으로 설정하고 사용되는 보조 데이터베이스에는 다른 값(예: 0)을 설정합니다.  
  
- 데이터베이스와 관계없이 쿼리 최적화 프로그램 카디널리티 추정 모델을 호환성 수준으로 설정합니다.  
  
- 데이터베이스 수준에서 매개 변수 스니핑을 사용하거나 사용하지 않도록 설정합니다.
  
- 데이터베이스 수준에서 쿼리 최적화 프로그램 핫픽스를 사용하거나 사용하지 않도록 설정합니다.

- 데이터베이스 수준에서 id 캐시를 사용 하지 않도록 설정 하거나 사용 합니다.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER DATABASE SCOPED CONFIGURATION  
{        
     {  [ FOR SECONDARY] SET <set_options>  }    
}  
| CLEAR PROCEDURE_CACHE  
| SET < set_options >
[;]    
  
< set_options > ::=    
{  
    MAXDOP = { <value> | PRIMARY}    
    | LEGACY_CARDINALITY_ESTIMATION = { ON | OFF | PRIMARY}    
    | PARAMETER_SNIFFING = { ON | OFF | PRIMARY}    
    | QUERY_OPTIMIZER_HOTFIXES = { ON | OFF | PRIMARY}
    | IDENTITY_CACHE = { ON | OFF }
}  
```  
  
## <a name="arguments"></a>인수  
 
보조에 대 한  
 
보조 데이터베이스 (모든 보조 데이터베이스가 동일한 값을 가져야 합니다)에 대 한 설정을 지정 합니다.  
  
MAXDOP  **=**  {\<값 > | 기본}  
**\<값 >**  
  
문에 대 한 설정 MAXDOP를 사용 해야 기본을 지정 합니다. 0 값은 기본값 및 서버 구성 대신 사용 됩니다. 데이터베이스 범위에 대 한 MAXDOP (0으로 설정 되어) 있지 재정의 **x degree of** sp_configure로 서버 수준에서 설정 합니다. 쿼리 힌트는 DB 재정의할 수도 있습니다 MAXDOP 다른 설정을 필요로 하는 특정 쿼리를 조정 하기 위해 범위가 지정 합니다. 이러한 모든 설정은 작업 그룹에 대 한 설정 MAXDOP 제한 됩니다.   

max degree of parallelism 옵션을 사용하여 병렬 계획 실행에 사용할 프로세서 수를 제한할 수 있습니다. SQL Server 쿼리, 인덱스 데이터 정의 언어 (DDL) 작업, 병렬 삽입에 대 한 병렬 실행 계획으로 간주, 온라인 열, 병렬 통계 collectiion 및 정적 커서와 키 집합 커서 채우기의 변경 합니다.
 
인스턴스 수준에서이 옵션을 설정 하려면 참조 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)합니다. 

> [!TIP] 
> 이를 위해 쿼리 수준에서 추가 된 **MAXDOP** [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md)합니다.  
  
PRIMARY  
  
주 서버, 데이터베이스에는 동안 보조 데이터베이스에만 설정할 수 있습니다 및 구성을 기본 데이터베이스에 설정 된 것을 나타냅니다. 기본 변경 내용이 보조 데이터베이스에 있는 값에 대 한 구성을 변경 않을 경우 적절 하 게 설정할 필요 없이 보조 서버의 값 명시적으로 되어 있어야 합니다. **기본** 보조 데이터베이스에 대 한 기본 설정입니다.  
  
LEGACY_CARDINALITY_ESTIMATION  **=**  {ON | **OFF** | 기본}  

SQL Server 2012 및 이전 버전에 쿼리 최적화 프로그램 카디널리티 추정 모델을 데이터베이스의 호환성 수준에 관계 설정할 수 있습니다. 기본값은 **OFF**, 쿼리 최적화 프로그램 카디널리티 추정 모델 데이터베이스의 호환성 수준에 따라로 설정 합니다. 이 값을 설정 **ON** 사용 하도록 설정 하는 것과 같습니다 [추적 플래그 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)합니다. 

> [!TIP] 
> 이를 위해 쿼리 수준에서 추가 된 **QUERYTRACEON** [쿼리 힌트](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)합니다. 부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] s p 1이를 위해 쿼리 수준에서 추가 **USE 힌트** [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md) 추적 플래그를 사용 하는 대신 합니다. 
  
PRIMARY  
  
이 값은 보조 복제본에서 주 서버, 데이터베이스 하는 동안에 유효 하 고 모든 보조 복제본에서 쿼리 최적화 프로그램 카디널리티 추정 모델 설정을 기본 데이터베이스에 설정 된 값이 되도록 지정 합니다. 쿼리 최적화 프로그램 카디널리티 추정 모델에 대 한 주 서버에서 구성을 변경 하는 경우 보조 데이터베이스에 있는 값이 그에 따라 변경 됩니다. **기본** 보조 데이터베이스에 대 한 기본 설정입니다.  
  
PARAMETER_SNIFFING  **=**  { **ON** | OFF | 기본}  

설정 하거나 해제 [매개 변수 스니핑](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)합니다. 기본값은 ON입니다. 이 설정은 [추적 플래그 4136](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)과 동일합니다.   

> [!TIP] 
> 이를 위해 쿼리 수준에서 참조 된 **OPTIMIZE FOR UNKNOWN** [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md)합니다. 부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 쿼리 수준에서 이렇게 하려면 s p 1는 **USE 힌트** [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md) 제공 됩니다. 
  
PRIMARY  
  
이 값은 보조 복제본에서 주 서버, 데이터베이스 하는 동안에 유효 하 고 모든 보조 복제본에서이 설정에 대 한 값 기본 데이터베이스에 설정 된 값이 되도록 지정 합니다. 경우에 사용 하기 위한 기본 구성 [매개 변수 스니핑](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing) 변경 내용을 보조 항목에 값이 변경 됩니다 적절 하 게 명시적으로 되어 있어야 값 보조 데이터베이스를 설정할 필요 없이 합니다. 보조 데이터베이스에 대 한 기본 설정입니다.  
  
QUERY_OPTIMIZER_HOTFIXES  **=**  {ON | **OFF** | 기본}  

데이터베이스의 호환성 수준에 관계 없이 쿼리 최적화 핫픽스를 사용 하지 않도록 설정 하거나 사용 합니다. 기본값은 **OFF**를 해제 합니다. 쿼리 최적화 핫픽스는 특정 버전에 대 한 가장 높은 호환성 수준 도입 된 후에 릴리스된입니다 (post RTM). 이 값을 설정 **ON** 사용 하도록 설정 하는 것과 같습니다 [추적 플래그 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)합니다.   

> [!TIP] 
> 이를 위해 쿼리 수준에서 추가 된 **QUERYTRACEON** [쿼리 힌트](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)합니다. 부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] s p 1이를 위해 쿼리 수준에서 사용 하 여 힌트 추가 [쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md) 추적 플래그를 사용 하는 대신 합니다.  
  
PRIMARY  
  
이 값은 보조 복제본에서 주 서버, 데이터베이스 하는 동안에 유효 하 고 모든 보조 복제본에서이 설정에 대 한 값 기본 데이터베이스에 설정 된 값이 되도록 지정 합니다. 기본 변경 내용이 보조 데이터베이스에 있는 값에 대 한 구성을 변경 않을 경우 적절 하 게 설정할 필요 없이 보조 서버의 값 명시적으로 되어 있어야 합니다. 보조 데이터베이스에 대 한 기본 설정입니다.  
  
지우기 PROCEDURE_CACHE  

데이터베이스에 대 한 절차 (계획) 캐시를 지웁니다. 주 데이터베이스와 보조 데이터베이스에서 모두 실행할 수 있습니다.  

IDENTITY_CACHE  **=**  { **ON** | OFF}  

**적용 대상**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] (기능은 공개 미리 보기 상태에서) 

데이터베이스 수준에서 id 캐시를 사용 하지 않도록 설정 하거나 사용 합니다. 기본값은 **ON**합니다. Identity 캐싱 id 열이 있는 테이블에서 삽입 성능을 개선 하기 위해 사용 됩니다. 서버가 예기치 않게 다시 시작 하거나 장애 조치 한 보조 서버에 있는 경우에 id 열 값 간의 간격을 방지 하려면 IDENTITY_CACHE 옵션을 사용 하지 않도록 설정 합니다. 이 옵션은 기존 비슷합니다 [추적 플래그 272](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)한다는 점을 제외 하는 서버 수준 에서만 아니라 데이터베이스 수준에서 설정할 수 있습니다.   

> [!NOTE] 
> 이 옵션은 기본 데이터베이스에 설정할 수 있습니다. 자세한 내용은 참조 [id 열](create-table-transact-sql-identity-property.md)합니다.  

##  <a name="Permissions"></a> 사용 권한  
 필요한 모든 데이터베이스 범위 구성 변경   
에 데이터베이스입니다. 데이터베이스에 대 한 CONTROL 권한이 있는 사용자가이 사용 권한을 부여할 수 있습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 보조 데이터베이스가 해당 주 서로 다른 범위 지정 된 구성 설정이 적용을 구성할 수도 있지만, 모든 보조 데이터베이스가 동일한 구성을 사용 합니다. 각 보조 복제본에 대 한 다양 한 설정은 구성할 수 없습니다.  
  
 이 문을 실행 하면 모든 쿼리를 다시 컴파일해야 할 합니다 즉 현재 데이터베이스에서 프로시저 캐시를 지워집니다.  
  
 3 부분으로 된 이름 쿼리에 대 한 쿼리에 대 한 현재 데이터베이스 연결에 대 한 설정을 현재 데이터베이스 컨텍스트에서 컴파일되는 SQL 모듈 (예:: 프로시저, 함수 및 트리거)에 대 한 외의 다른 적용 되 고 따라서의 옵션을 사용 합니다.는 존재 하는 데이터베이스입니다.  
  
 ALTER_DATABASE_SCOPED_CONFIGURATION 이벤트는 DDL 트리거를 시작 하는 데 사용할 수 있는 DDL 이벤트로 추가 됩니다. 이것이 ALTER_DATABASE_EVENTS 트리거 그룹의 자식입니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
**MAXDOP**  
  
 세부적인 설정을 있는 전역 구성을 재정의 하 고 해당 리소스 관리자는 다른 모든 MAXDOP 설정을 닫을 수 있습니다.  MAXDOP 설정에 대 한 논리는 다음과 같습니다.  
  
-   쿼리 힌트는 sp_configure와 범위를 한 데이터베이스 설정 보다 우선 합니다. 리소스 그룹 MAXDOP 작업 그룹에 대 한 설정 되어 있습니다.  
  
    -   쿼리 힌트를 0으로 설정 된 경우 리소스 관리자 설정에 의해 재정의 됩니다.  
  
    -   쿼리 힌트는 0, it 하지 하는 경우는 리소스 관리자 설정에 의해 제한 됩니다.  
  
-   DB 범위 (0이 아니면) 설정 하지 않으면 쿼리 힌트는 sp_configure 설정 보다 우선 하 고 리소스 관리자 설정에 의해 제한 됩니다.  
  
-   Sp_configure 설정은 리소스 관리자 설정에 의해 재정의 됩니다.  
  
**QUERY_OPTIMIZER_HOTFIXES**  
  
 레거시 쿼리 최적화 프로그램 또는 쿼리 최적화 프로그램 핫픽스를 사용할 수 있도록 QUERYTRACEON 힌트를 사용 하면 쿼리 힌트 및 데이터베이스 범위 구성 설정, 의미 중 하나를 사용 하는 경우에 옵션이 적용 됩니다 사이 OR 조건을 것입니다.  
  
**GeoDR**  
  
 예: Always On 가용성 그룹 및 GeoReplication을 읽기 가능한 보조 데이터베이스는 데이터베이스의 상태를 확인 하 여 보조 값을 사용 합니다. म 하지 않는 장애 조치 시 다시 컴파일하고 기술적으로 새 주 데이터베이스는 보조 설정을 사용 하는 쿼리, 있더라도 개념은 다른 워크 로드를 하 고 따라서 캐시 된 쿼리는 기본 및 보조 간 설정만 달라 집니다. 새 쿼리는 자신에 게 해당 하는 새 설정을 선택 하는 반면 최적의 설정을 사용 하 여 합니다.  
  
**DacFx**  
  
 내보내기 (데이터 없이 또는) 스키마의 예를 들어 이전 버전의 SQL Server로 가져와야 할 수 ALTER DATABASE SCOPED CONFIGURATION Azure SQL 데이터베이스 및 데이터베이스 스키마에 영향을 주는 SQL Server 2016의 새로운 기능 이므로, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 또는 < c2 > [!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)] 합니다. 예를 들어로 내보내기를 [DACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) 또는 [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) 에서 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 또는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이 새로운 기능을 사용 데이터베이스를 하위 수준 서버로 가져올 수 없게 됩니다.  
  
## <a name="metadata"></a>메타데이터  

[sys.database_scoped_configurations&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 시스템 뷰는 데이터베이스 내에서 범위 지정 된 구성에 대 한 정보를 제공 합니다. 데이터베이스 범위 구성 옵션 표시 sys.database_scoped_configurations 멤버인 서버 차원의 기본 설정으로 재정의 합니다. [sys.configurations&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 시스템 뷰는 서버 수준의 설정을 표시 합니다.  
  
## <a name="examples"></a>예  
이 예에서는 ALTER DATABASE SCOPED CONFIGURATION의 사용을 보여 줍니다.  
  
### <a name="a-grant-permission"></a>1. 권한 부여  

이 예에서는 ALTER DATABASE SCOPED CONFIGURATION을 실행 하는 데 필요한 사용 권한 부여     
사용자 [Joe].  
  
```tsql  
GRANT ALTER ANY DATABASE SCOPED CONFIGURATION to [Joe] ;  
```  
  
### <a name="b-set-maxdop"></a>2. MAXDOP를 설정 합니다.  

MAXDOP를 설정 하는이 예제 = 1 주 데이터베이스 및 MAXDOP = 4 지리적 복제 시나리오에서 보조 데이터베이스에 대 한 합니다.  
  
```tsql  
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 1 ;  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=4 ;  
```  
  
이 예에서는 지역 간 복제 시나리오에 해당 주 데이터베이스에 대해 설정 되어 있어서 동일 해야 보조 데이터베이스의 MAXDOP를 설정 합니다.  
  
```tsql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=PRIMARY ;
```  
  
### <a name="c-set-legacycardinalityestimation"></a>3. LEGACY_CARDINALITY_ESTIMATION 설정  

이 예에서는 지역 간 복제 시나리오에서 보조 데이터베이스에 대해 ON으로 LEGACY_CARDINALITY_ESTIMATION를 설정합니다.  
  
```tsql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=ON ;  
```  
  
이 예에서는 지역 간 복제 시나리오에 해당 주 데이터베이스의 경우와 보조 데이터베이스에 대 한 LEGACY_CARDINALITY_ESTIMATION을 설정 합니다.  
  
```tsql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=PRIMARY ;  
```  
  
### <a name="d-set-parametersniffing"></a>4. PARAMETER_SNIFFING 설정  

이 예에서는 지역 간 복제 시나리오에서 주 데이터베이스에 대해 OFF로 PARAMETER_SNIFFING를 설정합니다.  
  
```tsql  
ALTER DATABASE SCOPED CONFIGURATION SET PARAMETER_SNIFFING =OFF ;  
```  
  
이 예에서는 지역 간 복제 시나리오에서 주 데이터베이스에 대해 OFF로 PARAMETER_SNIFFING를 설정합니다.  
  
```tsql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=OFF ;  
```  
  
이 예제에서는 설정 PARAMETER_SNIFFING 보조 데이터베이스에 대 한 주 데이터베이스에 있음   
지리적 복제 시나리오입니다.  
  
```tsql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=PRIMARY ;  
```  
  
### <a name="e-set-queryoptimizerhotfixes"></a>5. QUERY_OPTIMIZER_HOTFIXES 설정  

주 데이터베이스에 대 한 QUERY_OPTIMIZER_HOTFIXES ON으로 설정   
지리적 복제 시나리오입니다.  

```tsql  
ALTER DATABASE SCOPED CONFIGURATION SET QUERY_OPTIMIZER_HOTFIXES=ON ;  
```  
  
### <a name="f-clear-procedure-cache"></a>6. 프로시저 캐시 지우기  

이 예에서는 프로시저 캐시를 (주 데이터베이스에 대해서만 사용 가능)를 지웁니다.  
  
```tsql  
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE ;  
```  

### <a name="g-set-identitycache"></a>7. IDENTITY_CACHE 설정

**적용 대상**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] (기능은 공개 미리 보기 상태에서) 

이 예제는 id 캐시를 해제합니다.

```tsql 
ALTER DATABASE SCOPED CONFIGURATION SET IDENTITY_CACHE=OFF ; 
```

## <a name="additional-resources"></a>추가 리소스

### <a name="maxdop-resources"></a>MAXDOP 리소스 
* [병렬 처리 수준](../../relational-databases/query-processing-architecture-guide.md#DOP)
* [SQL Server에서 "max degree of parallelism" 구성 옵션에 대 한 지침 및 권장 사항](https://support.microsoft.com/en-us/kb/2806535) 

### <a name="legacycardinalityestimation-resources"></a>LEGACY_CARDINALITY_ESTIMATION 리소스    
* [카디널리티 추정 (SQL Server)](../../relational-databases/performance/cardinality-estimation-sql-server.md)
* [SQL Server 2014 카디널리티 추정기로 쿼리 계획 최적화](https://msdn.microsoft.com/library/dn673537.aspx)

### <a name="parametersniffing-resources"></a>PARAMETER_SNIFFING 리소스    
* [매개 변수 검색](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)
* ["냄새가 나 매개 변수는!"](https://blogs.msdn.microsoft.com/queryoptteam/2006/03/31/i-smell-a-parameter/)

### <a name="queryoptimizerhotfixes-resources"></a>QUERY_OPTIMIZER_HOTFIXES 리소스    
* [추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
* [SQL Server 쿼리 최적화 프로그램 핫픽스 추적 플래그 4199 서비스 모델](https://support.microsoft.com/en-us/kb/974006)

## <a name="more-information"></a>자세한 정보  
 [sys.database_scoped_configurations&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)   
 [sys.configurations&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [데이터베이스 및 파일 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [서버 구성 옵션 &#40; SQL Server &#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md) [sys.configurations&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)  
  
  

