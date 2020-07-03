---
title: sp_delete_jobsteplog (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobsteplog
- sp_delete_jobsteplog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobsteplog
ms.assetid: e9ef4c99-abde-4038-b6a3-a25dcbaf0958
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b1ae68a2c09ca79917288381db0a0f9c92d4e33c
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85863676"
---
# <a name="sp_delete_jobsteplog-transact-sql"></a>sp_delete_jobsteplog(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 인수로 지정되는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계 로그를 제거합니다. 이 저장 프로시저를 사용 하 여 **msdb** 데이터베이스에서 **sysjobstepslogs** 테이블을 유지 관리 합니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
       [ , [ @step_id = ] step_id | [ @step_name = ] 'step_name' ]  
       [ , [ @older_than = ] 'date' ]  
       [ , [ @larger_than = ] 'size_in_bytes' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] 'job_id'`제거할 작업 단계 로그가 포함 된 작업의 id입니다. *job_id* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @job_name = ] 'job_name'`작업의 이름입니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
> **참고:** *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다.  
  
`[ @step_id = ] step_id`작업 단계 로그를 삭제할 작업 단계의 id 번호입니다. 포함 되지 않은 경우 ** \@ older_than** 또는 ** \@ larger_than** 지정 되지 않은 경우 작업의 모든 작업 단계 로그가 삭제 됩니다. *step_id* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @step_name = ] 'step_name'`작업 단계 로그를 삭제할 작업 단계의 이름입니다. *step_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
> **참고:** *Step_id* 또는 *step_name* 를 지정할 수 있지만 둘 다 지정할 수는 없습니다.  
  
`[ @older_than = ] 'date'`유지 하려는 가장 오래 된 작업 단계 로그의 날짜와 시간입니다. 이 날짜와 시간보다 오래된 모든 작업 단계 로그는 제거됩니다. *날짜* 는 **datetime**이며 기본값은 NULL입니다. ** \@ Older_than** 와 ** \@ larger_than** 를 모두 지정할 수 있습니다.  
  
`[ @larger_than = ] 'size_in_bytes'`유지 하려는 가장 큰 작업 단계 로그의 크기 (바이트)입니다. 이 크기보다 큰 모든 작업 단계 로그는 제거됩니다. ** \@ Larger_than** 와 ** \@ older_than** 를 모두 지정할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **sp_delete_jobsteplog** **msdb** 데이터베이스에 있습니다.  
  
 ** \@ Job_id** 또는 ** \@ job_name** 를 제외한 인수가 지정 되지 않은 경우 지정 된 작업에 대 한 모든 작업 단계 로그가 삭제 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **Sysadmin** 의 멤버만 다른 사용자가 소유한 작업 단계 로그를 삭제할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-removing-all-job-step-logs-from-a-job"></a>A. 작업에서 모든 작업 단계 로그 제거  
 다음 예에서는 작업 `Weekly Sales Data Backup`에 대한 모든 작업 단계 로그를 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup';  
GO  
```  
  
### <a name="b-removing-the-job-step-log-for-a-particular-job-step"></a>B. 특정 작업 단계에 대한 작업 단계 로그 제거  
 다음 예에서는 작업 `Weekly Sales Data Backup`의 2단계에 대한 작업 단계 로그를 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 2;  
GO  
```  
  
### <a name="c-removing-all-job-step-logs-based-on-age-and-size"></a>C. 만든 날짜와 크기를 기준으로 모든 작업 단계 로그 제거  
 다음 예에서는 2005년 10월 25일 정오 이전 항목이면서 100MB를 초과하는 모든 작업 단계 로그를 작업 `Weekly Sales Data Backup`에서 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @older_than = '10/25/2005 12:00:00',  
    @larger_than = 104857600;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_help_jobsteplog &#40;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [Transact-sql&#41;&#40;저장 프로시저 SQL Server 에이전트](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
