---
title: LEAD(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- LEAD_TSQL
- LEAD
dev_langs:
- TSQL
helpviewer_keywords:
- LEAD function
- analytic functions, LEAD
ms.assetid: 21f66bbf-d1ea-4f75-a3c4-20dc7fc1c69e
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9e046a46ff7ef709b0c6ae9b334e07fdbf557a84
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43062985"
---
# <a name="lead-transact-sql"></a>LEAD(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 자체 조인을 사용하지 않고 동일한 결과 집합에 있는 다음 행의 데이터에 액세스합니다. LEAD 함수를 사용하면 현재 행 뒤에 나오는, 지정한 실제 오프셋에 있는 행에 액세스할 수 있습니다. SELECT 문에서 이 분석 함수를 사용하여 현재 행의 값을 다음 행의 값과 비교할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
LEAD ( scalar_expression [ ,offset ] , [ default ] )   
    OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
## <a name="arguments"></a>인수  
 *scalar_expression*  
 지정한 오프셋에 따라 반환할 값입니다. 단일(스칼라) 값을 반환하는 모든 유형의 식입니다. *scalar_expression*은 분석 함수일 수 없습니다.  
  
 *offset*  
 현재 행 뒤에 있는 행의 수로, 그 수만큼 뒤에 있는 행에서 값을 가져옵니다. 이 인수를 지정하지 않으면 기본값은 1입니다. *offset*은 열, 하위 쿼리 또는 양의 정수로 계산되거나 암시적으로 **bigint**로 변환될 수 있는 기타 식일 수 있습니다. *offset*은 음수 또는 분석 함수일 수 없습니다.  
  
 *default*  
 *offset*의 *scalar_expression*이 NULL일 경우 반환할 값입니다. 기본값이 지정되어 있지 않으면 NULL이 반환됩니다. *default*는 열, 하위 쿼리 또는 기타 식일 수 있지만 분석 함수일 수는 없습니다. *default*는 *scalar_expression*과 호환되는 형식이어야 합니다.  
  
 OVER **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause*는 FROM 절이 생성한 결과 집합을 함수가 적용되는 파티션으로 나눕니다. 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. *order_by_clause*는 함수를 적용하기 전에 데이터의 순서를 결정합니다. *partition_by_clause*가 지정되면 각 파티션 내의 데이터 순서를 결정합니다. *order_by_clause*가 필요합니다. 자세한 내용은 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요.  
  
## <a name="return-types"></a>반환 형식  
 지정한 *scalar_expression*의 데이터 형식입니다. *scalar_expression*이 Null 값을 허용하거나 *default*가 NULL로 설정되어 있으면 NULL이 반환됩니다.  
  
 LEAD는 비결정적입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-compare-values-between-years"></a>1. 연도 간 값 비교  
 다음 쿼리에서는 LEAD 함수를 사용하여 특정 직원의 연도별 판매 할당량 간 차이를 반환합니다. 마지막 행의 경우 뒤에 나오는 값이 없으므로 기본값(0)이 반환됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, YEAR(QuotaDate) AS SalesYear, SalesQuota AS CurrentQuota,   
    LEAD(SalesQuota, 1,0) OVER (ORDER BY YEAR(QuotaDate)) AS NextQuota  
FROM Sales.SalesPersonQuotaHistory  
WHERE BusinessEntityID = 275 and YEAR(QuotaDate) IN ('2005','2006');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID SalesYear   CurrentQuota          NextQuota  
---------------- ----------- --------------------- ---------------------  
275              2005        367000.00             556000.00  
275              2005        556000.00             502000.00  
275              2006        502000.00             550000.00  
275              2006        550000.00             1429000.00  
275              2006        1429000.00            1324000.00  
275              2006        1324000.00            0.00  
```  
  
### <a name="b-compare-values-within-partitions"></a>2. 파티션 내의 값 비교  
 다음 예에서는 LEAD 함수를 사용하여 직원별 연간 누계 매출을 비교합니다. 결과 집합의 행을 판매 지역별로 분할하기 위해 PARTITION BY 절이 지정되었습니다. LEAD 함수는 각 파티션에 별도로 적용되고 각 파티션에 대해 계산이 다시 시작됩니다. OVER 절에 지정된 ORDER BY 절은 함수를 적용하기 전에 각 파티션의 행을 정렬합니다. SELECT 문의 ORDER BY 절은 전체 결과 집합의 행을 정렬합니다. 각 파티션에 있는 마지막 행의 경우 뒤에 나오는 값이 없으므로 기본값(0)이 반환됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT TerritoryName, BusinessEntityID, SalesYTD,   
       LEAD (SalesYTD, 1, 0) OVER (PARTITION BY TerritoryName ORDER BY SalesYTD DESC) AS NextRepSales  
FROM Sales.vSalesPerson  
WHERE TerritoryName IN (N'Northwest', N'Canada')   
ORDER BY TerritoryName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```   
TerritoryName            BusinessEntityID SalesYTD              NextRepSales  
-----------------------  ---------------- --------------------- ---------------------  
Canada                   282              2604540.7172          1453719.4653  
Canada                   278              1453719.4653          0.00  
Northwest                284              1576562.1966          1573012.9383  
Northwest                283              1573012.9383          1352577.1325  
Northwest                280              1352577.1325          0.00  
  
```  
  
### <a name="c-specifying-arbitrary-expressions"></a>3. 임의의 식 지정  
 다음 예에서는 LEAD 함수 구문에서 다양한 임의의 식을 지정하는 방법을 보여 줍니다.  
  
```sql  
CREATE TABLE T (a int, b int, c int);   
GO  
INSERT INTO T VALUES (1, 1, -3), (2, 2, 4), (3, 1, NULL), (4, 3, 1), (5, 2, NULL), (6, 1, 5);   
  
SELECT b, c,   
    LEAD(2*c, b*(SELECT MIN(b) FROM T), -c/2.0) OVER (ORDER BY a) AS i  
FROM T;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
b           c           i  
----------- ----------- -----------  
1           -3          8  
2           4           2  
1           NULL        2  
3           1           0  
2           NULL        NULL  
1           5           -2  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-compare-values-between-quarters"></a>D: 분기별 값 비교  
 다음 예에서는 LEAD 함수를 보여줍니다. 쿼리는 이후의 분기 동안 지정된 직원에 대한 판매 할당량 값의 차이를 가져옵니다. 마지막 행 다음에 사용 가능한 선행(lead) 값이 없기 때문에 기본값인 0이 사용됩니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       LEAD(SalesAmountQuota,1,0) OVER (ORDER BY CalendarYear, CalendarQuarter) AS NextQuota,  
   SalesAmountQuota - LEAD(Sale sAmountQuota,1,0) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Diff  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear IN (2001,2002)  
ORDER BY CalendarYear, CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year Quarter  SalesQuota  NextQuota  Diff  
---- -------  ----------  ---------  -------------  
2001 3        28000.0000   7000.0000   21000.0000 
2001 4         7000.0000  91000.0000  -84000.0000  
2001 1        91000.0000 140000.0000  -49000.0000  
2002 2       140000.0000   7000.0000    7000.0000  
2002 3         7000.0000 154000.0000   84000.0000  
2002 4       154000.0000      0.0000  154000.0000
```  
  
## <a name="see-also"></a>참고 항목  
 [LAG&#40;Transact-SQL&#41;](../../t-sql/functions/lag-transact-sql.md)  
  
  


