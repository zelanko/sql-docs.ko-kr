---
title: ISNULL (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISNULL
- ISNULL_TSQL
- IFNULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- replacing null values
- null values [SQL Server], ISNULL
- null values [SQL Server], replacement values
- ISNULL function
ms.assetid: 6f3e5802-864b-4e77-9862-657bb5430b68
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8d364548d3303de493343365bd16677ffdfd5641
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="isnull-transact-sql"></a>ISNULL(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  NULL을 지정된 대체 값으로 바꿉니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ISNULL ( check_expression , replacement_value )  
```  
  
## <a name="arguments"></a>인수  
 *check_expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) NULL에 대해 확인할 합니다. *check_expression* 형식일 수 있습니다.  
  
 *replacement_value*  
 경우 반환할 식 *check_expression* 은 NULL입니다. *replacement_value* 의 형식으로 암시적으로 변환 될 수 있는 형식 이어야 합니다 *check_expresssion*합니다.  
  
## <a name="return-types"></a>반환 형식  
 과 같은 유형을 반환 *check_expression*합니다. 리터럴 NULL으로 제공 되 면 *check_expression*의 데이터 형식을 반환 된 *replacement_value*합니다. 리터럴 NULL으로 제공 되 면 *check_expression* 및 no *replacement_value* 제공, 반환 된 **int**합니다.  
  
## <a name="remarks"></a>주의  
 값 *check_expression* 없는 경우 NULL이 고, 그렇지 않으면 *replacement_value* 의 형식으로 암시적으로 변환 된 후 반환 됩니다 *check_expression*유형은 서로 다른 경우. *replacement_value* 경우 문자열이 잘릴 수 *replacement_value* 보다 길면 *check_expression*합니다.  
  
> [!NOTE]  
>  사용 하 여 [COALESCE &#40; Transact SQL &#41; ](../../t-sql/language-elements/coalesce-transact-sql.md) 첫 번째 null이 아닌 값을 반환 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-isnull-with-avg"></a>1. AVG와 함께 ISNULL 사용  
 다음 예에서는 모든 제품의 평균 무게를 구하는 방법을 보여 줍니다. `50` 테이블의 `Weight` 열에 있는 모든 NULL 항목을 `Product` 값으로 대체합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT AVG(ISNULL(Weight, 50))  
FROM Production.Product;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 -------------------------- 
59.79  
  
 (1 row(s) affected)
 ```  
  
### <a name="b-using-isnull"></a>2. ISNULL 사용  
 다음 예에서는 `AdventureWorks2012`에서 모든 특별 행사에 대한 설명, 할인율, 최소 수량 및 최대 수량을 선택하는 방법을 보여 줍니다. 특정한 특별 행사에 대한 최대 수량이 NULL인 경우 결과 집합의 `MaxQty`는 `0.00`으로 표시됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Description, DiscountPct, MinQty, ISNULL(MaxQty, 0.00) AS 'Max Quantity'  
FROM Sales.SpecialOffer;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|  Description       |  DiscountPct    |   MinQty    |   최대 수량       |
|  ---------------   |  -------------  |   --------  |   ---------------    |
|  No Discount       |  0.00           |   0         |   0                  |
|  Volume Discount   |  0.02           |   11        |   14                 |
|  Volume Discount   |  0.05           |   15        |   4                  |
|  Volume Discount   |  0.10           |   25        |   0                  |
|  Volume Discount   |  0.15           |   41        |   0                  |
|  Volume Discount   |  0.20           |   61        |   0                  |
|  Mountain-100 Cl   |  0.35           |   0         |   0                  |
|  스포츠 Helmet Di   |  0.10           |   0         |   0                  |
|  Road-650 Overst   |  0.30           |   0         |   0                  |
|  Mountain Tire S   |  0.50           |   0         |   0                  |
|  스포츠 Helmet Di   |  0.15           |   0         |   0                  |
|  LL도로 프레임 S   |  0.35           |   0         |   0                  |
|  Touring 3000 Pr   |  0.15           |   0         |   0                  |
|  Touring-1000 Pr   |  0.20           |   0         |   0                  |
|  1/2 가격 Peda   |  0.50           |   0         |   0                  |
|  Mountain-500 Si   |  0.40           |   0         |   0                  |

 `(16 row(s) affected)`  
  
### <a name="c-testing-for-null-in-a-where-clause"></a>3. WHERE 절에서 NULL 테스트  
 NULL 값을 찾는 데 ISNULL을 사용하지 마세요. 대신 IS NULL을 사용합니다. 다음 예에서는 무게 열에 `NULL`이 있는 모든 제품을 찾는 방법을 보여 줍니다. `IS`와 `NULL` 사이에 공백이 있습니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name, Weight  
FROM Production.Product  
WHERE Weight IS NULL;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-isnull-with-avg"></a>4. AVG와 함께 ISNULL 사용  
 다음 예제에서는 예제 테이블의 모든 제품 중량의 평균을 찾습니다. `50` 테이블의 `Weight` 열에 있는 모든 NULL 항목을 `Product` 값으로 대체합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT AVG(ISNULL(Weight, 50))  
FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------------------------   
52.88   
```  
  
### <a name="e-using-isnull"></a>5. ISNULL 사용  
 다음 예제에서는 열에 NULL 값에 대 한 테스트를 ISNULL를 사용 하 여 `MinPaymentAmount` 값을 표시할 `0.00` 해당 행에 대 한 합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT ResellerName,   
       ISNULL(MinPaymentAmount,0) AS MinimumPayment  
FROM dbo.DimReseller  
ORDER BY ResellerName;  
  
```  
  
 다음은 결과 집합의 일부입니다.  
  
|  ResellerName                |  MinimumPayment    |
|  -------------------------   |  --------------    |
|  자전거 연결       |     0.0000         |
|  Bike Store                |     0.0000         |
|  주기 상점                |     0.0000         |
|  좋은 자전거 회사     |     0.0000         |
|  일반 자전거 매장         |   200.0000         |
|  허용 가능한 판매 및 서비스  |     0.0000         |
  
### <a name="f-using-is-null-to-test-for-null-in-a-where-clause"></a>6. WHERE 절에서 NULL에 대 한 테스트 하려면 IS NULL를 사용 하 여  
 다음 예제에서는 모든 제품을 찾습니다 `NULL` 에 `Weight` 열입니다. `IS`와 `NULL` 사이에 공백이 있습니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT EnglishProductName, Weight  
FROM dbo.DimProduct  
WHERE Weight IS NULL;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [NULL &#40; Transact SQL &#41;](../../t-sql/queries/is-null-transact-sql.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [COALESCE &#40; Transact SQL &#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  


