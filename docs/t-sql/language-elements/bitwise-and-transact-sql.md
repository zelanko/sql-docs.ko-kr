---
description: '&amp;(비트 AND)(Transact-SQL)'
title: '&amp;(비트 AND)(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 06b82d0789044206003c69bd2a6399b43e4718bf
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439208"
---
# <a name="amp-bitwise-and-transact-sql"></a>&amp;(비트 AND)(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  두 정수 값 간에 비트 논리 AND 연산을 수행합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
expression & expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *expression*  
 정수 데이터 형식 범주에 속하는 데이터 형식, **bit**, **binary** 또는 **varbinary** 데이터 형식 중 하나인 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *expression* 은 비트 연산의 이진 숫자로 처리됩니다.  
  
> [!NOTE]  
>  비트 연산에서는 하나의 *식* 이 **binary** 또는 **varbinary** 데이터 형식이 될 수 있습니다.  
  
## <a name="result-types"></a>결과 형식  
 입력 값이 **int** 이면 **int** 입니다.  
  
 입력 값이 **smallint** 이면 **smallint** 입니다.  
  
 입력된 값이 **tinyint** 또는 **bit** 인 경우 **tinyint** 입니다.  
  
## <a name="remarks"></a>설명  
 **&** 비트 연산자는 두 식 간에 비트 논리 AND를 수행하고 양쪽 식에서 해당 비트를 취합니다. 결과의 비트는 입력 식에 있는 양쪽 비트(확인 중인 현재 비트)의 값이 1이면 1로 설정되고 그렇지 않으면 0으로 설정됩니다.  
  
 왼쪽과 오른쪽 식의 정수 데이터 형식이 서로 다르면(예: 왼쪽 *식* 은 **smallint** 이고 오른쪽 *식* 은 **int** 임) 더 작은 데이터 형식의 인수가 더 큰 데이터 형식으로 변환됩니다. 이 경우에 **smallint** 식이 **int** 로 변환됩니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 값을 저장하기 위해 **int** 데이터 형식을 사용하여 테이블을 만들고 두 값을 한 행에 삽입하는 방법을 보여 줍니다.  
  
```sql
CREATE TABLE bitwise (   
  a_int_value INT NOT NULL,  
  b_int_value INT NOT NULL);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 이 쿼리는 `a_int_value`와 `b_int_value` 열 간에 비트 AND를 수행합니다.  
  
```sql  
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
  
 170의 이진 표현(`a_int_value` 또는 `A`)은 `0000 0000 1010 1010`입니다. 75의 이진 표현(`b_int_value` 또는 `B`)은 `0000 0000 0100 1011`입니다. 이 두 값에 대해 비트 AND 연산을 수행하면 이진수로 `0000 0000 0000 1010`이 산출되며 십진수로는 10입니다.  
  
```  
(A & B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 0000 1010  
```  
  
  
## <a name="see-also"></a>참고 항목  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [비트 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [&=&#40;비트 AND 대입&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
 [복합 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


