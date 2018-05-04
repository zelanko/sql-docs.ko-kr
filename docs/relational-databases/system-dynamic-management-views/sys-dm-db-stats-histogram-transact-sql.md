---
title: sys.dm_db_stats_histogram (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sys.dm_db_stats_histogram
- sys.dm_db_stats_histogram_TSQL
- dm_db_stats_histogram
- dm_db_stats_histogram_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_stats_histogram dynamic management function
ms.assetid: 1897fd4a-8d51-461e-8ef2-c60be9e563f2
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b285993ef96bd434e26988dbf922cbfdc1926d65
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmdbstatshistogram-transact-sql"></a>sys.dm_db_stats_histogram (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

현재에서 지정 된 데이터베이스 개체 (테이블 또는 인덱싱된 뷰)에 대 한 통계 히스토그램 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다. 유사한 `DBCC SHOW_STATISTICS WITH HISTOGRAM`합니다.

> [!NOTE] 
> 이 DMF 부터는 ´ ï ´ [!INCLUDE[ssSQL15](../../includes/ssSQL15-md.md)] SP1 CU2

## <a name="syntax"></a>구문  
  
```  
sys.dm_db_stats_histogram (object_id, stats_id)  
```  
  
## <a name="arguments"></a>인수  
 *object_id*  
 해당 통계 중 하나의 속성이 요청되는 현재 데이터베이스에 포함된 개체의 ID입니다. *object_id* 는 **int**입니다.  
  
 *stats_id*  
 지정된 *object_id*통계의 ID입니다. 통계 ID는 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) 동적 관리 뷰에서 얻을 수 있습니다. *stats_id* 는 **int**입니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_id |**int**|통계 개체의 속성을 반환하는 개체(테이블 또는 인덱싱된 뷰)의 ID입니다.|  
|stats_id |**int**|통계 개체의 ID입니다. 테이블 또는 인덱싱된 뷰 내에서 고유합니다. 자세한 내용은 [sys.stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)를 참조하세요.|  
|step_number |**int** |히스토그램 단계 수입니다. |
|range_high_key |**sql_variant** |히스토그램 단계의 상한 열 값입니다. 열 값은 키 값이라고도 합니다.|
|range_rows |**real** |상한을 제외한 히스토그램 단계 내에 열 값이 있는 예상 행 수입니다. |
|equal_rows |**real** |히스토그램 단계에서 상한과 열 값이 동일한 예상 행 수입니다. |
|distinct_range_rows |**bigint** |상한을 제외한 히스토그램 단계 내에 고유한 열 값이 있는 예상 행 수입니다. |
|average_range_rows |**real** |상한을 제외한 히스토그램 단계 내에서 중복 열 값이 있는 행의 평균 수 (`RANGE_ROWS / DISTINCT_RANGE_ROWS` 에 대 한 `DISTINCT_RANGE_ROWS > 0`). |
  
 ## <a name="remarks"></a>주의  
 
 에 대 한 결과 집합 `sys.dm_db_stats_histogram` 유사한 정보를 반환 `DBCC SHOW_STATISTICS WITH HISTOGRAM` 포함 `object_id`, `stats_id`, 및 `step_number`합니다.

 때문에 열 `range_high_key` 는 sql_variant 데이터 형식에 사용 해야 할 수도 `CAST` 또는 `CONVERT` 조건자 문자열이 아닌 상수와 비교를 수행 하는 경우.

### <a name="histogram"></a>히스토그램
  
 히스토그램은 데이터 집합에서 각 고유 값의 발생 빈도를 측정합니다. 쿼리 최적화 프로그램은 행을 통계적으로 샘플링하거나 테이블 또는 뷰의 모든 행에 대해 전체 검색을 수행하는 방법으로 열 값을 선택하여 통계 개체의 첫 번째 키 열에 있는 열 값에 대한 히스토그램을 계산합니다. 샘플링된 행 집합으로 히스토그램을 만드는 경우 저장된 행 수의 합계와 고유 값의 수는 예상치이며 정수일 필요가 없습니다.  
  
 쿼리 최적화 프로그램에서는 히스토그램을 만들기 위해 열 값을 정렬하고 고유한 각 열 값과 일치하는 값의 수를 계산한 다음 열 값을 최대 200개의 연속적인 히스토그램 단계로 집계합니다. 각 단계의 범위는 열 값에서 상한 열 값까지입니다. 범위는 경계 값 자체를 제외하고 경계 값 사이의 모든 가능한 열 값을 포함합니다. 정렬된 열 값 중 가장 낮은 값은 첫 번째 히스토그램 단계의 상한 값입니다.  
  
 다음 다이어그램에서는 6단계의 히스토그램을 보여 줍니다. 첫 번째 상한 값 왼쪽의 영역이 1단계입니다.  
  
 ![](../../relational-databases/system-dynamic-management-views/media/histogram_2.gif "히스토그램")  
  
 각 히스토그램 단계를 살펴보면 다음과 같습니다.  
  
