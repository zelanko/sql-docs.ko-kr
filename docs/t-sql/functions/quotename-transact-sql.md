---
description: QUOTENAME(Transact-SQL)
title: QUOTENAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- QUOTENAME_TSQL
- QUOTENAME
dev_langs:
- TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- input strings [SQL Server]
- Unicode [SQL Server], delimited identifiers
- QUOTENAME function
- valid identifiers [SQL Server]
ms.assetid: 34d47f1e-2ac7-4890-8c9c-5f60f115e076
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: caf85043caf455285e4030e3715dca8675d99d7d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481984"
---
# <a name="quotename-transact-sql"></a>QUOTENAME(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  입력 문자열이 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구분 식별자가 되도록 구분 기호가 추가된 유니코드 문자열을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
QUOTENAME ( 'character_string' [ , 'quote_character' ] )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 '*character_string*'  
 유니코드 문자 데이터로 이루어진 문자열입니다. *character_string* 은 **sysname** 이며 128자로 제한됩니다. 128자가 넘는 문자열을 입력하면 NULL이 반환됩니다.  
  
 '*quote_character*'  
 구분 기호로 사용되는 단일 문자 문자열입니다. 작은따옴표( **'** ), 왼쪽 또는 오른쪽 대괄호( **[]** ), 큰따옴표( **"** ), 왼쪽 또는 오른쪽 괄호( **()** ), 초과 또는 미만 기호( **><** ), 왼쪽 또는 오른쪽 중괄호( **{}** ) 또는 억음 악센트 기호( **\`** )일 수 있습니다. 허용되지 않는 문자를 입력하는 경우 NULL이 반환됩니다. *quote_character* 를 지정하지 않은 경우 대괄호가 사용됩니다.  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar(258)**  
  
## <a name="examples"></a>예  
 다음 예에서는 `abc[]def` 문자열에 `[` 및 `]` 문자를 추가하여 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구분 식별자로 만듭니다.  
  
```sql
SELECT QUOTENAME('abc[]def');
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc[]]def]
  
(1 row(s) affected)  
```  
  
 `abc[]def` 문자열에서 오른쪽 대괄호는 이중으로 사용되었는데, 이것은 이스케이프 문자를 나타내기 위한 것입니다.  
 
 다음 예에서는 열의 이름을 지정하는 데 사용할 따옴표 붙은 문자열을 준비합니다.  
  
```sql
DECLARE @columnName NVARCHAR(255)='user''s "custom" name'
DECLARE @sql NVARCHAR(MAX) = 'SELECT FirstName AS ' + QUOTENAME(@columnName) + ' FROM dbo.DimCustomer'

EXEC sp_executesql @sql
```
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 `abc def` 문자열에 `[` 및 `]` 문자를 추가하여 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구분 식별자로 만듭니다.  
  
```sql
SELECT QUOTENAME('abc def');   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc def]  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목  
 [PARSENAME&#40;Transact-SQL&#41;](../../t-sql/functions/parsename-transact-sql.md)  
 [CONCAT&#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS&#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [REPLACE&#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE&#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG&#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE&#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF&#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE&#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
