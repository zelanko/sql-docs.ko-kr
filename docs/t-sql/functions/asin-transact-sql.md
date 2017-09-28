---
title: ASIN (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ASIN_TSQL
- ASIN
dev_langs:
- TSQL
helpviewer_keywords:
- ASIN function
- sine
- arcsine
ms.assetid: 6256dd7d-83d5-486e-a933-1d59afc7e417
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1ddfa04e926b4fd0e99455ea91774c31d34b0601
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="asin-transact-sql"></a>ASIN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

사인이 지정 된 라디안 단위로 각도 반환 **float** 식입니다. 이를 아크사인이라고도 합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
ASIN ( float_expression )  
```  
  
## <a name="arguments"></a>인수  
*float_expression*  
이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 형식의 **float** 또는 1부터 1 까지입니다 값이 float로 암시적으로 변환 될 수 있는 형식의 합니다. 값이 이 범위를 벗어나면 NULL이 반환되고 도메인 오류가 보고됩니다.
  
## <a name="return-types"></a>반환 형식
**float**
  
## <a name="examples"></a>예  
다음 예제에서는 **float** 식과 지정된 된 각도의 ASIN 반환 합니다.
  
```sql
/* The first value will be -1.01. This fails because the value is   
outside the range.*/  
DECLARE @angle float  
SET @angle = -1.01  
SELECT 'The ASIN of the angle is: ' + CONVERT(varchar, ASIN(@angle))  
GO  
  
-- The next value is -1.00.  
DECLARE @angle float  
SET @angle = -1.00  
SELECT 'The ASIN of the angle is: ' + CONVERT(varchar, ASIN(@angle))  
GO  
  
-- The next value is 0.1472738.  
DECLARE @angle float  
SET @angle = 0.1472738  
SELECT 'The ASIN of the angle is: ' + CONVERT(varchar, ASIN(@angle))  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-------------------------  
.Net SqlClient Data Provider: Msg 3622, Level 16, State 1, Line 3  
A domain error occurred.  
  
---------------------------------   
The ASIN of the angle is: -1.5708                          
  
(1 row(s) affected)  
  
----------------------------------   
The ASIN of the angle is: 0.147811                         
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
다음 예제에서는 1.00의 아크사인 값을 반환합니다.
  
```sql
SELECT ASIN(1.00) AS asinCalc;  
```  
  
다음 예에서는 허용 되는 범위를 벗어난 값에 대 한 아크사인 값을 요청 하기 때문에 오류를 반환 합니다.
  
```sql
SELECT ASIN(1.1472738) AS asinCalc;  
```  
  
## <a name="see-also"></a>참고 항목
[천장 &#40; Transact SQL &#41;](../../t-sql/functions/ceiling-transact-sql.md)  
[수치 연산 함수 &#40; Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[SET arithignore 옵션 &#40; Transact SQL &#41;](../../t-sql/statements/set-arithignore-transact-sql.md)  
[SET arithabort&#40; Transact SQL &#41;](../../t-sql/statements/set-arithabort-transact-sql.md)
  
  


