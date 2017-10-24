---
title: FLOOR (Transact SQL) | Microsoft Docs
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
- FLOOR_TSQL
- FLOOR
dev_langs:
- TSQL
helpviewer_keywords:
- integers [SQL Server]
- largest integers
- FLOOR function [Transact-SQL]
ms.assetid: 4f26c784-9240-491f-b854-754be3fccae4
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 765cdfb78d13dfa2054571812a051250b19d9d8e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="floor-transact-sql"></a>FLOOR(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  지정된 숫자 식보다 작거나 같은 최대 정수를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
FLOOR ( numeric_expression )  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression*  
 제외 하 고 정확한 수치 또는 근사치 숫자 데이터 형식 범주의 식이 **비트** 데이터 형식입니다.  
  
## <a name="return-types"></a>반환 형식  
 *numeric_expression*과 같은 유형을 반환합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `FLOOR` 함수의 인수로 양수, 음수 및 통화 값을 넣고 계산합니다.  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR($123.45);  
```  
  
 결과 동일한 데이터 형식으로 계산된 된 값의 정수 부분인 *numeric_expression*합니다.  
  
```  
---------      ---------     -----------  
123            -124          123.0000     
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 숫자 음수를 양의 숫자를 보여주며, 값을 `FLOOR` 함수입니다.  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR($123.45);  
```  
  
 결과 동일한 데이터 형식으로 계산된 된 값의 정수 부분인 *numeric_expression*합니다.  
  
 ```
 -----   ---------    -----------  
  
 123     -124         123
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [수치 연산 함수 &#40; Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  


