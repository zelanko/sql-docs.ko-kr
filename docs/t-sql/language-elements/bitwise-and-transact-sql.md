---
title: "&amp;(비트 AND) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- bitwise
- '&'
- '&_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- AND, bitwise AND
- '& (bitwise AND)'
- bitwise AND (&)
ms.assetid: 20275755-4fa7-47b1-a9be-ac85606d63b0
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e862f742a97f0ea66edcfe32d28224c6fbbeff70
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="amp-bitwise-and-transact-sql"></a>&amp;(비트 AND) (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  두 정수 값 간에 비트 논리 AND 연산을 수행합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
expression & expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md) integer 데이터 형식 범주의 데이터 형식 중 또는 **비트**, 또는 **이진** 또는 **varbinary** 데이터 형식입니다. *식* 비트 연산을 위해 이진 숫자로 취급 됩니다.  
  
> [!NOTE]  
>  하나의 비트 연산에서는 *식* 될 수 **이진** 또는 **varbinary** 데이터 형식입니다.  
  
## <a name="result-types"></a>결과 형식  
 **int** 입력된 값이 **int**합니다.  
  
 **smallint** 입력된 값이 **smallint**합니다.  
  
 **tinyint** 입력된 값이 **tinyint** 또는 **비트**합니다.  
  
## <a name="remarks"></a>주의  
  **&**  비트 연산자를 각 해당 양쪽 식에 비트 받아서 두 식 간에 비트 논리 AND를 수행 합니다. 결과의 비트는 입력 식에 있는 양쪽 비트(확인 중인 현재 비트)의 값이 1이면 1로 설정되고 그렇지 않으면 0으로 설정됩니다.  
  
 왼쪽 및 오른쪽 식의 경우에 다른 정수 데이터 형식 (예를 들어 왼쪽 *식* 은 **smallint** 및 오른쪽 *식* 은  **int**), 더 작은 데이터 형식의 인수를 더 큰 데이터 형식으로 변환 합니다. 이 경우는 **smallint***식* 변환 되는 **int**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 사용 하 여 테이블을 만듭니다는 **int** 데이터 입력 값을 저장 하 고 한 행에 두 개의 값을 삽입 합니다.  
  
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
  
 이 쿼리는 `a_int_value`와 `b_int_value` 열 간에 비트 AND를 수행합니다.  
  
```  
SELECT a_int_value & b_int_value  
FROM bitwise;  
GO  
```  
  
 결과 집합은 다음과 같습니다.  
  
```  
-----------   
10            
  
(1 row(s) affected)  
```  
  
 170의 이진 표현 (`a_int_value` 또는 `A`)은 `0000 0000 1010 1010`합니다. 75의 이진 표현(`b_int_value` 또는 `B`)은 `0000 0000 0100 1011`입니다. 이 두 값에 대해 비트 AND 연산을 수행하면 이진수로 `0000 0000 0000 1010`이 산출되며 십진수로는 10입니다.  
  
```  
(A & B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 0000 1010  
```  
  
  
## <a name="see-also"></a>관련 항목:  
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [비트 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [& = &#40; 비트 AND EQUALS &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
 [복합 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  



