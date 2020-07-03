---
title: sysmail_delete_log_sp (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: db6f15fe8ce2f515bf79211e6db49a135eb6fb3f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890974"
---
# <a name="sysmail_delete_log_sp-transact-sql"></a>sysmail_delete_log_sp(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  데이터베이스 메일 로그에서 이벤트를 삭제합니다. 로그의 모든 이벤트를 삭제하거나 날짜나 유형 기준에 맞는 이벤트만을 삭제할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_delete_log_sp  [ [ @logged_before = ] 'logged_before' ]  
    [, [ @event_type = ] 'event_type' ]  
  
```  
  
## <a name="arguments"></a>인수  
`[ @logged_before = ] 'logged_before'`*Logged_before* 인수에 지정 된 날짜 및 시간 까지의 항목을 삭제 합니다. *logged_before* 은 **datetime** 이며 기본값은 NULL입니다. NULL은 모든 날짜를 나타냅니다.  
  
`[ @event_type = ] 'event_type'`*Event_type*지정 된 유형의 로그 항목을 삭제 합니다. *event_type* 는 **varchar (15)** 이며 기본값은 없습니다. 유효한 항목은 **성공**, **경고**, **오류**및 **정보**입니다. NULL은 모든 이벤트 유형을 나타냅니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **Sysmail_delete_log_sp** 저장 프로시저를 사용 하 여 데이터베이스 메일 로그에서 항목을 영구적으로 삭제할 수 있습니다. 옵션 인수를 사용하여 특정 날짜 및 시간보다 오래된 항목만 삭제할 수 있습니다. 이 인수에 지정된 날짜 및 시간보다 오래된 이벤트는 삭제됩니다. 선택적 인수를 사용 하면 **event_type** 인수로 지정 된 특정 형식의 이벤트만 삭제할 수 있습니다.  
  
 데이터베이스 메일 로그에서 항목을 삭제해도 데이터베이스 메일 테이블의 전자 메일 항목은 삭제되지 않습니다. [Sysmail_delete_mailitems_sp](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md) 를 사용 하 여 데이터베이스 메일 테이블에서 전자 메일을 삭제할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만이 프로시저에 액세스할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-deleting-all-events"></a>A. 모든 이벤트 삭제  
 다음 예에서는 데이터베이스 메일 로그의 모든 이벤트를 삭제합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp ;  
GO  
```  
  
### <a name="b-deleting-the-oldest-events"></a>B. 오래된 이벤트 삭제  
 다음 예에서는 데이터베이스 메일 로그에서 2005년 10월 9일 이전의 이벤트를 삭제합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @logged_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-events-of-a-certain-type"></a>C. 특정 유형의 모든 이벤트 삭제  
 다음 예에서는 데이터베이스 메일 로그의 성공 메시지를 삭제합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @event_type = 'success' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sysmail_event_log &#40;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [Transact-sql&#41;sysmail_delete_mailitems_sp &#40;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)   
 [데이터베이스 메일 메시지 및 이벤트 로그 보관을 처리하는 SQL Server 에이전트 작업 만들기](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
