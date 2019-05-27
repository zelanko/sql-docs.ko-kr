---
title: + (단항 더하기)(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- + (positive)
- +
- positive
dev_langs:
- TSQL
helpviewer_keywords:
- + (positive operator)
- positive operator (+)
- positive values [SQL Server]
ms.assetid: 0f31c5cc-3078-4f6a-9870-7eb1a98053fb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6b37c60fa27af53949803c2077ba0736bf5de7e1
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65981011"
---
# <a name="unary-operators---positive"></a>단항 연산자 - 양수
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

숫자 식(단항 연산자)의 값을 반환합니다. 단항 연산자는 숫자 데이터 형식 범주에 속하는 데이터 형식의 한 식에 대해서만 연산을 수행합니다.   
  
|연산자|의미|  
|--------------|-------------|  
|[+(양수)](../../t-sql/language-elements/unary-operators-positive.md)|숫자 값이 양수입니다.|  
|[-(음수)](../../t-sql/language-elements/unary-operators-negative.md)|숫자 값이 음수입니다.|  
|[~(비트 단위 NOT)](../../t-sql/language-elements/bitwise-not-transact-sql.md)|해당 수의 1의 보수를 반환합니다.|  
  
 +(양수) 및 -(음수) 연산자는 숫자 데이터 형식 범주에 속하는 데이터 형식의 식에서 사용할 수 있습니다. ~(비트 NOT) 연산자는 정수 데이터 형식 범주에 속하는 데이터 형식 중 하나의 식에서만 사용할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
+ numeric_expression  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression*  
 숫자 데이터 형식 범주에서 **datetime** 및 **smalldatetime** 데이터 형식을 제외한 숫자 데이터 형식 범주의 데이터 형식 중 하나에 대한 올바른 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
## <a name="result-types"></a>결과 형식  
 *numeric_expression*의 데이터 형식을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 단항 더하기는 숫자 식 앞에 올 수 있지만 해당 식에서 반환하는 값에 대해서는 연산을 수행하지 않습니다. 특히 단항 더하기는 음수 식에서 양수 값을 반환하지 않습니다. 음수 식에서 양수 값을 반환하려면 [ABS](../../t-sql/functions/abs-transact-sql.md) 함수를 사용하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-setting-a-variable-to-a-positive-value"></a>1. 변수를 양수 값으로 설정  
 다음 예에서는 변수를 양수 값으로 설정합니다.  
  
```  
DECLARE @MyNumber decimal(10,2);  
SET @MyNumber = +123.45;  
SELECT @MyNumber;  
GO  
```  
  
 결과 집합은 다음과 같습니다.  
  
```  
-----------   
123.45            
  
(1 row(s) affected)  
```  
  
### <a name="b-using-the-unary-plus-operator-with-a-negative-value"></a>2. 음수 값에 단항 더하기 연산자 사용  
 다음 예에서는 같은 음수 식에 단항 더하기와 ABS() 함수를 사용하는 것을 보여 줍니다. 단항 더하기는 식에 영향을 주지 않지만 ABS 함수는 식의 양수 값을 반환합니다.  
  
```  
USE tempdb;  
GO  
DECLARE @Num1 int;  
SET @Num1 = -5;  
SELECT +@Num1, ABS(@Num1);  
GO  
```  
  
 결과 집합은 다음과 같습니다.  
  
```  
----------- -----------  
-5          5  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [ABS&#40;Transact-SQL&#41;](../../t-sql/functions/abs-transact-sql.md)  
  
  
