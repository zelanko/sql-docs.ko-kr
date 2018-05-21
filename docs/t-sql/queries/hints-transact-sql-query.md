---
title: 쿼리 힌트(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Query_Hint_TSQL
- Query_TSQL
- Query
- Query Hint
- MAX_GRANT_PERCENT
- MAX_GRANT_PERCENT_TSQL
- MIN_GRANT_PERCENT
- MIN_GRANT_PERCENT_TSQL
- EXTERNALPUSHDOWN
- EXTERNALPUSHDOWN_TSQL
- NOLOCK_TSQL
- MAXDOP_TSQL
- USE_HINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REPORT PLAN query hint
- FORCE ORDER query hint
- HASH JOIN query hint
- query hints [SQL Server]
- OPTIMIZE FOR query hint
- FORCESCAN query hint
- RECOMPILE query hint
- MAXRECURSION query hint
- MERGE JOIN query hint
- HASH GROUP query hint
- KEEP PLAN query hint
- UNION query hint
- FORCESEEK query hint
- ORDER GROUP query hint
- LOOP JOIN query hint
- KEEPFIXED PLAN query hint
- FAST query hint
- MAXDOP query hint
- PARAMETERIZATION query hint
- hints [SQL Server], query
- JOIN query hint
- USE PLAN query hint
- EXPAND VIEWS query hint
- MAX_GRANT_PERCENT query hint
- MIN_GRANT_PERCENT query hint
- EXTERNALPUSHDOWN query hint
- USE HINT query hint
ms.assetid: 66fb1520-dcdf-4aab-9ff1-7de8f79e5b2d
caps.latest.revision: 136
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1a5246b1d7d6a00e4500c95bae20fb2975bbebc9
ms.sourcegitcommit: bac61a04d11fdf61deeb03060e66621c0606c074
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2018
---
# <a name="hints-transact-sql---query"></a>힌트(Transact-SQL) - 쿼리
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  쿼리 힌트는 해당 힌트가 전체 쿼리에 사용해야 하는 힌트임을 나타냅니다. 문의 모든 연산자에 영향을 줍니다. 기본 쿼리에 UNION이 포함된 경우 UNION 연산과 연관된 마지막 쿼리에만 OPTION 절을 포함할 수 있습니다. 쿼리 힌트는 [OPTION 절](../../t-sql/queries/option-clause-transact-sql.md)의 일부로 지정됩니다. 하나 이상의 쿼리 힌트로 인해 쿼리 최적화 프로그램에서 유효한 계획을 생성할 수 없는 경우 8622 오류가 발생합니다.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 일반적으로 쿼리에 대해 최적의 실행 계획을 선택하므로 힌트는 숙련된 개발자나 데이터베이스 관리자가 최후의 수단으로만 사용하는 것이 좋습니다.  
  
 **적용 대상:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
<query_hint > ::=   
{ { HASH | ORDER } GROUP   
  | { CONCAT | HASH | MERGE } UNION   
  | { LOOP | MERGE | HASH } JOIN   
  | EXPAND VIEWS   
  | FAST number_rows   
  | FORCE ORDER   
  | { FORCE | DISABLE } EXTERNALPUSHDOWN  
  | IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
  | KEEP PLAN   
  | KEEPFIXED PLAN  
  | MAX_GRANT_PERCENT = percent  
  | MIN_GRANT_PERCENT = percent  
  | MAXDOP number_of_processors   
  | MAXRECURSION number   
  | NO_PERFORMANCE_SPOOL   
  | OPTIMIZE FOR ( @variable_name { UNKNOWN | = literal_constant } [ , ...n ] )  
  | OPTIMIZE FOR UNKNOWN  
  | PARAMETERIZATION { SIMPLE | FORCED }  
  | RECOMPILE  
  | ROBUST PLAN   
  | USE HINT ( '<hint_name>' [ , ...n ] )
  | USE PLAN N'xml_plan'  | TABLE HINT ( exposed_object_name [ , <table_hint> [ [, ]...n ] ] )  
}  
  
<table_hint> ::=  
[ NOEXPAND ] {   
    INDEX ( index_value [ ,...n ] ) | INDEX = ( index_value )  
  | FORCESEEK [( index_value ( index_column_name [,... ] ) ) ]  
  | FORCESCAN  
  | HOLDLOCK   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | READUNCOMMITTED   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT  
  | SPATIAL_WINDOW_MAX_CELLS = integer  
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK  
}  
```  
  
## <a name="arguments"></a>인수  
 { HASH | ORDER } GROUP  
 쿼리의 GROUP BY 또는 DISTINCT 절에 지정된 집계에서 해시나 정렬을 사용하도록 지정합니다.  
  
 { MERGE | HASH | CONCAT } UNION  
 UNION 집합을 병합, 해시 또는 연결하여 모든 UNION 연산을 수행하도록 지정합니다. 둘 이상의 UNION 힌트를 지정한 경우 쿼리 최적화 프로그램에서는 지정한 힌트 중 가장 부담이 적은 전략을 선택합니다.  
  
 { LOOP | MERGE | HASH } JOIN  
 전체 쿼리에서 모든 조인 연산이 LOOP JOIN, MERGE JOIN 또는 HASH JOIN에 의해 수행되도록 지정합니다. 조인 힌트를 둘 이상 지정한 경우 최적화 프로그램에서는 허용되는 힌트 중 가장 부담이 적은 조인 방법을 선택합니다.  
  
 같은 쿼리에서 특정 테이블 쌍에 대해 FROM 절에 조인 힌트도 지정한 경우 두 테이블의 조인에서 조인 힌트가 우선적으로 적용되지만 쿼리 힌트도 고려됩니다. 따라서 테이블 쌍에 대한 조인 힌트는 쿼리 힌트에서 허용되는 조인 방법의 선택만 제한하게 될 수도 있습니다. 자세한 내용은 [조인 힌트#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-join.md)를 참조하세요.  
  
 EXPAND VIEWS  
 인덱싱된 뷰를 확장하고 쿼리 최적화 프로그램에서 인덱싱된 뷰를 쿼리 일부를 대체하는 것으로 간주하지 않도록 지정합니다. 쿼리 텍스트에 있는 뷰 정의에 의해 뷰 이름이 바뀌면 뷰가 확장됩니다.  
  
 이 쿼리 힌트는 쿼리 계획에서 인덱싱된 뷰와 인덱싱된 뷰의 인덱스를 직접 사용하도록 허용하지 않습니다.  
  
 인덱싱된 뷰는 쿼리의 SELECT 부분에서 뷰를 직접 참조하고 WITH (NOEXPAND) 또는 WITH (NOEXPAND, INDEX( *index_value* [ **,***...n* ] ) )가 지정된 경우에만 확장되지 않습니다. 쿼리 힌트 WITH (NOEXPAND)에 대한 자세한 내용은 [FROM](../../t-sql/queries/from-transact-sql.md)을 참조하세요.  
  
 INSERT, UPDATE, MERGE 및 DELETE 문을 비롯한 문의 SELECT 부분에 있는 뷰만 힌트의 영향을 받습니다.  
  
 FAST *number_rows*  
 첫 번째 *number_rows*를 빨리 검색하기 위해 쿼리를 최적화하도록 지정합니다. 음수가 아닌 정수입니다. 첫 번째 *number_rows*를 반환한 후에 쿼리는 계속 실행하여 전체 결과 집합을 만듭니다.  
  
 FORCE ORDER  
 쿼리 구문에 지정된 조인 순서가 쿼리 최적화 시 유지되도록 지정합니다. FORCE ORDER를 사용해도 쿼리 최적화 프로그램이 취할 수 있는 역할 반전 동작에는 영향을 미치지 않습니다.  
  
> [!NOTE]  
> MERGE 문에서 WHEN SOURCE NOT MATCHED 절이 지정되어 있지 않으면 원본 테이블은 기본 조인 순서에 따라 대상 테이블보다 먼저 액세스됩니다. FORCE ORDER를 지정하면 이러한 기본 동작이 유지됩니다.  
  
 { FORCE | DISABLE } EXTERNALPUSHDOWN  
 Hadoop에서 조건에 맞는 식 계산을 강제로 밀어내거나 사용하지 않도록 설정합니다. PolyBase를 사용한 쿼리에만 적용됩니다. Azure Storage로 밀어내지 않습니다.  
  
 KEEP PLAN  
 쿼리 최적화 프로그램에서 쿼리에 대한 예상 다시 컴파일 임계값을 완화하도록 합니다. 예상된 다시 컴파일 임계값은 테이블에 UPDATE, DELETE, MERGE 또는 INSERT 문을 실행하여 인덱싱된 열을 예상 수만큼 변경했을 때 쿼리가 자동으로 다시 컴파일되는 시점입니다. 테이블이 자주 업데이트되는 경우 KEEP PLAN을 지정하면 쿼리가 지나치게 자주 다시 컴파일되지 않아 유용합니다.  
  
 KEEPFIXED PLAN  
 통계 변경 시에는 최적화 프로그램이 쿼리를 다시 컴파일하지 않도록 합니다. KEEPFIXED PLAN을 지정하면 원본으로 사용하는 테이블의 스키마가 바뀌거나 테이블에 대해 **sp_recompile**이 실행되는 경우에만 쿼리를 다시 컴파일합니다.  
  
 IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 쿼리에 비클러스터형 메모리 액세스에 최적화된 columnstore 인덱스가 사용되지 않도록 방지합니다. 쿼리에 Columnstore 인덱스 사용을 방지하기 위한 쿼리 힌트와 Columnstore 인덱스를 사용하기 위한 인덱스 힌트가 포함되어 있으면 힌트가 충돌하게 되고 오류가 반환됩니다.  
  
 MAX_GRANT_PERCENT = *percent*  
 PERCENT 단위의 최대 메모리 부여 크기입니다. 쿼리가 이 제한을 초과하지 않게 보장합니다. 리소스 관리자(resource governor) 설정이 이보다 낮으면 실제 제한을 더 낮게 설정할 수 있습니다. 유효한 값은 0.0에서 100.0 사이의 값입니다.  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 MIN_GRANT_PERCENT = *percent*  
 PERCENT 단위의 최소 메모리 크기 = 기본 제한의 %. 쿼리를 시작하기 위해서는 최소한의 필수 메모리가 필요하기 때문에 이 쿼리는 MAX(필수 메모리, 최소 부여)를 가져오도록 보장됩니다. 유효한 값은 0.0에서 100.0 사이의 값입니다.  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 MAXDOP *숫자*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 이 옵션을 지정하는 쿼리에 대해 **sp_configure** 및 Resource Governor의 **최대 병렬 처리 수준** 구성 옵션을 무시합니다. MAXDOP 쿼리 힌트는 sp_configure로 구성한 값을 초과할 수 있습니다. MAXDOP가 Resource Governor로 구성한 값을 초과하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]가 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)에서 설명한 Resource Governor MAXDOP 값을 사용합니다. **최대 병렬 처리 수준** 구성 옵션에 사용된 모든 의미 체계 규칙을 MAXDOP 쿼리 힌트 사용 시 적용할 수 있습니다. 자세한 내용은 [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요.  
  
> [!WARNING]     
> MAXDOP가 0으로 설정되면 서버는 최대 병렬 처리 수준을 선택합니다.  
  
 MAXRECURSION *숫자*     
 해당 쿼리에 대해 허용되는 최대 재귀 횟수를 지정합니다. *숫자*는 0에서 32,767 사이의 음수가 아닌 정수입니다. 0을 지정하면 제한이 적용되지 않습니다. 이 옵션을 지정하지 않은 경우 서버에 대한 기본 한도는 100입니다.  
  
 쿼리 실행 중에 MAXRECURSION 한도로 지정된 횟수 또는 기본 횟수에 도달하면 쿼리가 종료되고 오류가 반환됩니다.  
  
 이 오류로 인해 문의 모든 결과가 롤백됩니다. 문이 SELECT 문인 경우 결과의 일부가 반환되거나 아무런 결과도 반환되지 않을 수 있습니다. 반환된 일부 결과에는 지정한 최대 재귀 수준을 초과한 재귀 수준의 모든 행이 포함되지 않을 수 있습니다.  
  
 자세한 내용은 [WITH common_table_expression&#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)을 참조하세요.     
  
 NO_PERFORMANCE_SPOOL    
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 스풀 연산자가 쿼리 계획에 추가되지 않게 합니다(유효한 업데이트 의미 체계를 보증하기 위해 스풀이 필요한 계획 제외). 일부 시나리오에서는 스풀 연산자로 인해 성능이 저하될 수 있습니다. 예를 들어 스풀 연산과 함께 여러 쿼리가 동시에 실행되는 경우 스풀이 사용하는 tempdb 및 tempdb 경합이 발생할 수 있습니다.  
  
 OPTIMIZE FOR ( *@variable_name* { UNKNOWN | = *literal_constant }* [ **,** ...*n* ] )     
 쿼리가 컴파일되고 최적화될 때 쿼리 최적화 프로그램이 지역 변수에 대해 특정 값을 사용하도록 지시합니다. 해당 값은 쿼리 최적화 중에만 사용되고 쿼리 실행 중에는 사용되지 않습니다.  
  
 *@variable_name*  
 쿼리에서 사용된 지역 변수의 이름이며 OPTIMIZE FOR 쿼리 힌트와 함께 사용하도록 값을 할당할 수 있습니다.  
  
 *UNKNOWN*  
 쿼리 최적화 프로그램이 쿼리 최적화 동안 초기 값 대신 통계 데이터를 사용하여 지역 변수 값을 결정하도록 지정합니다.  
  
 *literal_constant*  
 OPTIMIZE FOR 쿼리 힌트와 함께 사용하도록 *@variable_name*을 할당할 리터럴 상수 값입니다. *literal_constant*는 쿼리 최적화 중에만 사용되며 쿼리 실행 중에는 *@variable_name*의 값으로 사용되지 않습니다. *literal_constant*는 리터럴 상수로 표현할 수 있는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식이 될 수 있습니다. *literal_constant*의 데이터 형식은 쿼리에서 *@variable_name*이 참조하는 데이터 형식으로 암시적으로 변환될 수 있어야 합니다.  
  
 OPTIMIZE FOR는 최적화 프로그램의 기본 매개 변수 감지 동작을 무효로 만들 수 있으며 계획 지침을 만들 때 사용할 수 있습니다. 자세한 내용은 [저장 프로시저 다시 컴파일](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)을 참조하십시오.  
  
 OPTIMIZE FOR UNKNOWN  
 쿼리가 컴파일 및 최적화될 때 쿼리 최적화 프로그램이 강제 매개 변수화를 통해 만든 매개 변수를 비롯한 모든 지역 변수에 대해 초기 값 대신 통계 데이터를 사용하도록 지시합니다.  
  
 같은 쿼리 힌트에서 OPTIMIZE FOR @variable_name = *literal_constant* 및 OPTIMIZE FOR UNKNOWN을 사용하면 쿼리 최적화 프로그램이 특정 값에는 지정된 *literal_constant*를 사용하고 나머지 변수 값에는 UNKNOWN을 사용합니다. 해당 값은 쿼리 최적화 중에만 사용되고 쿼리 실행 중에는 사용되지 않습니다.  
  
 PARAMETERIZATION { SIMPLE | FORCED }     
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램에서 쿼리 컴파일 시 적용하는 매개 변수화 규칙을 지정합니다.  
  
> [!IMPORTANT]  
> PARAMETERIZATION 쿼리 힌트는 계획 지침 내에서 PARAMETERIZATION 데이터베이스 SET 옵션의 현재 설정을 재정의하도록 지정될 수 있습니다. 쿼리 내에서 직접 지정할 수는 없습니다.    
> 자세한 내용은 [계획 지침을 사용하여 쿼리 매개 변수화 동작 지정](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)을 참조하세요.
  
 SIMPLE은 쿼리 최적화 프로그램이 단순 매개 변수화를 시도하도록 지시합니다. FORCED는 쿼리 최적화 프로그램이 강제 매개 변수화를 시도하도록 지시합니다. 자세한 내용은 [쿼리 처리 아키텍처 가이드에서 강제 매개 변수화](../../relational-databases/query-processing-architecture-guide.md#ForcedParam) 및 [쿼리 처리 아키텍처 가이드에서 단순 매개 변수화](../../relational-databases/query-processing-architecture-guide.md#SimpleParam)를 참조하세요.  
  
 RECOMPILE  
 쿼리를 실행한 후 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 해당 쿼리에 대해 생성된 계획을 삭제하도록 하여 다음에 같은 쿼리가 실행될 때 쿼리 최적화 프로그램이 쿼리 계획을 다시 컴파일하도록 지시합니다. RECOMPILE을 지정하지 않으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 쿼리 계획을 캐시하여 다시 사용합니다. 쿼리 계획을 컴파일할 때 RECOMPILE 쿼리 힌트는 쿼리에 있는 지역 변수의 현재 값을 사용하며 쿼리가 저장 프로시저 안에 있는 경우 매개 변수에 전달된 현재 값을 사용합니다.  
  
 RECOMPILE은 전체 저장 프로시저가 아닌 저장 프로시저 내 쿼리의 하위 집합만 다시 컴파일해야 하는 경우 WITH RECOMPILE 절을 사용하는 저장 프로시저를 만드는 데 유용합니다. 자세한 내용은 [저장 프로시저 다시 컴파일](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)을 참조하십시오. RECOMPILE은 계획 지침을 만들 때도 유용합니다.  
  
 ROBUST PLAN  
 쿼리 최적화 프로그램에서 성능이 저하되더라도 잠재적 최대 행 크기를 정의할 수 있는 계획을 세우도록 합니다. 쿼리가 처리될 때 중간 테이블 및 연산자가 입력 행보다 큰 행을 저장하고 처리해야 할 수 있습니다. 행이 너무 커서 특정 연산자가 행을 처리하지 못하는 경우도 있습니다. 이런 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 쿼리 실행 중에 오류를 생성합니다. ROBUST PLAN을 사용하면 쿼리 최적화 프로그램에서 이러한 문제가 발생할 수 있는 쿼리 계획을 고려하지 않도록 할 수 있습니다.  
  
 이러한 계획이 불가능할 경우 쿼리 최적화 프로그램은 쿼리 실행 시 오류를 검색하도록 지연시키지 않고 오류를 반환합니다. 행에는 가변 길이 열이 포함될 수 있으며 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 처리할 수 있는 범위 이상의 잠재적 최대 크기를 가진 행을 정의하도록 허용합니다. 그러나 대개 응용 프로그램은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 처리할 수 있는 한도 내의 실제 크기를 가진 행을 저장합니다. 너무 긴 행이 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 실행 오류를 반환합니다.  
 
<a name="use_hint"></a> USE HINT ( **'***hint_name***'** )    
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1로 시작) 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 적용됩니다.
 
 힌트 이름 **작은 따옴표 안**에서 지정한 대로 쿼리 프로세서에 하나 이상의 추가 힌트를 제공합니다.   

 지원되는 힌트는 다음과 같습니다.    
 
*  'DISABLE_OPTIMIZED_NESTED_LOOP'  
 쿼리 프로세서가 쿼리 계획을 생성할 때 최적화된 중첩 루프 조인을 위해 정렬 연산(일괄 처리 정렬)을 사용하지 않도록 지시합니다 이 설정은 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2340과 동일합니다.
*  'FORCE_LEGACY_CARDINALITY_ESTIMATION'  
 쿼리 최적화 프로그램이 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 이전 버전의 [카디널리티 추정](../../relational-databases/performance/cardinality-estimation-sql-server.md) 모델을 사용하도록 강제 적용합니다. [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481 또는 [데이터베이스 범위 구성](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 설정 LEGACY_CARDINALITY_ESTIMATION=ON에 해당합니다.
*  'ENABLE_QUERY_OPTIMIZER_HOTFIXES'  
 쿼리 최적화 프로그램 핫픽스(SQL Server 누적 업데이트 및 서비스 팩에서 릴리스된 변경 내용)를 사용하도록 설정합니다. [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4199 또는 [데이터베이스 범위 구성](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 설정 QUERY_OPTIMIZER_HOTFIXES=ON에 해당합니다.
*  'DISABLE_PARAMETER_SNIFFING'  
 쿼리 계획이 쿼리를 컴파일할 때 처음 사용된 매개 변수 값과 독립적이되도록, 쿼리 최적화 프로그램이 하나 이상의 매개 변수가 있는 쿼리를 컴파일할 때 평균 데이터 분산을 사용하도록 지시합니다. [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4136 또는 [데이터베이스 범위 구성](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 설정 PARAMETER_SNIFFING=OFF에 해당합니다.
*  'ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES'  
 SQL Server가 상관 관계에 해당하는 필터에 대해 AND 조건자를 추정할 때 최소 선택을 사용하여 계획을 생성하게 합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 그 이전 버전의 카디널리티 추정 모델에 사용하던 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4137에 해당하며 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9471을 카디널리티 추정 모델 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상에서 사용할 때 결과가 비슷합니다.
*  'DISABLE_OPTIMIZER_ROWGOAL'  
 SQL Server가 TOP, OPTION (FAST N), IN 또는 EXISTS 키워드를 포함하는 쿼리에 행 목표 조정을 사용하지 않는 계획을 생성하게 합니다. [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4138과 동일합니다.
*  'ENABLE_HIST_AMENDMENT_FOR_ASC_KEYS'  
 카디널리티 추정이 필요한 모든 선행 인덱스 열에 대해 자동으로 생성된 빠른 통계(히스토그램 수정)를 사용합니다. 카디널리티 추정에 사용되는 히스토그램은 이 열의 실제 최댓값 또는 최솟값을 반영하기 위해 쿼리 컴파일 시점에 조정됩니다. 이 설정은 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4139와 동일합니다. 
*  'ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS'  
 SQL Server가 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상의 쿼리 최적화 프로그램 [카디널리티 추정](../../relational-databases/performance/cardinality-estimation-sql-server.md) 모델에서 조인에 기본 베이스 제약 가정 대신 단순 제약을 사용하여 쿼리를 생성하게 합니다. 이 설정은 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9476과 동일합니다. 
*  'FORCE_DEFAULT_CARDINALITY_ESTIMATION'  
 쿼리 최적화 프로그램이 현재 데이터베이스 호환성 수준에 해당하는 [카디널리티 추정](../../relational-databases/performance/cardinality-estimation-sql-server.md) 모델을 사용하도록 강제 적용합니다. 이 힌트를 사용하여 [데이터베이스 범위 구성](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 설정 LEGACY_CARDINALITY_ESTIMATION=ON 또는 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481을 재정의합니다.
* 'DISABLE_INTERLEAVED_EXECUTION_TVF'는 다중 문 테이블 반환 함수에 대한 인터리브 실행을 비활성화합니다.
* 'DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK'은 일괄 처리 모드 메모리 부여 피드백을 비활성화합니다.
* 'DISABLE_BATCH_MODE_ADAPTIVE_JOINS'는 일괄 처리 모드 적응형 조인을 비활성화합니다.
 
> [!TIP]
> 힌트 이름은 대/소문자를 구분하지 않습니다.
  
  지원되는 모든 USE HINT 이름 목록은 동적 관리 뷰 [sys.dm_exec_valid_use_hints](../../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md)를 사용하여 쿼리할 수 있습니다.    
  
> [!IMPORTANT] 
> 일부 USE HINT 힌트는 전역 또는 세션 수준에서 사용하는 추적 플래그나 데이터베이스 범위 구성 설정과 충돌할 수 있습니다. 이 경우 쿼리 수준 힌트(USE HINT)가 항상 우선합니다. USE HINT가 쿼리 수준에서 사용하는 다른 쿼리 힌트나 추적 플래그와 충돌하는 경우(예: QUERYTRACEON) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 쿼리를 실행할 때 오류를 생성합니다. 

 USE PLAN N **'***xml_plan***'**     
 쿼리 최적화 프로그램이 **'***xml_plan***'** 에 의해 지정된 쿼리에 대해 기존의 쿼리 계획을 사용하도록 합니다. USE PLAN은 INSERT, UPDATE, MERGE 또는 DELETE 문에서 지정할 수 없습니다.  
  
TABLE HINT **(***exposed_object_name* [ **,** \<table_hint> [ [**,** ]...*n* ] ] **)** 지정된 테이블 힌트를 *exposed_object_name*에 해당하는 테이블 또는 뷰에 적용합니다. 테이블 힌트는 [계획 지침](../../relational-databases/performance/plan-guides.md)의 컨텍스트에서 쿼리 힌트로만 사용하는 것이 좋습니다.  
  
 *exposed_object_name*은 다음 참조 중 하나일 수 있습니다.  
  
-   쿼리의 [FROM](../../t-sql/queries/from-transact-sql.md) 절에서 테이블 또는 뷰에 별칭을 사용하는 경우 *exposed_object_name*은 해당 별칭입니다.  
  
-   별칭을 사용하지 않는 경우 *exposed_object_name*은 FROM 절에서 참조되는 테이블 또는 뷰와 일치합니다. 예를 들어 테이블 또는 뷰가 두 부분으로 된 이름을 사용하여 참조되는 경우 *exposed_object_name*도 똑같이 두 부분으로 된 이름입니다.  
  
 테이블 힌트는 지정하지 않고 *exposed_object_name*만 지정하면 쿼리에 개체에 대한 테이블 힌트의 일부로 지정된 인덱스가 모두 무시되고 쿼리 최적화 프로그램에서 인덱스 사용 여부를 결정합니다. 이 방법은 원래 쿼리를 수정할 수 없을 때 INDEX 테이블 힌트의 효과를 제거하는 데 이용할 수 있습니다. 자세한 내용은 예 10을 참조하세요.  
  
**\<table_hint> ::=** { [ NOEXPAND ] { INDEX ( *index_value* [ ,...*n* ] ) | INDEX = ( *index_value* ) | FORCESEEK [**(***index_value***(***index_column_name* [**,**... ] **))** ]| FORCESCAN | HOLDLOCK | NOLOCK | NOWAIT | PAGLOCK | READCOMMITTED | READCOMMITTEDLOCK | READPAST | READUNCOMMITTED | REPEATABLEREAD | ROWLOCK | SERIALIZABLE | SNAPSHOT | SPATIAL_WINDOW_MAX_CELLS | TABLOCK | TABLOCKX | UPDLOCK | XLOCK } *exposed_object_name*에 해당하는 테이블 또는 뷰에 쿼리 힌트로 적용하는 테이블 힌트 이러한 힌트에 대한 설명은 [테이블 힌트 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)을 참조하세요.  
  
 쿼리에 테이블 힌트를 지정하는 WITH 절이 없다면 INDEX, FORCESCAN 및 FORCESEEK 이외의 테이블 힌트를 쿼리 힌트로 사용할 수 없습니다. 자세한 내용은 설명 부분을 참조하세요.  
  
> [!CAUTION] 
> 매개 변수와 함께 FORCESEEK를 지정할 경우 매개 변수 없이 FORCESEEK를 지정할 때보다 최적화 프로그램에서 고려할 수 있는 계획 수가 더 제한됩니다. 이로 인해 "계획을 생성할 수 없음" 오류가 많은 사례에서 발생하는 원인이 될 수도 있습니다. 후속 릴리스에서는 더 많은 계획을 고려할 수 있도록 최적화 프로그램이 수정될 것입니다.  
  
## <a name="remarks"></a>Remarks  
 쿼리 힌트는 명령문 내에 SELECT 절이 사용되는 경우를 제외하고 INSERT 문에서 지정할 수 없습니다.  
  
 쿼리 힌트는 하위 쿼리가 아닌 최상위 쿼리에서만 지정할 수 있습니다. 테이블 힌트를 쿼리 힌트로 지정하면 해당 힌트를 최상위 쿼리나 하위 쿼리에 지정할 수 있지만 TABLE HINT 절에서 *exposed_object_name*에 대해 지정한 값이 쿼리 또는 하위 쿼리의 표시 이름과 일치해야 합니다.  
  
## <a name="specifying-table-hints-as-query-hints"></a>테이블 힌트를 쿼리 힌트로 지정  
 INDEX, FORCESCAN 또는 FORCESEEK 테이블 힌트는 [계획 지침](../../relational-databases/performance/plan-guides.md)의 컨텍스트에서만 쿼리 힌트로 사용하는 것이 좋습니다. 계획 지침은 타사 응용 프로그램인 경우와 같이 원래 쿼리를 수정할 수 없을 때 유용합니다. 계획 지침에 지정되어 있는 쿼리 힌트는 쿼리가 컴파일 및 최적화되기 전에 쿼리에 추가됩니다. 임시 쿼리의 경우 계획 지침 문을 테스트할 때에만 TABLE HINT 절을 사용하세요. 임시 쿼리 이외의 모든 경우 이러한 힌트를 테이블 힌트로만 지정하는 것이 좋습니다.  
  
 INDEX, FORCESCAN 및 FORCESEEK 테이블 힌트를 쿼리 힌트로 지정하는 경우 다음 개체에 대해서 유효합니다.  
  
-   테이블  
-   뷰  
-   인덱싱된 뷰  
-   공통 테이블 식(공통 테이블 식을 채울 결과 집합을 위한 SELECT 문에 힌트를 지정해야 함)  
-   동적 관리 뷰  
-   명명된 하위 쿼리  
  
 기존 테이블 힌트가 없는 쿼리에 대해 INDEX, FORCESCAN 및 FORCESEEK 테이블 힌트를 쿼리 힌트로 지정할 수 있습니다. 또는 INDEX 및 FORCESEEK 힌트를 사용하여 쿼리에 있는 기존 INDEX, FORCESCAN 또는 FORCESEEK 힌트를 각각 대체할 수 있습니다. 쿼리에 테이블 힌트를 지정하는 WITH 절이 없다면 INDEX, FORCESCAN 및 FORCESEEK 이외의 테이블 힌트를 쿼리 힌트로 사용할 수 없습니다. 이 경우 OPTION 절에 TABLE HINT를 사용하여 일치하는 힌트를 쿼리 힌트로 지정함으로써 쿼리의 의미 체계를 유지해야 합니다. 예를 들어 쿼리에 테이블 힌트 NOLOCK이 있는 경우 계획 지침의 **@hints** 매개 변수에 있는 OPTION 절에도 NOLOCK 힌트가 있어야 합니다. 예 K를 참조하세요. 일치하는 쿼리 힌트 없이 OPTION 절에 TABLE HINT를 사용하여 INDEX, FORCESCAN 또는 FORCESEEK 이외의 테이블 힌트를 지정하거나 그 반대의 경우 OPTION 절로 인해 쿼리의 의미 체계가 변경되고 쿼리가 실패할 수 있음을 나타내는 오류 8702가 발생합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-merge-join"></a>1. MERGE JOIN 사용  
 다음 예에서는 쿼리의 JOIN 연산이 MERGE JOIN에 의해 수행되도록 지정합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```sql  
SELECT *   
FROM Sales.Customer AS c  
INNER JOIN Sales.CustomerAddress AS ca ON c.CustomerID = ca.CustomerID  
WHERE TerritoryID = 5  
OPTION (MERGE JOIN);  
GO    
```  
  
### <a name="b-using-optimize-for"></a>2. OPTIMIZE FOR 사용  
 다음 예에서는 쿼리를 최적화할 때 쿼리 최적화 프로그램이 지역 변수 `'Seattle'`에 `@city_name` 값을 사용하고 통계 데이터를 사용하여 지역 변수 `@postal_code`의 값을 결정하도록 지시합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```sql  
DECLARE @city_name nvarchar(30);  
DECLARE @postal_code nvarchar(15);  
SET @city_name = 'Ascheim';  
SET @postal_code = 86171;  
SELECT * FROM Person.Address  
WHERE City = @city_name AND PostalCode = @postal_code  
OPTION ( OPTIMIZE FOR (@city_name = 'Seattle', @postal_code UNKNOWN) );  
GO  
```  
  
### <a name="c-using-maxrecursion"></a>3. MAXRECURSION 사용  
 잘못 구성된 재귀 공통 테이블 식이 무한 루프에 진입하는 것을 방지하는 데 MAXRECURSION을 사용할 수 있습니다. 다음 예에서는 의도적으로 무한 루프를 만들고 MAXRECURSION 힌트를 사용하여 재귀 수준을 2로 제한하는 방법을 보여 줍니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```sql  
--Creates an infinite loop  
WITH cte (CustomerID, PersonID, StoreID) AS  
(  
    SELECT CustomerID, PersonID, StoreID  
    FROM Sales.Customer  
    WHERE PersonID IS NOT NULL  
  UNION ALL  
    SELECT cte.CustomerID, cte.PersonID, cte.StoreID  
    FROM cte   
    JOIN  Sales.Customer AS e   
        ON cte.PersonID = e.CustomerID  
)  
--Uses MAXRECURSION to limit the recursive levels to 2  
SELECT CustomerID, PersonID, StoreID  
FROM cte  
OPTION (MAXRECURSION 2);  
GO  
```  
  
 코딩 오류를 교정한 다음에는 더 이상 MAXRECURSION이 필요하지 않습니다.  
  
### <a name="d-using-merge-union"></a>4. MERGE UNION 사용  
 다음 예에서는 MERGE UNION 쿼리 힌트를 사용합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```sql  
SELECT *  
FROM HumanResources.Employee AS e1  
UNION  
SELECT *  
FROM HumanResources.Employee AS e2  
OPTION (MERGE UNION);  
GO  
```  
  
### <a name="e-using-hash-group-and-fast"></a>5. HASH GROUP 및 FAST 사용  
 다음 예에서는 HASH GROUP 및 FAST 쿼리 힌트를 사용합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```sql  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (HASH GROUP, FAST 10);  
GO    
```  
  
### <a name="f-using-maxdop"></a>6. MAXDOP 사용  
 다음 예에서는 MAXDOP 쿼리 힌트를 사용합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```sql  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (MAXDOP 2);    
GO
```  
  
### <a name="g-using-index"></a>7. INDEX 사용  
 다음 예에서는 INDEX 힌트를 사용합니다. 첫 번째 예에서는 단일 인덱스를 지정하고, 두 번째 예에서는 단일 테이블 참조에 대해 여러 인덱스를 지정합니다. 두 예에서 INDEX 힌트는 별칭을 사용하는 테이블에 적용되므로 TABLE HINT 절에서도 표시된 개체 이름과 동일한 별칭을 지정해야 합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide1',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e, INDEX (IX_Employee_ManagerID)))';  
GO  
EXEC sp_create_plan_guide   
    @name = N'Guide2',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e, INDEX(PK_Employee_EmployeeID, IX_Employee_ManagerID)))';  
GO    
```  
  
### <a name="h-using-forceseek"></a>8. FORCESEEK 사용  
 다음 예에서는 FORCESEEK 테이블 힌트를 사용합니다. 이 예에서 INDEX 힌트는 두 부분으로 된 이름을 사용하는 테이블에 적용되므로 TABLE HINT 절에서도 표시된 개체 이름과 동일한 두 부분으로 된 이름을 지정해야 합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide3',   
    @stmt = N'SELECT c.LastName, c.FirstName, HumanResources.Employee.Title  
              FROM HumanResources.Employee  
              JOIN Person.Contact AS c ON HumanResources.Employee.ContactID = c.ContactID  
              WHERE HumanResources.Employee.ManagerID = 3  
              ORDER BY c.LastName, c.FirstName;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT( HumanResources.Employee, FORCESEEK))';  
