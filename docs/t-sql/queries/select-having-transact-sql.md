---
title: HAVING (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9bff75a84689090f6e416db052a2561e57fa98a6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="select---having-transact-sql"></a>선택-것 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  그룹 또는 집계에 대한 검색 조건을 지정합니다. HAVING은 SELECT 문하고만 사용될 수 있으며 일반적으로 GROUP BY 절에 사용됩니다. GROUP BY가 사용되지 않으면 HAVING은 WHERE 절처럼 작동합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
[ HAVING <search condition> ]  
```  
  
## <a name="arguments"></a>인수  
\<c h _ c >에 맞게는 그룹이 나 집계에 대 한 검색 조건을 지정 합니다.  
  
 **텍스트**, **이미지**, 및 **ntext** 데이터 형식은 HAVING 절에 사용할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 단순한 `HAVING` 절을 사용하여 `SalesOrderID` 테이블에서 `SalesOrderDetail`를 초과하는 각 `$100000.00`의 총계를 검색합니다.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail  
GROUP BY SalesOrderID  
HAVING SUM(LineTotal) > 100000.00  
ORDER BY SalesOrderID ;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예제에서는 `HAVING` 각각에 대 한 합계를 검색 하는 절 `SalesAmount` 에서 `FactInternetSales` 하면 테이블의 `OrderDateKey` 2004 이상 연도 있습니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING SUM(SalesAmount) > 80000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [GROUP BY &#40; Transact SQL &#41;](../../t-sql/queries/select-group-by-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


