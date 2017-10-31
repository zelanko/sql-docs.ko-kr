---
title: STATS_DATE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
ms.assetid: f9ec3101-1e41-489d-b519-496a0d6089fb
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 44fc7524040db874abc5d596b641cba985dcf893
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="statsdate-transact-sql"></a>STATS_DATE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  테이블 또는 인덱싱된 뷰의 통계에 대한 가장 최근의 업데이트 날짜를 반환합니다.  
  
 통계를 업데이트 하는 방법에 대 한 자세한 내용은 참조 [통계](../../relational-databases/statistics/statistics.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
STATS_DATE ( object_id , stats_id )  
```  
  
## <a name="arguments"></a>인수  
 *object_id*  
 통계를 포함하는 테이블 또는 인덱싱된 뷰의 ID입니다.  
  
 *stats_id*  
 통계 개체의 ID입니다.  
  
## <a name="return-types"></a>반환 형식  
 반환 **datetime** 성공 합니다. 반환 **NULL** 오류 발생 시.  
  
## <a name="remarks"></a>주의  
 시스템 함수는 SELECT 목록, WHERE 절 및 식이 사용되는 모든 위치에서 사용할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 db_owner 고정 데이터베이스 역할의 멤버이어야 하거나, 테이블이나 인덱싱된 뷰의 메타데이터를 볼 수 있는 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-return-the-dates-of-the-most-recent-statistics-for-a-table"></a>1. 테이블에 대한 가장 최근 통계의 날짜 반환  
 다음 예에서는 `Person.Address` 테이블에 있는 각 통계 개체에 대한 가장 최근의 업데이트 날짜를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_update_date  
FROM sys.stats   
WHERE object_id = OBJECT_ID('Person.Address');  
GO  
```  
  
 통계가 인덱스에 대응 하는 경우는 *stats_id* 값는 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) 카탈로그 뷰는 동일는 *index_id* 값에 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰와 다음 쿼리는 이전 쿼리와와 동일한 결과 반환 합니다. 통계가 인덱스에 대응하지 않으면 통계는 sys.indexes 결과가 아닌 sys.stats 결과에 포함됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT name AS index_name,   
    STATS_DATE(object_id, index_id) AS statistics_update_date  
FROM sys.indexes   
WHERE object_id = OBJECT_ID('Person.Address');  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-learn-when-a-named-statistics-was-last-updated"></a>2. 명명 된 통계를 마지막으로 업데이트에 대해 알아봅니다  
 다음 예에서는 DimCustomer 테이블의 LastName 열에 대 한 통계를 만듭니다. 통계의 날짜를 표시 하도록 쿼리를 실행 합니다. 그 다음 통계를 업데이트 하 고 다시 업데이트 날짜를 표시 하려면 쿼리를 실행 합니다.  
  
```  
  
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
  
### <a name="c-view-the-date-of-the-last-update-for-all-statistics-on-a-table"></a>3. 테이블에서 모든 통계에 대 한 마지막 업데이트 날짜를 보려면  
 이 예에서는 DimCustomer 테이블에서 각 통계 개체를 마지막으로 업데이트 하는 경우에 대 한 날짜를 반환 합니다.  
  
```  
--Return the dates all statistics on the table were last updated.  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer');  
GO  
```  
  
 통계가 인덱스에 대응 하는 경우는 *stats_id* 값는 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) 카탈로그 뷰는 동일는 *index_id* 값에 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰와 다음 쿼리는 이전 쿼리와와 동일한 결과 반환 합니다. 통계가 인덱스에 대응하지 않으면 통계는 sys.indexes 결과가 아닌 sys.stats 결과에 포함됩니다.  
  
```  
USE AdventureWorksPDW2012;  
GO  
SELECT name AS index_name,   
    STATS_DATE(object_id, index_id) AS statistics_update_date  
FROM sys.indexes   
WHERE object_id = OBJECT_ID('dbo.DimCustomer');  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_autostats &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [통계](../../relational-databases/statistics/statistics.md)  
  
  


