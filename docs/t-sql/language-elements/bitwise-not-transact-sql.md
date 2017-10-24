---
title: "~ (비트 NOT) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ~_TSQL
- bitwise
- NOT
- ~
- Bitwise NOT
dev_langs:
- TSQL
helpviewer_keywords:
- NOT keyword
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: 02da8016-f6c0-41ae-8d59-33eaa02bfc95
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3cfe0944a896548bfd0e0e0612b832ac91417016
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="-bitwise-not-transact-sql"></a>~(비트 NOT)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  정수 값에 비트 논리 NOT 연산을 수행합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
~ expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md) integer 데이터 형식 범주의 데이터 형식 중 하나는 **비트**, 또는 **이진** 또는 **varbinary** 데이터 형식입니다. *식* 비트 연산을 위해 이진 숫자로 취급 됩니다.  
  
> [!NOTE]  
>  하나의 *식* 될 수 **이진** 또는 **varbinary** 연산의 데이터 형식입니다.  
  
## <a name="result-types"></a>결과 형식  
 **int** 입력된 값이 **int**합니다.  
  
 **smallint** 입력된 값이 **smallint**합니다.  
  
 **tinyint** 입력된 값이 **tinyint**합니다.  
  
 **비트** 입력된 값이 **비트**합니다.  
  
## <a name="remarks"></a>주의  
  **~**  비트 논리 NOT을 수행 하는 비트 or 연산자에 대 한는 *식*, 각 비트를 차례로 합니다. 경우 *식* 값 0을 결과 집합의 비트가 1로 설정 됩니다; 값 0 결과에서 비트는 해제 하는 그렇지 않은 경우. 즉, 1은 0으로 변경되고 0은 1로 변경됩니다.  
  
> [!IMPORTANT]  
>  비트 연산을 수행할 때는 연산에 사용되는 식의 저장 길이가 중요합니다. 값을 저장할 때는 동일한 바이트 수를 사용하는 것이 좋습니다. 예를 들어 5로 10 진수 값을 저장 한 **tinyint**, **smallint**, 또는 **int** 함께 바이트 수가 다르게 저장 된 값이 생성: **tinyint** 1 바이트,를 사용 하 여 데이터를 저장 합니다. **smallint** 2 바이트를 사용 하 여 데이터를 저장 하 고 **int** 4 바이트를 사용 하 여 데이터를 저장 합니다. 따라서에 비트 연산을 수행는 **int** 10 진수 값에서 직접 이진 또는 16 진수 변환을 사용 하 여 다른 결과 산출 특히 경우는  **~**  드 ( 비트 NOT) 연산자를 사용 합니다. 비트 NOT 연산은 길이가 짧은 변수에서 발생할 수 있습니다. 이 경우 길이가 짧은 변수를 길이가 긴 데이터 형식 변수로 변환할 때 상위 8비트는 예상된 값으로 설정되지 않을 수 있습니다. 작은 데이터 형식 변수를 큰 데이터 형식 변수로 변환한 다음 그 결과에서 NOT 연산을 수행하는 것이 좋습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 사용 하 여 테이블을 만듭니다는 **int** 데이터 입력 값을 저장 하 고 한 행에 두 값을 삽입 합니다.  
  
```  
CREATE TABLE bitwise  
(   
a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 다음 쿼리는 `a_int_value` 및 `b_int_value` 열에 비트 NOT 연산을 수행합니다.  
  
```  
SELECT ~ a_int_value, ~ b_int_value  
FROM bitwise;  
```  
  
 결과 집합은 다음과 같습니다.  
  
```  
--- ---   
-171  -76   
  
(1 row(s) affected)  
```  
  
 170의 이진 표현 (`a_int_value` 또는 `A`)은 `0000 0000 1010 1010`합니다. 이 값에 대해 비트 NOT 연산을 수행하면 10진수 -171에 해당되는 이진 결과 `1111 1111 0101 0101`이 생성됩니다. 75의 이진 표현은 `0000 0000 0100 1011`입니다. 비트 NOT 연산을 수행하면 `1111 1111 1011 0100`(10진수 -76)이 생성됩니다.  
  
```  
 (~A)     
         0000 0000 1010 1010  
         -------------------  
         1111 1111 0101 0101  
(~B)     
         0000 0000 0100 1011  
         -------------------  
         1111 1111 1011 0100  
```  
  
 
## <a name="see-also"></a>관련 항목:  
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [비트 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  



