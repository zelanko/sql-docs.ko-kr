---
title: VARP (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- VARP_TSQL
- VARP
dev_langs:
- TSQL
helpviewer_keywords:
- statistical variances
- expressions [SQL Server], statistical variance
- VARP function [Transact-SQL]
ms.assetid: ce5d2e32-01da-4e18-b8ed-a08b61d84456
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d27f781da75ee96b634a2ecd1239aa063807225e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="varp-transact-sql"></a>VARP(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정한 식에 있는 모든 값의 모집단에 대한 통계적 분산을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
VARP ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )  nh  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregate Function Syntax   
VARP ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax  
VARP (expression) OVER ( [ partition_by_clause ] order_by_clause)  
```  
  
## <a name="arguments"></a>인수  
 **ALL**  
 모든 값에 함수를 적용합니다. 기본값은 ALL입니다.  
  
 DISTINCT  
 각 고유 값을 고려하도록 지정합니다.  
  
 *expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 정확한 수치 또는 근사치 숫자 데이터 형식 범주에서를 제외 하 고는 **비트** 데이터 형식입니다. 집계 함수와 하위 쿼리는 허용되지 않습니다.  
  
 통해 **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause* 함수가 적용 되는 파티션으로 FROM 절에서 생성 한 결과 집합을 나눕니다. 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. *order_by_clause* 작업이 수행 되는 논리적 순서를 결정 합니다. *order_by_clause* 가 필요 합니다. 자세한 내용은 참조 [OVER 절 &#40; Transact SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>반환 형식  
 **float**  
  
## <a name="remarks"></a>주의  
 VARP가 SELECT 문의 모든 항목에서 사용되는 경우 결과 집합의 각 값은 계산에 포함됩니다. VARP와 함께 사용할 수 있는 것은 숫자 열뿐입니다. Null 값은 무시됩니다.  
  
 VARP는 OVER 및 ORDER BY 절 없이 사용되는 경우 결정적 함수이고, OVER 및 ORDER BY 절과 함께 지정되는 경우 비결정적 함수입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-varp"></a>A: VARP를 사용 하 여  
 다음은 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `SalesPerson` 테이블에 있는 모든 보너스 값의 모집단에 대한 분산을 반환하는 예입니다.  
  
```  
SELECT VARP(Bonus)  
FROM Sales.SalesPerson;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-varp"></a>B: VARP을 사용 하 여  
 다음 예제에서는 반환 된 `VARP`테이블의 판매 할당량 값의 `dbo.FactSalesQuota`합니다. 첫 번째 열의 모든 고유 값의 분산을 포함 하 고 모든 중복 값을 포함 한 모든 값의 분산을 포함 하는 두 번째 열입니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT VARP(DISTINCT SalesAmountQuota)AS Distinct_Values, VARP(SalesAmountQuota) AS All_Values  
FROM dbo.FactSalesQuota;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Distinct_Values   All_Values
----------------  ----------------
158146830494.18   157788848582.94
```  
  
### <a name="c-using-varp-with-over"></a>3. VARP OVER 사용  
 다음 예제에서는 반환 된 `VARP` 역 년의 분기별 판매 할당량 값의 합니다. OVER 절에서 ORDER BY 정렬 통계적 분산을 ORDER BY SELECT 문의 결과 집합을 정렬 방식을 살펴봅니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       VARP(SalesAmountQuota) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Variance  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear = 2002  
ORDER BY CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year  Quarter  SalesQuota              Variance
----  -------  ----------------------  -------------------
2002  1         91000.0000             0.00
2002  2        140000.0000             600250000.00
2002  3         70000.0000             860222222.22
2002  4        154000.0000             1185187500.00
```  
  
## <a name="see-also"></a>관련 항목:  
 [집계 함수 &#40; Transact SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [절 &#40; 조치 Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  


