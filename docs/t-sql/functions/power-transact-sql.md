---
title: POWER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- POWER_TSQL
- POWER
dev_langs:
- TSQL
helpviewer_keywords:
- POWER function
ms.assetid: 0fd34494-90b9-4559-8011-a8c1b9f40239
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ea25c7b1324a3786cb5cd9f28d3e1201ab3cc108
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003781"
---
# <a name="power-transact-sql"></a>POWER(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  지정된 식을 거듭제곱한 값을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
POWER ( float_expression , y )  
```  
  
## <a name="arguments"></a>인수  
 *float_expression*  
 [float](../../t-sql/language-elements/expressions-transact-sql.md) 형식 또는 **float**로 암시적으로 변환되는 형식의 **식**입니다.  
  
 *y*  
 *float_expression*의 거듭제곱입니다. *y*는 **bit** 데이터 형식을 제외한 정확한 수치 또는 근사치 데이터 형식 범주의 식일 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 반환 형식은 *float_expression*의 입력 형식에 따라 달라집니다.
 
|입력 형식|반환 형식|  
|----------|-----------|  
|**float**, **real**|**float**|
|**10진수(*p*, *s*)**|**10진수(38, *s*)**|
|**int**, **smallint**, **tinyint**|**int**|
|**bigint**|**bigint**|
|**money**, **smallmoney**|**money**|
|**bit**, **char**, **nchar**, **varchar**, **nvarchar**|**float**|
 
결과가 반환 형식에 맞지 않으면 산술 오버플로 오류가 발생합니다.
  
## <a name="examples"></a>예  
  
### <a name="a-using-power-to-return-the-cube-of-a-number"></a>A. POWER를 사용하여 숫자의 세제곱 반환  
 다음 예에서는 3의 승수로 거듭 제곱한 수(숫자의 세제곱)를 보여줍니다.  
  
```  
DECLARE @input1 FLOAT;  
DECLARE @input2 FLOAT;  
SET @input1= 2;  
SET @input2 = 2.5;  
SELECT POWER(@input1, 3) AS Result1, POWER(@input2, 3) AS Result2;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result1                Result2  
---------------------- ----------------------  
8                      15.625  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-power-to-show-results-of-data-type-conversion"></a>B. POWER를 사용하여 데이터 형식 자동 변환 표시  
 다음 예에서는 *float_expression*에서 예기치 않은 결과를 반환할 수 있는 데이터 형식을 유지하는 방법을 보여 줍니다.  
  
```  
SELECT   
POWER(CAST(2.0 AS FLOAT), -100.0) AS FloatResult,  
POWER(2, -100.0) AS IntegerResult,  
POWER(CAST(2.0 AS INT), -100.0) AS IntegerResult,  
POWER(2.0, -100.0) AS Decimal1Result,  
POWER(2.00, -100.0) AS Decimal2Result,  
POWER(CAST(2.0 AS DECIMAL(5,2)), -100.0) AS Decimal2Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
FloatResult            IntegerResult IntegerResult Decimal1Result Decimal2Result Decimal2Result  
---------------------- ------------- ------------- -------------- -------------- --------------  
7.88860905221012E-31   0             0             0.0            0.00           0.00  
```  
  
### <a name="c-using-power"></a>C. POWER 사용  
 다음 예에서는 `POWER`에 대한 `2` 결과를 반환합니다.  
  
```  
DECLARE @value INT, @counter INT;  
SET @value = 2;  
SET @counter = 1;  
  
WHILE @counter < 5  
   BEGIN  
      SELECT POWER(@value, @counter)  
      SET NOCOUNT ON  
      SET @counter = @counter + 1  
      SET NOCOUNT OFF  
   END;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------   
2             
  
(1 row(s) affected)  
  
-----------   
4             
  
(1 row(s) affected)  
  
-----------   
8             
  
(1 row(s) affected)  
  
-----------   
16            
  
(1 row(s) affected)  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-power-to-return-the-cube-of-a-number"></a>4\. POWER를 사용하여 숫자의 세제곱 반환  
 다음 예에서는 `POWER`의 세제곱에 대한 `2.0` 결과를 반환합니다.  
  
```  
SELECT POWER(2.0, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
------------ 
8.0
```  
  
## <a name="see-also"></a>참고 항목  
 [decimal 및 numeric&#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [float 및 real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)   
 [int, bigint, smallint 및 tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)   
 [수치 연산 함수&#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [money 및 smallmoney&#40;Transact-SQL&#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
  
  

