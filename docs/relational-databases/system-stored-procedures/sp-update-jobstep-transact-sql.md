---
title: sp_update_jobstep (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 02697937d5a0402edbaf959ed52731010eab1ce6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723074"
---
# <a name="sp_update_jobstep-transact-sql"></a>sp_update_jobstep(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  자동 동작을 수행하기 위해 사용되는 작업의 단계에 대한 설정을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @job_id = ] job_id`단계가 속한 작업의 id 번호입니다. *job_id*은 **uniqueidentifier**이며 기본값은 NULL입니다. *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
`[ @job_name = ] 'job_name'`단계가 속한 작업의 이름입니다. *job_name*는 **sysname**이며 기본값은 NULL입니다. *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
`[ @step_id = ] step_id`수정할 작업 단계의 id입니다. 이 번호는 변경할 수 없습니다. *step_id*는 **int**이며 기본값은 없습니다.  
  
`[ @step_name = ] 'step_name'`단계에 대 한 새 이름입니다. *step_name*는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subsystem = ] 'subsystem'`Microsoft SQL Server 에이전트가 *명령을*실행 하는 데 사용 하는 하위 시스템입니다. *하위 시스템* 은 **nvarchar (40)** 이며 기본값은 NULL입니다.  
  
`[ @command = ] 'command'`*하위 시스템*을 통해 실행할 명령입니다. *명령은* **nvarchar (max)** 이며 기본값은 NULL입니다.  
  
`[ @additional_parameters = ] 'parameters'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @cmdexec_success_code = ] success_code`*명령이* 성공적으로 실행 되었음을 나타내는 **CmdExec** 하위 시스템 명령에서 반환 하는 값입니다. *success_code* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @on_success_action = ] success_action`단계가 성공할 경우 수행할 동작입니다. *success_action* 은 **tinyint**이며 기본값은 NULL이 고 다음 값 중 하나일 수 있습니다.  
  
|값|설명(동작)|  
|-----------|----------------------------|  
|**1**|성공적으로 종료|  
|**2**|실패로 종료|  
|**3**|다음 단계로 이동|  
|**4**|Success_step_id 단계로 이동 *합니다.*|  
  
`[ @on_success_step_id = ] success_step_id`단계가 성공 하 고 *success_action* **4**인 경우이 작업을 실행할 단계의 id입니다. *success_step_id* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @on_fail_action = ] fail_action`단계가 실패할 경우 수행할 동작입니다. *fail_action* 은 **tinyint**이며 기본값은 NULL이 고 다음 값 중 하나를 사용할 수 있습니다.  
  
|값|설명(동작)|  
|-----------|----------------------------|  
|**1**|성공적으로 종료|  
|**2**|실패로 종료|  
|**3**|다음 단계로 이동|  
|**4**|*Fail_step_id * * 단계로 이동 합니다.*|  
  
`[ @on_fail_step_id = ] fail_step_id`단계가 실패 하 고 *fail_action* **4**인 경우이 작업에서 실행할 단계의 id입니다. *fail_step_id* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @server = ] 'server'`[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *서버* 는 **nvarchar (128)** 이며 기본값은 NULL입니다.  
  
`[ @database_name = ] 'database'`단계를 실행할 데이터베이스의 이름입니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] . *데이터베이스*는 **sysname**입니다. 이름을 대괄호([ ])로 묶는 것은 허용되지 않습니다. 기본값은 NULL입니다.  
  
`[ @database_user_name = ] 'user'`단계를 실행할 때 사용할 사용자 계정의 이름입니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] . *사용자*는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @retry_attempts = ] retry_attempts`이 단계가 실패 하는 경우 다시 시도 하는 횟수입니다. *retry_attempts*은 **int**이며 기본값은 NULL입니다.  
  
`[ @retry_interval = ] retry_interval`다시 시도 간의 시간 간격 (분)입니다. *retry_interval* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @os_run_priority = ] run_priority` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @output_file_name = ] 'file_name'`이 단계의 출력이 저장 되는 파일의 이름입니다. *file_name* 은 **nvarchar (200)** 이며 기본값은 NULL입니다. 이 매개 변수는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 CmdExec 하위 시스템에서 실행되는 명령과 함께 사용하는 경우에만 유효합니다.  
  
 Output_file_name를 다시 NULL로 설정 하려면 *output_file_name* 을 빈 문자열 (' ') 또는 빈 문자 문자열로 설정 해야 하지만 **CHAR (32)** 함수는 사용할 수 없습니다. 예를 들어 다음과 같이 이 인수를 빈 문자열로 설정합니다.  
  
 **@output_file_name= ' '**  
  
`[ @flags = ] flags`동작을 제어 하는 옵션입니다. *flags* 는 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0** (기본값)|출력 파일을 덮어씁니다.|  
|**2**|출력 파일에 추가합니다.|  
|**4**|Transact-SQL 작업 단계 출력을 단계 기록에 씁니다.|  
|**8**|테이블에 로그를 씁니다(기존 기록을 덮어씀).|  
|**16**|테이블에 로그를 씁니다(기존 기록에 추가).|  
  
`[ @proxy_id = ] proxy_id`작업 단계가 실행 되는 프록시의 ID입니다. *proxy_id* 은 **int**형식 이며 기본값은 NULL입니다. *Proxy_id* 지정 되지 않은 경우 *proxy_name* 지정 되지 않고 *user_name* 지정 되지 않은 경우 작업 단계는 에이전트의 서비스 계정으로 실행 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
`[ @proxy_name = ] 'proxy_name'`작업 단계가 실행 되는 프록시의 이름입니다. *proxy_name* 는 **sysname**형식 이며 기본값은 NULL입니다. *Proxy_id* 지정 되지 않은 경우 *proxy_name* 지정 되지 않고 *user_name* 지정 되지 않은 경우 작업 단계는 에이전트의 서비스 계정으로 실행 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_update_jobstep** 는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
 작업 단계를 업데이트하면 작업 버전 번호가 증가합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **Sysadmin** 의 멤버만 다른 사용자가 소유한 작업 단계를 업데이트할 수 있습니다.  
  
 작업 단계에서 프록시에 액세스해야 할 경우 작업 단계를 만든 사람에게 작업 단계의 프록시에 대한 액세스 권한이 있어야 합니다. Transact-SQL을 제외한 모든 하위 시스템에서는 프록시 계정이 필요합니다. **Sysadmin** 의 멤버는 모든 프록시에 액세스할 수 있으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프록시에 대 한 에이전트 서비스 계정을 사용할 수 있습니다.  
  
## <a name="examples"></a>예제  
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
  
## <a name="see-also"></a>참고 항목  
 [작업 보기 또는 수정](../../ssms/agent/view-or-modify-jobs.md)   
 [Transact-sql&#41;sp_delete_jobstep &#40;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [Transact-sql&#41;sp_help_jobstep &#40;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
