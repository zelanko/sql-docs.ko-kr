---
title: sp_help_jobsteplog (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobsteplog_TSQL
- sp_help_jobsteplog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobsteplog
ms.assetid: 1a0be7b1-8f31-4b4c-aadb-586c0e00ed04
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 905386a1e346ed982c3ad84baf57f532aa5b020f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828361"
---
# <a name="sphelpjobsteplog-transact-sql"></a>sp_help_jobsteplog(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  특정에 대 한 메타 데이터 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계 로그 합니다. **sp_help_jobsteplog** 실제 로그를 반환 하지 않습니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]  
     [ , [ @step_name = ] 'step_name' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@job_id =**] **'***job_id***'**  
 작업 단계 로그 정보를 반환할 작업 ID입니다. *job_id* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [ **@job_name =**] **'***job_name***'**  
 작업의 이름입니다. *job_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
 [ **@step_id =**] *step_id*  
 작업 단계의 ID입니다. 지정하지 않은 경우 작업의 모든 단계가 포함됩니다. *step_id* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [ **@step_name =**] **'***step_name***'**  
 작업 단계의 이름입니다. *step_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|작업의 고유 식별자입니다.|  
|**job_name**|**sysname**|작업의 이름입니다.|  
|**step_id**|**int**|작업 내 단계에 대한 식별자입니다. 예를 들어 단계, 작업의 첫 번째 단계는 해당 *step_id* 1입니다.|  
|**step_name**|**sysname**|작업 단계의 이름입니다.|  
|**step_uid**|**uniqueidentifier**|작업의 단계에 대해 시스템에서 생성된 고유 식별자입니다.|  
|**date_created**|**datetime**|단계가 생성된 날짜입니다.|  
|**date_modified**|**datetime**|단계가 마지막으로 수정된 날짜입니다.|  
|**log_size**|**float**|작업 단계 로그의 크기(MB)입니다.|  
|**log**|**nvarchar(max)**|작업 단계 로그 출력입니다.|  
  
## <a name="remarks"></a>Remarks  
 **sp_help_jobsteplog** 에 **msdb** 데이터베이스입니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 멤버인 **SQLAgentUserRole** 자신이 소유한 작업 단계에 대 한 작업 단계 로그 메타 데이터를 보기만 할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returns-job-step-log-information-for-all-steps-in-a-specific-job"></a>1. 특정 작업의 모든 단계에 대한 작업 단계 로그 정보 반환  
 다음 예에서는 `Weekly Sales Data Backup`이라는 작업에 관한 모든 작업 단계 로그 정보를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobsteplog  
    @job_name = N'Weekly Sales Data Backup' ;  
GO  
```  
  
### <a name="b-return-job-step-log-information-about-a-specific-job-step"></a>2. 특정 작업 단계에 관한 작업 단계 로그 정보 반환  
 다음 예에서는 `Weekly Sales Data Backup`이라는 첫 번째 작업 단계에 관한 작업 단계 로그 정보를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_add_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_delete_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_delete_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_delete_jobsteplog &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)   
 [SQL Server 에이전트 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
