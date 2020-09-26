---
description: TRIM(Transact-SQL)
title: TRIM(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jrasnick
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
author: julieMSFT
ms.author: jrasnick
monikerRange: = azure-sqldw-latest||=azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2c2110b541ad06770b1218e3e48e77056085eaeb
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379528"
---
# <a name="trim-transact-sql"></a>TRIM(Transact-SQL)

[!INCLUDE [sqlserver2017-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2017-asdb-asdbmi-asa.md)]

문자열의 시작 또는 끝에서 공백 문자 `char(32)` 및 기타 지정되지 않은 문자를 제거합니다.  

## <a name="syntax"></a>구문

```syntaxsql
-- Syntax for SQL Server and Azure SQL Database
TRIM ( [ characters FROM ] string )
```

```syntaxsql
-- Syntax for Azure Synapse Analytics
TRIM ( string )
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수

문자는 제거해야 하는 문자가 포함된 비-LOB 문자 형식(`nvarchar`, `varchar`, `nchar` 또는 `char`)의 리터럴, 변수 또는 함수 호출입니다. `nvarchar(max)` 및 `varchar(max)` 형식은 허용되지 않습니다.

문자열은 문자를 제거해야 하는 모든 문자 형식(`nvarchar`, `varchar`, `nchar` 또는 `char`)의 식입니다.

## <a name="return-types"></a>반환 형식

양쪽에서 공백 문자 `char(32)` 또는 기타 지정되지 않은 문자가 제거되는 문자열 인수 형식의 문자 식을 반환합니다. 입력 문자열이 `NULL`인 경우 `NULL`을 반환합니다.

## <a name="remarks"></a>설명

기본적으로 `TRIM` 함수는 문자열의 시작과 끝에서 공백 문자를 제거합니다. 이 동작은 `LTRIM(RTRIM(@string))`과 동일합니다.

## <a name="examples"></a>예제

### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>A.  문자열의 양쪽에서 공백 문자를 제거합니다.

다음 예에서는 단어 `test`의 앞과 뒤에서 공백을 제거합니다.

```sql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

```
test
```

### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>B.  문자열의 양쪽에서 지정된 문자를 제거합니다.

다음 예제에서는 단어 `#`의 앞과 `test`의 뒤에서 후행 마침표와 공백을 제거합니다.

```sql
SELECT TRIM( '.,! ' FROM  '     #     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
#     test
```

## <a name="see-also"></a>참고 항목

- [LEFT&#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
- [LTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
- [RIGHT&#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
- [RTRIM&#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
- [STRING_SPLIT&#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
- [SUBSTRING&#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
- [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
