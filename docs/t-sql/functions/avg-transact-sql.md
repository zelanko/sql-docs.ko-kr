---
title: AVG (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AVG_TSQL
- AVG
dev_langs:
- TSQL
helpviewer_keywords:
- AVG function [Transact-SQL]
- GROUP BY clause, AVG function
- DISTINCT keyword
- values [SQL Server], average
- average values
ms.assetid: 4534b705-d946-441b-9b5d-5fbe561c9131
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: 1e7598f8ee20f88346dfcbba1757f1173b34fe5c
ms.contentlocale: ko-kr
ms.lasthandoff: 10/12/2017

---
# <a name="avg-transact-sql"></a>AVG(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

그룹에 속한 값의 평균을 반환합니다. Null 값은 무시됩니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
AVG ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )    
```  
  
## <a name="arguments"></a>인수  
ALL  
모든 값에 집계 함수를 적용합니다. 기본값은 ALL입니다.
  
DISTINCT  
값이 중복될 경우 횟수에 관계 없이 무시하고 고유한 값에 대해서만 AVG를 수행하도록 지정합니다.
  
*expression*  
이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 정확한 수치 또는 근사치 숫자 데이터 형식 범주에서를 제외 하 고는 **비트** 데이터 형식입니다. 집계 함수와 하위 쿼리는 허용되지 않습니다.
  
통해 **(** [ *partition_by_clause* ] *order_by_clause***)**  
*partition_by_clause* 함수가 적용 되는 파티션으로 FROM 절에서 생성 한 결과 집합을 나눕니다. 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. *order_by_clause* 작업이 수행 되는 논리적 순서를 결정 합니다. *order_by_clause* 가 필요 합니다. 자세한 내용은 참조 [OVER 절 &#40; Transact SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>반환 형식
반환 형식은 계산된 된 결과의 유형에 따라 결정 됩니다 *식*합니다.
  
|식 결과|반환 형식|  
|---|---|
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**ssNoversion**|**int**|  
|**bigint**|**bigint**|  
|**10 진수** 범주 (p, s)|**10 진수 (38, s)** 나눈 **decimal (10, 0)**|  
|**money** 및 **smallmoney** 범주|**money**|  
|**float** 및 **실제** 범주|**float**|  
  
## <a name="remarks"></a>주의  
데이터 형식이 *식* 이 별칭 데이터 형식, 반환 형식 이기도 별칭 데이터 형식입니다. 그러나 기본 데이터 유형의 경우 별칭 데이터 형식이 승격 되 면 from **tinyint** 를 **int**, 승격 된 데이터의 반환 값은 형식 및 별칭 데이터 형식입니다.
  
AVG ()는 값 집합의 합계를 Null이 아닌 값의 개수로 나눠 이러한 값에 대한 평균을 계산합니다. 합계가 반환 값의 데이터 형식에 대한 최대값을 초과할 경우 오류가 반환됩니다.
  
AVG는 OVER 및 ORDER BY 절 없이 사용되는 경우 결정적 함수이고, OVER 및 ORDER BY 절과 함께 지정되는 경우 비결정적 함수입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-sum-and-avg-functions-for-calculations"></a>1. SUM 함수와 AVG 함수를 사용한 계산  
다음 예에서는 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]의 부사장들이 이용한 평균 휴가 시간과 병가 시간의 합계를 계산합니다. 각 집계 함수는 검색된 모든 행에 대해 단일 요약 값을 계산합니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스를 사용합니다.
  
```sql
SELECT AVG(VacationHours)AS 'Average vacation hours',   
    SUM(SickLeaveHours) AS 'Total sick leave hours'  
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Vice President%';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Average vacation hours       Total sick leave hours
 ----------------------       ----------------------
25                           97
  
(1 row(s) affected)
```
  
### <a name="b-using-the-sum-and-avg-functions-with-a-group-by-clause"></a>2. GROUP BY 절과 함께 SUM 함수 및 AVG 함수 사용  
집계 함수를 `GROUP BY` 절과 함께 사용하면 전체 테이블이 아니라 각 그룹당 한 개의 값을 생성합니다. 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 각각의 판매 분야에 대한 요약 값을 계산합니다. 각 분야의 영업 사원이 받은 평균 보너스와 분야별 연간 판매량 합계를 요약하여 나열합니다.
  
```sql
SELECT TerritoryID, AVG(Bonus)as 'Average bonus', SUM(SalesYTD) as 'YTD sales'  
FROM Sales.SalesPerson  
GROUP BY TerritoryID;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
TerritoryID Average Bonus         YTD Sales  
----------- --------------------- ---------------------  
NULL        0.00                  1252127.9471  
1           4133.3333             4502152.2674  
2           4100.00               3763178.1787  
3           2500.00               3189418.3662  
4           2775.00               6709904.1666  
5           6700.00               2315185.611  
6           2750.00               4058260.1825  
7           985.00                3121616.3202  
8           75.00                 1827066.7118  
9           5650.00               1421810.9242  
10          5150.00               4116871.2277  
  
