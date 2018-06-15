---
title: GROUPING(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GROUPING
- GROUPING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], GROUPING function
- grouping columns
- ROLLUP operator
- GROUP BY clause, GROUPING function
- GROUPING function
- CUBE operator
ms.assetid: 4efa3868-1fc4-4626-8fb1-e863cc03e422
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 513a61c37f0a885bd4f594af062ce6137b84f882
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33052874"
---
# <a name="grouping-transact-sql"></a>GROUPING(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  GROUP BY 목록에 지정된 열 식이 집계되었는지 여부를 나타냅니다. GROUPING은 집계된 경우 결과 집합에 1을 반환하고 집계되지 않은 경우 0을 반환합니다. GROUP BY 절이 지정된 경우 GROUPING은 SELECT \<select> 목록, HAVING 및 ORDER BY 절에만 사용할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
GROUPING ( <column_expression> )  
```  
  
## <a name="arguments"></a>인수  
 \<column_expression>  
 [GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md) 절에 열을 포함하는 열 또는 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 **tinyint**  
  
## <a name="remarks"></a>Remarks  
 GROUPING은 ROLLUP, CUBE 또는 GROUPING SETS에서 반환된 Null 값과 표준 Null 값을 구분하기 위해 사용됩니다. ROLLUP, CUBE 또는 GROUPING SETS 작업의 결과로 반환되는 Null은 특별한 Null입니다. 이것은 결과 집합에서 열 자리 표시자로 사용되며 "모두"를 의미합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `SalesQuota`를 그룹화하고 `SaleYTD` 금액을 집계합니다. `GROUPING` 함수는 `SalesQuota` 열에 적용됩니다.  
  
```  
SELECT SalesQuota, SUM(SalesYTD) 'TotalSalesYTD', GROUPING(SalesQuota) AS 'Grouping'  
FROM Sales.SalesPerson  
GROUP BY SalesQuota WITH ROLLUP;  
GO  
```  
  
 결과 집합에는 `SalesQuota` 아래 2개의 Null 값이 있습니다. 첫 번째 `NULL`은 테이블에 있는 이 열의 Null 값 그룹을 나타냅니다. 두 번째 `NULL`은 ROLLUP 작업으로 추가된 요약 행에 있습니다. 요약 행은 모든 `TotalSalesYTD` 그룹의 `SalesQuota` 양을 보여 주고 `1` 열에서 `Grouping`로 표시됩니다.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 SalesQuota     TotalSalesYTD       Grouping  
------------   -----------------   --------  
NULL           1533087.5999          0  
250000.00      33461260.59           0  
300000.00      9299677.9445          0  
NULL           44294026.1344         1  

(4 row(s) affected)
```  
  
## <a name="see-also"></a>참고 항목  
 [GROUPING_ID&#40;Transact-SQL&#41;](../../t-sql/functions/grouping-id-transact-sql.md)   
 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  
