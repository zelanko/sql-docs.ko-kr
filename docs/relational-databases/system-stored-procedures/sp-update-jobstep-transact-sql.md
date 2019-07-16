---
title: sp_update_jobstep (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_jobstep
- sp_update_jobstep_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_jobstep
ms.assetid: e158802c-c347-4a5d-bf75-c03e5ae56e6b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7914e3b56dd02d96c02835bf6b4dcc5eb90e8f4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084883"
---
# <a name="spupdatejobstep-transact-sql"></a>sp_update_jobstep(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  자동 동작을 수행하기 위해 사용되는 작업의 단계에 대한 설정을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_update_jobstep   
     {   [@job_id =] job_id   
       | [@job_name =] 'job_name' } ,  
     [@step_id =] step_id  
     [ , [@step_name =] 'step_name' ]  
     [ , [@subsystem =] 'subsystem' ]   
     [ , [@command =] 'command' ]  
     [ , [@additional_parameters =] 'parameters' ]  
     [ , [@cmdexec_success_code =] success_code ]  
     [ , [@on_success_action =] success_action ]   
     [ , [@on_success_step_id =] success_step_id ]  
     [ , [@on_fail_action =] fail_action ]   
     [ , [@on_fail_step_id =] fail_step_id ]  
     [ , [@server =] 'server' ]   
     [ , [@database_name =] 'database' ]  
     [ , [@database_user_name =] 'user' ]   
     [ , [@retry_attempts =] retry_attempts ]  
     [ , [@retry_interval =] retry_interval ]   
     [ , [@os_run_priority =] run_priority ]  
     [ , [@output_file_name =] 'file_name' ]   
     [ , [@flags =] flags ]  
     [ ,  {   [ @proxy_id = ] proxy_id   
            | [ @proxy_name = ] 'proxy_name' }   
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] job_id` 단계가 속한 작업의 id. *job_id*됩니다 **uniqueidentifier**, 기본값은 NULL입니다. 어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
`[ @job_name = ] 'job_name'` 단계가 속한 작업의 이름입니다. *job_name*됩니다 **sysname**, 기본값은 NULL입니다. 어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
`[ @step_id = ] step_id` 수정할 작업 단계의 id. 이 번호는 변경할 수 없습니다. *step_id*됩니다 **int**, 기본값은 없습니다.  
  
`[ @step_name = ] 'step_name'` 단계의 새 이름이입니다. *step_name*됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @subsystem = ] 'subsystem'` Microsoft SQL Server 에이전트에서 실행 하는 데 하위 시스템 *명령*입니다. *하위 시스템* 됩니다 **nvarchar(40)** , 기본값은 NULL입니다.  
  
`[ @command = ] 'command'` 통해 실행할 명령 *하위 시스템*입니다. *명령* 됩니다 **nvarchar (max)** , 기본값은 NULL입니다.  
  
`[ @additional_parameters = ] 'parameters'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @cmdexec_success_code = ] success_code` 반환 된 값을 **CmdExec** 나타내는 하위 시스템 명령 *명령* 성공적으로 실행 합니다. *success_code* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @on_success_action = ] success_action` 단계가 성공 하는 경우 수행할 동작입니다. *success_action* 됩니다 **tinyint**, 기본값은 NULL 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|설명(동작)|  
|-----------|----------------------------|  
|**1**|성공적으로 종료|  
|**2**|실패로 종료|  
|**3**|다음 단계로 이동|  
|**4**|단계로 이동 *success_step_id 합니다.*|  
  
`[ @on_success_step_id = ] success_step_id` 단계가 성공 하는 경우에 실행할이 작업 단계의 id 번호 및 *success_action* 됩니다 **4**합니다. *success_step_id* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @on_fail_action = ] fail_action` 단계가 실패 하는 경우 수행할 동작입니다. *fail_action* 됩니다 **tinyint**, 기본값은 NULL 사용 하 여 다음이 값 중 하나일 수 있습니다.  
  
|값|설명(동작)|  
|-----------|----------------------------|  
|**1**|성공적으로 종료|  
|**2**|실패로 종료|  
|**3**|다음 단계로 이동|  
|**4**|단계로 이동 *fail_step_id * * 합니다.*|  
  