GO    
```  
  
### <a name="i-using-multiple-table-hints"></a>9. 여러 테이블 힌트 사용  
 다음 예에서는 한 테이블에 INDEX 힌트를 적용하고 다른 테이블에 FORCESEEK 힌트를 적용합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide4',   
    @stmt = N'SELECT e.ManagerID, c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, INDEX( IX_Employee_ManagerID))   
                       , TABLE HINT (c, FORCESEEK))';  
GO  
```  
  
### <a name="j-using-table-hint-to-override-an-existing-table-hint"></a>10. TABLE HINT를 사용하여 기존 테이블 힌트 다시 정의  
 다음 예에서는 힌트를 지정하지 않고 TABLE HINT 힌트를 사용하여 쿼리의 FROM 절에 지정된 INDEX 테이블의 동작을 다시 정의하는 방법을 보여 줍니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide5',   
    @stmt = N'SELECT e.ManagerID, c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e WITH (INDEX (IX_Employee_ManagerID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e))';  
GO    
```  
  
### <a name="k-specifying-semantics-affecting-table-hints"></a>11. 의미 체계에 영향을 주는 테이블 힌트 지정  
 다음 예의 쿼리에는 두 가지 테이블 힌트가 포함되어 있습니다. 하나는 의미 체계에 영향을 주는 NOLOCK이고 다른 하나는 의미 체계에 영향을 주지 않는 INDEX입니다. 쿼리의 의미 체계를 유지하기 위해 계획 지침의 OPTIONS 절에 NOLOCK 힌트가 지정됩니다. NOLOCK 힌트 외에 INDEX 및 FORCESEEK 힌트가 지정되고 문을 컴파일 및 최적화할 때 쿼리에서 의미 체계에 영향을 주지 않는 INDEX 힌트를 대체합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide6',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
                   WITH (NOLOCK, INDEX (PK_Employee_EmployeeID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',  
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, INDEX(IX_Employee_ManagerID), NOLOCK, FORCESEEK))';  
GO    
```  
  
 다음 예에서는 최적화 프로그램에서 테이블 힌트에 지정된 인덱스 이외의 인덱스를 선택할 수 있도록 하면서 쿼리의 의미 체계를 유지하는 다른 방법을 보여 줍니다. 이 작업은 의미 체계에 영향을 주는 NOLOCK 힌트를 OPTIONS 절에 지정하고 테이블 참조만 있고 INDEX 힌트는 없는 TABLE HINT 키워드를 지정하여 수행됩니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide7',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
                   WITH (NOLOCK, INDEX (PK_Employee_EmployeeID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',  
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, NOLOCK))';  
GO  
```  
### <a name="l-using-use-hint"></a>12. USE HINT 사용  
 다음 예에서는 RECOMPILE 및 USE HINT 쿼리 힌트를 사용합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
```sql  
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (RECOMPILE, USE HINT ('ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES', 'DISABLE_PARAMETER_SNIFFING')); 
GO  
```  
    
## <a name="see-also"></a>참고 항목  
 [힌트&#40;Transact SQL&#41;](../../t-sql/queries/hints-transact-sql.md)   
 [sp_create_plan_guide&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
