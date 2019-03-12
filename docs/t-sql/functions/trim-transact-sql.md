---
title: TRIM(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- TRIM
- TRIM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- TRIM function
ms.assetid: a00245aa-32c7-4ad4-a0d1-64f3d6841153
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7561c69a9a0e0186f9564441839816247797998b
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57578233"
---
# <a name="trim-transact-sql"></a>TRIM(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

문자열의 시작 또는 끝에서 공백 문자 `char(32)` 또는 기타 지정되지 않은 문자를 제거합니다.  
 
## <a name="syntax"></a>구문   
```
TRIM ( [ characters FROM ] string ) 
```
[//]: # "[ BOTH | LEADING | TRAILING ]은 아직 사용할 수 없습니다."

## <a name="arguments"></a>인수   

문자   
제거해야 하는 문자가 포함된 비-LOB 문자 형식(`nvarchar`, `varchar`, `nchar` 또는 `char`)의 리터럴, 변수 또는 함수 호출입니다. `nvarchar(max)` 및 `varchar(max)` 형식은 허용되지 않습니다.

string   
문자를 제거해야 하는 모든 문자 형식(`nvarchar`, `varchar`, `nchar` 또는 `char`)의 식입니다.

## <a name="return-types"></a>반환 형식   
양쪽에서 공백 문자 `char(32)` 또는 기타 지정되지 않은 문자가 제거되는 문자열 인수 형식의 문자 식을 반환합니다. 입력 문자열이 `NULL`인 경우 `NULL`을 반환합니다.

## <a name="remarks"></a>Remarks   
기본적으로 `TRIM` 함수는 양쪽에서 공백 문자 `char(32)`를 제거합니다. 이 동작은 `LTRIM(RTRIM(@string))`과 동일합니다. 지정된 문자가 포함된 `TRIM` 함수의 동작은 시작 또는 끝의 문자가 빈 문자열로 대체되는 `REPLACE` 함수의 동작과 동일합니다.


## <a name="examples"></a>예
### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>1.  문자열의 양쪽에서 공백 문자를 제거합니다.   
다음 예에서는 단어 `test`의 앞과 뒤에서 공백을 제거합니다.   
```sql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

`test`


### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>2.  문자열의 양쪽에서 지정된 문자를 제거합니다.   
다음 예에서는 후행 마침표와 후행 공백을 제거합니다.
```sql
SELECT TRIM( '.,! ' FROM  '#     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
`#     test`


## <a name="see-also"></a>참고 항목
 [LEFT&#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT&#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT&#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING&#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  

