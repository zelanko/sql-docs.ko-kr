---
title: DBCC SHOW_STATISTICS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SHOW_STATISTICS_TSQL
- DBCC SHOW_STATISTICS
- SHOW_STATISTICS
- DBCC_SHOW_STATISTICS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query optimization statistics [SQL Server], densities
- histograms [SQL Server]
- statistical information [SQL Server], viewing statistics objects
- current distribution statistics
- query optimization statistics [SQL Server], histograms
- DBCC SHOW_STATISTICS statement
- distribution statistics
- statistical information [SQL Server], densities
- statistics objects
- statistical information [SQL Server], histograms
- query optimization statistics [SQL Server], viewing statistics objects
- statistical information [SQL Server], distribution
- densities [SQL Server]
- displaying distribution statistics
ms.assetid: 12be2923-7289-4150-b497-f17e76a50b2e
caps.latest.revision: 75
author: uc-msft
ms.author: umajay
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 45f0e42f637f452b12ff32a0b2f580c3c87e9bd3
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39454637"
---
# <a name="dbcc-showstatistics-transact-sql"></a>DBCC SHOW_STATISTICS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

DBCC SHOW_STATISTICS는 테이블 또는 인덱싱된 뷰에 대한 현재 쿼리 최적화 통계를 표시합니다. 쿼리 최적화 프로그램은 통계를 사용하여 쿼리 결과의 카디널리티 또는 행 수를 예상함으로써 고품질의 쿼리 계획을 생성할 수 있습니다. 예를 들어 쿼리 최적화 프로그램은 카디널리티 예상치를 통해 쿼리 계획에서 index scan 연산자 대신 index seek 연산자를 선택하여 리소스가 많이 소요되는 index scan을 피함으로써 쿼리 성능을 개선할 수 있습니다.
  
쿼리 최적화 프로그램은 테이블 또는 인덱싱된 뷰에 대한 통계를 통계 개체에 저장합니다. 테이블의 경우 통계 개체는 인덱스 또는 테이블 열의 목록에 생성됩니다. 통계 개체에는 통계에 대한 메타데이터가 있는 헤더, 통계 개체의 첫 번째 키 열에 있는 값의 분포에 대한 히스토그램, 그리고 열 간 상관 관계를 측정하는 밀도 벡터가 포함됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 통계 개체의 일부 데이터를 사용하여 카디널리티 예상치를 계산할 수 있습니다.
  
DBCC SHOW_STATISTICS는 통계 개체에 저장된 데이터를 바탕으로 헤더, 히스토그램 및 밀도 벡터를 표시합니다. 이 구문을 사용하면 대상 인덱스 이름, 통계 이름 또는 열 이름과 함께 테이블 또는 인덱싱된 뷰를 지정할 수 있습니다. 이 항목에서는 통계를 표시하고 표시된 결과를 읽는 방법을 설명합니다.
  
자세한 내용은 [Statistics](../../relational-databases/statistics/statistics.md)을(를) 참조하세요.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```
-- Syntax for SQL Server and Azure SQL Database  
  
DBCC SHOW_STATISTICS ( table_or_indexed_view_name , target )   
[ WITH [ NO_INFOMSGS ] < option > [ , n ] ]  
< option > :: =  
    STAT_HEADER | DENSITY_VECTOR | HISTOGRAM | STATS_STREAM  
```  
  
