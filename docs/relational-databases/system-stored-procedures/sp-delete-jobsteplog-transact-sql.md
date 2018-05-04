---
title: sp_delete_jobsteplog (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_jobsteplog
- sp_delete_jobsteplog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobsteplog
ms.assetid: e9ef4c99-abde-4038-b6a3-a25dcbaf0958
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 99f60818976dc3c89e11d2fd1256a7aecd7d8b63
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spdeletejobsteplog-transact-sql"></a>sp_delete_jobsteplog(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 인수로 지정되는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계 로그를 제거합니다. 이 저장된 프로시저를 사용 하 여 유지 관리 하는 **sysjobstepslogs** 테이블에 **msdb** 데이터베이스입니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
       [ , [ @step_id = ] step_id | [ @step_name = ] 'step_name' ]  
       [ , [ @older_than = ] 'date' ]  
       [ , [ @larger_than = ] 'size_in_bytes' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@job_id =**] **'***job_id***'**  
 제거할 작업 단계 로그가 포함된 작업의 ID입니다. *job_id* 은 **int**, 기본값은 NULL입니다.  
  
 [ **@job_name =**] **'***job_name***'**  
 작업의 이름입니다. *job_name* 은 **sysname**, 기본값은 NULL입니다.  
  
> **참고:** 어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
 [ **@step_id =**] *step_id*  
 작업 단계 로그를 삭제할 작업 단계의 ID입니다. 하지 않으면 작업의 모든 작업 단계 로그가 삭제 됩니다 하지 않은 경우 **@older_than** 또는 **@larger_than** 지정 됩니다. *step_id* 은 **int**, 기본값은 NULL입니다.  
  
 [ **@step_name =**] **'***step_name***'**  
 작업 단계 로그를 삭제할 작업 단계의 이름입니다. *step_name* 은 **sysname**, 기본값은 NULL입니다.  
  
> **참고:** 어느 *step_id* 또는 *step_name* 지정할 수 있습니다 하지만 둘 다 지정할 수 없습니다.  
  
 [ **@older_than =**] **'***date***'**  
 유지할 가장 오래된 작업 단계 로그의 날짜와 시간입니다. 이 날짜와 시간보다 오래된 모든 작업 단계 로그는 제거됩니다. *날짜* 은 **datetime**, 기본값은 NULL입니다. 둘 다 **@older_than** 및 **@larger_than** 지정할 수 있습니다.  
  
 [ **@larger_than =**] **'***size_in_bytes***'**  
 유지할 가장 큰 작업 단계 로그의 크기(바이트)입니다. 이 크기보다 큰 모든 작업 단계 로그는 제거됩니다. 둘 다 **@larger_than** 및 **@older_than** 지정할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 **sp_delete_jobsteplog** 에 **msdb** 데이터베이스입니다.  
  
 하는 경우를 제외 하 고 인수 없이 **@job_id** 또는 **@job_name** 지정 된 경우 지정된 된 작업에 대 한 모든 작업 단계 로그가 삭제 됩니다.  
  
## <a name="permissions"></a>Permissions  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)을 참조하세요.  
  
 구성원만 **sysadmin** 다른 사용자가 소유 하는 작업 단계 로그를 삭제할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-removing-all-job-step-logs-from-a-job"></a>1. 작업에서 모든 작업 단계 로그 제거  
 다음 예에서는 작업 `Weekly Sales Data Backup`에 대한 모든 작업 단계 로그를 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup';  
GO  
```  
  
### <a name="b-removing-the-job-step-log-for-a-particular-job-step"></a>2. 특정 작업 단계에 대한 작업 단계 로그 제거  
 다음 예에서는 작업 `Weekly Sales Data Backup`의 2단계에 대한 작업 단계 로그를 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 2;  
GO  
```  
  
### <a name="c-removing-all-job-step-logs-based-on-age-and-size"></a>3. 만든 날짜와 크기를 기준으로 모든 작업 단계 로그 제거  
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
  
## <a name="see-also"></a>관련 항목:  
 [sp_help_jobsteplog &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [SQL Server 에이전트 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
