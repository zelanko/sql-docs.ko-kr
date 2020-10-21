---
description: ~(비트 NOT)(Transact-SQL)
title: ~(비트 NOT)(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ~_TSQL
- bitwise
- NOT
- "~"
- Bitwise NOT
dev_langs:
- TSQL
helpviewer_keywords:
- NOT keyword
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: 02da8016-f6c0-41ae-8d59-33eaa02bfc95
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dd89533ee030204cfb0b57a3c51d4a03bb790462
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92189238"
---
# <a name="-bitwise-not-transact-sql"></a>~(비트 NOT)(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  정수 값에 비트 논리 NOT 연산을 수행합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
~ expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *expression*  
 정수 데이터 형식 범주에 속하는 데이터 형식, **bit**, **binary** 또는 **varbinary** 데이터 형식 중 하나인 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *expression*은 비트 연산의 이진 숫자로 처리됩니다.  
  
> [!NOTE]  
>  비트 연산에서는 하나의 *expression*만 **binary** 또는 **varbinary** 데이터 형식이 될 수 있습니다.  
  
## <a name="result-types"></a>결과 형식  
 입력 값이 **int**이면 **int**입니다.  
  
 입력 값이 **smallint**이면 **smallint**입니다.  
  
 입력 값이 **tinyint**이면 **tinyint**입니다.  
  
 입력 값이 **bit**이면 **bit**입니다.  
  
## <a name="remarks"></a>설명  
 **~** 비트 연산자는 각 비트를 차례로 가져와서 *expression*에 대한 비트 논리 NOT을 수행합니다. *expression*의 값이 0이면 결과 집합의 비트가 1로 설정되며, 그렇지 않으면 결과 비트가 0 값으로 지워집니다. 즉, 1은 0으로 변경되고 0은 1로 변경됩니다.  
  
> [!IMPORTANT]  
>  비트 연산을 수행할 때는 연산에 사용되는 식의 스토리지 길이가 중요합니다. 값을 저장할 때는 동일한 바이트 수를 사용하는 것이 좋습니다. 예를 들어 5(10진수 값)를 **tinyint**, **smallint** 또는 **int**로 저장하면 다른 바이트 수로 저장되는 값을 생성합니다. 즉 **tinyint**는 1바이트, **smallint**는 2바이트, **int**는 4바이트를 사용하는 데이터를 저장합니다. 따라서 **int** 10진수 값에 대해 비트 연산을 수행하면, 특히 **~**(비트 NOT) 연산자가 사용될 때 직접 이진 또는 16진수 변환을 사용하는 것과 다른 결과를 생성할 수 있습니다. 비트 NOT 연산은 길이가 짧은 변수에서 발생할 수 있습니다. 이 경우 길이가 짧은 변수를 길이가 긴 데이터 형식 변수로 변환할 때 상위 8비트는 예상된 값으로 설정되지 않을 수 있습니다. 작은 데이터 형식 변수를 큰 데이터 형식 변수로 변환한 다음 그 결과에서 NOT 연산을 수행하는 것이 좋습니다.  
  
## <a name="examples"></a>예제  
 다음 예제에서는 **int** 데이터 형식을 사용하여 테이블을 만들어 값을 저장하고 한 행에 두 값을 삽입합니다.  
  
```sql  
CREATE TABLE bitwise (  
  a_int_value INT NOT NULL,  
  b_int_value INT NOT NULL); 
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 다음 쿼리는 `a_int_value` 및 `b_int_value` 열에 비트 NOT 연산을 수행합니다.  
  
```sql  
SELECT ~ a_int_value, ~ b_int_value  
FROM bitwise;  
```  
  
 결과 집합은 다음과 같습니다.  
  
```  
--- ---   
-171  -76   
  
(1 row(s) affected)  
```  
  
 170의 이진 표현(`a_int_value` 또는 `A`)은 `0000 0000 1010 1010`입니다. 이 값에 대해 비트 NOT 연산을 수행하면 10진수 -171에 해당되는 이진 결과 `1111 1111 0101 0101`이 생성됩니다. 75의 이진 표현은 `0000 0000 0100 1011`입니다. 비트 NOT 연산을 수행하면 `1111 1111 1011 0100`(10진수 -76)이 생성됩니다.  
  
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
  
 
## <a name="see-also"></a>참고 항목  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [비트 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  


