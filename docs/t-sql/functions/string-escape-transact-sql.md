---
title: STRING_ESCAPE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/25/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRING_ESCAPE
- STRING_ESCAPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_ESCAPE function
ms.assetid: 2163bc7a-3816-4304-9c40-8954804f5465
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 41f969e292eff76c9a836ccd3177519d88e355ac
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="stringescape-transact-sql"></a>STRING_ESCAPE (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  텍스트에서 특수 문자를 이스케이프 하 고 이스케이프 문자가 있는 텍스트를 반환 합니다. **STRING_ESCAPE** 는 결정적 함수입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
STRING_ESCAPE( text , type )  
```  
  
## <a name="arguments"></a>인수  
 *text*  
 이 **nvarchar**[식](../../t-sql/language-elements/expressions-transact-sql.md) 이스케이프 해야 하는 개체를 나타내는 식입니다.  
  
 *type*  
 적용 되는 이스케이프 규칙입니다. 현재 지원 되는 값은 `'json'`합니다.  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar (max)** 이스케이프 된 특수 한 및 제어 문자가 포함 된 텍스트입니다. 현재 **STRING_ESCAPE** 만 다음 표에 표시 된 JSON 특수 문자를 이스케이프할 수 있습니다.  
  
|특수 문자|인코딩된 시퀀스|  
|-----------------------|----------------------|  
|따옴표(")|\\"|  
|역방향 solidus (\\)|\\\|  
|Solidus (/)|\\/|  
|백스페이스|\b|  
|용지 공급|\f|  
|줄 바꿈|\n|  
|캐리지 리턴|\r|  
|가로 탭|\t|  
  
|제어 문자|인코딩된 시퀀스|  
|-----------------------|----------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|...|...|  
|CHAR(31)|\u001f|  
  
## <a name="remarks"></a>주의  
  
## <a name="examples"></a>예  
  
### <a name="a--escape-text-according-to-the-json-formatting-rules"></a>1.  JSON 서식 설정 규칙에 따라 텍스트를 이스케이프 합니다.  
 다음 쿼리는 JSON 규칙을 사용 하는 특수 문자를 이스케이프 하 고 이스케이프 된 텍스트를 반환 합니다.  
  
```  
SELECT STRING_ESCAPE('\   /  
\\    "     ', 'json') AS escapedText;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
escapedText  
-------------------------------------------------------------  
\\\t\/\n\\\\\t\"\t
```  
  
### <a name="b-format-json-object"></a>2. JSON 개체의 서식  
 다음 쿼리는 숫자 및 문자열 변수에서 JSON 텍스트를 만들고 변수에 있는 특수 한 JSON 문자를 이스케이프 합니다.  
  
```  
SET @json = FORMATMESSAGE('{ "id": %d,"name": "%s", "surname": "%s" }',   
    17, STRING_ESCAPE(@name,'json'), STRING_ESCAPE(@surname,'json') );  
```  
  
## <a name="see-also"></a>관련 항목:  
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [부분 문자열 &#40; Transact SQL &#41;](../../t-sql/functions/substring-transact-sql.md)  
  
  

