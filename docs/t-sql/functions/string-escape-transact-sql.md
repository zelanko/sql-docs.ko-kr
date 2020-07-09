---
title: STRING_ESCAPE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STRING_ESCAPE
- STRING_ESCAPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_ESCAPE function
ms.assetid: 2163bc7a-3816-4304-9c40-8954804f5465
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 491336ff6f405306fe7d74bd97769981ed909bfa
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85995087"
---
# <a name="string_escape-transact-sql"></a>STRING_ESCAPE(Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

텍스트의 특수 문자를 이스케이프하고 이스케이프 문자가 포함된 텍스트를 반환합니다. **STRING_ESCAPE**는 SQL Server 2016에서 도입된 결정 함수입니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql
STRING_ESCAPE( text , type )  
```  
  
## <a name="arguments"></a>인수

 *text*  
 이스케이프해야 하는 개체를 나타내는 **nvarchar**[expression](../../t-sql/language-elements/expressions-transact-sql.md) 식입니다.  
  
 *type*  
 적용될 규칙을 이스케이프합니다. 현재 지원되는 값은 `'json'`입니다.  
  
## <a name="return-types"></a>반환 형식

 이스케이프된 특수 및 제어 문자가 포함된 **nvarchar(max)** 텍스트입니다. 현재 **STRING_ESCAPE**는 다음 표에 나와 있는 JSON 특수 문자만 이스케이프할 수 있습니다.  
  
|특수 문자|인코딩된 시퀀스|  
|-----------------------|----------------------|  
|따옴표(")|\\"|  
|백슬래시(\\)| \\\\ |  
|슬래시(/)|\\/|  
|백스페이스|\b|  
|용지 공급|\f|  
|새 줄|\n|  
|캐리지 리턴|\r|  
|가로 탭|\t|  
  
|제어 문자|인코딩된 시퀀스|  
|-----------------------|----------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|...|...|  
|CHAR(31)|\u001f|  
  
## <a name="remarks"></a>설명  
  
## <a name="examples"></a>예  
  
### <a name="a--escape-text-according-to-the-json-formatting-rules"></a>A.  JSON 서식 지정 규칙에 따라 텍스트를 이스케이프합니다

 다음 쿼리는 JSON 규칙을 사용하여 특수 문자를 이스케이프하며 이스케이프된 텍스트를 반환합니다.  
  
```sql
SELECT STRING_ESCAPE('\   /  
\\    "     ', 'json') AS escapedText;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
escapedText  
-------------------------------------------------------------  
\\\t\/\n\\\\\t\"\t
```  
  
### <a name="b-format-json-object"></a>B. JSON 개체 서식 지정

 다음 쿼리는 숫자 및 문자열 변수에서 JSON 텍스트를 만들며 변수의 모든 특수 JSON 문자를 이스케이프합니다.  
  
```
SET @json = FORMATMESSAGE('{ "id": %d,"name": "%s", "surname": "%s" }',
    17, STRING_ESCAPE(@name,'json'), STRING_ESCAPE(@surname,'json') );  
```  
  
## <a name="see-also"></a>참고 항목

- [CONCAT&#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
- [CONCAT_WS&#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
- [FORMATMESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
- [QUOTENAME&#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
- [REPLACE&#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
- [REVERSE&#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
- [STRING_AGG&#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
- [STUFF&#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
- [TRANSLATE&#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
- [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
