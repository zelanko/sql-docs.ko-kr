---
title: LOG10 (Transact SQL) | Microsoft Docs
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
- LOG10
- LOG10_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- float expressions
- LOG10 function
- base-10 logarithms
- logarithm of expression
ms.assetid: 1eb7fb34-1937-4a39-a936-f5c0c7c7e06f
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d8cc5b0ef6af319e55744a3ca373f0e6b11e230b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="log10-transact-sql"></a>LOG10(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정 된 밑이 10 인 로그 값을 반환 **float** 식입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
LOG10 ( float_expression )  
```  
  
## <a name="arguments"></a>인수  
 *float_expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 형식의 **float** 또는 암시적으로 변환할 수 있는 형식의 **float**합니다.  
  
## <a name="return-types"></a>반환 형식  
 **float**  
  
## <a name="remarks"></a>주의  
 LOG10과 POWER 함수는 서로 역함수 관계에 있습니다. 예를 들어 10 ^ LOG10 (*n*) =  *n* 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-calculating-the-base-10-logarithm-for-a-variable"></a>1. 변수에 대한 상용 로그 계산  
 다음 예에서는 지정된 변수의 `LOG10`을 계산하는 방법을 보여 줍니다.  
  
```  
DECLARE @var float;  
SET @var = 145.175643;  
SELECT 'The LOG10 of the variable is: ' + CONVERT(varchar,LOG10(@var));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The LOG10 of the variable is: 2.16189      
  
(1 row(s) affected)  
```  
  
### <a name="b-calculating-the-result-of-raising-a-base-10-logarithm-to-a-specified-power"></a>2. 상용 로그를 지정된 거듭제곱으로 올린 결과 계산  
 다음 예에서는 상용 로그를 지정된 거듭제곱으로 올린 결과를 반환하는 방법을 보여 줍니다.  
  
```  
SELECT POWER (10, LOG10(5));   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------  
5  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-calculating-the-base-10-logarithm-for-a-value"></a>C: 밑을 10으로 사용 하는 값에 대 한 계산 하는입니다.  
 다음 예에서는 계산 된 `LOG10` 지정 된 값입니다.  
  
```  
SELECT LOG10(145.175642);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `-------------------`  
  
 `2.16`  
  
## <a name="see-also"></a>관련 항목:  
 [수치 연산 함수 &#40; Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [전원 &#40; Transact SQL &#41;](../../t-sql/functions/power-transact-sql.md)   
 [로그 &#40; Transact SQL &#41;](../../t-sql/functions/log-transact-sql.md)  
  
  


