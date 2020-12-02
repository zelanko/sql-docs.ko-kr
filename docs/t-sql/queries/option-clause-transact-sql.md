---
description: OPTION 절(Transact-SQL)
title: OPTION 절(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPTION clause
- OPTION_TSQL
- OPTION
- OPTION_clause_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- clauses [SQL Server], OPTION
- OPTION clause
ms.assetid: f47e2f3f-9302-4711-9d66-16b1a2a7ffe3
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 468ffd5a95bcb0bf6fa2c5d4cb9a1cb343102acd
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91227179"
---
# <a name="option-clause-transact-sql"></a>OPTION 절(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  지정한 쿼리 힌트가 전체 쿼리에서 사용되도록 지정합니다. 여러 개의 쿼리 힌트가 허용되지만 각 쿼리 힌트는 한 번만 지정할 수 있습니다. 문에서 하나의 OPTION 절만 지정할 수 있습니다.  
  
 SELECT, DELETE, UPDATE 및 MERGE 문에서 이 절을 지정할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
[ OPTION ( <query_hint> [ ,...n ] ) ]   
```  
  
```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
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
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *query_hint*  
 데이터베이스 엔진에서 최적화 프로그램 힌트를 사용하여 문을 처리하는 방법을 사용자 지정한다는 것을 나타내는 키워드입니다. 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
  
## <a name="examples"></a>예제  
  
### <a name="a-using-an-option-clause-with-a-group-by-clause"></a>A. GROUP BY 절과 함께 OPTION 절 사용  
 다음 예에서는 `OPTION` 절과 함께 `GROUP BY` 절을 사용하는 방법을 보여 줍니다.  
  
```sql
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
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-select-statement-with-a-label-in-the-option-clause"></a>B. OPTION 절에서 레이블을 사용하는 SELECT 문  
 다음 예제에서는 OPTION 절에서 레이블을 사용하는 간단한 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] SELECT 문을 보여 줍니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT * FROM FactResellerSales  
  OPTION ( LABEL = 'q17' );  
```  
  
### <a name="c-select-statement-with-a-query-hint-in-the-option-clause"></a>C. OPTION 절에서 쿼리 힌트를 사용하는 SELECT 문  
 다음 예제에서는 OPTION 절에서 HASH JOIN 쿼리 힌트를 사용하는 SELECT 문을 보여 줍니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT COUNT (*) FROM dbo.DimCustomer a  
INNER JOIN dbo.FactInternetSales b   
ON (a.CustomerKey = b.CustomerKey)  
OPTION (HASH JOIN);  
```  
  
### <a name="d-select-statement-with-a-label-and-multiple-query-hints-in-the-option-clause"></a>D. OPTION 절에서 레이블 및 여러 쿼리 힌트를 사용하는 SELECT 문  
 다음 예제는 레이블 및 여러 쿼리 힌트를 포함하는 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] SELECT 문입니다. 쿼리가 컴퓨팅 노드에서 실행될 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 결정하는 가장 적합한 전략에 따라 해시 조인 또는 병합 조인을 적용합니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT COUNT (*) FROM dbo.DimCustomer a  
INNER JOIN dbo.FactInternetSales b   
ON (a.CustomerKey = b.CustomerKey)  
OPTION ( Label = 'CustJoin', HASH JOIN, MERGE JOIN);  
```  
  
### <a name="e-using-a-query-hint-when-querying-a-view"></a>E. 뷰를 쿼리할 때 쿼리 힌트 사용  
 다음 예제에서는 CustomerView라는 뷰를 만든 다음, 뷰 및 테이블을 참조하는 쿼리에서 HASH JOIN 쿼리 힌트를 사용합니다.  
  
```sql
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
  
### <a name="f-query-with-a-subselect-and-a-query-hint"></a>F. 하위 select 및 쿼리 힌트가 있는 쿼리  
 다음 예제에서는 하위 select 및 쿼리 힌트 모두를 포함하는 쿼리를 보여 줍니다. 쿼리 힌트는 전역적으로 적용됩니다. 쿼리 힌트는 하위 select 문에 추가되도록 허용되지 않습니다.  
  
```sql
-- Uses AdventureWorks  
  
CREATE VIEW CustomerView AS  
SELECT CustomerKey, FirstName, LastName FROM ssawPDW..DimCustomer;  
  
SELECT * FROM (  
SELECT COUNT (*) AS a FROM dbo.CustomerView a  
INNER JOIN dbo.FactInternetSales b  
ON ( a.CustomerKey = b.CustomerKey )) AS t  
OPTION (HASH JOIN);  
```  
  
### <a name="g-force-the-join-order-to-match-the-order-in-the-query"></a>G. 쿼리의 순서와 일치하도록 조인 순서 강제 적용  
 다음 예제에서는 FORCE ORDER 힌트를 사용하여 쿼리에서 지정된 조인 순서를 사용하도록 쿼리 계획을 강제로 적용합니다. 모든 쿼리가 아닌 일부 쿼리에서 성능을 향상시킵니다.  
  
```sql
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
  
### <a name="h-using-externalpushdown"></a>H. EXTERNALPUSHDOWN 사용  
 다음 예제에서는 외부 Hadoop 테이블의 MapReduce 작업에 WHERE 절의 푸시다운을 강제로 적용합니다.  
  
```sql
SELECT ID FROM External_Table_AS A   
WHERE ID < 1000000  
OPTION (FORCE EXTERNALPUSHDOWN);  
```  
  
 다음 예제에서는 외부 Hadoop 테이블의 MapReduce 작업에 WHERE 절의 푸시다운을 강제로 방지합니다. WHERE 절이 적용되는 PDW에 모든 행이 반환됩니다.  
  
```sql
SELECT ID FROM External_Table_AS A   
WHERE ID < 10  
OPTION (DISABLE EXTERNALPUSHDOWN);  
```  
  
## <a name="see-also"></a>참고 항목  
 [힌트&#40;Transact SQL&#41;](../../t-sql/queries/hints-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [MERGE&#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)   
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)  
  
  

