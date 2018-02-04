---
title: DATABASE Compatibility LEVEL (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/30/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 750578d028077079b051a08cc2a0ed4276983cda
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="alter-database-transact-sql-compatibility-level"></a>ALTER DATABASE (Transact SQL) 호환성 수준
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

특정 데이터베이스 동작이 지정된 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 호환되도록 설정합니다. 다른 ALTER DATABASE 옵션을 참조 하세요. [ALTER database&#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER DATABASE database_name   
SET COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 | 90 }  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 수정할 데이터베이스의 이름입니다.  
  
 COMPATIBILITY_LEVEL {140 | 130 | 120 | 110 | 100 | 90 | 80}  
 데이터베이스가 호환되도록 설정할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전입니다. 다음 호환성 수준 값을 구성할 수 있습니다.  
  
|Product|데이터베이스 엔진 버전|호환성 수준 지정|지원 되는 호환성 수준 값|  
|-------------|-----------------------------|-------------------------------------|------------------------------------------|  
|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]|14|140|140, 130, 120, 110, 100|
|[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|12|130|140, 130, 120, 110, 100|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|13|130|130, 120, 110, 100|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|12|120|120, 110, 100|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|11|110|110, 100, 90|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|10.5|100|100, 90, 80|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|10|100|100, 90, 80|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|9|90|90, 80|  
|SQL Server 2000|8|80|80|  
  
> [!NOTE]  
> **Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]**  V12 2014 년 12 월에에서 발표 되었습니다. 출시에의 한 가지 측면인 새로 만든된 데이터베이스의 호환성 수준은 120으로 설정 했습니다. 2015 SQL 데이터베이스 기본값 120으로 남아 있지만 수준 130에 대 한 지원을 시작 했습니다.  
> 
> 부터는 **mid-2016 년 6 월**에 [!INCLUDE[ssSDS](../../includes/sssds-md.md)], 기본 호환성 수준 130에 대 한 120 대신는 **새로 만든** 데이터베이스. Mid-2016 년 6 월 이전에 만든 기존 데이터베이스는 영향을 받지 및 (100, 110, 또는 120)는 현재 호환성 수준을 유지 합니다. 
> 
> 일반적으로 데이터베이스에 대 한 수준 130을 원하는 수준 110 선호 하는 이유가 있는 경우 **카디널리티 추정** 알고리즘 참조 [ALTER DATABASE SCOPED configuration&#40; Transact SQL &#41; ](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md), 특히 및 해당 키워드 `LEGACY_CARDINALITY_ESTIMATION = ON`합니다.  
>  
>  두 호환성 수준은 간의 가장 중요 한 쿼리의 성능 차이 평가 하는 방법에 대 한 내용은 [!INCLUDE[ssSDS](../../includes/sssds-md.md)], 참조 [Azure SQL 데이터베이스의 호환성 수준을 130으로 쿼리 성능을 향상](http://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)합니다.


 버전을 확인 하려면 다음 쿼리를 실행 된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결 되어 있는 합니다.  
  
```sql  
SELECT SERVERPROPERTY('ProductVersion');  
```  
  
> [!NOTE]  
> 호환성 수준에 따라 달라 지는 일부 기능에서 지원 됩니다 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  

 현재 호환성 수준을 확인 하려면 쿼리는 **compatibility_level** 열 [sys.databases&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
```sql  
SELECT name, compatibility_level FROM sys.databases;  
```  
  
## <a name="remarks"></a>주의  
모든 설치에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 기본 호환성 수준을의 버전으로 설정 되는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]합니다. 데이터베이스는이 수준으로 설정 하지 않으면는 **모델** 데이터베이스의 호환성 수준이 이보다 낮지 합니다. 데이터베이스의 이전 버전에서 업그레이드할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 데이터베이스는 최소 이상 해당 인스턴스에 대 한 허용 하는 경우의 기존 호환성 수준이 유지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 허용 된 수준 보다 낮은 호환성 수준으로 데이터베이스를 업그레이드 하는, 데이터베이스 허용 수준이 가장 낮은 호환성 설정 합니다. 이는 시스템 및 사용자 데이터베이스 모두에 적용됩니다. 사용 하 여 **ALTER DATABASE** 데이터베이스의 호환성 수준을 변경할 수 있습니다. 데이터베이스의 현재 호환성 수준을 보려면, 쿼리는 **compatibility_level** 열에는 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰.  
  
## <a name="using-compatibility-level-for-backward-compatibility"></a>이전 버전과의 호환을 위해 호환성 수준 사용  
 호환성 수준은 전체 서버가 아닌 지정된 데이터베이스의 동작에만 적용됩니다. 호환성 수준은 부분적으로만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전과의 호환성을 제공합니다. 호환 모드 130 이상에서는 새로운 쿼리 계획에 영향을 주는 기능 새 호환성 모드에만 추가 되었습니다. 쿼리 계획 변경으로 인해 성능이 저하 될 때 발생 하는 업그레이드 중 위험을 최소화 하기 위해이 수행 하지 않았습니다. 응용 프로그램 관점에서 목표를 최신 호환성 수준 수는 쿼리 최적화 프로그램은 공간에서 수행 하는 성능 향상 뿐만 아니라 새로운 기능 중 일부를 상속 하기 위해 있지만 이렇게 하려면 적절된 한 방법에서 여전히입니다. 중간 마이그레이션 도구로 호환성 수준을 사용하여 관련 호환성 수준 설정에서 제어하는 동작의 버전 차이를 해결할 수 있습니다. 자세한 내용은 뒷부분에서 업그레이드 모범 사례를 참조 합니다.  
  
 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 응용 프로그램의 사용 중인 버전에서 동작의 차이 영향 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 새 호환성 모드와 매끄럽게 작동 하도록 응용 프로그램으로 변환 합니다. 다음 사용 하 여 `ALTER DATABASE` 을 호환성 수준을 130으로 변경 합니다. 데이터베이스에 대 한 새로운 호환성 설정은 하면 적용 됩니다는 `USE <database>` 발급 또는 새 로그인 기본 데이터베이스와 해당 데이터베이스를 사용 하 여 처리 됩니다.  
 
> [!IMPORTANT]
> 에 도입 된 기능을 지원 되지 않는 한 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 호환성 수준으로 보호 되지 않습니다.
> 
> 예를 들어는 `FASTFIRSTROW` 힌트에서 더 이상 사용할 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 대체는 `OPTION (FAST n )` 힌트입니다. 데이터베이스 호환성 수준을 110으로 설정 지원 되지 않는 힌트를 복원 하지 않습니다.
> 지원 되지 않는 기능에 대 한 자세한 내용은 참조 하십시오. [SQL Server 2016에서 데이터베이스 엔진 기능 지원 되지 않는](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md), [SQL Server 2014에서 데이터베이스 엔진 기능 지원 되지 않는](http://msdn.microsoft.com/library/ms144262(v=sql.120)), [지원 되지 않는 SQL Server 2012의에서 데이터베이스 엔진 기능](http://msdn.microsoft.com/library/ms144262(v=sql.110)), 및 [지원 되지 않는 SQL Server 2008에서에서 데이터베이스 엔진 기능](http://msdn.microsoft.com/library/ms144262(v=sql.100))합니다.

> [!IMPORTANT]
> 에 도입 된 주요 변경 내용은 주어진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 **수 있습니다** 호환성 수준에 따라 보호 되지 않습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]동작은 호환성 수준에 따라 일반적으로 보호 됩니다. 그러나 변경 되거나 제거 된 시스템 개체는 **하지** 호환성 수준으로 보호 합니다.
>
> 주요 변경의 예가 **보호** 호환성 수준을 datetime2 데이터 형식으로 날짜/시간에서의 암시적 변환이 있습니다. 데이터베이스 호환성 수준 130에서 이러한 표시 정확성 향상된 소수 자릿수 밀리초를 고려 하 여 결과적으로 다른 값을 변환 합니다. 이전 변환 동작을 복원 하려면 데이터베이스 호환성 수준을 120 이하로 설정 합니다.
>
> 주요 변경의 예가 **보호 되지 않는** 수준이 호환성:
> -  시스템 개체의 변경 된 열 이름입니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 열 *single_pages_kb* sys.dm_os_sys_info에서로 변경 되어 *pages_kb*합니다. 쿼리는 호환성 수준에 관계 없이 `SELECT single_pages_kb FROM sys.dm_os_sys_info` 오류 207 (잘못 된 열 이름)을 생성 합니다.
> -  제거 된 시스템 개체입니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 는 `sp_dboption` 제거 되었습니다. 문은 호환성 수준에 관계 없이 `EXEC sp_dboption 'AdventureWorks2016CTP3', 'autoshrink', 'FALSE';` 오류 2812 (찾을 수 없음 저장된 프로시저 'sp_dboption')를 생성 합니다.
>
> 주요 변경 내용에 대 한 자세한 내용은 참조 하십시오. [SQL Server 2017에 데이터베이스 엔진 기능의 주요 변경 내용](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2017.md), [SQL Server 2016 데이터베이스 엔진 기능의 주요 변경 내용](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md), [ 데이터베이스에 주요 변경 내용은 엔진에서는 SQL Server 2014 기능](http://msdn.microsoft.com/library/ms143179(v=sql.120)), [SQL Server 2012 데이터베이스 엔진 기능의 주요 변경 내용](http://msdn.microsoft.com/library/ms143179(v=sql.110)), 및 [SQL 데이터베이스 엔진 기능의 주요 변경 내용 서버 2008](http://msdn.microsoft.com/library/ms143179(v=sql.100))합니다.
  
## <a name="best-practices"></a>최선의 구현 방법  
호환성 수준을 업그레이드에 대 한 권장된 워크플로 참조 하십시오. [데이터베이스 호환성 모드 변경 및 쿼리 저장소를 사용 하 여](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)합니다.  
  
## <a name="compatibility-levels-and-stored-procedures"></a>호환성 수준 및 저장 프로시저  
 저장 프로시저가 실행될 때 저장 프로시저는 정의된 데이터베이스의 현재 호환성 수준을 사용합니다. 데이터베이스의 호환성 설정이 변경되면 모든 저장 프로시저도 그에 맞게 자동으로 다시 컴파일됩니다.  

## <a name="differences-between-compatibility-level-130-and-level-140"></a>호환성 수준 130와 수준 140 차이점  
이 섹션에서는 호환성 수준 140으로 정의 된 새로운 동작을 설명 합니다.

|130 또는 더 낮은 호환성 수준 설정|140의 호환성 수준 설정|  
|--------------------------------------------------|-----------------------------------------|  
|함수는 고정된 행 추측을 사용 하 여 다중 문 테이블 반환을 참조 하는 문에 대 한 카디널리티 예상치입니다.|함수는 함수 출력의 실제 카디널리티를 사용 하는 적합 한 문이 참조 하는 다중 문 테이블 반환에 대 한 카디널리티 예상치입니다.  이 통해 사용 **실행을 인터리빙 된** 다중 문 테이블 반환 함수에 대 한 합니다.|
|메모리가 부족 하 여 요청 하는 일괄 처리 모드 쿼리는 디스크에 작업의 결과에 연속 실행 문제를 계속할 수 있는 크기를 부여 합니다.|디스크에 작업의 결과 수 연속 실행의 성능을 개선 했습니다 부족 한 메모리 부여 크기를 요청 하는 일괄 처리 모드 쿼리 합니다. 이 통해 사용 **일괄 처리 모드 메모리 부여 피드백** 그러면 spill 일괄 처리 모드 연산자에 대해 발생 한 경우에 캐시 된 계획의 메모리 부여 크기에 업데이트 됩니다. |
|과도 한 메모리를 요청 하는 일괄 처리 모드 쿼리 동시성 문제에 대 한 결과에 연속 실행 문제를 계속할 수 있는 크기를 부여 합니다.|과도 한 메모리를 요청 하는 일괄 처리 모드 쿼리 부여 향상 연속 실행에서 동시성 동시성 문제가 발생 하는 크기에 있습니다. 이 통해 사용 **일괄 처리 모드 메모리 부여 피드백** 그러면 요청한 지나치게 많은 경우 캐시 된 계획의 메모리 부여 크기 업데이트 됩니다.|
|조인 연산자를 포함 하는 일괄 처리 모드 쿼리는 중첩 된 루프, 해시 조인이 병합 조인이 등 세 개의 물리적 조인 알고리즘에 적합 합니다. 카디널리티 예측 조인 입력에 대 한 잘못 된 경우에 부적절 한 join 알고리즘을 선택할 수 있습니다. 이 경우 성능이 저하 됩니다 한 부적절 한 조인 알고리즘은 남아 있게 사용 중인 캐시 된 계획이 다시 컴파일됩니다.|호출 하는 추가 조인 연산자가 **적응 조인**합니다. 외부 빌드 조인 입력에 대 한 잘못 된 카디널리티 예상치는 부적절 한 조인 알고리즘을 선택할 수 있습니다. 이 문제가 발생 하는 경우 적응 조인에 대 한 대상이 되는 문이 중첩된 루프 조인 입력을 더 작은에 사용할 및 해시 조인에 사용할 큰 조인 입력 동적으로 다시 컴파일할 필요 없이 합니다. |
|Columnstore 인덱스를 참조 하는 간단한 계획은 일괄 처리 모드 실행 수 없습니다. |Columnstore 인덱스를 참조 하는 간단한 계획 일괄 처리 모드 실행에 해당 되는 계획 하기 위해 무시 됩니다.|
|`sp_execute_external_script` UDX 연산자 행 모드 에서만 실행할 수 있습니다.|`sp_execute_external_script` UDX 연산자는 일괄 처리 모드 실행으로 적합 합니다.|  
|다중 문 테이블 반환 함수 (TVF의) 인터리브 방식된으로 실행 하지 않은 |계획의 품질을 개선 하기 위해 다중 문 Tvf에 대 한 인터리브 방식된으로 실행 합니다. |

이전 버전의 SQL Server 2017 하기 전에 SQL Server에서 추적 플래그 4199 되 입니다는 이제 기본적으로 사용 됩니다. 호환 모드가 140입니다. 추적 플래그 4199 SQL Server 2017 이후에 릴리스되는 새로운 쿼리 최적화 프로그램 수정에 적용 됩니다. 추적 플래그 4199에 대 한 정보를 참조 하십시오. [추적 플래그 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199)합니다.  
  
## <a name="differences-between-compatibility-level-120-and-level-130"></a>호환성 수준 120 및 130 수준 간의 차이  
이 섹션에서는 호환성 수준 130에 도입 된 새로운 동작을 설명 합니다.   

|호환성 수준 설정 120 이하로|호환성 수준 130 설정|  
|--------------------------------------------------|-----------------------------------------|  
|Insert select 문 내에 삽입은 단일 스레드입니다.|Insert select 문 내에 삽입이 다중 스레드로 수행 또는 병렬 계획을 가질 수 있습니다.|  
|메모리 액세스에 최적화 된 테이블에 대 한 쿼리는 단일 스레드를 실행합니다.|이제 메모리 액세스에 최적화 된 테이블에 대 한 쿼리 병렬 계획을 가질 수 있습니다.|  
|SQL 2014 카디널리티 평가기를 도입 **CardinalityEstimationModelVersion = "120"**|자세한 카디널리티 추정 (CE) 쿼리에서 표시 되는 카디널리티 추정 모델 130 개선이 계획 합니다. **CardinalityEstimationModelVersion="130"**|  
|Columnstore 인덱스와 일괄 처리 모드와 행 모드 변경<br /><br /> 행 모드에 있는 Columnstore 인덱스가 있는 테이블에 정렬 합니다.<br /><br /> 기간 이동 함수 집계와 같은 행 모드에서 작동 `LAG` 또는`LEAD`<br /><br /> 여러 distinct 절 행 모드에서 작동할 수 있는 Columnstore 테이블에 대 한 쿼리<br /><br /> MAXDOP 1에서 실행 되거나 행 모드에서 실행 되는 직렬 계획을 사용 하는 쿼리 | Columnstore 인덱스와 일괄 처리 모드와 행 모드 변경<br /><br /> Columnstore 인덱스가 있는 테이블에 정렬 합니다. 현재 일괄 처리 모드 위치는<br /><br /> 기간 이동 집계 이제 일괄 처리 모드로 작동와 같은 `LAG` 또는`LEAD`<br /><br /> 여러 distinct 절이 있는 Columnstore 테이블에 대 한 쿼리 일괄 처리 모드로 작동<br /><br /> Maxdop1에서 실행 되거나 직렬 계획을 사용 하는 쿼리 일괄 처리 모드에서 실행|  
| 통계를 자동으로 업데이트할 수 있습니다. | 자동으로 통계를 업데이트 하는 논리는 대형 테이블에 더 엄격한입니다.  실제로이 사례가 고객 위치는 통계에 업데이트 되지 해당 값을 포함 하지만 자주 새로 삽입된 된 행을 쿼리 하는 위치 쿼리 성능 문제를 표시 한 줄여야 합니다. |  
| 2371 추적에 기본적으로 꺼져 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]합니다. | [2371 추적](https://blogs.msdn.microsoft.com/psssql/2016/10/04/default-auto-statistics-update-threshold-change-for-sql-server-2016/) 에 기본적으로 켜져 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]합니다. 추적 플래그 2371을 매우 많은 행이 있는 테이블에서 행의 더 작은 아직 현명 해 집니다 일부만 샘플링 자동 통계 업데이트 도구를 알려 줍니다. <br/> <br/> 하나의 개선 최근에 삽입 된 행이 이상 샘플에 포함 하는 것입니다. <br/> <br/> 개선 된 또 다른 업데이트 통계 프로세스는 실행을 차단 하기 보다는 쿼리 하는 동안 실행 하는 쿼리를 사용 하는 것입니다. |  
| 수준 120에 대 한 통계에서 샘플링 된 *단일*-프로세스 스레드입니다. | 수준 130에 대 한 통계에서 샘플링 된 *다중*-프로세스 스레드입니다. |  
| 253 들어오는 외래 키에는 한계입니다. | 최대 10, 000 개의 들어오는 외래 키 또는 유사한 참조 하 여 지정된 된 테이블을 참조할 수 있습니다. 제한 사항에 대해서는 [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md)를 참조하세요. |  
|사용 되지 않는 MD2, MD4, MD5, SHA 및 SHA1 해시 알고리즘 허용 됩니다.|SHA2_256 및 SHA2_512 해시 알고리즘이 허용 됩니다.|
||[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 일부 데이터 형식 변환 및 (주로 드문) 일부 작업에 향상 된 기능을 포함합니다. 자세한 내용은 [일부 데이터 형식 및 일반적이 지 않은 작업을 처리 하는 SQL Server 2016 향상 된 기능](https://support.microsoft.com/help/4010261/sql-server-2016-improvements-in-handling-some-data-types-and-uncommon)합니다.|
  
수정 프로그램이에서 추적 플래그 4199 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전에 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이제 기본적으로 활성화 됩니다. 호환 모드가 130입니다. 추적 플래그 4199를 이후에 릴리스되는 새로운 쿼리 최적화 프로그램 수정에 대 한 적용 될 여전히 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]합니다. 이전 쿼리 최적화 프로그램에서 사용 하려면 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 호환성 수준 110 선택 해야 합니다. 추적 플래그 4199에 대 한 정보를 참조 하십시오. [추적 플래그 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199)합니다.  
  
## <a name="differences-between-lower-compatibility-levels-and-level-120"></a>낮은 호환성 수준과 수준 120 사이의 차이  
 이 섹션에서는 호환성 수준 120으로 정의된 새로운 동작에 대해 설명합니다.  
  
|호환성 수준 설정 110 이하|호환성 수준 설정 120|  
|--------------------------------------------------|-----------------------------------------|  
|이전 쿼리 최적화 프로그램이 사용됩니다.|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 만들고 쿼리 계획을 최적화 하는 구성 요소에 크게 향상 된 기능을 포함 합니다. 이러한 새로운 쿼리 최적화 프로그램 기능은 데이터베이스 호환성 수준 120의 사용에 따라 달라집니다. 이러한 향상된 기능을 활용하려면 데이터베이스 호환성 수준 120을 사용하여 새 데이터베이스 응용 프로그램을 개발해야 합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 마이그레이션된 응용 프로그램의 경우 좋은 성능이 유지되거나 향상되었는지 확인하려면 신중하게 테스트해야 합니다. 성능이 저하되면 데이터베이스 호환성 수준을 110 이하로 설정하여 이전 쿼리 최적화 프로그램 방법을 사용할 수 있습니다.<br /><br /> 데이터베이스 호환성 수준 120은 최신 데이터 웨어하우징 및 OLTP 작업에 대해 조정된 새로운 카디널리티 평가기를 사용합니다. 참조의 쿼리 계획 섹션에서 권장 하는 데이터베이스 호환성 수준이 110으로 성능 문제로 인해을 설정 하기 전에 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [데이터베이스 엔진의 새로운](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md) 항목입니다.|  
|120 미만의 호환성 수준에서 변환할 때 언어 설정이 무시 됩니다는 **날짜** 값을 문자열 값입니다. 이 동작에만 특정는 **날짜** 유형입니다. 아래 예 섹션의 예제 B를 참조 하십시오.|변환할 때 언어 설정이 무시 되지 않습니다는 **날짜** 값을 문자열 값입니다.|  
|오른쪽에 있는 재귀 참조는 `EXCEPT` 절 무한 루프를 만듭니다. 예 3 아래 예 섹션에서이 동작을 보여 줍니다.|재귀 참조는 `EXCEPT` 절은 ANSI SQL 표준에 따라 오류를 생성 합니다.|  
|재귀 공통 테이블 식 (CTE) 중복 된 열 이름을 허용합니다.|재귀적 CTE에서 중복 열 이름을 허용하지 않습니다.|  
|해제된 트리거는 트리거가 변경되는 경우 설정됩니다.|트리거를 변경하는 경우 트리거의 상태(설정 또는 해제)가 변경되지 않습니다.|  
|OUTPUT INTO 테이블 절을 무시 된 `IDENTITY_INSERT SETTING = OFF` 명시적 값을 삽입할 수 있습니다.|테이블에 id 열에 대 한 명시적 값을 삽입할 수 없을 때 `IDENTITY_INSERT` 가 OFF로 설정 합니다.|  
|데이터베이스 포함에 부분 설정 되 면 유효성 검사는 `$action` 필드에 `OUTPUT` 절은 `MERGE` 데이터 정렬 오류를 반환할 수 있습니다.|반환 하는 값의 데이터 정렬의 `$action` 절은 `MERGE` 문을 서버 데이터 정렬 대신 데이터베이스 데이터 정렬 이며 데이터 정렬 충돌 오류가 반환 되지 않습니다.|  
|`SELECT INTO` 문은 항상 단일 스레드 삽입 작업을 만듭니다.|`SELECT INTO` 문은 병렬 삽입 작업을 만들 수 있습니다. 많은 수의 행을 삽입하는 경우 병렬 작업은 성능을 향상시킬 수 있습니다.|  
  
## <a name="differences-between-lower-compatibility-levels-and-levels-110-and-120"></a>낮은 호환성 수준과 수준 110 및 120 사이의 차이  
 이 섹션에서는 호환성 수준 110으로 정의된 새로운 동작에 대해 설명합니다.   이 섹션은 또한 수준 120에도 적용됩니다.  
  
|호환성 수준 설정 100 이하|호환성 수준 설정 110 이상|  
|--------------------------------------------------|--------------------------------------------------|  
|CLR(공용 언어 런타임) 데이터베이스 개체는 CLR 버전 4를 사용하여 실행됩니다. 그러나 CLR 버전 4에 도입된 일부 동작 변경은 발생하지 않습니다. 자세한 내용은 참조 [CLR 통합의 새로운](../../relational-databases/clr-integration/clr-integration-what-s-new.md)합니다.|CLR 데이터베이스 개체는 CLR 버전 4를 사용하여 실행됩니다.|  
|XQuery 함수 **문자열 길이** 및 **부분 문자열** 각 서로게이트 두 문자로 계산 합니다.|XQuery 함수 **문자열 길이** 및 **부분 문자열** 각 서로게이트 한 문자로 계산 합니다.|  
|`PIVOT`재귀 공통 테이블 식 (CTE) 쿼리에서 허용 됩니다. 그러나 그룹화당 여러 행이 있는 경우에는 쿼리에서 잘못된 결과가 반환됩니다.|`PIVOT`재귀 공통 테이블 식 (CTE) 쿼리에서 허용 되지 않습니다. 오류가 반환됩니다.|  
|RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.|RC4 또는 RC4_128를 사용하여 새 자료를 암호화할 수 없습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.|  
|에 대 한 기본 스타일 `CAST` 및 `CONVERT` 에 대 한 작업 **시간** 및 **datetime2** 데이터 형식 유형 중 하나는 계산된 열 식에 사용 되는 경우를 제외 하 고는 121입니다. 계산 열의 경우 기본 스타일은 0입니다. 이 동작은 자동 매개 변수화와 관련된 쿼리에서 이러한 연산이 만들어지고 사용될 때 또는 제약 조건 정의에 사용될 때 계산 열에 영향을 줍니다.<br /><br /> 예 4 아래 예 섹션에서 스타일 0과 스타일 121의 차이점을 보여 줍니다. 위에서 설명한 동작은 보여 주지 않습니다. 날짜 및 시간 스타일에 대 한 자세한 내용은 참조 [CAST 및 convert&#40; Transact SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).|호환성 수준 110에서에 대 한 기본 스타일 `CAST` 및 `CONVERT` 에 대 한 작업 **시간** 및 **datetime2** 데이터 형식을 항상 121입니다. 쿼리에 이전 동작이 적용되는 경우 110보다 낮은 호환성 수준을 사용하거나, 해당 쿼리에서 스타일 0을 명시적으로 지정해야 합니다.<br /><br /> 데이터베이스를 호환성 수준 110으로 업그레이드할 경우 디스크에 저장된 사용자 데이터는 변경되지 않습니다. 수동으로 이 데이터를 적절하게 수정해야 합니다. 예를 들어, 사용 하는 경우 `SELECT INTO` 위에서 설명한 계산된 열 식을 포함 하는 원본에서 테이블을 만들려고 (스타일 0을 사용 하 여) 데이터 계산된 열 정의 자체가 아니라 저장 합니다. 스타일 121과 일치하도록 이 데이터를 수동으로 업데이트해야 합니다.|  
|형식의 원격 테이블의 모든 열 **smalldatetime** 분할 뷰에서 참조 되는으로 매핑되고 **datetime**합니다. (Select 목록의 동일한 서 수 위치)에 로컬 테이블의 해당 열 형식 이어야 합니다 **datetime**합니다.|형식의 원격 테이블의 모든 열 **smalldatetime** 분할 뷰에서 참조 되는으로 매핑되고 **smalldatetime**합니다. (Select 목록의 동일한 서 수 위치)에 로컬 테이블의 해당 열 형식 이어야 합니다 **smalldatetime**합니다.<br /><br /> 110으로 업그레이드한 후에는 데이터 형식이 일치하지 않으므로 분산형 분할 뷰가 실패합니다. 에 원격 테이블에서 데이터 형식을 변경 하 여이 문제를 해결할 수 있습니다 **datetime** 또는 수준 100으로 로컬 데이터베이스의 호환성을 설정 합니다.|  
|`SOUNDEX`함수는 다음 규칙을 구현합니다.<br /><br /> 1) 대문자 H 또는 대문자 W에 같은 번호가 지정 된 두 개의 자음을 구분 하는 경우 무시 되 고 `SOUNDEX` 코드입니다.<br /><br /> 2) 경우의 처음 2 자 *character_expression* 번호가 동일한는 `SOUNDEX` 코드 문자를 모두 포함 됩니다. 나란히 자음 집합이 동일한 수 경우에 다른는 `SOUNDEX` 첫 번째를 제외한 모든 코드에서 제외 됩니다.|`SOUNDEX`함수는 다음 규칙을 구현합니다.<br /><br /> 1) 경우는 동일한 수 있는 대문자 H 또는 대문자 W 별도 두 개의 자음은 `SOUNDEX` 코드에서는 오른쪽의 자음은 무시 됩니다.<br /><br /> 2)-나란히 자음 집합이 동일한 수 경우는 `SOUNDEX` 첫 번째를 제외한 모든 코드에서 제외 됩니다.<br /><br /> <br /><br /> 추가 규칙에서 계산 된 값이 달라질 수 있습니다는 `SOUNDEX` 함수과 이전 호환성 수준에서 계산 된 값입니다. 호환성 수준 110으로 업그레이드 한 후를 힙, 인덱스, 다시 작성 하거나 CHECK 제약 조건을 사용 하는 할 수 있습니다는 `SOUNDEX` 함수입니다. 자세한 내용은 참조 [SOUNDEX &#40; Transact SQL &#41;](../../t-sql/functions/soundex-transact-sql.md)|  
  
## <a name="differences-between-compatibility-level-90-and-level-100"></a>호환성 수준 90과 수준 100 사이의 차이  
 이 섹션에서는 호환성 수준 100으로 정의된 새로운 동작에 대해 설명합니다.  
  
|호환성 수준 설정 90|호환성 수준 설정 100|영향력|  
|----------------------------------------|-----------------------------------------|---------------------------|  
|세션 수준 설정과 상관없이 다중 문 테이블 반환 함수를 만든 경우 이 함수에 대해 QUOTED_IDENTIFER 설정은 항상 ON으로 설정됩니다.|다중 문 테이블 반환 함수를 만든 경우 QUOTED IDENTIFIER 세션 설정이 적용됩니다.|보통|  
|만들거나 파티션 함수를 변경 하면 **datetime** 및 **smalldatetime** US_English로의 언어 설정 가정 리터럴 함수에서 평가 됩니다.|현재 언어 설정을 평가 하는데 사용 됩니다 **datetime** 및 **smalldatetime** 파티션 함수에서는 리터럴.|보통|  
|`FOR BROWSE` 절 허용 (및 무시)에서 `INSERT` 및 `SELECT INTO` 문.|`FOR BROWSE` 절에서 허용 되지 않는 `INSERT` 및 `SELECT INTO` 문.|보통|  
|전체 텍스트 조건자가 허용 된 `OUTPUT` 절.|전체 텍스트 조건자에서 허용 되지 않습니다는 `OUTPUT` 절.|낮음|  
|`CREATE FULLTEXT STOPLIST``ALTER FULLTEXT STOPLIST`, 및 `DROP FULLTEXT STOPLIST` 지원 되지 않습니다. 시스템 중지 목록은 자동으로 새로운 전체 텍스트 인덱스와 연결됩니다.|`CREATE FULLTEXT STOPLIST``ALTER FULLTEXT STOPLIST`, 및 `DROP FULLTEXT STOPLIST` 지원 됩니다.|낮음|  
|`MERGE`예약 된 키워드로 적용 되지 않습니다.|MERGE는 완전 예약 키워드입니다. `MERGE` 문은 호환성 수준 100 및 90 모두에서 지원 됩니다.|낮음|  
|사용 하는 \<dml_table_source > INSERT 문은의 인수에 구문 오류가 발생 합니다.|중첩된 INSERT, UPDATE, DELETE 또는 MERGE 문에서 OUTPUT 절의 결과를 캡처하고 그 결과를 대상 테이블이나 뷰에 삽입할 수 있습니다. 이렇게 사용 하는 \<dml_table_source > INSERT 문의 인수입니다.|낮음|
|하지 않는 한 `NOINDEX` 지정 된 `DBCC CHECKDB` 또는 `DBCC CHECKTABLE` 물리적 및 논리적 일관성 검사는 단일 테이블 또는 인덱싱된 뷰에 대 한 모든 해당 비클러스터형 및 XML 인덱스를 모두 수행 합니다. 공간 인덱스는 지원되지 않습니다.|하지 않는 한 `NOINDEX` 지정 된 `DBCC CHECKDB` 또는 `DBCC CHECKTABLE` 단일 테이블 켜고 모든 비클러스터형 인덱스에서 모두 물리적 및 논리적 일관성 검사를 수행 합니다. 그러나 XML 인덱스, 공간 인덱스 및 인덱싱된 뷰에 대해서는 기본적으로 물리적 일관성 검사만 수행됩니다.<br /><br /> 경우 `WITH EXTENDED_LOGICAL_CHECKS` 지정 된 경우 있는 경우 인덱싱된 뷰, XML 인덱스 및 공간 인덱스에 논리적 검사가 수행 됩니다. 기본적으로 물리적 일관성 검사는 논리적 일관성 검사 전에 수행됩니다. 경우 `NOINDEX` 옵션도 지정 된 경우에 논리적 검사만 수행 됩니다.|낮음|  
|DML(데이터 조작 언어)로 OUTPUT 절을 사용하는 경우 문 실행 중에 런타임 오류가 발생하면 전체 트랜잭션이 종료되고 롤백됩니다.|경우는 `OUTPUT` 데이터 조작 언어 (DML) 문을 사용 하 여 절을 사용 하 고 실행 시 오류가 발생 하는 문 실행 중, 동작은에 따라는 `SET XACT_ABORT` 설정 합니다. 경우 `SET XACT_ABORT` DML 문을 사용 하 여 생성 된 문 중단 오류가 off로 설정 되는 `OUTPUT` 절에는 문이 종료 됩니다 있지만 일괄 처리의 실행이 계속 되 고 트랜잭션이 롤백됩니다 되지 않습니다. 경우 `SET XACT_ABORT` on, OUTPUT 절을 사용 하 여 DML 문에 의해 생성 된 모든 런타임 오류에는 일괄 처리를 종료 되 고 트랜잭션이 롤백됩니다.|낮음|  
|CUBE 및 ROLLUP은 예약 키워드가 아닙니다.|`CUBE`및 `ROLLUP` 는 GROUP BY 절 내에서 예약 된 키워드입니다.|낮음|  
|XML의 요소에 엄격한 유효성 검사가 적용 됩니다 **anyType** 유형입니다.|Lax 유효성 검사의 요소에 적용 되는 **anyType** 유형입니다. 자세한 내용은 참조 [와일드 카드 구성 요소 및 콘텐츠 유효성 검사](../../relational-databases/xml/wildcard-components-and-content-validation.md)합니다.|낮음|  
|특수 특성 **xsi: nil** 및 **xsi: type** 쿼리하거나 데이터 조작 언어 문으로 수정할 수 없습니다.<br /><br /> 즉 `/e/@xsi:nil` 실패 하는 동안 `/e/@*` 무시는 **xsi: nil** 및 **xsi: type** 특성입니다. 그러나 `/e` 반환 된 **xsi: nil** 및 **xsi: type** 특성의 일관성을 위해 `SELECT xmlCol`경우에 `xsi:nil = "false"`합니다.|특수 특성 **xsi: nil** 및 **xsi: type** 일반 특성으로 저장 및 쿼리할 및 수정할 수 있습니다.<br /><br /> 예를 들어 쿼리를 실행 `SELECT x.query('a/b/@*')` 포함 하 여 특성을 모두 반환 **xsi: nil** 및 **xsi: type**합니다. 쿼리에서 이러한 유형을 제외 하려면 대체 `@*` 와 `@*[namespace-uri(.) != "` *xsi 네임 스페이스 uri 삽입* `"` 아닌 `(local-name(.) = "type"` 또는`local-name(.) ="nil".`|낮음|  
|XML 상수 문자열 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datetime 형식으로 변환하는 사용자 정의 함수를 결정적 함수로 표시합니다.|XML 상수 문자열 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datetime 형식으로 변환하는 사용자 정의 함수를 비결정적 함수로 표시합니다.|낮음|  
|XML union 및 list 형식 중 일부는 지원되지 않습니다.|다음 기능을 포함하여 union 및 list 형식은 모두 지원됩니다.<br /><br /> 목록의 합집합<br /><br /> 합집합의 합집합<br /><br /> 원자성 유형의 목록<br /><br /> 합집합의 목록|낮음|  
|인라인 테이블 반환 함수 또는 뷰에 xQuery 메서드가 포함된 경우 이 메서드에 필요한 SET 옵션의 유효성을 검사하지 않습니다.|인라인 테이블 반환 함수 또는 뷰에 xQuery 메서드가 포함된 경우 이 메서드에 필요한 SET 옵션의 유효성을 검사합니다. 메서드의 SET 옵션을 잘못 설정하면 오류가 발생합니다.|낮음|  
|줄 끝 문자(캐리지 리턴 및 줄 바꿈)를 포함하는 XML 특성 값은 XML 표준에 따라 정규화되지 않습니다. 즉, 하나의 줄 바꿈 문자 대신 두 문자 모두 반환됩니다.|줄 끝 문자(캐리지 리턴 및 줄 바꿈)를 포함하는 XML 특성 값은 XML 표준에 따라 정규화됩니다. 즉, 문서 엔터티를 포함하여 구문 분석된 외부 엔터티의 모든 줄 바꿈은 2자 시퀀스 #xD #xA 및 뒤에 #xA가 오지 않는 #xD 모두를 하나의 #xA 문자로 변환하여 입력에서 정규화됩니다.<br /><br /> 특성을 사용하여 줄 끝 문자를 포함하는 문자열 값을 변환하는 응용 프로그램은 이러한 제출된 문자를 다시 수신하지 않습니다. 정규화 프로세스를 방지하려면 XML 숫자 문자 엔터티를 사용하여 모든 줄 끝 문자를 인코딩합니다.|낮음|  
|열 속성 `ROWGUIDCOL` 및 `IDENTITY` 수 수 이름이 잘못 지정 제약 조건으로 합니다. 예를 들어 `CREATE TABLE T (C1 int CONSTRAINT MyConstraint IDENTITY)` 문은 실행되긴 하지만 제약 조건 이름이 보존되지 않으며 이를 통해 사용자에게 액세스할 수 없습니다.|열 속성 `ROWGUIDCOL` 및 `IDENTITY` 제약 조건으로 명명할 수 없습니다. 오류 156이 반환됩니다.|낮음|  
|와 같은 양방향 할당을 사용 하 여 열을 업데이트 `UPDATE T1 SET @v = column_name = <expression>` 는 라이브 변수 값을 사용할 수 있으므로 다른 절에서와 같은 예기치 않은 결과가 발생할 수 있습니다는 `WHER`E 및 `ON` 절 대신 문 실행 중에서 문 시작 값입니다. 그 결과 각 행에서 조건자의 의미가 예기치 않게 변경될 수 있습니다.<br /><br /> 이 동작은 호환성 수준이 90으로 설정된 경우에만 발생합니다.|양방향 할당을 사용하여 열을 업데이트하면 문 실행 중에 열의 문 시작 값만 액세스되므로 예상대로 결과가 나타납니다.|낮음|  
|아래 예 섹션에서 예를 참조 하십시오.|아래 예 섹션에서 F 예제를 참조 하십시오.|낮음|  
|ODBC 함수 {fn CONVERT()}는 언어의 기본 날짜 형식을 사용합니다. 일부 언어에 대 한 기본 형식은 YDM convert ()와 같은 다른 함수와 결합 된 경우 변환 오류가 발생할 수 있는 `{fn CURDATE()}`, YMD 형식을 예상입니다.|ODBC 함수 `{fn CONVERT()}` 스타일 121 (언어와 관계 없는 YMD 형식)을 사용 하 여 경우 SQL_TIMESTAMP, SQL_DATE, SQL_TIME, SQLDATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP 형식은 ODBC 데이터를 변환 합니다.|낮음|  
|DATEPART와 같은 datetime 내장 함수에서 문자열 입력 값은 유효한 datetime 리터럴이 아니어도 됩니다. 예를 들어 `SELECT DATEPART (year, '2007/05-30')` 성공적으로 컴파일됩니다.|와 같은 Datetime 내장 함수 `DATEPART` 문자열 입력 값을 유효한 datetime 리터럴이어야 합니다. 유효하지 않은 datetime 리터럴을 사용하면 오류 241이 반환됩니다.|낮음|  
  
## <a name="reserved-keywords"></a>예약 키워드  
 호환성 설정은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 예약되는 키워드도 결정합니다. 다음 표에서는 각 호환성 수준에 의해 정의된 예약 키워드를 보여 줍니다.  
  
|호환성 수준 설정|예약 키워드|  
|----------------------------------|-----------------------|  
|130|이 결정 됩니다.|  
|120|없음|  
|110|WITHIN GROUP, TRY_CONVERT, SEMANTICKEYPHRASETABLE, SEMANTICSIMILARITYDETAILSTABLE, SEMANTICSIMILARITYTABLE|  
|100|CUBE, MERGE, ROLLUP|  
|90|EXTERNAL, PIVOT, UNPIVOT, REVERT, TABLESAMPLE|  
  
 지정된 호환성 수준의 예약 키워드에는 해당 수준 또는 그 아래 수준에서 정의된 모든 키워드가 포함됩니다. 따라서 수준이 110인 응용 프로그램의 경우에는 위 표에 나열된 모든 키워드가 예약되어 있습니다. 더 낮은 호환성 수준에서 수준이 100인 키워드는 유효한 개체 이름으로 유지되지만 해당 키워드에 대한 수준이 110인 언어 기능은 사용할 수 없습니다.  
  
 정의된 키워드는 예약된 상태로 유지됩니다. 예를 들어 호환성 수준 90에서 정의된 예약 키워드 PIVOT은 수준 100, 110 및 120에서도 예약되어 있습니다.  
  
 응용 프로그램이 호환성 수준에 대한 키워드로 예약되어 있는 식별자를 사용할 경우 제대로 실행되지 않습니다. 이 해결 하려면 식별자 중 하나에 있는 대괄호 사이 묶습니다 (**[]**) 나 따옴표 (**""**) 예: 식별자를 사용 하는 응용 프로그램을 업그레이드 하려면 **외부** 호환성 수준 90으로 식별자 중 하나를 변경할 수 있습니다 **[EXTERNAL]** 또는 **"외부"**합니다.  
  
 자세한 내용은 [예약된 키워드&#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)를 참조하세요.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-the-compatibility-level"></a>1. 호환성 수준 변경  
 다음 예에서는 변경의 호환성 수준을 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 `110,` [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]합니다.  
  
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
  
### <a name="b-ignoring--the-set-language-statement-except-under-compatibility-level-120"></a>2. 호환성 수준이 120 미만일 제외 하 고 SET LANGUAGE 문을 무시합니다.  
 다음 쿼리는 호환성 수준이 120 미만일 제외 하 고 SET LANGUAGE 문을 무시합니다.  
  
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
  
### <a name="c"></a>3.  
 호환성 수준 설정 110 이하로 EXCEPT 절의 오른쪽에 있는 재귀 참조는 무한 루프를 만듭니다.  
  
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
  
### <a name="d"></a>4.  
 이 예에서는 스타일 0과 스타일 121의 차이점을 보여 줍니다. 날짜 및 시간 스타일에 대 한 자세한 내용은 참조 [CAST 및 convert&#40; Transact SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
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
  
### <a name="e"></a>5.  
 최상위 UNION 연산자가 포함된 문에 변수를 할당할 수 있지만 예상치 않은 결과가 반환됩니다. 예를 들어 다음 문에서 지역 변수 `@v`에는 두 테이블의 합집합의 열 `BusinessEntityID` 값이 할당됩니다. 원래 SELECT 문에서 둘 이상의 값을 반환하면 반환된 값 중 마지막 값이 변수에 할당됩니다. 이 경우 변수에 마지막 값이 올바르게 할당되지만 SELECT UNION 문의 결과 집합도 함께 반환됩니다.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET compatibility_level = 90;  
GO  
USE AdventureWorks2012;  
GO  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM HumanResources.Employee  
UNION ALL  
SELECT @v = BusinessEntityID FROM HumanResources.EmployeeAddress;  
SELECT @v;  
```  
  
### <a name="f"></a>6.  
 최상위 UNION 연산자가 포함된 문에는 변수를 할당할 수 없습니다. 오류 10734가 반환됩니다. 오류를 해결하려면 다음 예와 같이 쿼리를 다시 작성합니다.  
  
```sql  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM   
    (SELECT BusinessEntityID FROM HumanResources.Employee  
     UNION ALL  
     SELECT BusinessEntityID FROM HumanResources.EmployeeAddress) AS Test;  
SELECT @v;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [예약 키워드&#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
 [데이터베이스의 호환성 수준 보기 또는 변경](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) 
  
