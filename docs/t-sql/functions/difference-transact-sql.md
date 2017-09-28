---
title: "차이 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DIFFERENCE
- DIFFERENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DIFFERENCE function
- comparing SOUNDEX values
- SOUNDEX values
ms.assetid: c58ca25d-d6ea-48fa-93bb-c9374b0b2a2b
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3ea034f7217d031c21cf22f6b5aaff9bf16355a9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="difference-transact-sql"></a>DIFFERENCE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  두 문자 식에서 SOUNDEX 값의 차이를 나타내는 정수 값을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DIFFERENCE ( character_expression , character_expression )  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 영숫자 [식](../../t-sql/language-elements/expressions-transact-sql.md) 문자 데이터입니다. *character_expression* 상수, 변수 또는 열일 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>주의  
 반환된 정수는 SOUNDEX 값에서 동일한 문자 수입니다. 반환 값의 범위는 0부터 4: 0 적거나 없음을 나타내며 4는 유사점이 많거나 동일한 값 나타냅니다.  
  
 DIFFERENCE 및 SOUNDEX는 데이터 정렬을 인식합니다.  
  
## <a name="examples"></a>예  
 다음 예의 첫 번째 부분에서 매우 유사한 두 개의 문자열에 대한 `SOUNDEX` 값이 비교됩니다. Latin1_General 데이터 정렬에 대 한 `DIFFERENCE` 의 값을 반환 `4`합니다. 다음 예제에서는 두 번째 부분에는 `SOUNDEX` 값를 매우 다른 두 개의 문자열을 비교에 대 한 및 Latin1_General 데이터 정렬에 대 한 `DIFFERENCE` 의 값을 반환 `0`합니다.  
  
```  
-- Returns a DIFFERENCE value of 4, the least possible difference.  
SELECT SOUNDEX('Green'), SOUNDEX('Greene'), DIFFERENCE('Green','Greene');  
GO  
-- Returns a DIFFERENCE value of 0, the highest possible difference.  
SELECT SOUNDEX('Blotchet-Halls'), SOUNDEX('Greene'), DIFFERENCE('Blotchet-Halls', 'Greene');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----- ----- -----------   
G650  G650  4             
  
(1 row(s) affected)  
  
----- ----- -----------   
B432  G650  0             
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예의 첫 번째 부분에서 매우 유사한 두 개의 문자열에 대한 `SOUNDEX` 값이 비교됩니다. Latin1_General 데이터 정렬에 대 한 `DIFFERENCE` 의 값을 반환 `4`합니다. 다음 예제에서는 두 번째 부분에는 `SOUNDEX` 값를 매우 다른 두 개의 문자열을 비교에 대 한 및 Latin1_General 데이터 정렬에 대 한 `DIFFERENCE` 의 값을 반환 `0`합니다.  
  
```  
-- Returns a DIFFERENCE value of 4, the least possible difference.  
SELECT SOUNDEX('Green'), SOUNDEX('Greene'), DIFFERENCE('Green','Greene');  
GO  
-- Returns a DIFFERENCE value of 0, the highest possible difference.  
SELECT SOUNDEX('Blotchet-Halls'), SOUNDEX('Greene'), DIFFERENCE('Blotchet-Halls', 'Greene');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----- ----- -----------   
G650  G650  4             
  
(1 row(s) affected)  
  
----- ----- -----------   
B432  G650  0             
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SOUNDEX &#40; Transact SQL &#41;](../../t-sql/functions/soundex-transact-sql.md)   
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