-   굵은 선은 상한 값(*range_high_key*)과 발생한 횟수(*equal_rows*)를 나타냅니다.  
  
-   *range_high_key* 왼쪽의 채워진 영역은 열 값의 범위와 각 열 값이 발생한 평균 횟수(*average_range_rows*)를 나타냅니다. 첫 번째 히스토그램 단계의 *average_range_rows*는 항상 0입니다.  
  
-   점선은 범위 내 고유 값의 총 개수(*distinct_range_rows*) 및 범위 내 값의 총 개수(*range_rows*)를 예상하는 데 사용되는 샘플링된 값을 나타냅니다. 쿼리 최적화 프로그램은 *range_rows* 및 *distinct_range_rows*를 사용하여 *average_range_rows*를 계산하며 샘플링된 값은 저장하지 않습니다.  
  
 쿼리 최적화 프로그램은 통계적 중요성에 따라 히스토그램 단계를 정의합니다. 또한 히스토그램의 단계 수를 최소화하면서 경계 값 간의 차이를 최대화하기 위해 최대 차이 알고리즘을 사용합니다. 최대 단계 수는 200개입니다. 히스토그램 단계 수는 경계 지점이 200개 미만인 열에서도 고유 값의 개수보다 적을 수 있습니다. 예를 들어 100개의 고유 값을 가진 열의 히스토그램에 100개 미만의 경계 지점이 있을 수 있습니다.  
  
## <a name="permissions"></a>Permissions  

사용자가 통계 열에 대한 select 권한이 있거나 테이블을 소유하거나 `sysadmin` 고정 서버 역할, `db_owner` 고정 데이터베이스 역할, 또는 `db_ddladmin` 고정 데이터베이스 역할의 멤버여야 합니다.

## <a name="examples"></a>예  

### <a name="a-simple-example"></a>1. 간단한 예    
다음 예제에서는 만들고 간단한 테이블을 채웁니다. 그런 다음에 통계를 작성은 `Country_Name` 열입니다.

```sql
CREATE TABLE Country
(Country_ID int IDENTITY PRIMARY KEY,
Country_Name varchar(120) NOT NULL);
INSERT Country (Country_Name) VALUES ('Canada'), ('Denmark'), ('Iceland'), ('Peru');

CREATE STATISTICS Country_Stats  
    ON Country (Country_Name) ;  
```   
기본 키를 차지 `stat_id` 번호가 1, 없으므로 호출 `sys.dm_db_stats_histogram` 에 대 한 `stat_id` 번호 2에 대 한 통계 히스토그램을 반환 하는 `Country` 테이블입니다.    
```sql     
SELECT * FROM sys.dm_db_stats_histogram(OBJECT_ID('Country'), 2);
```

### <a name="b-useful-query"></a>2. 유용한 쿼리:   
```sql  
SELECT hist.step_number, hist.range_high_key, hist.range_rows, 
    hist.equal_rows, hist.distinct_range_rows, hist.average_range_rows
FROM sys.stats AS s
CROSS APPLY sys.dm_db_stats_histogram(s.[object_id], s.stats_id) AS hist
WHERE s.[name] = N'<statistic_name>';
```

### <a name="c-useful-query"></a>3. 유용한 쿼리:
다음 예에서는 테이블에서 선택 `Country` 열에 대 한 조건자가 있는 `Country_Name`합니다.

```sql  
SELECT * FROM Country 
WHERE Country_Name = 'Canada';
```

다음 예에서는 테이블에 대해 이전에 만든된 통계 살펴봅니다 `Country` 및 열 `Country_Name` 위의 쿼리에서 조건자와 일치 하는 히스토그램 단계에 대 한 합니다.

```sql  
SELECT ss.name, ss.stats_id, shr.steps, shr.rows, shr.rows_sampled, 
    shr.modification_counter, shr.last_updated, sh.range_rows, sh.equal_rows
FROM sys.stats ss
INNER JOIN sys.stats_columns sc 
    ON ss.stats_id = sc.stats_id AND ss.object_id = sc.object_id
INNER JOIN sys.all_columns ac 
    ON ac.column_id = sc.column_id AND ac.object_id = sc.object_id
CROSS APPLY sys.dm_db_stats_properties(ss.object_id, ss.stats_id) shr
CROSS APPLY sys.dm_db_stats_histogram(ss.object_id, ss.stats_id) sh
WHERE ss.[object_id] = OBJECT_ID('Country') 
    AND ac.name = 'Country_Name'
    AND sh.range_high_key = CAST('Canada' AS CHAR(8));
```
  
## <a name="see-also"></a>관련 항목:  
[DBCC SHOW_STATISTICS (TRANSACT-SQL)](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
[개체 관련된 동적 관리 뷰 및 함수 (Transact SQL)](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)  
[sys.dm_db_stats_properties(Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)  
