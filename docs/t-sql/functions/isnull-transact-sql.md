---
description: ISNULL(Transact-SQL)
title: ISNULL(Transact-SQL)
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5275acd28786f984a7a3855108019c29783ee54d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478634"
---
# <a name="isnull-transact-sql"></a>ISNULL(Transact-SQL) 

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

NULL을 지정된 대체 값으로 바꿉니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
ISNULL ( check_expression , replacement_value )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *check_expression*  
 NULL 여부를 검사할 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *check_expression* 은 임의 형식이 될 수 있습니다.  
  
 *replacement_value*  
 *check_expression* 이 NULL인 경우 반환할 식입니다. *replacement_value* 는 암시적으로 *check_expression* 형식으로 변환되는 형식이어야 합니다.  
  
## <a name="return-types"></a>반환 형식  
 *check_expression* 식과 같은 유형을 반환합니다. 리터럴 NULL이 *check_expression* 으로 제공된 경우 *replacement_value* 데이터 형식을 반환합니다. 리터럴 NULL이 *check_expression* 으로 제공되고 *replacement_value* 가 제공되지 않은 경우 **int** 를 반환합니다.  
  
## <a name="remarks"></a>설명  
 NULL이 아닐 경우 *check_expression* 값이 반환되고, 그렇지 않고 형식이 다른 경우는 *check_expression* 형식으로 암시적으로 변환된 후 *replacement_value* 가 반환됩니다. *replacement_value* 는 *replacement_value* 가 *check_expression* 보다 긴 경우 잘릴 수 있습니다.  
  
> [!NOTE]  
>  첫 번째 Null이 아닌 값을 반환하려면 [COALESCE&#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)를 사용합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-isnull-with-avg"></a>A. AVG와 함께 ISNULL 사용  
 다음 예에서는 모든 제품의 평균 무게를 구하는 방법을 보여 줍니다. `50` 테이블의 `Weight` 열에 있는 모든 NULL 항목을 `Product` 값으로 대체합니다.  
  
```sql  
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
  
### <a name="b-using-isnull"></a>B. ISNULL 사용  
 다음 예에서는 `AdventureWorks2012`에서 모든 특별 행사에 대한 설명, 할인율, 최소 수량 및 최대 수량을 선택하는 방법을 보여 줍니다. 특정한 특별 행사에 대한 최대 수량이 NULL인 경우 결과 집합의 `MaxQty`는 `0.00`으로 표시됩니다.  
  
```sql  
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
|  Sport Helmet Di   |  0.10           |   0         |   0                  |
|  Road-650 Overst   |  0.30           |   0         |   0                  |
|  Mountain Tire S   |  0.50           |   0         |   0                  |
|  Sport Helmet Di   |  0.15           |   0         |   0                  |
|  LL Road Frame S   |  0.35           |   0         |   0                  |
|  Touring-3000 Pr   |  0.15           |   0         |   0                  |
|  Touring-1000 Pr   |  0.20           |   0         |   0                  |
|  Half-Price Peda   |  0.50           |   0         |   0                  |
|  Mountain-500 Si   |  0.40           |   0         |   0                  |

 `(16 row(s) affected)`  
  
### <a name="c-testing-for-null-in-a-where-clause"></a>C. WHERE 절에서 NULL 테스트  
 NULL 값을 찾는 데 ISNULL을 사용하지 마세요. 대신 IS NULL을 사용합니다. 다음 예에서는 무게 열에 `NULL`이 있는 모든 제품을 찾는 방법을 보여 줍니다. `IS`와 `NULL` 사이에 공백이 있습니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name, Weight  
FROM Production.Product  
WHERE Weight IS NULL;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-isnull-with-avg"></a>D. AVG와 함께 ISNULL 사용  
 다음 예에서는 샘플 표에 있는 모든 제품의 평균 무게를 구하는 방법을 보여 줍니다. `50` 테이블의 `Weight` 열에 있는 모든 NULL 항목을 `Product` 값으로 대체합니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT AVG(ISNULL(Weight, 50))  
FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------------------------   
52.88   
```  
  
### <a name="e-using-isnull"></a>E. ISNULL 사용  
 다음 예에서는 ISNULL을 사용하여 `MinPaymentAmount` 열에 있는 NULL 값을 테스트하고 해당 열의 `0.00` 값을 표시합니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT ResellerName,   
       ISNULL(MinPaymentAmount,0) AS MinimumPayment  
FROM dbo.DimReseller  
ORDER BY ResellerName;  
  
```  
  
 다음은 결과 집합의 일부입니다.  
  
|  ResellerName                |  MinimumPayment    |
|  -------------------------   |  --------------    |
|  자전거 연합       |     0.0000         |
|  자전거 매장                |     0.0000         |
|  사이클 상점                |     0.0000         |
|  대형 자전거 회사     |     0.0000         |
|  일반 자전거 상점         |   200.0000         |
|  허용 가능 매출 및 서비스  |     0.0000         |
  
### <a name="f-using-is-null-to-test-for-null-in-a-where-clause"></a>F. WHERE 절에서 NULL 테스트를 위해 IS NULL 사용  
 다음 예에서는 `NULL` 열에 `Weight`이 있는 모든 제품을 찾는 방법을 보여 줍니다. `IS`와 `NULL` 사이에 공백이 있습니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT EnglishProductName, Weight  
FROM dbo.DimProduct  
WHERE Weight IS NULL;  
```  
  
## <a name="see-also"></a>참고 항목  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [IS NULL&#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [COALESCE&#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  

