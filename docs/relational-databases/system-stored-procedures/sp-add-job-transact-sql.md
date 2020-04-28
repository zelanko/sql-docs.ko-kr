---
title: sp_add_job (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_job_TSQL
- sp_add_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_job
ms.assetid: 6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7752b8fcb453f545c357c529774d570e41201ed1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72381907"
---
# <a name="sp_add_job-transact-sql"></a>sp_add_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  SQL 에이전트 서비스에서 실행 하는 새 작업을 추가 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
 > [!IMPORTANT]  
 > [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)대부분의 SQL Server 에이전트 기능은 현재 지원 되지 않습니다. 자세한 내용은 [Azure SQL Database Managed Instance t-sql 차이점 SQL Server을](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) 참조 하세요.
 
## <a name="syntax"></a>구문  
  
```  
  
sp_add_job [ @job_name = ] 'job_name'  
     [ , [ @enabled = ] enabled ]   
     [ , [ @description = ] 'description' ]   
     [ , [ @start_step_id = ] step_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @category_id = ] category_id ]   
     [ , [ @owner_login_name = ] 'login' ]   
     [ , [ @notify_level_eventlog = ] eventlog_level ]   
     [ , [ @notify_level_email = ] email_level ]   
     [ , [ @notify_level_netsend = ] netsend_level ]   
     [ , [ @notify_level_page = ] page_level ]   
     [ , [ @notify_email_operator_name = ] 'email_name' ]   
          [ , [ @notify_netsend_operator_name = ] 'netsend_name' ]   
     [ , [ @notify_page_operator_name = ] 'page_name' ]   
     [ , [ @delete_level = ] delete_level ]   
     [ , [ @job_id = ] job_id OUTPUT ]   
```  
  
## <a name="arguments"></a>인수  
`[ @job_name = ] 'job_name'`작업의 이름입니다. 이름은 고유 해야 하며 백분율 (**%**) 문자를 포함할 수 없습니다. *job_name*은 **nvarchar (128)** 이며 기본값은 없습니다.  
  
`[ @enabled = ] enabled`추가 된 작업의 상태를 나타냅니다. *enabled*는 **tinyint**이며 기본값은 1 (사용)입니다. **0**인 경우 작업이 활성화 되지 않으며 일정에 따라 실행 되지 않습니다. 그러나 수동으로 실행할 수도 있습니다.  
  
`[ @description = ] 'description'`작업에 대 한 설명입니다. *description* 은 **nvarchar (512)** 이며 기본값은 NULL입니다. *설명을* 생략 하면 "사용할 수 있는 설명이 없습니다."가 사용 됩니다.  
  
`[ @start_step_id = ] step_id`작업에 대해 실행할 첫 번째 단계의 id입니다. *step_id*은 **int**이며 기본값은 1입니다.  
  
`[ @category_name = ] 'category'`작업의 범주입니다. *category*는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @category_id = ] category_id`작업 범주를 지정 하는 언어 독립적 메커니즘입니다. *category_id*은 **int**이며 기본값은 NULL입니다.  
  
`[ @owner_login_name = ] 'login'`작업을 소유 하는 로그인의 이름입니다. *login*은 **sysname**이며 기본값은 현재 로그인 이름으로 해석 되는 NULL입니다. **Sysadmin** 고정 서버 역할의 멤버만 ** \@owner_login_name**에 대 한 값을 설정 하거나 변경할 수 있습니다. **Sysadmin** 역할의 멤버가 아닌 사용자가 ** \@owner_login_name**값을 설정 하거나 변경 하는 경우이 저장 프로시저의 실행이 실패 하 고 오류가 반환 됩니다.  
  
`[ @notify_level_eventlog = ] eventlog_level`Microsoft Windows 응용 프로그램 로그에서이 작업에 대 한 항목을 저장할 시간을 나타내는 값입니다. *eventlog_level*은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|안 함|  
|**1**|성공한 경우|  
|**2** (기본값)|실패한 경우|  
|**3**|항상|  
  
`[ @notify_level_email = ] email_level`이 작업이 완료 될 때 전자 메일을 보낼 시간을 나타내는 값입니다. *email_level*는 **int**이며 기본값은 never를 나타내는 **0**입니다. *email_level*는 *eventlog_level*와 동일한 값을 사용 합니다.  
  
`[ @notify_level_netsend = ] netsend_level`이 작업이 완료 될 때 네트워크 메시지를 보낼 시간을 나타내는 값입니다. *netsend_level*는 **int**이며 기본값은 never를 나타내는 **0**입니다. *netsend_level* 는 *eventlog_level*와 동일한 값을 사용 합니다.  
  
`[ @notify_level_page = ] page_level`이 작업이 완료 될 때 페이지를 보낼지 여부를 나타내는 값입니다. *page_level*는 **int**이며 기본값은 never를 나타내는 **0**입니다. *page_level*는 *eventlog_level*와 동일한 값을 사용 합니다.  
  
`[ @notify_email_operator_name = ] 'email_name'`*Email_level* 에 도달 했을 때 전자 메일을 보낼 사람의 전자 메일 이름입니다. *email_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @notify_netsend_operator_name = ] 'netsend_name'`이 작업이 완료 될 때 네트워크 메시지가 전송 되는 운영자의 이름입니다. *netsend_name*는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @notify_page_operator_name = ] 'page_name'`이 작업이 완료 될 때 페이지로 이동할 사람의 이름입니다. *page_name*는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @delete_level = ] delete_level`작업을 삭제할 시간을 나타내는 값입니다. *delete_value*은 **int**이며 기본값은 0으로,이는 never를 의미 합니다. *delete_level*는 *eventlog_level*와 동일한 값을 사용 합니다.  
  