(11 row(s) affected)  
```  
  
### <a name="c-using-avg-with-distinct"></a>3. AVG 함수에 DISTINCT 사용  
다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 제품의 평균 정가를 반환합니다. DISTINCT를 지정하면 계산 시 고유 값만 사용됩니다.
  
```sql
SELECT AVG(DISTINCT ListPrice)  
FROM Production.Product;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
------------------------------
437.4042
  
(1 row(s) affected)
```
  
### <a name="d-using-avg-without-distinct"></a>4. DISTINCT 없이 AVG 사용  
DISTINCT를 지정하지 않고 `AVG` 함수를 사용하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `Product` 테이블에서 중복 값을 포함한 모든 제품의 평균 가격을 찾습니다.
  
```sql
SELECT AVG(ListPrice)  
FROM Production.Product;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
------------------------------
438.6662
  
(1 row(s) affected)
```
  
### <a name="e-using-the-over-clause"></a>5. OVER 절 사용  
다음 예에서는 AVG 함수에 OVER 절을 사용하여 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `Sales.SalesPerson` 테이블에서 각 지역에 대한 연간 매출의 이동 평균을 구합니다. 데이터는 `TerritoryID`를 기준으로 분할되고 `SalesYTD`를 기준으로 논리적으로 정렬됩니다. 즉, AVG 함수는 판매 연도를 기준으로 각 지역에 대해 계산됩니다. `TerritoryID` 1의 경우 2005년도에 대한 두 개의 행이 있습니다. 이 두 행은 해당 연도의 두 영업 사원과 매출을 나타냅니다. 이 두 행의 평균 매출이 계산된 다음 2006년도 매출을 나타내는 세 번째 행이 계산에 포함됩니다.
  
```sql
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                           ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY TerritoryID,SalesYear;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           559,697.56           559,697.56  
287              NULL        2006        519,905.93           539,801.75           1,079,603.50  
285              NULL        2007        172,524.45           417,375.98           1,252,127.95  
283              1           2005        1,573,012.94         1,462,795.04         2,925,590.07  
280              1           2005        1,352,577.13         1,462,795.04         2,925,590.07  
284              1           2006        1,576,562.20         1,500,717.42         4,502,152.27  
275              2           2005        3,763,178.18         3,763,178.18         3,763,178.18  
277              3           2005        3,189,418.37         3,189,418.37         3,189,418.37  
276              4           2005        4,251,368.55         3,354,952.08         6,709,904.17  
281              4           2005        2,458,535.62         3,354,952.08         6,709,904.17  
  
(10 row(s) affected)  
  
```  
  
이 예에서는 OVER 절에 PARTITION BY가 포함되어 있지 않습니다. 즉, 이 함수는 쿼리에서 반환된 모든 행에 적용됩니다. OVER 절에 지정된 ORDER BY 절은 AVG 함수가 적용되는 논리적 순서를 결정합니다. 이 쿼리는 WHERE 절에 지정된 모든 판매 지역의 연도별 매출 이동 평균을 반환합니다. SELECT 문에 지정된 ORDER BY 절은 쿼리의 행이 표시되는 순서를 결정합니다.
  
```sql
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY SalesYear;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           2,449,684.05         17,147,788.35  
275              2           2005        3,763,178.18         2,449,684.05         17,147,788.35  
276              4           2005        4,251,368.55         2,449,684.05         17,147,788.35  
277              3           2005        3,189,418.37         2,449,684.05         17,147,788.35  
280              1           2005        1,352,577.13         2,449,684.05         17,147,788.35  
281              4           2005        2,458,535.62         2,449,684.05         17,147,788.35  
283              1           2005        1,573,012.94         2,449,684.05         17,147,788.35  
284              1           2006        1,576,562.20         2,138,250.72         19,244,256.47  
287              NULL        2006        519,905.93           2,138,250.72         19,244,256.47  
285              NULL        2007        172,524.45           1,941,678.09         19,416,780.93  
(10 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목
[집계 함수 &#40; Transact SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[절 &#40; 조치 Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

