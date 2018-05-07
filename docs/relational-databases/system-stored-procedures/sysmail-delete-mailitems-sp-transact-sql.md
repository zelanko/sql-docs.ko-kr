---
title: sysmail_delete_mailitems_sp (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_delete_mailitems_sp_TSQL
- sysmail_delete_mailitems_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_mailitems_sp
ms.assetid: f87c9f4a-bda1-4bce-84b2-a055a3229ecd
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca730dc633f8aad10aa79fd34bb7e94870a48076
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
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
 [ **@sent_before=** ] **'***sent_before***'**  
 날짜와으로 제공 된 시간 까지의 전자 메일을 삭제는 *sent_before* 인수입니다. *sent_before* 은 **datetime** 기본값으로 null입니다. NULL은 모든 날짜를 나타냅니다.  
  
 [ **@sent_status=** ] **'***sent_status***'**  
 지정 된 형식의 전자 메일을 삭제 *sent_status*합니다. *sent_status* 은 **varchar(8)** 이며 기본값은 없습니다. 유효한 항목은 **전송**, **보내지 않은**, **다시 시도**, 및 **실패**합니다. NULL은 모든 상태를 나타냅니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 데이터베이스 메일 메시지 및 첨부 파일에 저장 됩니다는 **msdb** 데이터베이스입니다. 방지 하기 위해 메시지를 주기적으로 삭제 해야 **msdb** 예상 보다 더 크게 증가 하 고 조직의 문서 보존 프로그램 준수 하도록 합니다. 사용 하 여 **sysmail_delete_mailitems_sp** 저장 프로시저를 데이터베이스 메일 테이블에서 전자 메일 메시지를 영구적으로 삭제 합니다. 옵션 인수를 사용하여 특정 날짜 및 시간보다 오래된 전자 메일만 삭제할 수 있습니다. 이 인수에 지정된 날짜 및 시간보다 오래된 전자 메일은 삭제됩니다. 다른 선택적 인수를 사용 하면 특정 형식으로 지정 된 전자 메일만 삭제할 수 있습니다는 **sent_status** 인수입니다. 인수에 대해 제공 해야 **@sent_before** 또는 **@sent_status**합니다. 사용 하 여 모든 메시지를 삭제 하려면  **@sent_before getdate () =** 합니다.  
  
 전자 메일을 삭제하면 해당 메시지와 관련된 첨부 파일도 삭제됩니다. 전자 메일을 삭제 해도의 해당 항목은 삭제 되지 않습니다 **sysmail_event_log**합니다. 사용 하 여 [sysmail_delete_log_sp](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md) 를 로그에서 항목을 삭제 합니다.  
  
## <a name="permissions"></a>Permissions  
 기본적으로이 저장된 프로시저는 실행에 대 한 구성원에 게 부여 해제는 **sysadmin** 고정된 서버 역할 및 **DatabaseMailUserRole**합니다. 멤버는 **sysadmin** 고정된 서버 역할에서 모든 사용자가 보낸 전자 메일을 삭제 하려면이 절차를 실행할 수 있습니다. 멤버 **DatabaseMailUserRole** 해당 사용자가 보내는 전자 메일만 삭제할 수 있습니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [sysmail_allitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_event_log &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_mailattachments &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)   
 [데이터베이스 메일 메시지 및 이벤트 로그 보관을 처리하는 SQL Server 에이전트 작업 만들기](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
