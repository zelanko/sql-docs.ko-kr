---
title: STUFF(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STUFF
- STUFF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting characters
- STUFF function
- length characters
- removing characters
- replacing characters
- characters [SQL Server], replacing
- inserting data
ms.assetid: abb0afa9-44f6-42a2-a871-5f471dfb222b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0bb5b030b138fa49f90c77c13e12bf2f64968da3
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71341996"
---
# <a name="stuff-transact-sql"></a>STUFF(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  STUFF 함수는 다른 문자열에 문자열을 삽입합니다. 이 함수는 지정된 시작 위치와 문자 수에 따라 첫 번째 문자열의 문자를 삭제하고 두 번째 문자열을 시작 위치에 삽입합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
STUFF ( character_expression , start , length , replaceWith_expression )  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 문자 데이터의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *character_expression*은 문자나 이진 데이터의 상수, 변수 또는 열일 수 있습니다.  
  
 *start*  
 삭제 및 삽입 시작 위치를 지정하는 정수 값입니다. *start*가 음수 또는 0이면 Null 문자열이 반환됩니다. *start*가 첫 번째 *character_expression*보다 긴 경우 null 문자열이 반환됩니다. *start*는 **bigint** 형식일 수 있습니다.  
  
 *length*  
 삭제할 문자 수를 지정하는 정수입니다. *length*가 음수이면 null 문자열이 반환됩니다. *length*가 첫 번째 *character_expression*보다 긴 경우 마지막 *character_expression*의 마지막 문자까지 삭제됩니다.  *길이*가 0인 경우, *시작* 위치에 삽입이 발생하고 어떤 문자도 삭제되지 않습니다. *length*는 **bigint** 형식일 수 있습니다.

 *replaceWith_expression*  
 문자 데이터의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *character_expression*은 문자나 이진 데이터의 상수, 변수 또는 열일 수 있습니다. 이 식은 *character_expression*에서 *start*부터 *length*문자를 바꿉니다. `NULL`를 *replaceWith_expression*으로 제공할 경우 아무 것도 삽입하지 않고 문제를 제거합니다.   
  
## <a name="return-types"></a>반환 형식  
 지원되는 문자 데이터 형식 중 *character_expression*이 이 있을 경우 문자 데이터를 반환합니다. 지원되는 이진 데이터 형식 중 *character_expression*이 이 있을 경우 이진 데이터를 반환합니다.  
  
## <a name="remarks"></a>설명  
 시작 위치 또는 길이가 음수이거나 시작 위치가 첫 번째 문자열의 길이를 넘어서면 null 문자열이 반환됩니다. 시작 위치가 0일 경우 Null 값이 반환됩니다. 삭제할 길이가 첫 번째 문자열보다 길면 첫 번째 문자열의 첫 번째 문자까지 삭제됩니다.  

결과 값이 반환 유형이 지원하는 최대값보다 크면 오류가 발생합니다.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>보조 문자(서로게이트 쌍)  
 SC 데이터 정렬을 사용할 경우 *character_expression* 및 *replaceWith_expression* 모두 서로게이트 쌍을 포함할 수 있습니다. 길이 매개 변수는 *character_expression*의 각 서로게이트를 단일 문자로 계산합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 첫 문자열 `abcdef`에서 `2` 위치의 `b`부터 세 문자를 삭제하고 삭제 지점에 두 번째 문자열을 삽입하여 만든 문자열을 반환합니다.  
  
```  
SELECT STUFF('abcdef', 2, 3, 'ijklmn');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------   
aijklmnef   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목  
 [CONCAT&#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS&#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME&#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE&#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE&#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG&#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE&#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [TRANSLATE&#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