```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

DBCC SHOW_STATISTICS ( table_name , target )   
    [ WITH {STAT_HEADER | DENSITY_VECTOR | HISTOGRAM } [ ,...n ] ]  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *table_or_indexed_view_name*  
 통계 정보를 표시할 테이블 또는 인덱싱된 뷰의 이름입니다.  
  
 *table_name*  
 표시할 통계가 들어 있는 테이블의 이름입니다. 테이블은 외부 테이블일 수 없습니다.  
  
 *대상*  
 통계 정보를 표시할 인덱스, 통계 또는 열의 이름입니다. *대상*은 대괄호, 작은 따옴표, 큰 따옴표 또는 따옴표 없음으로 묶입니다. *target*이 테이블 또는 인덱싱된 뷰의 기존 인덱스 또는 통계 이름인 경우 이 대상에 대한 통계 정보가 반환됩니다. *target*이 기존 열의 이름이고 이 열에 자동으로 생성된 통계가 있는 경우 자동 생성된 통계에 대한 정보가 반환되며, 열 대상에 자동으로 생성된 통계가 없는 경우에는 오류 메시지 2767이 반환됩니다.  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 *target*은 열 이름이 될 수 없습니다.  
  
 NO_INFOMSGS  
 심각도가 0에서 10 사이인 모든 정보 메시지를 표시하지 않습니다.  
  
 STAT_HEADER | DENSITY_VECTOR | HISTOGRAM | STATS_STREAM [ **,***n* ]  
 이 옵션 중 하나 이상을 지정하면 문에서 반환하는 결과 집합이 지정한 옵션으로 제한됩니다. 옵션을 지정하지 않으면 모든 통계 정보가 반환됩니다.  
  
 STATS_STREAM은 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]입니다.  
  
## <a name="result-sets"></a>결과 집합  
다음 표에서는 STAT_HEADER를 지정한 경우 결과 집합에 반환되는 열을 설명합니다.
  
|열 이름|설명|  
|-----------------|-----------------|  
|속성|통계 개체의 이름입니다.|  
|업데이트|통계가 마지막으로 업데이트된 날짜와 시간입니다. [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) 함수를 사용하여 이 정보를 검색할 수도 있습니다. 자세한 내용은 이 페이지의 [주의](#Remarks) 섹션을 참조하세요.|  
|행|통계가 마지막으로 업데이트되었을 때 테이블 또는 인덱싱된 뷰의 전체 행 수입니다. 통계가 필터링되거나 필터링된 인덱스에 해당하는 경우 행 수가 테이블의 행 수보다 적을 수 있습니다. 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.|  
|샘플링한 행|통계 계산을 위해 샘플링된 전체 행 수입니다. 샘플링된 행 수가 전체 행 수보다 적은 경우 표시되는 히스토그램과 밀도 결과는 샘플링된 행을 기준으로 하는 예상치입니다.|  
|단계|히스토그램의 총 단계 수입니다. 각 단계의 범위는 열 값에서 상한 열 값까지입니다. 히스토그램 단계는 통계의 첫 번째 키 열에 정의됩니다. 최대 단계 수는 200개입니다.|  
|밀도|히스토그램 경계 값을 제외하고 통계 개체의 첫 번째 키 열에 있는 모든 값에 대해 1/ *고유 값* 으로 계산됩니다. 이 밀도 값은 쿼리 최적화 프로그램에서 사용되지 않으며 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이전 버전과의 호환성을 위해 표시됩니다.|  
|평균 키 길이|통계 개체의 키 열에 있는 모든 값에 대한 값당 평균 바이트 수입니다.|  
|문자열 인덱스|'예'는 통계 개체에 LIKE 연산자를 사용하는 쿼리 조건자(예: `WHERE ProductName LIKE '%Bike'`)의 카디널리티 예상치 정확도를 높이기 위한 문자열 요약 통계가 있음을 나타냅니다. 문자열 요약 통계는 히스토그램과는 별도로 저장되며 통계 개체에서 **char**, **varchar**, **nchar**, **nvarchar**, **varchar(max)**, **nvarchar(max)**, **text**또는 **ntext**형식인 첫 번째 키 열에 생성됩니다.|  
|필터 식|통계 개체에 포함된 테이블 행의 하위 집합에 대한 조건자입니다. NULL = 필터링되지 않은 통계입니다. 필터링된 조건자에 대한 자세한 내용은 [필터링된 인덱스 만들기](../../relational-databases/indexes/create-filtered-indexes.md)를 참조하세요. 필터링된 통계에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.|  
|필터링되지 않은 행|필터 식을 적용하기 전 테이블에 있는 전체 행 수입니다. 필터 식이 NULL이면 필터링되지 않은 행과 행이 동일합니다.|  
|지속된 샘플 비율|샘플링 비율을 명시적으로 지정하지 않은 통계 업데이트에 사용되는 샘플 비율을 유지합니다. 값이 0이면 이 통계에 대해 지속 된 샘플 백분율이 설정되지 않습니다.<br /><br /> **적용 대상:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4| 
  
다음 표에서는 DENSITY_VECTOR를 지정한 경우 결과 집합에 반환되는 열을 설명합니다.
  
|열 이름|설명|  
|-----------------|-----------------|  
|모든 밀도|밀도는 1/ *고유 값*입니다. 결과에는 통계 개체에 있는 각 열 접두사의 밀도가 한 행씩 표시됩니다. 고유 값은 행별 및 열 접두사별 열 값의 고유한 목록입니다. 예를 들어 통계 개체가 키 열 (A, B, C)를 포함하는 경우 결과에서 밀도는 이러한 각 열 접두사의 고유 값 목록인 (A), (A,B) 및 (A, B, C)로 보고됩니다. 접두사 (A, B, C)를 사용하면 이러한 각 목록은 고유 값 목록 (3, 5, 6), (4, 4, 6), (4, 5, 6), (4, 5, 7)입니다. 접두사 (A, B)를 사용하면 동일한 열 값은 이러한 고유 값 목록 (3, 5), (4, 4) 및 (4, 5)를 가집니다.|  
|평균 길이|열 접두사의 열 값 목록을 저장하기 위한 평균 길이(바이트)입니다. 예를 들어 목록 (3, 5, 6)의 각 값에 4바이트가 필요한 경우 길이는 12바이트입니다.|  
|열|모든 밀도 및 평균 길이가 표시되는 접두사의 열 이름입니다.|  
  
다음 표에서는 HISTOGRAM 옵션을 지정한 경우 결과 집합에 반환된 열을 설명합니다.
  
|열 이름|설명|  
|---|---|
|RANGE_HI_KEY|히스토그램 단계의 상한 열 값입니다. 열 값은 키 값이라고도 합니다.|  
|RANGE_ROWS|상한을 제외한 히스토그램 단계 내에 열 값이 있는 예상 행 수입니다.|  
|EQ_ROWS|히스토그램 단계에서 상한과 열 값이 동일한 예상 행 수입니다.|  
|DISTINCT_RANGE_ROWS|상한을 제외한 히스토그램 단계 내에 고유한 열 값이 있는 예상 행 수입니다.|  
|AVG_RANGE_ROWS|상한을 제외한 히스토그램 단계 내에 중복 열 값이 있는 평균 행 수입니다(DISTINCT_RANGE_ROWS > 0인 경우 RANGE_ROWS/DISTINCT_RANGE_ROWS).| 
  
## <a name="Remarks"></a> 주의 

통계 업데이트 날짜는 [히스토그램](#histogram) 및 [밀도 벡터](#density)와 함께 메타데이터가 아닌 [통계 BLOB 개체](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics)에 저장됩니다. 통계 데이터를 생성하기 위해 읽은 데이터가 없으면 통계 BLOB이 만들어지지 않고 날짜를 사용할 수 없으며, *updated* 열은 NULL입니다. 이 경우는 조건자가 행을 반환하지 않는 필터링된 통계 또는 빈 테이블에 대해 필터링된 통계에 해당하는 경우입니다.
  
## <a name="histogram"></a> 히스토그램  
히스토그램은 데이터 집합에서 각 고유 값의 발생 빈도를 측정합니다. 쿼리 최적화 프로그램은 행을 통계적으로 샘플링하거나 테이블 또는 뷰의 모든 행에 대해 전체 검색을 수행하는 방법으로 열 값을 선택하여 통계 개체의 첫 번째 키 열에 있는 열 값에 대한 히스토그램을 계산합니다. 샘플링된 행 집합으로 히스토그램을 만드는 경우 저장된 행 수의 합계와 고유 값의 수는 예상치이며 정수일 필요가 없습니다.
  
쿼리 최적화 프로그램에서는 히스토그램을 만들기 위해 열 값을 정렬하고 고유한 각 열 값과 일치하는 값의 수를 계산한 다음 열 값을 최대 200개의 연속적인 히스토그램 단계로 집계합니다. 각 단계의 범위는 열 값에서 상한 열 값까지입니다. 범위는 경계 값 자체를 제외하고 경계 값 사이의 모든 가능한 열 값을 포함합니다. 정렬된 열 값 중 가장 낮은 값은 첫 번째 히스토그램 단계의 상한 값입니다.
  
다음 다이어그램에서는 6단계의 히스토그램을 보여 줍니다. 첫 번째 상한 값 왼쪽의 영역이 1단계입니다.
  
![](../../relational-databases/system-dynamic-management-views/media/a0ce6714-01f4-4943-a083-8cbd2d6f617a.gif "a0ce6714-01f4-4943-a083-8cbd2d6f617a")
  
각 히스토그램 단계를 살펴보면 다음과 같습니다.
-   굵은 선은 상한 값(RANGE_HI_KEY)과 발생한 횟수(EQ_ROWS)를 나타냅니다.  
-   RANGE_HI_KEY 왼쪽의 채워진 영역은 열 값의 범위와 각 열 값이 발생한 평균 횟수(AVG_RANGE_ROWS)를 나타냅니다. 첫 번째 히스토그램 단계의 AVG_RANGE_ROWS는 항상 0입니다.  
-   점선은 범위 내 고유 값의 총 개수(DISTINCT_RANGE_ROWS) 및 범위 내 값의 총 개수(RANGE_ROWS)를 예상하는 데 사용되는 샘플링된 값을 나타냅니다. 쿼리 최적화 프로그램은 RANGE_ROWS 및 DISTINCT_RANGE_ROWS를 사용하여 AVG_RANGE_ROWS를 계산하며 샘플링된 값은 저장하지 않습니다.  
  
쿼리 최적화 프로그램은 통계적 중요성에 따라 히스토그램 단계를 정의합니다. 또한 히스토그램의 단계 수를 최소화하면서 경계 값 간의 차이를 최대화하기 위해 최대 차이 알고리즘을 사용합니다. 최대 단계 수는 200개입니다. 히스토그램 단계 수는 경계 지점이 200개 미만인 열에서도 고유 값의 개수보다 적을 수 있습니다. 예를 들어 100개의 고유 값을 가진 열의 히스토그램에 100개 미만의 경계 지점이 있을 수 있습니다.
  
## <a name="density"></a> 밀도 벡터  
쿼리 최적화 프로그램은 같은 테이블 또는 인덱싱된 뷰에서 여러 열을 반환하는 쿼리의 카디널리티 예상치 정확도를 높이기 위해 밀도를 사용합니다. 밀도 벡터는 통계 개체에 있는 각 열 접두사당 한 개의 밀도를 포함합니다. 예를 들어 통계 개체에 `CustomerId`, `ItemId`, `Price` 키 열이 있는 경우 다음의 각 열 접두사에 대해 밀도가 계산됩니다.
  
|열 접두사|밀도 계산 기준|  
|---|---|
|(CustomerId)|CustomerId의 값이 일치하는 행|  
|(CustomerId, ItemId)|CustomerId 및 ItemId의 값이 일치하는 행|  
|(CustomerId, ItemId, Price)|CustomerId, ItemId 및 Price의 값이 일치하는 행|  
  
## <a name="restrictions"></a>Restrictions  
 DBCC SHOW_STATISTICS는 공간 인덱스 또는 xVelocity 메모리 최적화 columnstore 인덱스에 대한 통계를 제공하지 않습니다.  
  
## <a name="permissions-for-includessnoversionincludesssnoversion-mdmd-and-includesssdsincludessssds-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 대한 사용 권한  
통계 개체를 보려면 테이블의 소유자이거나 `sysadmin` 고정 서버 역할, `db_owner` 고정 데이터베이스 역할 또는 `db_ddladmin` 고정 데이터베이스 역할의 멤버여야 합니다.
  
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1에서는 권한 제한을 수정하여 사용자가 SELECT 권한을 통해 이 명령을 사용할 수 있게 되었습니다. 다음 요구 사항에서는 명령을 실행하기 위해 SELECT 권한이 있어야 합니다.
-   사용자는 통계 개체의 모든 열에 대해 권한이 있어야 합니다.  
-   사용자는 필터 조건(있는 경우)에서 모든 열에 대해 권한이 있어야 합니다.  
-   테이블에 행 수준 보안 정책을 사용할 수 없습니다.  
  
이 동작을 해제하려면 traceflag 9485를 사용하세요.
  
## <a name="permissions-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 대한 사용 권한  
DBCC SHOW_STATISTICS에는 다음 중 하나의 테이블이나 멤버 자격에 대한 SELECT 권한이 필요합니다.
-   고정 서버 역할(fixed server role)  
-   db_owner 고정 데이터베이스 역할  
-   db_ddladmin 고정 데이터베이스 역할  
  
## <a name="limitations-and-restrictions-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 대한 제한 사항  
DBCC SHOW_STATISTICS는 셸 데이터베이스의 제어 노드 수준에 저장된 통계를 표시합니다. Compute 노드에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 의해 자동 생성된 통계는 표시되지 않습니다.
  
DBCC SHOW_STATISTICS는 외부 테이블에 대해 지원되지 않습니다.
  
## <a name="examples-includessnoversionincludesssnoversion-mdmd-and-includesssdsincludessssds-mdmd"></a>예제: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
### <a name="a-returning-all-statistics-information"></a>1. 모든 통계 정보 반환  
다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 `Person.Address` 테이블의 `AK_Address_rowguid` 인덱스에 대한 모든 통계 정보를 표시합니다.
  
```sql
DBCC SHOW_STATISTICS ("Person.Address", AK_Address_rowguid);  
GO  
```  
  
### <a name="b-specifying-the-histogram-option"></a>2. HISTOGRAM 옵션 지정  
이렇게 하면 Customer_LastName에 대해 표시된 통계 정보를 HISTOGRAM 데이터로 제한합니다.
  
```sql
DBCC SHOW_STATISTICS ("dbo.DimCustomer",Customer_LastName) WITH HISTOGRAM;  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="c-display-the-contents-of-one-statistics-object"></a>3. 하나의 통계 개체 내용 표시  
 다음 예제는 DimCustomer 테이블의 Customer_LastName 통계 내용을 표시합니다.  
  
```sql
-- Uses AdventureWorks  
--First, create a statistics object  
CREATE STATISTICS Customer_LastName   
ON AdventureWorksPDW2012.dbo.DimCustomer (LastName);  
GO  
DBCC SHOW_STATISTICS ("dbo.DimCustomer",Customer_LastName);  
GO  
```  
  
결과는 헤더, 밀도 벡터 및 히스토그램 일부를 보여줍니다.
  
![DBCC SHOW_STATISTICS 결과](../../t-sql/database-console-commands/media/aps-sql-dbccshow-statistics.JPG "DBCC SHOW_STATISTICS 결과")
  
## <a name="see-also"></a>참고 항목  
[통계](../../relational-databases/statistics/statistics.md)  
[CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
[CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)  
[DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)  
[sp_autostats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)  
[sp_createstats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)  
[STATS_DATE&#40;Transact-SQL&#41;](../../t-sql/functions/stats-date-transact-sql.md)  
[UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)  
[sys.dm_db_stats_properties(Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)  
[sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
