---
title: TRIM (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TRIM
- TRIM_TSQL
dev_langs: TSQL
helpviewer_keywords: TRIM function
ms.assetid: a00245aa-32c7-4ad4-a0d1-64f3d6841153
caps.latest.revision: "4"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b7ea9bb6828182ee0cbc5d0ebef1065564bf03df
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="trim-transact-sql"></a>TRIM (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

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
```sql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

`test`


### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>2.  지정 된 문자열의 양쪽 모두에서 문자 제거   
다음 예제에서는 뒤에 마침표 및 후행 공백을 제거합니다.
```sql
SELECT TRIM( '.,! ' FROM  '#     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
`#     test`


## <a name="see-also"></a>관련 항목:
[문자열 함수 (Transact SQL)](../../t-sql/functions/string-functions-transact-sql.md)   
[LTRIM (Transact SQL)](../../t-sql/functions/ltrim-transact-sql.md)   
[RTRIM (Transact SQL)](../../t-sql/functions/rtrim-transact-sql.md)   
[REPLACE (Transact SQL)](../../t-sql/functions/replace-transact-sql.md)   
