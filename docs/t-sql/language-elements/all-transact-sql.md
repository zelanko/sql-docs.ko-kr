---
title: ALL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALL_TSQL
- ALL
dev_langs:
- TSQL
helpviewer_keywords:
- single-column set of values [SQL Server]
- ALL (Transact-SQL)
ms.assetid: 4b0c002e-1ffd-4425-a980-11fdc1f24af7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d30c93cd56467c6137db647e52ea97f2cc7641ac
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52509580"
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
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 비교 연산자입니다.  
  
 *subquery*  
 한 열의 결과 집합을 반환하는 하위 쿼리입니다. 반환된 열의 데이터 형식은 *scalar_expression*의 데이터 형식과 같아야 합니다.  
  
 하위 쿼리는 제한된 SELECT 문이며 ORDER BY 절 및 INTO 키워드는 허용되지 않습니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="result-value"></a>결과 값  
 모든 쌍(_scalar_expression_**,**_x)_ 에 대해 지정된 비교값이 TRUE일 경우 TRUE를 반환하고, 그렇지 않으면 FALSE를 반환합니다. 이때 *x*는 단일 열 세트의 값입니다.  
  
## <a name="remarks"></a>Remarks  
 ALL의 경우 하위 쿼리에 의해 반환된 모든 값을 정확하게 비교하려면 *scalar_expression*이 필요합니다. 예를 들어 하위 쿼리에서 값 2와 3을 반환할 경우 *scalar_expression* <= ALL (하위 쿼리)은 2의 *scalar_expression*에 대해 TRUE로 계산됩니다. 하위 쿼리에서 값 2와 3을 반환할 경우에는 하위 쿼리 값(값 3)의 일부가 식의 조건을 만족하지 않으므로 *scalar_expression* = ALL(하위 쿼리)은 FALSE로 계산됩니다.  
  
 *scalar_expression*이 하위 쿼리에서 반환된 한 값에 대해서만 정확히 비교하도록 하는 문은 [SOME &#124; ANY &#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md)을 참조하세요.  
  
 이 항목에서는 하위 쿼리에 사용되는 경우의 ALL을 참조합니다. ALL은 [UNION](../../t-sql/language-elements/set-operators-union-transact-sql.md) 및 [SELECT](../../t-sql/queries/select-transact-sql.md)에도 사용될 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `SalesOrderID` 데이터베이스에서 지정한 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]의 모든 구성 요소를 지정된 기간 내에 제조할 수 있는지 여부를 결정하는 저장 프로시저를 만듭니다. 이 예제에서는 하위 쿼리를 사용하여 특정 `SalesOrderID`의 모든 구성 요소에 대한 `DaysToManufacture` 값 수의 목록을 만든 다음, 모든 `DaysToManufacture`가 지정한 일 수 범위에 있는지 확인합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [CASE&#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN&#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
  
