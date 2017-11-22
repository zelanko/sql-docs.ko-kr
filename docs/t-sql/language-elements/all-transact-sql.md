---
title: "모든 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- ALL_TSQL
- ALL
dev_langs: TSQL
helpviewer_keywords:
- single-column set of values [SQL Server]
- ALL (Transact-SQL)
ms.assetid: 4b0c002e-1ffd-4425-a980-11fdc1f24af7
caps.latest.revision: "40"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b6ea6be0d745ca5ce61a540e9a1e299671d8c7fd
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="all-transact-sql"></a>ALL(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  스칼라 값을 단일 열 집합 값과 비교합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
scalar_expression { = | <> | != | > | >= | !> | < | <= | !< } ALL ( subquery )  
```  
  
## <a name="arguments"></a>인수  
 *scalar_expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)합니다.  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 비교 연산자입니다.  
  
 *하위 쿼리*  
 한 열의 결과 집합을 반환하는 하위 쿼리입니다. 반환 된 열의 데이터 형식을의 데이터 형식으로 동일한 데이터 형식 이어야 합니다. *scalar_expression*합니다.  
  
 하위 쿼리는 제한된 SELECT 문이며 ORDER BY 절 및 INTO 키워드는 허용되지 않습니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="result-value"></a>결과 값  
 지정 된 비교값이 true 일 때 TRUE를 반환 합니다. 모든 쌍에 대 한 (*scalar_expression***,***x)*때 *x* 에서 값은 단일 열 집합입니다. 그렇지 않으면 FALSE를 반환합니다.  
  
## <a name="remarks"></a>주의  
 필요한 모든는 *scalar_expression* 하위 쿼리에서 반환 되는 모든 값을 정확 하 게 비교 합니다. 예를 들어 하위 쿼리에서 값 2와 3을 반환 하는 경우, *scalar_expression* < = ALL (하위 쿼리)에 대해 TRUE로 평가 된 *scalar_expression* 2입니다. 하위 쿼리에서 값 2와 3을 반환 하는 경우 *scalar_expression* = ALL (하위 쿼리)은 일부 값 (값 3)는 하위 쿼리 식의 조건을 만족 하지 않으므로 FALSE로 계산 됩니다.  
  
 필요로 하는 문에 *scalar_expression* 하위 쿼리에서 반환 되는 하나의 값을 정확 하 게 비교를 참조 하세요. [일부 &#124; 모든 &#40; Transact SQL &#41; ](../../t-sql/language-elements/some-any-transact-sql.md).  
  
 이 항목에서는 하위 쿼리에 사용되는 경우의 ALL을 참조합니다. 함께 사용할 수도 모든 [UNION](../../t-sql/language-elements/set-operators-union-transact-sql.md) 및 [선택](../../t-sql/queries/select-transact-sql.md)합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 결정 하는 저장된 프로시저를 만듭니다. 있는지 여부를 지정 된 모든 구성 요소 `SalesOrderID` 에 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스는 지정 된 일 수 내에 제조할 수입니다. 수가 목록을 만드는 데 사용 하 여 하위 쿼리는 예제 `DaysToManufacture` 의 특정 구성 요소에 대 한 값 `SalesOrderID`, 있는지를 확인 하 고 모든는 `DaysToManufacture` 일 수가 지정 합니다.  
  
```  
-- Uses AdventureWorks  
  
CREATE PROCEDURE DaysToBuild @OrderID int, @NumberOfDays int  
AS  
IF   
@NumberOfDays >= ALL  
   (  
    SELECT DaysToManufacture  
    FROM Sales.SalesOrderDetail  
    JOIN Production.Product   
    ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID   
    WHERE SalesOrderID = @OrderID  
   )  
PRINT 'All items for this order can be manufactured in specified number of days or less.'  
ELSE   
PRINT 'Some items for this order cannot be manufactured in specified number of days or less.' ;  
  
```  
  
 프로시저를 테스트하려면 `SalesOrderID 49080`일이 필요한 한 개의 구성 요소 및 0일이 필요한 두 개의 구성 요소가 포함되어 있는 `2`을 사용하여 프로시저를 실행합니다. 아래 첫 번째 문은 조건을 만족합니다. 두 번째 쿼리는 조건을 만족하지 않습니다.  
  
```  
EXECUTE DaysToBuild 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in specified number of days or less.`  
  
```  
EXECUTE DaysToBuild 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Some items for this order cannot be manufactured in specified number of days or less.`  
  
## <a name="see-also"></a>관련 항목:  
 [대/소문자 &#40; Transact SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [마찬가지로 &#40; Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [&#40; Transact SQL &#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
  
