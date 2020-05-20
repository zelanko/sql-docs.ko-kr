---
title: sp_help_jobsteplog (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 522672192ab955ced5987184ed2f6ea2812a431a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827559"
---
# <a name="sp_help_jobsteplog-transact-sql"></a>sp_help_jobsteplog(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  특정 에이전트 작업 단계 로그에 대 한 메타 데이터를 반환 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **sp_help_jobsteplog** 은 실제 로그를 반환 하지 않습니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]  
     [ , [ @step_name = ] 'step_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] 'job_id'`작업 단계 로그 정보를 반환할 작업 id입니다. *job_id* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @job_name = ] 'job_name'`작업의 이름입니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다.  
  
`[ @step_id = ] step_id`작업 단계의 id입니다. 지정하지 않은 경우 작업의 모든 단계가 포함됩니다. *step_id* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @step_name = ] 'step_name'`작업 단계의 이름입니다. *step_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|작업의 고유 식별자입니다.|  
|**job_name**|**sysname**|작업의 이름입니다.|  
|**step_id**|**int**|작업 내 단계에 대한 식별자입니다. 예를 들어 단계가 작업의 첫 번째 단계 이면 해당 *step_id* 은 1입니다.|  
|**step_name**|**sysname**|작업 단계의 이름입니다.|  
|**step_uid**|**uniqueidentifier**|작업의 단계에 대해 시스템에서 생성된 고유 식별자입니다.|  
|**date_created**|**datetime**|단계가 생성된 날짜입니다.|  
|**date_modified**|**datetime**|단계가 마지막으로 수정된 날짜입니다.|  
|**log_size**|**float**|작업 단계 로그의 크기(MB)입니다.|  
|**로깅할**|**nvarchar(max)**|작업 단계 로그 출력입니다.|  
  
## <a name="remarks"></a>설명  
 **sp_help_jobsteplog** **msdb** 데이터베이스에 있습니다.  
  
## <a name="permissions"></a>권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **SQLAgentUserRole** 의 멤버는 자신이 소유한 작업 단계에 대 한 작업 단계 로그 메타 데이터만 볼 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returns-job-step-log-information-for-all-steps-in-a-specific-job"></a>A. 특정 작업의 모든 단계에 대한 작업 단계 로그 정보 반환  
 다음 예에서는 `Weekly Sales Data Backup`이라는 작업에 관한 모든 작업 단계 로그 정보를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobsteplog  
    @job_name = N'Weekly Sales Data Backup' ;  
GO  
```  
  
### <a name="b-return-job-step-log-information-about-a-specific-job-step"></a>B. 특정 작업 단계에 관한 작업 단계 로그 정보 반환  
 다음 예에서는 `Weekly Sales Data Backup`이라는 첫 번째 작업 단계에 관한 작업 단계 로그 정보를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_jobstep &#40;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [Transact-sql&#41;sp_delete_jobstep &#40;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [Transact-sql&#41;sp_help_jobstep &#40;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [Transact-sql&#41;sp_delete_jobstep &#40;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [Transact-sql&#41;sp_delete_jobsteplog &#40;](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)   
 [Transact-sql&#41;&#40;저장 프로시저 SQL Server 에이전트](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
