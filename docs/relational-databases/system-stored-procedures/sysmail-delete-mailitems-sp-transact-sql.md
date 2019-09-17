---
title: sysmail_delete_mailitems_sp (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: ad69cc6933b4f3d51d3b9ec11fad4edd6d555abe
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846643"
---
# <a name="sysmail_delete_mailitems_sp-transact-sql"></a>sysmail_delete_mailitems_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일의 내부 테이블에서 전자 메일 메시지를 영구 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_delete_mailitems_sp  [ [ @sent_before = ] 'sent_before' ]  
    [ , [ @sent_status = ] 'sent_status' ]  
```  
  
## <a name="arguments"></a>인수  
`[ \@sent_before = ] 'sent_before'`*Sent_before* 인수로 제공 된 날짜 및 시간 까지의 전자 메일을 삭제 합니다. *sent_before* 는 **datetime** 이며 기본값은 NULL입니다. NULL은 모든 날짜를 나타냅니다.  
  
`[ \@sent_status = ] 'sent_status'`*Sent_status*에 지정 된 유형의 전자 메일을 삭제 합니다. *sent_status* 은 **varchar (8)** 이며 기본값은 없습니다. 유효한 항목은 **전송**, **보내지**않음, **다시 시도**및 **실패**입니다. NULL은 모든 상태를 나타냅니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 데이터베이스 메일 메시지 및 첨부 파일은 **msdb** 데이터베이스에 저장 됩니다. **Msdb** 가 예상 보다 크게 증가 하는 것을 방지 하 고 조직 문서 보존 프로그램을 따르도록 메시지를 주기적으로 삭제 해야 합니다. **Sysmail_delete_mailitems_sp** 저장 프로시저를 사용 하 여 데이터베이스 메일 테이블에서 전자 메일 메시지를 영구적으로 삭제할 수 있습니다. 옵션 인수를 사용하여 특정 날짜 및 시간보다 오래된 전자 메일만 삭제할 수 있습니다. 이 인수에 지정된 날짜 및 시간보다 오래된 전자 메일은 삭제됩니다. 또 다른 선택적 인수를 사용 하면 **sent_status** 인수로 지정 된 특정 유형의 전자 메일만 삭제할 수 있습니다. **\@Sent_before** 또는 **sent_status 에대한인수를제공해야합니다.\@** 모든 메시지를 삭제 하려면  **\@sent_before = getdate ()** 를 사용 합니다.  
  
 전자 메일을 삭제하면 해당 메시지와 관련된 첨부 파일도 삭제됩니다. 전자 메일을 삭제 해도 **sysmail_event_log**의 해당 항목은 삭제 되지 않습니다. [Sysmail_delete_log_sp](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md) 를 사용 하 여 로그에서 항목을 삭제 합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할 및 **DatabaseMailUserRole**의 멤버에 대해이 저장 프로시저를 실행할 수 있습니다. **Sysadmin** 고정 서버 역할의 멤버는이 프로시저를 실행 하 여 모든 사용자가 보낸 전자 메일을 삭제할 수 있습니다. **DatabaseMailUserRole** 의 멤버는 해당 사용자가 보낸 전자 메일만 삭제할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-deleting-all-e-mails"></a>A. 모든 전자 메일 삭제  
 다음 예에서는 데이터베이스 메일 시스템의 모든 전자 메일을 삭제합니다.  
  
```  
DECLARE @GETDATE datetime  
SET @GETDATE = GETDATE();  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp @sent_before = @GETDATE;  
GO  
```  
  
### <a name="b-deleting-the-oldest-e-mails"></a>2\. 오래된 전자 메일 삭제  
 다음 예에서는 데이터베이스 메일 로그에서 `October 9, 2005` 이전의 전자 메일을 삭제합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp   
    @sent_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-e-mails-of-a-certain-type"></a>3\. 특정 유형의 모든 전자 메일 삭제  
 다음 예에서는 데이터베이스 메일 시스템에서 모든 실패한 전자 메일을 삭제합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp   
    @sent_status = 'failed' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sysmail_allitems &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_event_log &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_mailattachments &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)   
 [데이터베이스 메일 메시지 및 이벤트 로그 보관을 처리하는 SQL Server 에이전트 작업 만들기](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
