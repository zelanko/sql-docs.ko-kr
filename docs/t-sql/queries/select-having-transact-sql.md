---
title: HAVING(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HAVING
- HAVING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restricting conditions for result set
- search conditions [SQL Server], HAVING clause
- HAVING clause
- HAVING clause, about HAVING clause
ms.assetid: 55650709-001e-42f4-902f-ead09a3c34af
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2e17b738d116fa1a82733484fb9aa32a99ec1fa
ms.sourcegitcommit: 670082cb47f7d3d82e987b549b6f8e3a8968b5db
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57334440"
---
# <a name="select---having-transact-sql"></a>SELECT - HAVING(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  그룹 또는 집계에 대한 검색 조건을 지정합니다. HAVING은 SELECT 문하고만 사용될 수 있으며 HAVING은 일반적으로 GROUP BY 절에 사용됩니다. GROUP BY를 사용하지 않을 경우 암시적 단일 집계 그룹이 있습니다.   
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
[ HAVING <search condition> ]  
```  
  
## <a name="arguments"></a>인수  
\<search_condition> 그룹 및/또는 집계가 부합해야 하는 하나 이상의 조건자를 지정합니다. 검색 조건 및 조건자에 대한 자세한 내용은 [검색 조건&#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)을 참조하세요.  
  
 **text**, **image** 및 **ntext** 데이터 형식은 HAVING 절에 사용할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 단순한 `HAVING` 절을 사용하여 `SalesOrderID` 테이블에서 `SalesOrderDetail`를 초과하는 각 `$100000.00`의 총계를 검색합니다.  
  
```sql
USE AdventureWorks2012 ;  
GO  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail  
GROUP BY SalesOrderID  
HAVING SUM(LineTotal) > 100000.00  
ORDER BY SalesOrderID ;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예제에서는 `HAVING` 절을 사용하여 `OrderDateKey`가 2004 이상일 때 `FactInternetSales` 테이블에서 각 `SalesAmount`의 합계를 검색합니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING SUM(SalesAmount) > 80000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>참고 항목  
 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

