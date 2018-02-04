---
title: sp_update_job (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_update_job
- sp_update_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_job
ms.assetid: cbdfea38-9e42-47f3-8fc8-5978b82e2623
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 03171bfdee98063c9bf460b9555c1a7c5d02568d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="spupdatejob-transact-sql"></a>sp_update_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  작업의 특성을 변경합니다.  
  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_update_job [ @job_id =] job_id | [@job_name =] 'job_name'  
     [, [@new_name =] 'new_name' ]   
     [, [@enabled =] enabled ]  
     [, [@description =] 'description' ]   
     [, [@start_step_id =] step_id ]  
     [, [@category_name =] 'category' ]   
     [, [@owner_login_name =] 'login' ]  
     [, [@notify_level_eventlog =] eventlog_level ]  
     [, [@notify_level_email =] email_level ]  
     [, [@notify_level_netsend =] netsend_level ]  
     [, [@notify_level_page =] page_level ]  
     [, [@notify_email_operator_name =] 'operator_name' ]  
     [, [@notify_netsend_operator_name =] 'netsend_operator' ]  
     [, [@notify_page_operator_name =] 'page_operator' ]  
     [, [@delete_level =] delete_level ]   
     [, [@automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@job_id =**] *job_id*  
 업데이트할 작업의 ID입니다. *job_id*is **uniqueidentifier**.  
  
 [ **@job_name =**] **'***job_name***'**  
 작업의 이름입니다. *job_name*is **nvarchar(128)**.  
  
> **참고:** 어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
 [ **@new_name =**] **'***new_name***'**  
 작업의 새 이름입니다. *new_name*is **nvarchar(128)**.  
  
 [ **@enabled =**] *enabled*  
 작업이 사용 되는지 여부를 지정 합니다 (**1**) 또는 사용 안 함 (**0**). *활성화*은 **tinyint**합니다.  
  
 [ **@description =**] **'***description***'**  
 작업에 대한 설명입니다. *설명* 은 **nvarchar (512)**합니다.  
  
 [ **@start_step_id =**] *step_id*  
 작업을 실행하기 위한 첫 단계의 ID입니다. *step_id*은 **int**합니다.  
  
 [ **@category_name =**] **'***category***'**  
 작업 범주입니다. *category*is **nvarchar(128)**.  
  
 [ **@owner_login_name =**] **'***login***'**  
 작업을 소유하는 로그인의 이름입니다. *로그인*은 **nvarchar (128)** 의 구성원만는 **sysadmin** 고정된 서버 역할 작업 소유권을 변경할 수 있습니다.  
  
 [ **@notify_level_eventlog =**] *eventlog_level*  
 Microsoft Windows 응용 프로그램 로그에 이 작업에 대한 항목을 저장하는 시기를 지정합니다. *eventlog_level*은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|Value|설명(동작)|  
|-----------|----------------------------|  
|**0**|안 함|  
|**1**|성공한 경우|  
|**2**|실패한 경우|  
|**3**|항상|  
  
 [ **@notify_level_email =**] *email_level*  
 해당 작업이 완료될 때 전자 메일을 보낼 시기를 지정합니다. *email_level*은 **int**합니다. *email_level*같은 값을 사용 하 여 *eventlog_level*합니다.  
  
 [ **@notify_level_netsend =**] *netsend_level*  
 해당 작업이 완료되었을 때 네트워크 메시지를 보낼 시기를 지정합니다. *netsend_level*은 **int**합니다. *netsend_level*같은 값을 사용 하 여 *eventlog_level*합니다.  
  
 [ **@notify_level_page =**] *page_level*  
 해당 작업이 완료될 때 페이지를 보낼 시기를 지정합니다. *page_level*은 **int**합니다. *page_level*같은 값을 사용 하 여 *eventlog_level*합니다.  
  
 [ **@notify_email_operator_name =**] **'***operator_name***'**  
 에 전자 메일을 받을 때 운영자의 이름 *email_level* 에 도달 합니다. *email_name* 은 **nvarchar (128)**합니다.  
  
 [ **@notify_netsend_operator_name =**] **'***netsend_operator***'**  
 네트워크 메시지를 받을 운영자의 이름입니다. *netsend_operator* 은 **nvarchar (128)**합니다.  
  
 [ **@notify_page_operator_name =**] **'***page_operator***'**  
 페이지를 받을 운영자의 이름입니다. *page_operator* 은 **nvarchar (128)**합니다.  
  
 [ **@delete_level =**] *delete_level*  
 작업 삭제 시기를 지정합니다. *delete_value*은 **int**합니다. *delete_level*같은 값을 사용 하 여 *eventlog_level*합니다.  
  
 [ **@automatic_post =**] *automatic_post*  
 예약되어 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_update_job** 에서 실행 되어야 합니다는 **msdb** 데이터베이스입니다.  
  
 **sp_update_job** 는 매개 변수 값이 제공 되는 설정만 변경 합니다. 매개 변수가 생략되면 현재 설정이 보존됩니다.  
  
## <a name="permissions"></a>Permissions  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)을 참조하세요.  
  
 구성원만 **sysadmin** 이 저장된 프로시저를 사용 하 여 다른 사용자가 소유 하는 작업의 속성을 편집할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `NightlyBackups` 작업의 이름, 설명 및 활성화 상태를 변경합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_job  
    @job_name = N'NightlyBackups',  
    @new_name = N'NightlyBackups -- Disabled',  
    @description = N'Nightly backups disabled during server migration.',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_add_job&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_delete_job &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
