---
description: sp_help_jobstep(Transact-SQL)
title: sp_help_jobstep (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobstep_TSQL
- sp_help_jobstep
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobstep
ms.assetid: 4a13b804-45f2-4f82-987f-42d9a57dd6db
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 24ec19dc231ce2fedf3a3562312ddc0bf7311e39
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535247"
---
# <a name="sp_help_jobstep-transact-sql"></a>sp_help_jobstep(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 자동화된 작업을 수행하는 데 사용하는 작업의 단계에 대한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_jobstep { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]   
     [ , [ @step_name = ] 'step_name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] 'job_id'` 작업 정보를 반환할 작업 id입니다. *job_id* 은 **uniqueidentifier**이며 기본값은 NULL입니다.  
  
`[ @job_name = ] 'job_name'` 작업의 이름입니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다.  
  
`[ @step_id = ] step_id` 작업 단계의 id입니다. 지정하지 않은 경우 작업의 모든 단계가 포함됩니다. *step_id* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @step_name = ] 'step_name'` 작업 단계의 이름입니다. *step_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @suffix = ] suffix` 텍스트 설명이 출력의 **flags** 열에 추가 되는지 여부를 나타내는 플래그입니다. *접미사*는 **bit**이며 기본값은 **0**입니다. *접미사* 가 **1**인 경우 설명이 추가 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**step_id**|**int**|단계의 고유 식별자입니다.|  
|**step_name**|**sysname**|작업 단계의 이름입니다.|  
|**하위**|**nvarchar(40)**|단계 명령을 실행할 하위 시스템입니다.|  
|**command**|**nvarchar(max)**|단계에서 실행할 명령입니다.|  
|**flags**|**int**|단계 동작을 제어하는 값의 비트 마스크입니다.|  
|**cmdexec_success_code**|**int**|**CmdExec** 단계의 경우 성공한 명령의 프로세스 종료 코드입니다.|  
|**on_success_action**|**tinyint**|단계가 성공할 경우 수행되는 동작입니다.<br /><br /> **1** = 성공 보고 작업을 종료 합니다.<br /><br /> **2** = 실패를 보고 하는 작업을 종료 합니다.<br /><br /> **3** = 다음 단계로 이동 합니다.<br /><br /> **4** = 단계로 이동 합니다.|  
|**on_success_step_id**|**int**|**On_success_action** 이 4 인 경우 실행할 다음 단계를 나타냅니다.|  
|**on_fail_action**|**tinyint**|단계가 실패할 경우 수행되는 작업입니다. 값은 **on_success_action**와 동일 합니다.|  
|**on_fail_step_id**|**int**|**On_fail_action** 이 4 인 경우 실행할 다음 단계를 나타냅니다.|  
|**server**|**sysname**|예약되어 있습니다.|  
|**database_name**|**sysname**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 단계의 경우 명령이 실행되는 데이터베이스입니다.|  
|**database_user_name**|**sysname**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 단계의 경우 명령이 실행되는 데이터베이스 사용자 컨텍스트입니다.|  
|**retry_attempts**|**int**|단계가 성공하지 못한 경우에 명령을 재시도할 최대 횟수입니다.|  
|**retry_interval**|**int**|재시도 간격(분)입니다.|  
|**os_run_priority**|**int**|예약되어 있습니다.|  
|**output_file_name**|**nvarchar(200)**|명령 출력을 기록할 파일입니다 ( [!INCLUDE[tsql](../../includes/tsql-md.md)] , **CmdExec**및 **PowerShell** 단계에만 해당).|  
|**last_run_outcome**|**int**|단계가 마지막으로 실행되었을 때의 결과입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **2** = 다시 시도<br /><br /> **3** = 취소 됨<br /><br /> **5** = 알 수 없음|  
|**last_run_duration**|**int**|단계가 마지막으로 실행되었을 때의 시간(hhmmss)입니다.|  
|**last_run_retries**|**int**|단계를 마지막으로 실행했을 때 명령을 재시도할 횟수입니다.|  
|**last_run_date**|**int**|단계가 마지막으로 실행을 시작했을 때의 날짜입니다.|  
|**last_run_time**|**int**|단계가 마지막으로 실행을 시작했을 때의 시간입니다.|  
|**proxy_id**|**int**|작업 단계에 대한 프록시입니다.|  
  
## <a name="remarks"></a>설명  
 **sp_help_jobstep** **msdb** 데이터베이스에 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **SQLAgentUserRole** 의 멤버는 자신이 소유한 작업에 대 한 작업 단계만 볼 수 있습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-return-information-for-all-steps-in-a-specific-job"></a>A. 특정 작업의 모든 단계에 관한 정보 반환  
 다음 예에서는 `Weekly Sales Data Backup`이라는 작업의 모든 작업 단계를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobstep  
    @job_name = N'Weekly Sales Data Backup' ;  
GO  
```  
  
### <a name="b-return-information-about-a-specific-job-step"></a>B. 특정 작업 단계에 관한 정보 반환  
 다음 예에서는 `Weekly Sales Data Backup`이라는 작업의 첫 번째 작업 단계에 대한 정보를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_jobstep &#40;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [Transact-sql&#41;sp_delete_jobstep &#40;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [Transact-sql&#41;sp_help_job &#40;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [Transact-sql&#41;sp_update_jobstep &#40;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