> [!NOTE]  
>  *Delete_level* 가 **3**이면 작업에 대해 정의 된 일정에 관계 없이 작업이 한 번만 실행 됩니다. 또한 작업 자체를 삭제하는 경우 작업에 대한 모든 기록도 함께 삭제됩니다.  
  
`[ @job_id = ] _job_idOUTPUT`성공적으로 만들어진 경우 작업에 할당 된 작업 id 번호입니다. *job_id*은 **uniqueidentifier**형식의 출력 변수 이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 originating_server는 **sp_add_job** 에 있지만 인수 아래에는 나열 되지 않습니다. ** \@** originating_server는 내부용으로 예약 되어 있습니다. ** \@**  
  
 작업을 추가 하기 위해 **sp_add_job** 를 실행 한 후에는를 사용 하 여 작업에 대 한 작업을 수행 하는 단계를 추가할 수 **sp_add_jobstep** . **sp_add_jobschedule** 를 사용 하 여 에이전트 서비스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업을 실행 하는 데 사용 하는 일정을 만들 수 있습니다. **Sp_add_jobserver** 를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업이 실행 되는 인스턴스를 설정 하 고 **sp_delete_jobserver** 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 작업을 제거할 수 있습니다.  
  
 다중 서버 환경의 대상 서버 하나 이상에서 작업이 실행 되는 경우 **sp_apply_job_to_targets** 를 사용 하 여 작업에 대 한 대상 서버 또는 대상 서버 그룹을 설정 합니다. 대상 서버 또는 대상 서버 그룹에서 작업을 제거 하려면 **sp_remove_job_from_targets**을 사용 합니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 작업 구조를 만들고 관리할 수 있는 바람직한 방법을 제공하는데 이는 그래픽을 사용하여 쉽게 작업을 관리할 수 있는 방법입니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행 하려면 사용자가 **sysadmin** 고정 서버 역할의 멤버 이거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** 데이터베이스에 있는 다음 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 각 고정 데이터베이스 역할과 관련 된 특정 사용 권한에 대 한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조 하세요.  
  
 **Sysadmin** 고정 서버 역할의 멤버만 ** \@owner_login_name**에 대 한 값을 설정 하거나 변경할 수 있습니다. **Sysadmin** 역할의 멤버가 아닌 사용자가 ** \@owner_login_name**값을 설정 하거나 변경 하는 경우이 저장 프로시저의 실행이 실패 하 고 오류가 반환 됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-adding-a-job"></a>A. 작업 추가  
 다음 예에서는 `NightlyBackups`라는 새 작업을 추가합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-adding-a-job-with-pager-e-mail-and-net-send-information"></a>B. 호출기, 전자 메일 및 Net Send 정보를 사용한 작업 추가  
 다음 예에서는 호출기, 전자 메일 또는 네트워크 팝업 메시지를 사용하여 `Ad hoc Sales Data Backup`에게 알리는 `François Ajenstat`이라는 작업을 만들고 성공적으로 완료되면 해당 작업을 삭제합니다.  
  
> [!NOTE]  
>  다음 예에서는 `François Ajenstat`라는 운영자와 `françoisa`라는 로그인이 이미 있는 것으로 가정합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'Ad hoc Sales Data Backup',   
    @enabled = 1,  
    @description = N'Ad hoc backup of sales data',  
    @owner_login_name = N'françoisa',  
    @notify_level_eventlog = 2,  
    @notify_level_email = 2,  
    @notify_level_netsend = 2,  
    @notify_level_page = 2,  
    @notify_email_operator_name = N'François Ajenstat',  
    @notify_netsend_operator_name = N'François Ajenstat',   
    @notify_page_operator_name = N'François Ajenstat',  
    @delete_level = 1 ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_schedule &#40;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_add_jobstep &#40;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [Transact-sql&#41;sp_add_jobserver &#40;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [Transact-sql&#41;sp_apply_job_to_targets &#40;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [Transact-sql&#41;sp_delete_job &#40;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [Transact-sql&#41;sp_delete_jobserver &#40;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [Transact-sql&#41;sp_remove_job_from_targets &#40;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [Transact-sql&#41;sp_help_job &#40;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [Transact-sql&#41;sp_help_jobstep &#40;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [Transact-sql&#41;sp_update_job &#40;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
