---
description: STATS_DATE(Transact-SQL)
title: STATS_DATE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STATS_DATE_TSQL
- STATS_DATE
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], last time updated
- STATS_DATE function
- query optimization statistics [SQL Server], last time updated
- last time statistics updated
- stats update date
ms.assetid: f9ec3101-1e41-489d-b519-496a0d6089fb
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1bc07124925f28ea0114a95ec5a60319bd2112bf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467839"
---
# <a name="stats_date-transact-sql"></a>STATS_DATE(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  테이블 또는 인덱싱된 뷰의 통계에 대한 가장 최근의 업데이트 날짜를 반환합니다.  
  
 통계 업데이트에 대한 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
STATS_DATE ( object_id , stats_id )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *object_id*  
 통계를 포함하는 테이블 또는 인덱싱된 뷰의 ID입니다.  
  
 *stats_id*  
 통계 개체의 ID입니다.  
  
## <a name="return-types"></a>반환 형식  
 성공하면 **datetime**을 반환합니다. 통계 BLOB이 만들어지지 않으면 **NULL**을 반환합니다.  
  
## <a name="remarks"></a>설명  
 시스템 함수는 SELECT 목록, WHERE 절 및 식이 사용되는 모든 위치에서 사용할 수 있습니다.  
 
 통계 업데이트 날짜는 [히스토그램](../../relational-databases/statistics/statistics.md#histogram) 및 [밀도 벡터](../../relational-databases/statistics/statistics.md#density)와 함께 메타데이터가 아닌 [통계 BLOB 개체](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics)에 저장됩니다. 통계 데이터를 생성하기 위해 읽은 데이터가 없으면 통계 BLOB이 만들어지지 않고 날짜를 사용할 수 없습니다. 이 경우는 조건자가 행을 반환하지 않는 필터링된 통계 또는 빈 테이블에 대해 필터링된 통계에 해당하는 경우입니다.
 
 통계가 인덱스에 대응하면 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) 카탈로그 뷰의 *stats_id* 값은 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰의 *index_id* 값과 동일합니다.
  
## <a name="permissions"></a>사용 권한  
 db_owner 고정 데이터베이스 역할의 멤버이어야 하거나, 테이블이나 인덱싱된 뷰의 메타데이터를 볼 수 있는 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-return-the-dates-of-the-most-recent-statistics-for-a-table"></a>A. 테이블에 대한 가장 최근 통계의 날짜 반환  
 다음 예에서는 `Person.Address` 테이블에 있는 각 통계 개체에 대한 가장 최근의 업데이트 날짜를 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_update_date  
FROM sys.stats   
WHERE object_id = OBJECT_ID('Person.Address');  
GO  
```  
  
 통계가 인덱스에 대응하면 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) 카탈로그 뷰의 *stats_id* 값은 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰의 *index_id* 값과 같으며 다음 쿼리는 이전 쿼리와 동일한 결과를 반환합니다. 통계가 인덱스에 대응하지 않으면 통계는 sys.indexes 결과가 아닌 sys.stats 결과에 포함됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT name AS index_name,   
    STATS_DATE(object_id, index_id) AS statistics_update_date  
FROM sys.indexes   
WHERE object_id = OBJECT_ID('Person.Address');  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-learn-when-a-named-statistics-was-last-updated"></a>B. 명명된 통계가 마지막으로 업데이트된 시기 알아보기  
 다음 예에서는 DimCustomer 테이블의 LastName 열에 대한 통계를 만듭니다. 그런 다음, 쿼리를 실행하여 통계 날짜를 표시합니다. 다음으로, 통계를 업데이트하고 쿼리를 다시 실행하여 업데이트된 날짜를 표시합니다.  
  
```sql
--First, create a statistics object  
USE AdventureWorksPDW2012;  
GO  
CREATE STATISTICS Customer_LastName_Stats  
ON AdventureWorksPDW2012.dbo.DimCustomer (LastName)  
WITH SAMPLE 50 PERCENT;  
GO  
  
--Return the date when Customer_LastName_Stats was last updated  
USE AdventureWorksPDW2012;  
GO  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer')  
    AND s.name = 'Customer_LastName_Stats';  
GO  
  
--Update Customer_LastName_Stats so it will have a different timestamp in the next query  
GO  
UPDATE STATISTICS dbo.dimCustomer (Customer_LastName_Stats);  
  
--Return the date when Customer_LastName_Stats was last updated.  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer')  
    AND s.name = 'Customer_LastName_Stats';  
GO    
```  
  
### <a name="c-view-the-date-of-the-last-update-for-all-statistics-on-a-table"></a>C. 테이블의 모든 통계에 대한 마지막 업데이트 날짜 보기  
 이 예에서는 DimCustomer 테이블의 각 통계 개체가 마지막으로 업데이트된 날짜를 반환합니다.  
  
```sql  
--Return the dates all statistics on the table were last updated.  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer');  
GO  
```  
  
 통계가 인덱스에 대응하면 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) 카탈로그 뷰의 *stats_id* 값은 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰의 *index_id* 값과 같으며 다음 쿼리는 이전 쿼리와 동일한 결과를 반환합니다. 통계가 인덱스에 대응하지 않으면 통계는 sys.indexes 결과가 아닌 sys.stats 결과에 포함됩니다.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
SELECT name AS index_name,   
    STATS_DATE(object_id, index_id) AS statistics_update_date  
FROM sys.indexes   
WHERE object_id = OBJECT_ID('dbo.DimCustomer');  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_autostats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [통계](../../relational-databases/statistics/statistics.md)    
 [sys.dm_db_stats_properties&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
  
  

