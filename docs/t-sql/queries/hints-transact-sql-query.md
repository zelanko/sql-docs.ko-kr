---
title: "쿼리 힌트 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b866e3ab0ee44c8b65a7b5064f0feb1e4f52aff9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="hints-transact-sql---query"></a>쿼리 힌트 (Transact SQL)-
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  쿼리 힌트는 해당 힌트가 전체 쿼리에 사용해야 하는 힌트임을 나타냅니다. 문의 모든 연산자에 영향을 줍니다. 기본 쿼리에 UNION이 포함된 경우 UNION 연산과 연관된 마지막 쿼리에만 OPTION 절을 포함할 수 있습니다. 쿼리 힌트의 일부로 지정 된 된 [OPTION 절](../../t-sql/queries/option-clause-transact-sql.md)합니다. 하나 이상의 쿼리 힌트로 인해 쿼리 최적화 프로그램에서 유효한 계획을 생성할 수 없는 경우 8622 오류가 발생합니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 일반적으로 쿼리에 대해 최적의 실행 계획을 선택하므로 힌트는 숙련된 개발자나 데이터베이스 관리자가 최후의 수단으로만 사용하는 것이 좋습니다.  
  
 **적용 대상:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [병합](../../t-sql/statements/merge-transact-sql.md)  
  
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
  
 같은 쿼리에서 특정 테이블 쌍에 대해 FROM 절에 조인 힌트도 지정한 경우 두 테이블의 조인에서 조인 힌트가 우선적으로 적용되지만 쿼리 힌트도 고려됩니다. 따라서 테이블 쌍에 대한 조인 힌트는 쿼리 힌트에서 허용되는 조인 방법의 선택만 제한하게 될 수도 있습니다. 자세한 내용은 참조 [조인 힌트 &#40; Transact SQL &#41; ](../../t-sql/queries/hints-transact-sql-join.md).  
  
 EXPAND VIEWS  
 인덱싱된 뷰를 확장하고 쿼리 최적화 프로그램에서 인덱싱된 뷰를 쿼리 일부를 대체하는 것으로 간주하지 않도록 지정합니다. 쿼리 텍스트에 있는 뷰 정의에 의해 뷰 이름이 바뀌면 뷰가 확장됩니다.  
  
 이 쿼리 힌트는 쿼리 계획에서 인덱싱된 뷰와 인덱싱된 뷰의 인덱스를 직접 사용하도록 허용하지 않습니다.  
  
 WITH (NOEXPAND) 또는 WITH 및 쿼리의 SELECT 부분에는 뷰를 직접 참조 하는 경우에 인덱싱된 뷰의 확장 되지 않습니다 (NOEXPAND, INDEX ( *index_value* [ **,***...n*])) 지정 합니다. 쿼리 힌트 WITH (NOEXPAND)에 대 한 자세한 내용은 참조 [FROM](../../t-sql/queries/from-transact-sql.md)합니다.  
  
 INSERT, UPDATE, MERGE 및 DELETE 문을 비롯한 문의 SELECT 부분에 있는 뷰만 힌트의 영향을 받습니다.  
  
 빠른 *number_rows*  
 첫 번째 빨리 검색 하기 위해 쿼리를 최적화 하도록 지정 *number_rows 합니다.* 음수가 아닌 정수입니다. 첫 번째 후 *number_rows* 반환 되는 경우 쿼리 실행을 계속 하 고 전체 결과 집합을 생성 합니다.  
  
 FORCE ORDER  
 쿼리 구문에 지정된 조인 순서가 쿼리 최적화 시 유지되도록 지정합니다. FORCE ORDER를 사용해도 쿼리 최적화 프로그램이 취할 수 있는 역할 반전 동작에는 영향을 미치지 않습니다.  
  
> [!NOTE]  
>  MERGE 문에서 WHEN SOURCE NOT MATCHED 절이 지정되어 있지 않으면 원본 테이블은 기본 조인 순서에 따라 대상 테이블보다 먼저 액세스됩니다. FORCE ORDER를 지정하면 이러한 기본 동작이 유지됩니다.  
  
 {FORCE | 사용 안 함} EXTERNALPUSHDOWN  
 강제로 또는 조건에 맞는 식 Hadoop에 계산 푸시 다운을 사용 하지 않도록 설정 합니다. PolyBase를 사용 하 여 쿼리에만 적용 됩니다. 에서는 하지을 아래로 밀어냅니다 Azure 저장소에 있습니다.  
  
 KEEP PLAN  
 쿼리 최적화 프로그램에서 쿼리에 대한 예상 다시 컴파일 임계값을 완화하도록 합니다. 예상된 다시 컴파일 임계값은 테이블에 UPDATE, DELETE, MERGE 또는 INSERT 문을 실행하여 인덱싱된 열을 예상 수만큼 변경했을 때 쿼리가 자동으로 다시 컴파일되는 시점입니다. 테이블이 자주 업데이트되는 경우 KEEP PLAN을 지정하면 쿼리가 지나치게 자주 다시 컴파일되지 않아 유용합니다.  
  
 KEEPFIXED PLAN  
 통계 변경 시에는 최적화 프로그램이 쿼리를 다시 컴파일하지 않도록 합니다. KEEPFIXED PLAN을 지정 하면 기본 테이블의 스키마 변경 하거나 경우에는 쿼리를 다시 **sp_recompile** 해당 테이블에 대해 실행 됩니다.  
  
 IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 클러스터 되지 않은 메모리 최적화 columnstore 인덱스를 사용 하 여 쿼리를 방지 합니다. 쿼리에 Columnstore 인덱스 사용을 방지하기 위한 쿼리 힌트와 Columnstore 인덱스를 사용하기 위한 인덱스 힌트가 포함되어 있으면 힌트가 충돌하게 되고 오류가 반환됩니다.  
  
 MAX_GRANT_PERCENT = *%*  
 최대 메모리 부여 크기 백분율 단위에서입니다. 쿼리가이 한도 초과 수 없도록 보장 합니다. 실제 제한을 설정 하는 리소스 관리자는이 값 보다 작은 경우 더 낮은 수 있습니다. 유효한 값은 0.0에서 100.0 까지입니다.  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 MIN_GRANT_PERCENT = *%*  
 최소 메모리 부여 크기 %에서 = %의 기본 제한 합니다. 쿼리는 적어도 메모리는 쿼리를 시작 해야 하는 데 필요한 MAX (필요한 메모리, min 부여)를 가져오지 보장 됩니다. 유효한 값은 0.0에서 100.0 까지입니다.  
  
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 MAXDOP *번호*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 재정의 **x degree of** 구성 옵션의 **sp_configure** 및이 옵션을 지정 하는 쿼리에 대 한 리소스 관리자입니다. MAXDOP 쿼리 힌트는 sp_configure로 구성한 값을 초과할 수 있습니다. MAXDOP 리소스 관리자를 구성 된 값을 초과 하는 경우는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 설명 된 리소스 관리자 MAXDOP 값을 사용 하 여 [ALTER WORKLOAD group&#40; Transact SQL &#41; ](../../t-sql/statements/alter-workload-group-transact-sql.md). 함께 사용 하는 모든 의미 규칙은 **x degree of** 구성 옵션은 MAXDOP 쿼리 힌트를 사용 하는 경우 적용할 수 있습니다. 자세한 내용은 [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 참조하세요.  
  
> [!WARNING]  
>  MAXDOP가 0으로 설정되면 서버는 최대 병렬 처리 수준을 선택합니다.  
  
 MAXRECURSION *번호*  
 해당 쿼리에 대해 허용되는 최대 재귀 횟수를 지정합니다. *번호* 는 0에서 32767 사이의 음수가 아닌 정수입니다. 0을 지정하면 제한이 적용되지 않습니다. 이 옵션을 지정하지 않은 경우 서버에 대한 기본 한도는 100입니다.  
  
 쿼리 실행 중에 MAXRECURSION 한도로 지정된 횟수 또는 기본 횟수에 도달하면 쿼리가 종료되고 오류가 반환됩니다.  
  
 이 오류로 인해 문의 모든 결과가 롤백됩니다. 문이 SELECT 문인 경우 결과의 일부가 반환되거나 아무런 결과도 반환되지 않을 수 있습니다. 반환된 일부 결과에는 지정한 최대 재귀 수준을 초과한 재귀 수준의 모든 행이 포함되지 않을 수 있습니다.  
  
 자세한 내용은 참조 [common_table_expression &AMP; #40; Transact SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 NO_PERFORMANCE_SPOOL  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 스풀 연산자 (계획 spool이 유효한 업데이트 의미 체계를 보장 하기 위해 필요한 경우)를 제외한 쿼리 계획에 추가 되지 않도록 방지 합니다. 일부 시나리오에서 스풀 연산자는 성능이 저하 될 수 있습니다. 예를 들어 스풀 tempdb를 사용 하 여 및는 많은 동시 쿼리가 결과, 스풀 작업을 실행 하면 tempdb 경합이 발생할 수 있습니다.  
  
 OPTIMIZE FOR (  *@variable_name*  {알 수 없는 | = *literal_constant}* [ **,** ... *n* ] )  
 쿼리가 컴파일되고 최적화될 때 쿼리 최적화 프로그램이 지역 변수에 대해 특정 값을 사용하도록 지시합니다. 해당 값은 쿼리 최적화 중에만 사용되고 쿼리 실행 중에는 사용되지 않습니다.  
  
 *@variable_name*  
 쿼리에서 사용된 지역 변수의 이름이며 OPTIMIZE FOR 쿼리 힌트와 함께 사용하도록 값을 할당할 수 있습니다.  
  
 *알 수 없음*  
 쿼리 최적화 프로그램이 쿼리 최적화 동안 초기 값 대신 통계 데이터를 사용하여 지역 변수 값을 결정하도록 지정합니다.  
  
 *literal_constant*  
 할당할 리터럴 상수 값  *@variable_name*  OPTIMIZE FOR 쿼리 힌트와 함께 사용 합니다. *literal_constant* 은 쿼리 최적화 중에 아니라 사용 값  *@variable_name*  쿼리 실행 중입니다. *literal_constant* 모든 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 리터럴 상수로 표현할 수 있는 시스템 데이터 형식입니다. 데이터 형식이 *literal_constant* 수 암시적으로 데이터를 입력 해야 하는  *@variable_name*  쿼리에 대 한 참조입니다.  
  
 OPTIMIZE FOR는 최적화 프로그램의 기본 매개 변수 감지 동작을 무효로 만들 수 있으며 계획 지침을 만들 때 사용할 수 있습니다. 자세한 내용은 참조 [저장 프로시저를 다시 컴파일하려면](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)합니다.  
  
 OPTIMIZE FOR UNKNOWN  
 쿼리가 컴파일 및 최적화될 때 쿼리 최적화 프로그램이 강제 매개 변수화를 통해 만든 매개 변수를 비롯한 모든 지역 변수에 대해 초기 값 대신 통계 데이터를 사용하도록 지시합니다.  
  
 경우에 대해 최적화 @variable_name = *literal_constant* 와 같은 쿼리 힌트에서 OPTIMIZE FOR UNKNOWN 사용 되 고, 쿼리 최적화 프로그램이 사용 됩니다는 *literal_constant* 특정 값에 지정 된 및 나머지 변수 값에 대 한 알 수 없습니다. 해당 값은 쿼리 최적화 중에만 사용되고 쿼리 실행 중에는 사용되지 않습니다.  
  
 PARAMETERIZATION { SIMPLE | FORCED }  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램에서 쿼리 컴파일 시 적용하는 매개 변수화 규칙을 지정합니다.  
  
> [!IMPORTANT]  
>  PARAMETERIZATION 쿼리 힌트는 계획 지침 내에서만 지정할 수 있습니다. 쿼리 내에서 직접 지정할 수는 없습니다.  
  
 SIMPLE은 쿼리 최적화 프로그램이 단순 매개 변수화를 시도하도록 지시합니다. FORCED는 최적화 프로그램이 강제 매개 변수화를 시도하도록 지시합니다. PARAMETERIZATION 쿼리 힌트는 계획 지침 내에서 PARAMETERIZATION 데이터베이스 SET 옵션의 현재 설정을 무시하는 데 사용됩니다. 자세한 내용은 참조 [계획 지침 사용 하 여 쿼리 매개 변수화 동작 지정](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)합니다.  
  
 RECOMPILE  
 쿼리를 실행한 후 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 해당 쿼리에 대해 생성된 계획을 삭제하도록 하여 다음에 같은 쿼리가 실행될 때 쿼리 최적화 프로그램이 쿼리 계획을 다시 컴파일하도록 지시합니다. RECOMPILE을 지정 하지 않고는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 계획을 캐시 하 여 다시 사용 합니다. 쿼리 계획을 컴파일할 때 RECOMPILE 쿼리 힌트는 쿼리에 있는 지역 변수의 현재 값을 사용하며 쿼리가 저장 프로시저 안에 있는 경우 매개 변수에 전달된 현재 값을 사용합니다.  
  
 RECOMPILE은 전체 저장 프로시저가 아닌 저장 프로시저 내 쿼리의 하위 집합만 다시 컴파일해야 하는 경우 WITH RECOMPILE 절을 사용하는 저장 프로시저를 만드는 데 유용합니다. 자세한 내용은 참조 [저장 프로시저를 다시 컴파일하려면](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)합니다. RECOMPILE은 계획 지침을 만들 때도 유용합니다.  
  
 ROBUST PLAN  
 쿼리 최적화 프로그램에서 성능이 저하되더라도 잠재적 최대 행 크기를 정의할 수 있는 계획을 세우도록 합니다. 쿼리가 처리될 때 중간 테이블 및 연산자가 입력 행보다 큰 행을 저장하고 처리해야 할 수 있습니다. 행이 너무 커서 특정 연산자가 행을 처리하지 못하는 경우도 있습니다. 이런 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 쿼리 실행 중에 오류를 생성합니다. ROBUST PLAN을 사용하면 쿼리 최적화 프로그램에서 이러한 문제가 발생할 수 있는 쿼리 계획을 고려하지 않도록 할 수 있습니다.  
  
 이러한 계획이 불가능할 경우 쿼리 최적화 프로그램은 쿼리 실행 시 오류를 검색하도록 지연시키지 않고 오류를 반환합니다. 행에는 가변 길이 열이 포함될 수 있으며 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 처리할 수 있는 범위 이상의 잠재적 최대 크기를 가진 행을 정의하도록 허용합니다. 그러나 대개 응용 프로그램은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 처리할 수 있는 한도 내의 실제 크기를 가진 행을 저장합니다. 너무 긴 행이 있으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 실행 오류를 반환합니다.  
 
 사용 하 여 힌트 ( **'***hint_name***'** )  
 **적용 대상**: SQL Server (2016 s p 1부터 시작) 및 Azure SQL 데이터베이스에 적용 됩니다.
 
 힌트 이름에 지정 된 대로 쿼리 프로세서에 하나 이상의 추가 힌트를 제공 **단일 따옴표 안에**합니다. 
  **적용 대상**: 부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] s p 1입니다.

 다음 힌트 이름이 지원 됩니다.
 
*  ' DISABLE_OPTIMIZED_NESTED_LOOP'  
 쿼리 프로세서를 쿼리 계획을 생성할 때 최적화 된 중첩 된 루프 조인에 대 한 정렬 작업 (일괄 처리 정렬)을 사용 하지 않는 지시 합니다. 이에 해당 하는 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2340 합니다.
*  ' FORCE_LEGACY_CARDINALITY_ESTIMATION'  
 사용 하는 쿼리 최적화 프로그램이 [카디널리티 추정](../../relational-databases/performance/cardinality-estimation-sql-server.md) 의 모델 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 이전 버전입니다. 이에 해당 하는 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481 또는 [Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) LEGACY_CARDINALITY_ESTIMATION 설정 = ON입니다.
*  ' ENABLE_QUERY_OPTIMIZER_HOTFIXES'  
 사용 하면 쿼리 최적화 핫픽스 (SQL Server 누적 업데이트 및 서비스 팩에 릴리스된 변경). 이에 해당 하는 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4199 또는 [Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) QUERY_OPTIMIZER_HOTFIXES 설정 = ON입니다.
*  ' DISABLE_PARAMETER_SNIFFING'  
 쿼리 최적화 프로그램이 하나 이상의 매개 변수를 쿼리 계획 독립적인 쿼리가 컴파일될 때 처음 사용 된 매개 변수 값에 사용 하 여 쿼리를 컴파일하는 동안 평균 데이터 분산을 사용 하도록 지시 합니다. 이에 해당 하는 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4136 또는 [Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) PARAMETER_SNIFFING 설정 = OFF입니다.
*  ' ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES'  
 SQL Server를 사용 하 여 최소 선택도 필터에 대 한 AND 조건자를 예상할 때 상관 관계를 고려 하는 계획을 생성 하면 됩니다. 이에 해당 하는 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4137의 카디널리티 추정 모델을 사용한 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 이전 버전을 비슷한 영향을 주지 때 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9471 카디널리티와 함께 사용 됩니다 추정 모델의 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상.
*  ' DISABLE_OPTIMIZER_ROWGOAL'  
 사용 하면 SQL Server 위쪽, OPTION (FAST N)를 포함 하는 쿼리에서 행 목표 조정을 사용 하지 않는 계획을 생성 하거나 키워드 존재 합니다. 이에 해당 하는 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4138 합니다.
*  ' ENABLE_HIST_AMENDMENT_FOR_ASC_KEYS'  
 카디널리티 추정 필요한 모든 선행 인덱스 열에 대 한 빠른 자동으로 생성 된 통계 (히스토그램 수정)를 사용 하도록 설정 합니다. 카디널리티를 예측 하는 데 사용 되는 히스토그램이 열의 실제 최대 또는 최소 값을 설명 하기 위해 쿼리 컴파일 타임에 조정 됩니다. 이에 해당 하는 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4139 합니다. 
*  ' ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS'  
 사용 하면 SQL Server 기본 자료 제약 가정 하는 대신 간단한 포함 가정을 사용 하 여 쿼리 최적화 프로그램에서 조인에 대 한 쿼리 계획을 생성할 [카디널리티 추정](../../relational-databases/performance/cardinality-estimation-sql-server.md) 의 모델 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상. 이에 해당 하는 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9476 합니다. 
*  ' FORCE_DEFAULT_CARDINALITY_ESTIMATION'  
 사용 하는 쿼리 최적화 프로그램이 [카디널리티 추정](../../relational-databases/performance/cardinality-estimation-sql-server.md) 현재 데이터베이스 호환성 수준에 해당 하는 모델입니다. 이 힌트를 사용 하 여 재정의할 [Database Scoped Configuration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) LEGACY_CARDINALITY_ESTIMATION 설정 = ON 또는 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481 합니다.
 
> [!TIP]
> 힌트 이름은 대/소문자를 구분 하지 않습니다.
  
  동적 관리 뷰를 사용 하 여 모든 지원 되는 USE 힌트 이름의 목록을 쿼리할 수 [sys.dm_exec_valid_use_hints ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md)합니다.
> [!IMPORTANT] 
> USE 힌트는 힌트 전역에서 사용 하도록 설정 하는 추적 플래그와 충돌할 수 있습니다 또는 세션 수준 또는 데이터베이스 범위 구성 설정입니다. 이 경우 쿼리 수준 힌트 (사용 하 여 HINT) 항상 우선합니다. 다른 쿼리 힌트 또는 쿼리 수준에서 사용 추적 플래그를 사용 하 여 힌트가 충돌 하는 경우 (같은 QUERYTRACEON 여), SQL Server 쿼리를 실행 하려고 할 때 오류가 발생 합니다. 

 USE PLAN N**'***xml_plan***'**  
 지정 된 쿼리에 대 한 기존 쿼리 계획을 사용 하는 쿼리 최적화 프로그램이 **'***xml_plan***'**합니다. USE PLAN은 INSERT, UPDATE, MERGE 또는 DELETE 문에서 지정할 수 없습니다.  
  
테이블 힌트 **(***exposed_object_name* [ **,** \<테이블 힌트 > [[**,** ]...  *n*  ]] **)** 에 해당 하는 뷰나 테이블에 지정된 된 테이블 힌트를 적용 *exposed_object_name*합니다. 테이블 힌트의 컨텍스트에서만에서 쿼리 힌트로 사용할 수 있는 권장 된 [계획 지침](../../relational-databases/performance/plan-guides.md)합니다.  
  
 *exposed_object_name* 다음 참조 중 하나일 수 있습니다.  
  
-   테이블 또는 보기에 대해 별칭이 사용 되는 경우는 [FROM](../../t-sql/queries/from-transact-sql.md) 쿼리 절 *exposed_object_name* 은 별칭입니다.  
  
-   별칭을 사용 하지 않는 경우 *exposed_object_name* 테이블 또는 뷰의 FROM 절에서 참조 되는 정확히 일치 합니다. 예를 들어, 테이블 또는 뷰 참조 하는 경우 두 부분으로 이루어진 이름을 사용 하 여 *exposed_object_name* 동일한 두 부분으로 이루어진 이름입니다.  
  
 때 *exposed_object_name* 도 개체에 대 한 테이블 힌트의 일부인 무시 되 고 쿼리 최적화 프로그램에서 인덱스 사용 여부를 결정 하는 대로 쿼리에 지정 된 모든 인덱스의 테이블 힌트를 지정 하지 않고 지정 됩니다. 이 방법은 원래 쿼리를 수정할 수 없을 때 INDEX 테이블 힌트의 효과를 제거하는 데 이용할 수 있습니다. 자세한 내용은 예 10을 참조하세요.  
  
**\<테이블 힌트 >:: =** {[NOEXPAND] {인덱스 ( *index_value* [,... *n* ] ) | 인덱스 = ( *index_value* ) | FORCESEEK [**(***index_value***(***index_column_name* [**,**...] **))** ]| FORCESCAN | HOLDLOCK | NOLOCK | NOWAIT | PAGLOCK | READCOMMITTED | READCOMMITTEDLOCK | READPAST | READUNCOMMITTED | REPEATABLEREAD | ROWLOCK | 직렬화 가능 | 스냅숏 | SPATIAL_WINDOW_MAX_CELLS가 | TABLOCK | TABLOCKX | UPDLOCK | XLOCK}에 해당 하는 뷰나 테이블에 적용할 테이블 힌트는 *exposed_object_name* 를 쿼리 힌트로 합니다. 이러한 힌트에 대 한 참조 [테이블 힌트 &#40; Transact SQL &#41; ](../../t-sql/queries/hints-transact-sql-table.md).  
  
 쿼리에 테이블 힌트를 지정하는 WITH 절이 없다면 INDEX, FORCESCAN 및 FORCESEEK 이외의 테이블 힌트를 쿼리 힌트로 사용할 수 없습니다. 자세한 내용은 설명 부분을 참조하세요.  
  
> [!CAUTION] 
> 매개 변수와 함께 FORCESEEK를 지정할 경우 매개 변수 없이 FORCESEEK를 지정할 때보다 최적화 프로그램에서 고려할 수 있는 계획 수가 더 제한됩니다. 이로 인해 "계획을 생성할 수 없음" 오류가 많은 사례에서 발생하는 원인이 될 수도 있습니다. 후속 릴리스에서는 더 많은 계획을 고려할 수 있도록 최적화 프로그램이 수정될 것입니다.  
  
## <a name="remarks"></a>주의  
 쿼리 힌트는 문 내에 SELECT 절이 사용되는 경우를 제외하고 INSERT 문에서 지정할 수 없습니다.  
  
 쿼리 힌트는 하위 쿼리가 아닌 최상위 쿼리에서만 지정할 수 있습니다. 최상위 수준 쿼리에 또는 하위 쿼리에; 힌트를 지정할 수는 테이블 힌트를 쿼리 힌트로 지정 하는 경우 에 대 한 값을 지정 하는 반면 *exposed_object_name* TABLE HINT 절 쿼리 또는 하위 쿼리의 표시 이름과 일치 해야 합니다.  
  
## <a name="specifying-table-hints-as-query-hints"></a>테이블 힌트를 쿼리 힌트로 지정  
 INDEX, FORCESCAN 또는 FORCESEEK 테이블 힌트의 컨텍스트에서만에서 쿼리 힌트로 사용 하는 것이 좋습니다는 [계획 지침](../../relational-databases/performance/plan-guides.md)합니다. 계획 지침은 타사 응용 프로그램인 경우와 같이 원래 쿼리를 수정할 수 없을 때 유용합니다. 계획 지침에 지정되어 있는 쿼리 힌트는 쿼리가 컴파일 및 최적화되기 전에 쿼리에 추가됩니다. 임시 쿼리의 경우 계획 지침 문을 테스트할 때에만 TABLE HINT 절을 사용하세요. 임시 쿼리 이외의 모든 경우 이러한 힌트를 테이블 힌트로만 지정하는 것이 좋습니다.  
  
 INDEX, FORCESCAN 및 FORCESEEK 테이블 힌트를 쿼리 힌트로 지정하는 경우 다음 개체에 대해서 유효합니다.  
  
-   테이블  
  
-   뷰  
  
-   인덱싱된 뷰  
  
-   공통 테이블 식(공통 테이블 식을 채울 결과 집합을 위한 SELECT 문에 힌트를 지정해야 함)  
  
-   동적 관리 뷰  
  
-   명명된 하위 쿼리  
  
 기존 테이블 힌트가 없는 쿼리에 대해 INDEX, FORCESCAN 및 FORCESEEK 테이블 힌트를 쿼리 힌트로 지정할 수 있습니다. 또는 INDEX 및 FORCESEEK 힌트를 사용하여 쿼리에 있는 기존 INDEX, FORCESCAN 또는 FORCESEEK 힌트를 각각 대체할 수 있습니다. 쿼리에 테이블 힌트를 지정하는 WITH 절이 없다면 INDEX, FORCESCAN 및 FORCESEEK 이외의 테이블 힌트를 쿼리 힌트로 사용할 수 없습니다. 이 경우 OPTION 절에 TABLE HINT를 사용하여 일치하는 힌트를 쿼리 힌트로 지정함으로써 쿼리의 의미 체계를 유지해야 합니다. 예를 들어 있는 OPTION 절에 NOLOCK 테이블 힌트를 쿼리에  **@hints**  계획 지침의 매개 변수에 NOLOCK 힌트가 있어야 합니다. 예 11. 일치 하는 쿼리 힌트 없이 OPTION 절에 TABLE HINT를 사용 하 여 INDEX, FORCESCAN 또는 FORCESEEK 이외의 테이블 힌트를 지정 하거나 그 반대의 경우도 마찬가지입니다. (OPTION 절을 변경 하려면 쿼리의 의미 체계를 될 수 있다는 것을 나타냄) 오류 8702가 발생 하 고 쿼리가 실패 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-merge-join"></a>1. MERGE JOIN 사용  
 다음 예제에서는 쿼리에서 JOIN 연산을 병합 조인 하 여 수행 되도록 지정 합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```  
SELECT *   
FROM Sales.Customer AS c  
INNER JOIN Sales.CustomerAddress AS ca ON c.CustomerID = ca.CustomerID  
WHERE TerritoryID = 5  
OPTION (MERGE JOIN);  
GO    
```  
  
### <a name="b-using-optimize-for"></a>2. OPTIMIZE FOR 사용  
 다음 예제에서는 값을 사용 하려면 쿼리 최적화 프로그램에 지시 `'Seattle'` 지역 변수에 대해 `@city_name` 하 고 지역 변수에 값을 결정 하려면 통계 데이터를 사용 하도록 `@postal_code` 쿼리를 최적화할 때. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```  
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
 잘못 구성된 재귀 공통 테이블 식이 무한 루프에 진입하는 것을 방지하는 데 MAXRECURSION을 사용할 수 있습니다. 다음 예에서는 의도적으로 무한 루프를 만들고, MAXRECURSION 힌트를 사용 하 여 재귀 수준 2로 수를 제한 합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```tsql  
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
  
```  
SELECT *  
FROM HumanResources.Employee AS e1  
UNION  
SELECT *  
FROM HumanResources.Employee AS e2  
OPTION (MERGE UNION);  
GO  
```  
  
### <a name="e-using-hash-group-and-fast"></a>5. HASH GROUP 및 FAST 사용  
 다음 예제에서는 HASH GROUP 및 FAST 쿼리 힌트를 사용합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
```  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (HASH GROUP, FAST 10);  
GO    
```  
  
### <a name="f-using-maxdop"></a>6. MAXDOP 사용  
 다음 예제에서는 MAXDOP 쿼리 힌트를 사용합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
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
  
```  
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
  
```  
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
  
```  
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
  
```  
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
  
```  
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
  
```  
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
### <a name="l-using-use-hint"></a>12. USE 힌트를 사용 하 여  
 다음 예제에서는 재컴파일 및 사용 하 여 힌트 쿼리 힌트를 사용합니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스를 사용합니다.  
  
**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]합니다.  
  
```  
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (RECOMPILE, USE HINT ('ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES', 'DISABLE_PARAMETER_SNIFFING')); 
GO  
```  
    
## <a name="see-also"></a>관련 항목:  
 [힌트 &#40; Transact SQL &#41;](../../t-sql/queries/hints-transact-sql.md)   
 [sp_create_plan_guide&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_control_plan_guide&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
 [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  

