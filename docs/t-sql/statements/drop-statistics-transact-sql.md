---
title: DROP STATISTICS (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/22/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP STATISTICS
- DROP_STATISTICS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing statistics
- column statistics [SQL Server]
- DROP STATISTICS statement
- deleting statistics
- dropping statistics
- table statistics [SQL Server]
- statistical information [SQL Server], removing
ms.assetid: 222806b7-4e45-445b-8cd0-bd5461f3ca4a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 34cc65eaccfdfcbffd38e93f613f2b2d34de23d0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="drop-statistics-transact-sql"></a>DROP STATISTICS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스에서 지정한 테이블 내에 있는 여러 컬렉션에 대한 통계를 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP STATISTICS table.statistics_name | view.statistics_name [ ,...n ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP STATISTICS [ schema_name . ] table_name.statistics_name   
[;]  
```  
  
## <a name="arguments"></a>인수  
 *테이블* | *보기*  
 통계를 삭제할 대상 테이블이나 인덱싱된 뷰의 이름입니다. 에 대 한 규칙을 사용 하 여 테이블 및 뷰 이름은 따라야 [데이터베이스 식별자](../../relational-databases/databases/database-identifiers.md)합니다. 테이블이나 뷰 소유자 이름은 선택적으로 지정할 수 있습니다.  
  
 *statistics_name*  
 삭제할 통계 그룹의 이름입니다. 통계 이름은 식별자에 대한 규칙을 따라야 합니다.  
  
## <a name="remarks"></a>주의  
 통계를 삭제할 때는 주의하세요. 통계를 삭제하면 쿼리 최적화 프로그램이 선택한 실행 계획에 영향을 줄 수 있습니다.  
  
 인덱스에 대한 통계는 DROP STATISTICS를 사용하여 삭제할 수 없으며 인덱스가 존재하는 한 통계도 유지됩니다.  
  
 통계 표시 하는 방법에 대 한 자세한 내용은 참조 [DBCC show_statistics&#40; Transact SQL &#41; ](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 테이블이나 뷰에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-statistics-from-a-table"></a>1. 테이블에서 통계를 삭제 하는 중  
 다음 예에서는 두 테이블의 통계 그룹(컬렉션)을 삭제하는 방법을 보여 줍니다. `VendorCredit` 테이블의 `Vendor` 통계 그룹(컬렉션)과 `CustomerTotal` 테이블의 `SalesOrderHeader` 통계(컬렉션)가 삭제됩니다.  
  
```  
-- Create the statistics groups.  
USE AdventureWorks2012;  
GO  
CREATE STATISTICS VendorCredit  
    ON Purchasing.Vendor (Name, CreditRating)  
    WITH SAMPLE 50 PERCENT  
CREATE STATISTICS CustomerTotal  
    ON Sales.SalesOrderHeader (CustomerID, TotalDue)  
    WITH FULLSCAN;  
GO  
DROP STATISTICS Purchasing.Vendor.VendorCredit, Sales.SalesOrderHeader.CustomerTotal;  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-dropping-statistics-from-a-table"></a>2. 테이블에서 통계를 삭제 하는 중  
 다음 예에서는 drop는 `CustomerStats1` 테이블에서 통계 `Customer`합니다.  
  
```  
DROP STATISTICS Customer.CustomerStats1;  
DROP STATISTICS dbo.Customer.CustomerStats1;  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [sys.stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [sys.stats_columns &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [sp_autostats &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_createstats &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [USE&#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
  
  


