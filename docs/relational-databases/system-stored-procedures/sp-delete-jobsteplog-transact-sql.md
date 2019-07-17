---
title: sp_delete_jobsteplog (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5c1587b65df123400188ba062ef40e57f9a0a550
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085310"
---
# <a name="spdeletejobsteplog-transact-sql"></a>sp_delete_jobsteplog(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 인수로 지정되는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계 로그를 제거합니다. 유지 하기 위해이 저장된 프로시저를 사용 합니다 **sysjobstepslogs** 테이블에 **msdb** 데이터베이스입니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
       [ , [ @step_id = ] step_id | [ @step_name = ] 'step_name' ]  
       [ , [ @older_than = ] 'date' ]  
       [ , [ @larger_than = ] 'size_in_bytes' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] 'job_id'` 제거할 작업 단계 로그가 포함 된 작업에 대 한 작업 id. *job_id* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @job_name = ] 'job_name'` 작업의 이름입니다. *job_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> **참고:** 어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
`[ @step_id = ] step_id` 작업 단계 로그를 삭제할 작업 단계의 id. 하지 않으면 작업의 모든 작업 단계 로그가 삭제 됩니다 하지 않은 경우 **@older_than** 하거나 **@larger_than** 지정 됩니다. *step_id* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @step_name = ] 'step_name'` 작업 단계 로그를 삭제할 작업 단계의 이름입니다. *step_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> **참고:** 어느 *step_id* 하거나 *step_name* 지정할 수 있습니다. 하지만 둘 다 지정할 수 없습니다.  
  
`[ @older_than = ] 'date'` 날짜 및 가장 오래 된 작업 단계 로그의 시간을 유지 하려고 합니다. 이 날짜와 시간보다 오래된 모든 작업 단계 로그는 제거됩니다. *날짜* 됩니다 **datetime**, 기본값은 NULL입니다. 둘 다 **@older_than** 하 고 **@larger_than** 지정할 수 있습니다.  
  
`[ @larger_than = ] 'size_in_bytes'` 가장 큰 작업 단계 로그를 보관할의 바이트 크기입니다. 이 크기보다 큰 모든 작업 단계 로그는 제거됩니다. 둘 다 **@larger_than** 하 고 **@older_than** 지정할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 **sp_delete_jobsteplog** 에 **msdb** 데이터베이스입니다.  
  
 제외 하 고 인수가 없는 경우 **@job_id** 하거나 **@job_name** 지정 된 경우 지정된 된 된 작업에 대 한 모든 작업 단계 로그가 삭제 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 멤버만 **sysadmin** 다른 사용자가 소유한 작업 단계 로그를 삭제할 수 있습니다.  
  
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
  
### <a name="b-removing-the-job-step-log-for-a-particular-job-step"></a>2\. 특정 작업 단계에 대한 작업 단계 로그 제거  
 다음 예에서는 작업 `Weekly Sales Data Backup`의 2단계에 대한 작업 단계 로그를 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 2;  
GO  
```  
  
### <a name="c-removing-all-job-step-logs-based-on-age-and-size"></a>3\. 만든 날짜와 크기를 기준으로 모든 작업 단계 로그 제거  
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
  
## <a name="see-also"></a>관련 항목  
 [sp_help_jobsteplog &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [SQL Server 에이전트 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
