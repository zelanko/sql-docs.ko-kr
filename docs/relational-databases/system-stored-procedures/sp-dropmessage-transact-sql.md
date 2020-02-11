---
title: sp_dropmessage (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropmessage_TSQL
- sp_dropmessage
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropmessage
ms.assetid: 17287a15-cdde-43d1-bb18-9f920bc15db8
author: stevestein
ms.author: sstein
ms.openlocfilehash: a8e6a8187936e7a2f824315123937cf9c7eca9c5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933860"
---
# <a name="sp_dropmessage-transact-sql"></a>sp_dropmessage(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에서 지정한 사용자 정의 오류 메시지를 삭제합니다. 사용자 정의 메시지는 **sys. messages** 카탈로그 뷰를 사용 하 여 볼 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropmessage [ @msgnum = ] message_number  
    [ , [ @lang = ] 'language' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @msgnum = ] message_number`삭제할 메시지 번호입니다. *message_number* 는 메시지 번호가 5만 보다 큰 사용자 정의 메시지 여야 합니다. *message_number* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @lang = ] 'language'`삭제할 메시지의 언어입니다. **All** 을 지정 하면 *message_number* 의 모든 언어 버전이 삭제 됩니다. *language* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 및 **serveradmin** 고정 서버 역할의 멤버 자격이 필요 합니다.  
  
## <a name="remarks"></a>설명  
 *Language*에 대해 **all** 을 지정 하지 않은 경우 미국 영어 버전의 메시지를 삭제 하려면 먼저 모든 지역화 된 버전의 메시지를 삭제 해야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-a-user-defined-message"></a>A. 사용자 정의 메시지 삭제  
 다음 예에서는 **sys. 메시지**의 사용자 정의 메시지 번호 `50001`를 삭제 합니다.  
  
```  
USE master;  
GO  
EXEC sp_dropmessage 50001;  
```  
  
### <a name="b-dropping-a-user-defined-message-that-includes-a-localized-version"></a>B. 다른 언어 버전을 포함하는 사용자 정의 메시지 삭제  
 다음 예에서는 메시지의 해당 언어 버전을 포함한 메시지 번호가 `60000`인 사용자 정의 메시지를 삭제합니다.  
  
```  
USE master;  
GO  
  
-- Create a user-defined message in U.S. English  
EXEC sp_addmessage   
    @msgnum = 60000,  
    @severity = 16,  
    @msgtext = N'The item named %s already exists in %s.',   
    @lang = 'us_english';  
  
-- Create a localized version of the same message.  
EXEC sp_addmessage   
    @msgnum = 60000,  
    @severity = 16,  
    @msgtext = N'L''élément nommé %1! existe déjà dans %2!',  
    @lang = 'French';  
GO  
  
-- This statement will fail as long as the localized version  
-- of the message exists.  
EXEC sp_dropmessage 60000;  
GO  
  
-- This statement will drop the message.  
EXEC sp_dropmessage  
    @msgnum = 60000,  
    @lang = 'all';  
GO  
```  
  
### <a name="c-dropping-a-localized-version-of-a-user-defined-message"></a>C. 사용자 정의 메시지의 다른 언어 버전 삭제  
 다음 예에서는 전체 메시지를 삭제하지 않고 메시지 번호가 `60000`인 사용자 정의 메시지의 다른 언어 버전을 삭제합니다.  
  
```  
USE master;  
GO  
  
-- Create a user-defined message in U.S. English  
EXEC sp_addmessage   
    @msgnum = 60000,  
    @severity = 16,  
    @msgtext = N'The item named %s already exists in %s.',   
    @lang = 'us_english';  
  
-- Create a localized version of the same message.  
EXEC sp_addmessage   
    @msgnum = 60000,  
    @severity = 16,  
    @msgtext = N'L''élément nommé %1! existe déjà dans %2!',  
    @lang = 'French';  
GO  
-- This statement will remove only the localized version of the   
-- message.  
EXEC sp_dropmessage  
    @msgnum = 60000,  
    @lang = 'French';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [Transact-sql&#41;sp_addmessage &#40;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [Transact-sql&#41;sp_altermessage &#40;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [FORMATMESSAGE &#40;Transact-sql&#41;](../../t-sql/functions/formatmessage-transact-sql.md)   
 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
