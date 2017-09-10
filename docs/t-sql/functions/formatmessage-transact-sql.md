---
title: FORMATMESSAGE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FORMATMESSAGE
- FORMATMESSAGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmessages system table
- sys.messages catalog view
- FORMATMESSAGE function
- messages [SQL Server], formats
- errors [SQL Server], formats
ms.assetid: 83f18102-2035-4a87-acd0-8d96d03efad5
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 071f6def07baf0b74919fd5ce93e65494877dda0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="formatmessage-transact-sql"></a>FORMATMESSAGE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  제공 된 문자열 또는 sys.messages에 기존 메시지에서 메시지를 생성합니다. FORMATMESSAGE의 기능은 RAISERROR 문의 기능과 유사합니다. 단, RAISERROR는 메시지를 즉시 인쇄하는 반면 FORMATMESSAGE는 추가 처리를 위해 서식이 지정된 메시지를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
FORMATMESSAGE ( { msg_number  | ' msg_string ' } , [ param_value [ ,...n ] ] )  
```  
  
## <a name="arguments"></a>인수  
 *msg_number*  
 Sys.messages에 저장 된 메시지의 ID입니다. 경우 *msg_number* 가 < = 13000 또는 메시지 sys.messages에 없는 경우 NULL이 반환 됩니다.  
  
 *msg_string*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 자리 표시자에 작은따옴표와 매개 변수 값을 포함 하는 문자열 묶인입니다. 오류 메시지는 최대 2,047자까지 지정할 수 있습니다. 메시지의 문자가 2,048자 이상이면 처음 2,044자만 표시되고 메시지가 잘렸음을 나타내기 위해 줄임표가 추가됩니다. 내부 저장 방식의 특성상 대체 매개 변수는 출력에 표시되는 것보다 더 많은 수의 문자를 사용합니다.  메시지 문자열의 구조와 문자열에 매개 변수를 사용 하는 방법에 대 한 정보에 대 한 설명을 참조는 *msg_str* 인수 [RAISERROR &#40; Transact SQL &#41; ](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 *param_value*  
 메시지에 사용할 매개 변수 값입니다. 둘 이상의 매개 변수 값을 사용할 수 있습니다. 메시지에 자리 표시자 변수가 표시되는 순서대로 값을 지정해야 합니다. 값의 최대 개수는 20개입니다.  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar**  
  
## <a name="remarks"></a>주의  
 FORMATMESSAGE는 RAISERROR 문과 유사하게 메시지의 자리 표시자 변수를 제공된 매개 변수 값으로 대체하여 메시지를 편집합니다. 오류 메시지와 편집 프로세스에 사용할 수 있는 자리 표시자에 대 한 자세한 내용은 참조 하십시오. [RAISERROR &#40; Transact SQL &#41; ](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 FORMATMESSAGE는 사용자의 현재 언어로 된 메시지를 찾습니다. 메시지의 해당 언어 버전이 없으면 미국 영어를 사용합니다.  
  
 해당 언어 메시지의 경우 제공된 매개 변수 값이 반드시 미국 영어 버전의 매개 변수 자리 표시자와 일치해야 합니다. 즉, 해당 언어 버전의 매개 변수 1은 미국 영어 버전의 매개 변수 1과, 매개 변수 2는 매개 변수 2와 일치하는 방식으로 모두 일치해야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-example-with-a-message-number"></a>1. 메시지 번호의 예  
 다음 예제에서는 복제 메시지 `20009` 으로 sys.messages에 저장 됨을 "의 아티클 '%s' 없습니다 추가할 수 없습니다 게시 '%s'에." FORMATMESSAGE는 `First Variable` 및 `Second Variable` 값을 매개 변수 자리 표시자로 대체합니다. 결과 문자열을 로컬 변수에 저장 됨 "의 아티클 '첫 번째 변수' 없습니다 추가할 수 없습니다는 게시에 '두 번째 변수'.", `@var1`합니다.  
  
```  
SELECT text FROM sys.messages WHERE message_id = 20009 AND language_id = 1033;  
DECLARE @var1 VARCHAR(200);   
SELECT @var1 = FORMATMESSAGE(20009, 'First Variable', 'Second Variable');   
SELECT @var1;  
```  
  
### <a name="b-example-with-a-message-string"></a>2. 메시지 문자열의 예  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 다음 예제에서는 문자열을 입력 변수로 사용 합니다.  
  
```  
SELECT FORMATMESSAGE('This is the %s and this is the %s.', 'first variable', 'second variable') AS Result;  
```  
  
 이 반환 됩니다.`This is the first variable and this is the second variable.`  
  
### <a name="c-additional-message-string-formatting-examples"></a>3. 추가 메시지 문자열 형식 지정 예제  
 다음 예에서는 다양 한 서식 옵션을 보여 줍니다.  
  
```  
SELECT FORMATMESSAGE('Signed int %i, %d %i, %d, %+i, %+d, %+i, %+d', 5, -5, 50, -50, -11, -11, 11, 11);  
SELECT FORMATMESSAGE('Signed int with leading zero %020i', 5);  
SELECT FORMATMESSAGE('Signed int with leading zero 0 %020i', -55);  
SELECT FORMATMESSAGE('Unsigned int %u, %u', 50, -50);  
SELECT FORMATMESSAGE('Unsigned octal %o, %o', 50, -50);  
SELECT FORMATMESSAGE('Unsigned hexadecimal %x, %X, %X, %X, %x', 11, 11, -11, 50, -50);  
SELECT FORMATMESSAGE('Unsigned octal with prefix: %#o, %#o', 50, -50);  
SELECT FORMATMESSAGE('Unsigned hexadecimal with prefix: %#x, %#X, %#X, %X, %x', 11, 11, -11, 50, -50);  
SELECT FORMATMESSAGE('Hello %s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %20s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %-20s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %20s!', 'TEST');  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Throw&#40; Transact SQL &#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [sp_addmessage &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [Raiserror&#40; Transact SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  

