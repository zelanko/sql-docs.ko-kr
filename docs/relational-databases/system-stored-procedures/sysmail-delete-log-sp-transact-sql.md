---
title: sysmail_delete_log_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_log_sp_TSQL
- sysmail_delete_log_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_log_sp
ms.assetid: e94b37a1-70ad-46a5-86c0-721892156f7c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a1a61fa55fc9f2b1209d0f7da7f483c0fedce07f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649212"
---
# <a name="sysmaildeletelogsp-transact-sql"></a>sysmail_delete_log_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일 로그에서 이벤트를 삭제합니다. 로그의 모든 이벤트를 삭제하거나 날짜나 유형 기준에 맞는 이벤트만을 삭제할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_delete_log_sp  [ [ @logged_before = ] 'logged_before' ]  
    [, [ @event_type = ] 'event_type' ]  
  
```  
  
## <a name="arguments"></a>인수  
 [ **@logged_before** =] **'***logged_before***'**  
 날짜 및 지정 된 시간 까지의 항목을 삭제 합니다 *logged_before* 인수입니다. *logged_before* 됩니다 **datetime** 기본적으로 null입니다. NULL은 모든 날짜를 나타냅니다.  
  
 [ **@event_type** = ] **'***event_type***'**  
 로그로 지정 된 형식의 항목을 삭제 합니다 *event_type*합니다. *event_type* 됩니다 **varchar(15)** 기본값은 없습니다. 유효한 항목은 **성공**, **경고**합니다 **오류**, 및 **정보**합니다. NULL은 모든 이벤트 유형을 나타냅니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 사용 된 **sysmail_delete_log_sp** 저장 프로시저를 데이터베이스 메일 로그에서 항목을 영구적으로 삭제 합니다. 옵션 인수를 사용하여 특정 날짜 및 시간보다 오래된 항목만 삭제할 수 있습니다. 이 인수에 지정된 날짜 및 시간보다 오래된 이벤트는 삭제됩니다. 선택적 인수를 사용 하면 특정 형식으로 지정 된 이벤트만 삭제할 수 있습니다 합니다 **event_type** 인수입니다.  
  
 데이터베이스 메일 로그에서 항목을 삭제해도 데이터베이스 메일 테이블의 전자 메일 항목은 삭제되지 않습니다. 사용 하 여 [sysmail_delete_mailitems_sp](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md) 데이터베이스 메일 테이블에서 전자 메일을 삭제 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할에서이 절차를 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-deleting-all-events"></a>1. 모든 이벤트 삭제  
 다음 예에서는 데이터베이스 메일 로그의 모든 이벤트를 삭제합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp ;  
GO  
```  
  
### <a name="b-deleting-the-oldest-events"></a>2. 오래된 이벤트 삭제  
 다음 예에서는 데이터베이스 메일 로그에서 2005년 10월 9일 이전의 이벤트를 삭제합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @logged_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-events-of-a-certain-type"></a>3. 특정 유형의 모든 이벤트 삭제  
 다음 예에서는 데이터베이스 메일 로그의 성공 메시지를 삭제합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @event_type = 'success' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sysmail_event_log &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_delete_mailitems_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)   
 [데이터베이스 메일 메시지 및 이벤트 로그 보관을 처리하는 SQL Server 에이전트 작업 만들기](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
