---
title: '|(비트 OR)(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '|'
- '|_TSQL'
- Bitwise OR
- bitwise
- OR
dev_langs:
- TSQL
helpviewer_keywords:
- OR operator
- bitwise OR (|)
- '| (bitwise OR operator)'
ms.assetid: 86a3b87f-9688-4eaf-a552-29f1b01d880a
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 939fd07d8f484f9ae94ee4e59d1702399dc2498c
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39452387"
---
# <a name="-bitwise-or-transact-sql"></a>|(비트 OR)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 이진 식으로 변환되는 두 개의 지정된 정수 값 간에 비트 논리 OR 연산을 수행합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```   
expression | expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 정수 데이터 형식 범주나 **bit**, **binary** 또는 **varbinary** 데이터 형식의 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *식*은 비트 연산에서 이진 숫자로 취급됩니다.  
  
> [!NOTE]  
>  비트 연산에서는 하나의 *expression*만 **binary** 또는 **varbinary** 데이터 형식이 될 수 있습니다.  
  
## <a name="result-types"></a>결과 형식  
 입력 값이 **int**이면 **int**를, 입력 값이 **smallint**이면 **smallint**를, 입력 값이 **tinyint**이면 **tinyint**를 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 비트 | 연산자는 양쪽 식에 해당 비트를 취하면서 두 식 간에 비트 논리 OR를 수행합니다. 결과의 비트는 입력 식의 두 비트(확인 중인 현재 비트) 중 하나 또는 둘 모두의 값이 1이면 1로 설정됩니다. 입력 식에 값이 1인 비트가 없으면 결과의 비트는 0으로 설정됩니다.  
  
 왼쪽과 오른쪽 식의 정수 데이터 형식이 서로 다르면(예: 왼쪽 *식*은 **smallint**이고 오른쪽 *식*은 **int**임) 더 작은 데이터 형식의 인수가 더 큰 데이터 형식으로 변환됩니다. 이 예제에서는 **smallint***식*이 **int**로 변환됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 원래 값을 표시하도록 **int** 데이터 형식의 테이블을 만들고 테이블을 하나의 행에 삽입합니다.  
  
```sql  
CREATE TABLE bitwise  
(   
 a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 다음 쿼리는 **a_int_value** 및 **b_int_value** 열에 대해 비트 OR를 수행합니다.  
  
```  
SELECT a_int_value | b_int_value  
FROM bitwise;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------   
235           
  
(1 row(s) affected)  
```  
  
 170(**a_int_value** 또는 아래 `A`)의 이진 표현은 `0000 0000 1010 1010`입니다. 75(**b_int_value** 또는 아래 `B`)의 이진 표현은 `0000 0000 0100 1011`입니다. 이 두 값에 비트 OR 연산을 수행하면 10진수 235에 해당되는 이진 결과 `0000 0000 1110 1011`이 산출됩니다.  
  
```  
(A | B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 1110 1011  
```  
  
## <a name="see-also"></a>참고 항목  
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [비트 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [&#124;=&#40;비트 OR 대입&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
 [복합 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


