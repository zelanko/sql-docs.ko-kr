---
title: EXP (Transact SQL) | Microsoft Docs
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
- EXP_TSQL
- EXP
dev_langs:
- TSQL
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 5a9b8c52-6fb6-4e33-8b02-a878785b2f51
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c50757291a8f1fc3d58d8a9a131c4a24aa79a008
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="exp-transact-sql"></a>EXP(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정 된 지 수 값을 반환 **float** 식입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
EXP ( float_expression )  
```  
  
## <a name="arguments"></a>인수  
 *float_expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 형식의 **float** 또는 암시적으로 변환할 수 있는 형식의 **float**합니다.  
  
## <a name="return-types"></a>반환 형식  
 **float**  
  
## <a name="remarks"></a>주의  
 상수 **e** (2.718281 …)는 자연 로그의 기본 인터페이스입니다.  
  
 숫자의 지 수는 상수입니다. **e** 수의 거듭제곱입니다. 예를 들어 EXP(1.0) = e^1.0 = 2.71828182845905이며 EXP(10) = e^10 = 22026.4657948067입니다.  
  
 숫자의 자연 로그의 지 수는 번호 자체: EXP (로그 (*n*)) =  *n* 합니다. 숫자의 지 수 자연 로그는 번호 자체: 로그 (EXP (*n*)) =  *n* 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-finding-the-exponent-of-a-number"></a>1. 숫자의 지수 찾기  
 다음 예에서는 변수를 선언하고 텍스트 설명과 함께 지정된 변수(`10`)의 지수 값을 반환하는 방법을 보여 줍니다.  
  
```  
DECLARE @var float  
SET @var = 10  
SELECT 'The EXP of the variable is: ' + CONVERT(varchar,EXP(@var))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------------------------------------------  
The EXP of the variable is: 22026.5  
(1 row(s) affected)  
```  
  
### <a name="b-finding-exponentials-and-natural-logarithms"></a>2. 지수 및 자연 로그 찾기  
 다음 예에서는 `20`의 자연 로그 값을 구한 후 그 값의 지수 값을 계산하고, 다시 `20`의 지수 값을 구한 후 그 값의 자연 로그 값을 계산하여 반환합니다. 이 함수는 서로 역함수 관계에 있으며 두 함수의 반환 값은 모두 `20`입니다.  
  
```  
SELECT EXP( LOG(20)), LOG( EXP(20))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------------- ----------------------  
20                     20  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-finding-the-exponent-of-a-number"></a>3. 숫자의 지수 찾기  
 다음 예에서는 지정된 된 값의 지 수 값을 반환 (`10`).  
  
```  
SELECT EXP(10);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------  
22026.4657948067  
```  
  
### <a name="d-finding-exponential-values-and-natural-logarithms"></a>4. 지 수 값 및 자연 로그 찾기  
 다음 예에서는 `20`의 자연 로그 값을 구한 후 그 값의 지수 값을 계산하고, 다시 `20`의 지수 값을 구한 후 그 값의 자연 로그 값을 계산하여 반환합니다. 이 함수는 서로 역함수 관계에 있으며 두 함수의 반환 값은 모두 `20`입니다.  
  
```  
SELECT EXP( LOG(20)), LOG( EXP(20));  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------- -----------------  
20                  20  
```  
  
## <a name="see-also"></a>관련 항목:  
 [수치 연산 함수 &#40; Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [로그 &#40; Transact SQL &#41;](../../t-sql/functions/log-transact-sql.md)   
 [LOG10 &#40; Transact SQL &#41;](../../t-sql/functions/log10-transact-sql.md)  
  
  


