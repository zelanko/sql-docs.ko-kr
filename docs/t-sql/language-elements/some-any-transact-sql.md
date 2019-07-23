---
title: SOME | ANY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SOME
- SOME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- scalar values
- comparing scalar with single-column set
- ANY operator
- SOME | ANY keyword
- single-column set of values [SQL Server]
ms.assetid: 1f717ad6-f67b-4980-9397-577ecb0e5789
author: rothja
ms.author: jroth
ms.openlocfilehash: a5b722f37fb6a5e30a50307a5d7828868ecd1fba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072257"
---
# <a name="some--any-transact-sql"></a>SOME | ANY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  스칼라 값을 단일 열 집합 값과 비교합니다. SOME과 ANY는 동일합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
scalar_expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
     { SOME | ANY } ( subquery )   
```  
  
## <a name="arguments"></a>인수  
 *scalar_expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 유효한 비교 연산자입니다.  
  
 SOME | ANY  
 비교해야 함을 지정합니다.  
  
 *subquery*  
 하나의 열로 구성된 결과 집합을 갖는 하위 쿼리입니다. 반환되는 열의 데이터 형식은 *scalar_expression*과 같은 데이터 형식이어야 합니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="result-value"></a>결과 값  
 모든 쌍(_scalar_expression_ **,** _x_)에 대해 지정된 비교 값이 TRUE일 경우 SOME이나 ANY는 **TRUE**를 반환하고 그렇지 않으면 **FALSE**를 반환합니다. 여기서 *x*는 단일 열 세트의 값입니다.  
  
## <a name="remarks"></a>Remarks  
 SOME의 경우 하위 쿼리에서 반환한 하나 이상의 값을 정확하게 비교하려면 *scalar_expression*이 필요합니다. 하위 쿼리에서 반환한 모든 값을 정확하게 비교하기 위해 *scalar_expression*이 필요한 문에 대한 자세한 내용은 [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)을 참조하세요. 예를 들어 하위 쿼리에서 값 2와 3을 반환할 경우 *scalar_expression* = SOME(하위 쿼리)은 2의 *scalar_express*에 대해 TRUE로 계산됩니다. 하위 쿼리에서 값 2와 3을 반환할 경우에는 하위 쿼리 값(값 3)의 일부가 식의 조건을 만족하지 않으므로 *scalar_expression* = ALL(하위 쿼리)은 FALSE로 계산됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-running-a-simple-example"></a>1\. 간단한 예 실행  
 다음 문에서는 간단한 테이블을 만들고 `1` 열에 값 `2`, `3`, `4` 및 `ID`를 추가합니다.  
  
```  
CREATE TABLE T1  
(ID int) ;  
GO  
INSERT T1 VALUES (1) ;  
INSERT T1 VALUES (2) ;  
INSERT T1 VALUES (3) ;  
INSERT T1 VALUES (4) ;  
```  
  
 다음 쿼리는 `TRUE`이 테이블의 일부 값보다 작기 때문에 `3`를 반환합니다.  
  
```  
IF 3 < SOME (SELECT ID FROM T1)  
PRINT 'TRUE'   
ELSE  
PRINT 'FALSE' ;  
```  
  
 다음 쿼리는 `FALSE`이 테이블의 모든 값보다 작기 때문에 `3`를 반환합니다.  
  
```  
IF 3 < ALL (SELECT ID FROM T1)  
PRINT 'TRUE'   
ELSE  
PRINT 'FALSE' ;  
```  
  
### <a name="b-running-a-practical-example"></a>2\. 실제 예 실행  
 다음 예에서는 `SalesOrderID` 데이터베이스에서 지정한 `AdventureWorks2012`의 모든 구성 요소를 지정된 기간 내에 제조할 수 있는지 여부를 결정하는 저장 프로시저를 만듭니다. 이 예에서는 하위 쿼리를 사용하여 특정 `DaysToManufacture`의 모든 구성 요소에 대해 `SalesOrderID` 값의 숫자 목록을 만든 다음 하위 쿼리에서 반환한 값 중 지정된 일 수를 초과하는 값이 있는지 테스트합니다. 반환된 `DaysToManufacture`의 모든 값이 제공된 숫자보다 작을 경우 조건은 TRUE이며 첫 번째 메시지가 출력됩니다.  
  
```  
-- Uses AdventureWorks  
  
CREATE PROCEDURE ManyDaysToComplete @OrderID int, @NumberOfDays int  
AS  
IF   
@NumberOfDays < SOME  
   (  
    SELECT DaysToManufacture  
    FROM Sales.SalesOrderDetail  
    JOIN Production.Product   
    ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID   
    WHERE SalesOrderID = @OrderID  
   )  
PRINT 'At least one item for this order can't be manufactured in specified number of days.'  
ELSE   
PRINT 'All items for this order can be manufactured in the specified number of days or less.' ;  
  
```  
  
 프로시저를 테스트하려면 `2`일이 필요한 한 개의 구성 요소 및 0일이 필요한 두 개의 구성 요소가 포함되어 있는 `SalesOrderID``49080`을 사용하여 프로시저를 실행합니다. 첫 번째 문은 조건을 만족합니다. 두 번째 쿼리는 만족하지 않습니다.  
  
```  
EXECUTE ManyDaysToComplete 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in the specified number of days or less.`  
  
```  
EXECUTE ManyDaysToComplete 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `At least one item for this order can't be manufactured in specified number of days.`  
  
## <a name="see-also"></a>참고 항목  
 [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [CASE&#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN&#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
