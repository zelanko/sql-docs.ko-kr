---
description: STDEV(Transact-SQL)
title: STDEV(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDEV_TSQL
- STDEV
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], statistical standard deviation
- STDEV function [Transact-SQL]
- statistical standard deviation
ms.assetid: ff41b4fc-4f71-4f18-bf78-96614ea908cc
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 83249ba70c3110ec3b79874f8c8bbf2379a9f159
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461264"
---
# <a name="stdev-transact-sql"></a>STDEV(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  지정한 식의 모든 값에 대한 통계적 표준 편차를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql    
-- Aggregate Function Syntax   
STDEV ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax   
STDEV ([ ALL ] expression) OVER ( [ partition_by_clause ] order_by_clause)  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 **ALL**  
 모든 값에 함수를 적용합니다. 기본값은 ALL입니다.  
  
 DISTINCT  
 각 고유 값을 고려하도록 지정합니다.  
  
 *expression*  
 숫자 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 집계 함수와 하위 쿼리는 허용되지 않습니다. *expression* 은 **bit** 데이터 형식을 제외한 정확한 수치 또는 근사치 데이터 형식 범주의 식입니다.  
  
 OVER **(** [ *partition_by_clause* ] _order\_by\_clause_ **)**  
 _partition\_by\_clause_ 는 FROM 절이 생성한 결과 집합을 함수가 적용되는 파티션으로 나눕니다. 지정하지 않을 경우 쿼리 결과 집합의 모든 행이 단일 그룹으로 취급됩니다. _order\_by\_clause_ 는 작업이 수행되는 논리적 순서를 결정합니다. _order\_by\_clause_ 는 필수입니다. 자세한 내용은 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)을 참조하세요.  
  
## <a name="return-types"></a>반환 형식  
 **float**  
  
## <a name="remarks"></a>설명  
 STDEV가 SELECT 문의 모든 항목에서 사용되는 경우 결과 집합의 각 값이 계산에 포함됩니다. STDEV에는 숫자 열만 사용할 수 있습니다. Null 값은 무시됩니다.  
  
 STDEV는 OVER 및 ORDER BY 절 없이 사용되는 경우 결정적 함수이고, OVER 및 ORDER BY 절과 함께 지정되는 경우 비결정적 함수입니다. 자세한 내용은 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)을 참조하세요.  
  
## <a name="examples"></a>예제  
  
### <a name="a-using-stdev"></a>1. STDEV 사용  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `SalesPerson` 테이블에 있는 모든 보너스 값에 대한 표준 편차를 반환하는 방법을 보여 줍니다.  
  
```sql  
SELECT STDEV(Bonus)  
FROM Sales.SalesPerson;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-stdev"></a>2. STDEV 사용  
 다음 예에서는 `dbo.FactSalesQuota` 테이블의 판매 할당량 값에 대한 표준 편차를 반환합니다. 첫 번째 열은 모든 고유 값의 표준 편차를 포함하고 두 번째 열은 중복 값을 포함한 모든 값의 표준 편차를 포함합니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT STDEV(DISTINCT SalesAmountQuota)AS Distinct_Values, STDEV(SalesAmountQuota) AS All_Values  
FROM dbo.FactSalesQuota;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Distinct_Values   All_Values
----------------  ----------------
398974.27         398450.57
 ```  
  
### <a name="c-using-stdev-with-over"></a>C. OVER와 함께 STDEV 사용  
 다음 예에서는 한 해의 각 분기에 대한 판매 할당량 값의 표준 편차를 반환합니다. OVER 절에서 ORDER BY는 STDEV와 SELECT 문의 ORDER BY를 결과 집합으로 정렬합니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       STDEV(SalesAmountQuota) OVER (ORDER BY CalendarYear, CalendarQuarter) AS StdDeviation  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear = 2002  
ORDER BY CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year  Quarter  SalesQuota              StdDeviation
----  -------  ----------------------  -------------------
2002  1         91000.0000             null
2002  2        140000.0000             34648.23
2002  3         70000.0000             35921.21
2002  4        154000.0000             39752.36
 ```  
  
## <a name="see-also"></a>참고 항목  
 [집계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [OVER 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

