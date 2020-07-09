---
title: '- (음수) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- negative
dev_langs:
- TSQL
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
- negative values
ms.assetid: d6c14d14-d379-403b-82db-c197ad58c896
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f1da28f3633bfc42d6e0c1f90cf2d3ea89d991d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85998882"
---
# <a name="unary-operators---negative"></a>단항 연산자 - 음수
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  숫자 식의 음수 값을 반환합니다(단항 연산자). 단항 연산자는 숫자 데이터 형식 범주에 속하는 데이터 형식의 한 식에 대해서만 연산을 수행합니다.   
  
|연산자|의미|  
|--------------|-------------|  
|[+(양수)](../../t-sql/language-elements/unary-operators-positive.md)|숫자 값이 양수입니다.|  
|[-(음수)](../../t-sql/language-elements/unary-operators-negative.md)|숫자 값이 음수입니다.|  
|[~(비트 단위 NOT)](../../t-sql/language-elements/bitwise-not-transact-sql.md)|해당 수의 1의 보수를 반환합니다.|  
  
 +(양수) 및 -(음수) 연산자는 숫자 데이터 형식 범주에 속하는 데이터 형식의 식에서 사용할 수 있습니다. ~(비트 NOT) 연산자는 정수 데이터 형식 범주에 속하는 데이터 형식 중 하나의 식에서만 사용할 수 있습니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
- numeric_expression  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression*  
 숫자 데이터 형식 범주에서 날짜 및 시간 범주를 제외한 임의의 데이터 형식으로 된 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
## <a name="result-types"></a>결과 형식  
 *numeric_expression*의 데이터 형식을 반환합니다. 단, 부호 없는 **tinyint** 식은 부호 있는 **smallint** 결과로 승격됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-setting-a-variable-to-a-negative-value"></a>A. 변수를 음의 값으로 설정  
 다음 예에서는 변수를 음의 값으로 설정합니다.  
  
```  
USE tempdb;  
GO  
DECLARE @MyNumber decimal(10,2);  
SET @MyNumber = -123.45;  
SELECT @MyNumber AS NegativeValue;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
NegativeValue  
---------------------------------------  
-123.45  
  
(1 row(s) affected)  
  
```  
  
### <a name="b-changing-a-variable-to-a-negative-value"></a>B. 변수를 음의 값으로 변경  
 다음 예에서는 변수를 음의 값으로 변경합니다.  
  
```  
USE tempdb;  
GO  
DECLARE @Num1 int;  
SET @Num1 = 5;  
SELECT @Num1 AS VariableValue, -@Num1 AS NegativeValue;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
VariableValue NegativeValue  
------------- -------------  
5             -5  
  
(1 row(s) affected)  
  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-the-negative-of-a-positive-constant"></a>C. 양의 상수의 음수 반환  
 다음 예제에서는 양의 상수의 음수를 반환합니다.  
  
```  
USE ssawPDW;  
  
SELECT TOP (1) - 17 FROM DimEmployee;  
```  
  
 반환  
  
```  
-17  
```  
  
### <a name="d-returning-the-positive-of-a-negative-constant"></a>D. 음의 상수의 양수 반환  
 다음 예제에서는 음의 상수의 양수를 반환합니다.  
  
```  
USE ssawPDW;  
  
SELECT TOP (1) - ( - 17) FROM DimEmployee;  
```  
  
 반환  
  
```  
17  
```  
  
### <a name="e-returning-the-negative-of-a-column"></a>E. 열의 음수 반환  
 다음 예에서는 `BaseRate` 테이블의 각 직원에 대해 `dimEmployee` 값의 음수를 반환합니다.  
  
```  
USE ssawPDW;  
  
SELECT - BaseRate FROM DimEmployee;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  

