---
title: QUOTENAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 61a2da2f81701a32da0545a5b9b06b6e9ee8cd2c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="quotename-transact-sql"></a>QUOTENAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  입력 문자열이 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구분 식별자가 되도록 구분 기호가 추가된 유니코드 문자열을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
QUOTENAME ( 'character_string' [ , 'quote_character' ] )   
```  
  
## <a name="arguments"></a>인수  
 '*character_string*'  
 유니코드 문자 데이터로 이루어진 문자열입니다. *character_string*은 **sysname**이며 128자로 제한됩니다. 128자가 넘는 문자열을 입력하면 NULL이 반환됩니다.  
  
 '*quote_character*'  
 구분 기호로 사용되는 단일 문자 문자열입니다. 작은 따옴표( **'** ), 왼쪽 또는 오른쪽 대괄호( **[]** ) 또는 큰 따옴표( **"** )일 수 있습니다. *quote_character*를 지정하지 않은 경우 대괄호가 사용됩니다.  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar(258)**  
  
## <a name="examples"></a>예  
 다음 예에서는 `abc[]def` 문자열에 `[` 및 `]` 문자를 추가하여 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구분 식별자로 만듭니다.  
  
```  
SELECT QUOTENAME('abc[]def');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc[]]def]  
  
(1 row(s) affected)  
```  
  
 `abc[]def` 문자열에서 오른쪽 대괄호는 이중으로 사용되었는데, 이것은 이스케이프 문자를 나타내기 위한 것입니다.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 `abc def` 문자열에 `[` 및 `]` 문자를 추가하여 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구분 식별자로 만듭니다.  
  
```  
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
  
  

