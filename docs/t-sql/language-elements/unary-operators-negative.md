---
title: "- (음수) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 47a9eb729127e53dc3ee72fe5353ad536c56d922
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="unary-operators---negative"></a>단항 연산자-음수
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  숫자 식의 음수 값을 반환합니다(단항 연산자). 단항 연산자는 숫자 데이터 형식 범주에 속하는 데이터 형식의 한 식에 대해서만 연산을 수행합니다.   
  
|연산자|의미|  
|--------------|-------------|  
|[+(양수)](../../t-sql/language-elements/unary-operators-positive.md)|숫자 값이 양수입니다.|  
|[-(음수)](../../t-sql/language-elements/unary-operators-negative.md)|숫자 값이 음수입니다.|  
|[~ (비트 NOT)](../../t-sql/language-elements/bitwise-not-transact-sql.md)|해당 수의 1의 보수를 반환합니다.|  
  
 +(양수) 및 -(음수) 연산자는 숫자 데이터 형식 범주에 속하는 데이터 형식의 식에서 사용할 수 있습니다. ~(비트 NOT) 연산자는 정수 데이터 형식 범주에 속하는 데이터 형식 중 하나의 식에서만 사용할 수 있습니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
- numeric_expression  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md) 시간 범주를 확인 하 고 날짜를 제외 하 고 숫자 데이터 형식 범주의 데이터 형식 중 하나입니다.  
  
## <a name="result-types"></a>결과 형식  
 데이터 형식을 반환 *numeric_expression*한다는 점을 제외 하는 부호 없는 **tinyint** 식 승격 됩니다 부호 있는 **smallint** 결과입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-setting-a-variable-to-a-negative-value"></a>1. 변수를 음의 값으로 설정  
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
  
### <a name="b-changing-a-variable-to-a-negative-value"></a>2. 변수를 음의 값으로 변경  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-the-negative-of-a-positive-constant"></a>3. 양의 상수의 음수를 반환합니다.  
 다음 예에서는 양수 상수의 음수를 반환합니다.  
  
```  
USE ssawPDW;  
  
SELECT TOP (1) - 17 FROM DimEmployee;  
```  
  
 반환 값  
  
```  
-17  
```  
  
### <a name="d-returning-the-positive-of-a-negative-constant"></a>4. 음수 상수의 양수를 반환합니다.  
 다음 예에서는 음수 상수의 양수를 반환합니다.  
  
```  
USE ssawPDW;  
  
SELECT TOP (1) – ( - 17) FROM DimEmployee;  
```  
  
 반환 값  
  
```  
17  
```  
  
### <a name="e-returning-the-negative-of-a-column"></a>5. 열의 음수를 반환합니다.  
 다음 예의 부정을 반환는 `BaseRate` 각 직원에 대 한 값은 `dimEmployee` 테이블입니다.  
  
```  
USE ssawPDW;  
  
SELECT - BaseRate FROM DimEmployee;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  


