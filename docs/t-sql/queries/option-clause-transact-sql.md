---
title: "OPTION 절 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPTION clause
- OPTION_TSQL
- OPTION
- OPTION_clause_TSQL
dev_langs: TSQL
helpviewer_keywords:
- clauses [SQL Server], OPTION
- OPTION clause
ms.assetid: f47e2f3f-9302-4711-9d66-16b1a2a7ffe3
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cf74a87408ca73229636f3e4ad341838c861bc43
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="option-clause-transact-sql"></a>OPTION 절(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정한 쿼리 힌트가 전체 쿼리에서 사용되도록 지정합니다. 여러 개의 쿼리 힌트가 허용되지만 각 쿼리 힌트는 한 번만 지정할 수 있습니다. 문에서 하나의 OPTION 절만 지정할 수 있습니다.  
  
 SELECT, DELETE, UPDATE 및 MERGE 문에서 이 절을 지정할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[ OPTION ( <query_hint> [ ,...n ] ) ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
OPTION ( <query_option> [ ,...n ] )  
  
<query_option> ::=  
    LABEL = label_name |  
    <query_hint>  
  
<query_hint> ::=  
    HASH JOIN   
    | LOOP JOIN   
    | MERGE JOIN  
    | FORCE ORDER  
    | { FORCE | DISABLE } EXTERNALPUSHDOWN  
```  
  
## <a name="arguments"></a>인수  
 *query_hint*  
 데이터베이스 엔진에서 최적화 프로그램 힌트를 사용하여 문을 처리하는 방법을 사용자 지정한다는 것을 나타내는 키워드입니다. 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-an-option-clause-with-a-group-by-clause"></a>1. GROUP BY 절이 있는 OPTION 절을 사용 하 여  
 다음 예에서는 `OPTION` 절과 함께 `GROUP BY` 절을 사용하는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (HASH GROUP, FAST 10);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-select-statement-with-a-label-in-the-option-clause"></a>2. SELECT 문의 OPTION 절에는 레이블 사용  
 다음 예제에서는 간단한 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] SELECT 문의 OPTION 절에는 레이블 사용 합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactResellerSales  
  OPTION ( LABEL = 'q17' );  
```  
  
### <a name="c-select-statement-with-a-query-hint-in-the-option-clause"></a>3. SELECT 문의 OPTION 절에 쿼리 힌트와 함께  
 다음 예에서는 OPTION 절에 HASH JOIN 쿼리 힌트를 사용 하는 SELECT 문을 보여 줍니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT COUNT (*) FROM dbo.DimCustomer a  
INNER JOIN dbo.FactInternetSales b   
ON (a.CustomerKey = b.CustomerKey)  
OPTION (HASH JOIN);  
```  
  
### <a name="d-select-statement-with-a-label-and-multiple-query-hints-in-the-option-clause"></a>4. 레이블과 OPTION 절에 여러 개의 쿼리 힌트가 들어 있는 SELECT 문의  
 다음 예제는 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] 레이블 및 여러 개의 쿼리 힌트가 들어 있는 SELECT 문의 합니다. 쿼리가 계산 노드에서 실행 될 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 해시 조인 또는 병합 조인 전략에 따라 적용 됩니다 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 결정 하는 가장 적합 합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT COUNT (*) FROM dbo.DimCustomer a  
INNER JOIN dbo.FactInternetSales b   
ON (a.CustomerKey = b.CustomerKey)  
OPTION ( Label = 'CustJoin', HASH JOIN, MERGE JOIN);  
```  
  
### <a name="e-using-a-query-hint-when-querying-a-view"></a>5. 뷰를 쿼리할 때는 쿼리 힌트를 사용 하 여  
 다음 예제에서는 CustomerView 이라는 뷰를 만들고 HASH JOIN 쿼리 힌트를 사용 하 여 뷰와 테이블을 참조 하는 쿼리에서 합니다.  
  
```  
-- Uses AdventureWorks  
  
CREATE VIEW CustomerView  
AS  
SELECT CustomerKey, FirstName, LastName FROM ssawPDW..DimCustomer;  
  
SELECT COUNT (*) FROM dbo.CustomerView a  
INNER JOIN dbo.FactInternetSales b  
ON (a.CustomerKey = b.CustomerKey)  
OPTION (HASH JOIN);  
  
DROP VIEW CustomerView;  
  
```  
  
### <a name="f-query-with-a-subselect-and-a-query-hint"></a>6. 하위 select 및 쿼리 힌트는 쿼리  
 다음 예에서는 하위 select 및 쿼리 힌트를 모두 포함 하는 쿼리를 보여 줍니다. 쿼리 힌트는 전역적으로 적용 됩니다. 쿼리 힌트는 하위 select 문에서에 추가 되는 허용 되지 않습니다.  
  
```  
-- Uses AdventureWorks  
  
CREATE VIEW CustomerView AS  
SELECT CustomerKey, FirstName, LastName FROM ssawPDW..DimCustomer;  
  
SELECT * FROM (  
SELECT COUNT (*) AS a FROM dbo.CustomerView a  
INNER JOIN dbo.FactInternetSales b  
ON ( a.CustomerKey = b.CustomerKey )) AS t  
OPTION (HASH JOIN);  
```  
  
### <a name="g-force-the-join-order-to-match-the-order-in-the-query"></a>7. 조인 순서는 쿼리에서 순서와 일치 하도록을 강제 적용  
 다음 예제에서는 FORCE ORDER 힌트를 사용 하 여를 사용 하는 쿼리로 지정 된 조인 순서 쿼리 계획을 적용 합니다. 일부 쿼리;에서 성능을 향상이 일부 쿼리 합니다.  
  
```  
-- Uses AdventureWorks  
  
-- Obtain partition numbers, boundary values, boundary value types, and rows per boundary  
-- for the partitions in the ProspectiveBuyer table of the ssawPDW database.  
SELECT sp.partition_number, prv.value AS boundary_value, lower(sty.name) AS boundary_value_type, sp.rows   
FROM sys.tables st JOIN sys.indexes si ON st.object_id = si.object_id AND si.index_id <2  
JOIN sys.partitions sp ON sp.object_id = st.object_id AND sp.index_id = si.index_id  
JOIN sys.partition_schemes ps ON ps.data_space_id = si.data_space_id   
JOIN sys.partition_range_values prv ON prv.function_id = ps.function_id   
JOIN sys.partition_parameters pp ON pp.function_id = ps.function_id   
JOIN sys.types sty ON sty.user_type_id = pp.user_type_id AND prv.boundary_id = sp.partition_number   
WHERE st.object_id = (SELECT object_id FROM sys.objects WHERE name = 'FactResellerSales')   
ORDER BY sp.partition_number  
OPTION ( FORCE ORDER )  
;  
```  
  
### <a name="h-using-externalpushdown"></a>8. EXTERNALPUSHDOWN를 사용 하 여  
 다음 예제에서는 외부 Hadoop 테이블에 MapReduce 작업을 WHERE 절 푸시 다운을 강제로 적용 합니다.  
  
```  
SELECT ID FROM External_Table_AS A   
WHERE ID < 1000000  
OPTION (FORCE EXTERNALPUSHDOWN);  
```  
  
 다음 예제에서는 외부 Hadoop 테이블에 MapReduce 작업을 WHERE 절 푸시 다운을 방지합니다. PDW WHERE 절이 적용 되는 위치에 모든 행이 반환 됩니다.  
  
```  
SELECT ID FROM External_Table_AS A   
WHERE ID < 10  
OPTION (DISABLE EXTERNALPUSHDOWN);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [힌트 &#40; Transact SQL &#41;](../../t-sql/queries/hints-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [MERGE &#40; Transact SQL &#41;](../../t-sql/statements/merge-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)  
  
  

