---
title: ^(배타적 비트 OR)(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ^_TSQL
- Bitwise Exclusive OR
- Exclusive
- ^
- bitwise
- OR
dev_langs:
- TSQL
helpviewer_keywords:
- ^ (bitwise exclusive OR operator)
- OR operator
- exclusive OR mathematical operations
- bitwise exclusive OR (^)
ms.assetid: f38f0ad4-46d0-40ea-9851-0f928fda5293
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 71833dac842094b1f6fc8cdf0d0f96645fb70854
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="-bitwise-exclusive-or-transact-sql"></a>^(배타적 비트 OR)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  두 정수 값 사이에 배타적 비트 OR 연산을 수행합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
expression ^ expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 정수 데이터 형식 범주에 속하는 데이터 형식, **bit**, **binary** 또는 **varbinary** 데이터 형식 중 하나인 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *식*은 비트 연산에서 이진 숫자로 취급됩니다.  
  
> [!NOTE]  
>  비트 연산에서는 하나의 *expression*만 **binary** 또는 **varbinary** 데이터 형식이 될 수 있습니다.  
  
## <a name="result-types"></a>결과 형식  
 입력 값이 **int**이면 **int**입니다.  
  
 입력 값이 **smallint**이면 **smallint**입니다.  
  
 입력 값이 **tinyint**이면 **tinyint**입니다.  
  
## <a name="remarks"></a>Remarks  
 **^** 비트 연산자는 양쪽 연산에 해당 비트를 받아서 두 식 간에 배타적 비트 논리 OR를 수행합니다. 결과 비트는 입력 식에 있는 두 비트(확인 중인 현재 비트) 중 하나의 값이 1이면 1로 설정됩니다. 양쪽 비트 값이 모두 0 또는 1이면 결과 비트는 0으로 처리됩니다.  
  
 왼쪽과 오른쪽 식의 정수 데이터 형식이 서로 다르면(예: 왼쪽 *식*은 **smallint**이고 오른쪽 *식*은 **int**임) 더 작은 데이터 형식의 인수가 더 큰 데이터 형식으로 변환됩니다. 이 경우에 **smallint***식*이 **int**로 변환됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 원래 값을 저장하기 위해 **int** 데이터 형식을 사용하여 원래 값을 저장하는 테이블을 만들고 한 행에 두 개의 값을 삽입합니다.  
  
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
  
 다음 쿼리는 `a_int_value` 및 `b_int_value` 열에 배타적 비트 OR를 수행합니다.  
  
```  
SELECT a_int_value ^ b_int_value  
FROM bitwise;  
GO  
```  
  
 결과 집합은 다음과 같습니다.  
  
```  
-----------   
225           
  
(1 row(s) affected)  
```  
  
 170의 이진 표현(`a_int_value` 또는 `A`)은 `0000 0000 1010 1010`입니다. 75의 이진 표현(`b_int_value` 또는 `B`)은 `0000 0000 0100 1011`입니다. 이러한 두 값에 배타적 비트 OR 연산을 수행하면 결과는 이진수 `0000 0000 1110 0001`이며 십진수로는 225입니다.  
  
```  
(A ^ B)     
         0000 0000 1010 1010  
         0000 0000 0100 1011  
         -------------------  
         0000 0000 1110 0001  
```  
  

  
## <a name="see-also"></a>참고 항목  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [비트 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [^=&#40;배타적 비트 OR 대입&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)   
 [복합 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


