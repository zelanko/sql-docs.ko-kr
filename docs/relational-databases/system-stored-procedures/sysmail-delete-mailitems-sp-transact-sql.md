---
title: sysmail_delete_mailitems_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_mailitems_sp_TSQL
- sysmail_delete_mailitems_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_mailitems_sp
ms.assetid: f87c9f4a-bda1-4bce-84b2-a055a3229ecd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3a8549d33b000744f4d8430ee306e0083455894c
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531765"
---
# <a name="sysmaildeletemailitemssp-transact-sql"></a>sysmail_delete_mailitems_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일의 내부 테이블에서 전자 메일 메시지를 영구 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_delete_mailitems_sp  [ [ @sent_before = ] 'sent_before' ]  
    [ , [ @sent_status = ] 'sent_status' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @sent_before = ] 'sent_before'` 날짜 및 시간으로 제공 된 최대 전자 메일을 삭제 합니다 *sent_before* 인수입니다. *sent_before* 됩니다 **datetime** 기본적으로 null입니다. NULL은 모든 날짜를 나타냅니다.  
  
`[ @sent_status = ] 'sent_status'` 지정 된 형식의 전자 메일을 삭제 *sent_status*합니다. *sent_status* 됩니다 **varchar(8)** 기본값은 없습니다. 유효한 항목은 **전송**를 **보내지 않은**를 **을 다시 시도**, 및 **실패**합니다. NULL은 모든 상태를 나타냅니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 메일 메시지 및 첨부 파일에 저장 되는 **msdb** 데이터베이스입니다. 메시지를 방지 하려면에 주기적으로 삭제 해야 **msdb** 예상 보다 커지는 및 조직의 문서 보존 프로그램 사용을 준수 하도록 합니다. 사용 된 **sysmail_delete_mailitems_sp** 저장 프로시저를 데이터베이스 메일 테이블에서 전자 메일 메시지를 영구적으로 삭제 합니다. 옵션 인수를 사용하여 특정 날짜 및 시간보다 오래된 전자 메일만 삭제할 수 있습니다. 이 인수에 지정된 날짜 및 시간보다 오래된 전자 메일은 삭제됩니다. 다른 선택적 인수를 사용 하면 특정 형식으로 지정 된 전자 메일만 삭제할 수 있습니다 합니다 **sent_status** 인수입니다. 인수에 대해 제공 해야 합니다 **@sent_before** 하거나 **@sent_status**합니다. 모든 메시지를 삭제 하려면 사용 하 여  **@sent_before getdate () =** 합니다.  
  
 전자 메일을 삭제하면 해당 메시지와 관련된 첨부 파일도 삭제됩니다. 전자 메일을 삭제 해도의 해당 항목은 삭제 되지 않습니다 **sysmail_event_log**합니다. 사용 하 여 [sysmail_delete_log_sp](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md) 로그에서 항목을 삭제 합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로이 저장된 프로시저는 실행에 대 한 멤버에 게 부여 해제 합니다 **sysadmin** 고정된 서버 역할 및 **DatabaseMailUserRole**합니다. 멤버는 **sysadmin** 고정된 서버 역할에서 모든 사용자가 보낸 전자 메일을 삭제 하는이 절차를 실행할 수 있습니다. 멤버인 **DatabaseMailUserRole** 해당 사용자가 보낸 전자 메일만 삭제할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-deleting-all-e-mails"></a>1. 모든 전자 메일 삭제  
 다음 예에서는 데이터베이스 메일 시스템의 모든 전자 메일을 삭제합니다.  
  
```  
DECLARE @GETDATE datetime  
SET @GETDATE = GETDATE();  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp @sent_before = @GETDATE;  
GO  
```  
  
### <a name="b-deleting-the-oldest-e-mails"></a>2. 오래된 전자 메일 삭제  
 다음 예에서는 데이터베이스 메일 로그에서 `October 9, 2005` 이전의 전자 메일을 삭제합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp   
    @sent_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-e-mails-of-a-certain-type"></a>3. 특정 유형의 모든 전자 메일 삭제  
 다음 예에서는 데이터베이스 메일 시스템에서 모든 실패한 전자 메일을 삭제합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp   
    @sent_status = 'failed' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sysmail_allitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_event_log &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_mailattachments &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)   
 [데이터베이스 메일 메시지 및 이벤트 로그 보관을 처리하는 SQL Server 에이전트 작업 만들기](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
