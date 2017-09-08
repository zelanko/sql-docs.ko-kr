---
title: TRIM (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TRIM
- TRIM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- TRIM function
ms.assetid: a00245aa-32c7-4ad4-a0d1-64f3d6841153
caps.latest.revision: 4
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 64cef84a613d71e65b33bed1c1e740dc59eeed9d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="trim-transact-sql"></a>TRIM (Transact SQL)
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

공백 문자를 제거 `char(32)` 또는 시작 이나 문자열의 끝에서 지정 된 다른 문자입니다.  
 
## <a name="syntax"></a>구문   
```
TRIM ( [ characters FROM ] string ) 
```
[//]: # "[둘 다 | 선행 | 후행] 하지 아직 사용할 수 있습니다."

## <a name="arguments"></a>인수   

문자   
리터럴, 변수 또는 모든 비-LOB 문자 형식의 함수 호출 (`nvarchar`, `varchar`, `nchar`, 또는 `char`)를 제거 해야 하는 문자가 포함 된 합니다. `nvarchar(max)`및 `varchar(max)` 형식은 허용 되지 않습니다.

string   
모든 문자 형식의 식 (`nvarchar`, `varchar`, `nchar`, 또는 `char`) 문자를 제거 해야 합니다.

## <a name="return-types"></a>반환 형식   
문자열 인수는 형식 사용 하 고 문자 식을 반환 합니다. 여기서 공백 문자 `char(32)` 또는 양쪽 모두에서 지정 된 다른 문자를 제거 합니다. 반환 `NULL` 입력된 문자열의 형식이 `NULL`합니다.

## <a name="remarks"></a>주의   
기본적으로 `TRIM` 함수는 공백 문자를 제거 `char(32)` 양쪽 모두에서 합니다. `LTRIM(RTRIM(@string))`와 같습니다. 동작 `TRIM ` 문자로 지정 된 함수는의 동작과 동일 `REPLACE` 함수 시작 또는 끝에서 문자를 빈 문자열이 바뀝니다.


## <a name="examples"></a>예
### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>1.  문자열의 양쪽 모두에서 공백 문자를 제거합니다.   
다음 예에서는 앞에서 앞뒤로 공백을 제거 `test`합니다.   
```tsql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

`test`


### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>2.  지정 된 문자열의 양쪽 모두에서 문자 제거   
다음 예제에서는 뒤에 마침표 및 후행 공백을 제거합니다.
```tsql
SELECT TRIM( '.,! ' FROM  '#     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
`#     test`


## <a name="see-also"></a>관련 항목:
[문자열 함수 (Transact SQL)](../../t-sql/functions/string-functions-transact-sql.md)   
[LTRIM (Transact SQL)](../../t-sql/functions/ltrim-transact-sql.md)   
[RTRIM (Transact SQL)](../../t-sql/functions/rtrim-transact-sql.md)   
[REPLACE (Transact SQL)](../../t-sql/functions/replace-transact-sql.md)   