`[ @on_fail_step_id = ] fail_step_id` 단계가 실패 하는 경우에 실행할이 작업 단계의 id 번호 및 *fail_action* 됩니다 **4**합니다. *fail_step_id* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @server = ] 'server'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *서버* 됩니다 **nvarchar (128)** , 기본값은 NULL입니다.  
  
`[ @database_name = ] 'database'` 실행할 데이터베이스의 이름을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 단계입니다. *데이터베이스*됩니다 **sysname**합니다. 이름을 대괄호([ ])로 묶는 것은 허용되지 않습니다. 기본값은 NULL입니다.  
  
`[ @database_user_name = ] 'user'` 실행할 때 사용할 사용자 계정의 이름을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 단계입니다. *사용자*됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @retry_attempts = ] retry_attempts` 다시 시도 횟수는이 단계가 실패 하면를 사용 하려고 합니다. *retry_attempts*됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @retry_interval = ] retry_interval` 재시도 간격 (분) 시간의 양입니다. *retry_interval* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @os_run_priority = ] run_priority` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @output_file_name = ] 'file_name'` 이 단계의 출력이 저장 되는 파일의 이름입니다. *file_name* 됩니다 **nvarchar (200)** , 기본값은 NULL입니다. 이 매개 변수는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 CmdExec 하위 시스템에서 실행되는 명령과 함께 사용하는 경우에만 유효합니다.  
  
 Output_file_name을 다시 NULL로 설정 하려면 설정 해야 합니다 *output_file_name* 빈 문자열 (' ') 수 있지만 빈 문자의 문자열로 사용할 수 없습니다 또는 **CHAR(32)** 함수. 예를 들어 다음과 같이 이 인수를 빈 문자열로 설정합니다.  
  
 **@output_file_name = ' '**  
  
`[ @flags = ] flags` 동작을 제어 하는 옵션입니다. *플래그* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**0** (기본값)|출력 파일을 덮어씁니다.|  
|**2**|출력 파일에 추가합니다.|  
|**4**|Transact-SQL 작업 단계 출력을 단계 기록에 씁니다.|  
|**8**|테이블에 로그를 씁니다(기존 기록을 덮어씀).|  
|**16**|테이블에 로그를 씁니다(기존 기록에 추가).|  
  
`[ @proxy_id = ] proxy_id` 작업 단계가 실행 되는 프록시의 ID. *proxy_id* 형식인 **int**, 기본값은 NULL입니다. 없으면 *proxy_id* 지정 된 없습니다 *proxy_name* 지정 된 경우 및 no *user_name* 지정 된 경우 작업 단계에 대 한 서비스 계정으로 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트입니다.  
  
`[ @proxy_name = ] 'proxy_name'` 작업 단계가 실행 되는 프록시의 이름입니다. *proxy_name* 형식인 **sysname**, 기본값은 NULL입니다. 없으면 *proxy_id* 지정 된 없습니다 *proxy_name* 지정 된 경우 및 no *user_name* 지정 된 경우 작업 단계에 대 한 서비스 계정으로 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_update_jobstep** 에서 실행 해야 합니다 **msdb** 데이터베이스입니다.  
  
 작업 단계를 업데이트하면 작업 버전 번호가 증가합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 멤버만 **sysadmin** 다른 사용자가 소유한 작업 단계를 업데이트할 수 있습니다.  
  
 작업 단계에서 프록시에 액세스해야 할 경우 작업 단계를 만든 사람에게 작업 단계의 프록시에 대한 액세스 권한이 있어야 합니다. Transact-SQL을 제외한 모든 하위 시스템에서는 프록시 계정이 필요합니다. 멤버인 **sysadmin** 모든 프록시에 액세스할 수 있으며 사용할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프록시에 대 한 에이전트 서비스 계정입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Weekly Sales Data Backup` 작업의 첫 번째 단계에 대한 재시도 횟수를 변경합니다. 이 예를 실행한 후 재시도 횟수는 `10`이 됩니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1,  
    @retry_attempts = 10 ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [작업 보기 또는 수정](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_delete_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
