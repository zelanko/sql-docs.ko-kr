---
title: sp_start_job (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_start_job
- sp_start_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_start_job
ms.assetid: 8a91df6a-eb84-4512-9a17-4a6e32a9538a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1b3015651dc263d95aa80e6108db2e8017e112d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032834"
---
# <a name="spstartjob-transact-sql"></a>sp_start_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 즉시 작업을 실행하도록 지시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_start_job   
     {   [@job_name =] 'job_name'  
       | [@job_id =] job_id }  
     [ , [@error_flag =] error_flag]  
     [ , [@server_name =] 'server_name']  
     [ , [@step_name =] 'step_name']  
     [ , [@output_flag =] output_flag]  
```  
  
## <a name="arguments"></a>인수  
`[ @job_name = ] 'job_name'` 시작 작업의 이름입니다. 어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. *job_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @job_id = ] job_id` 시작 작업의 id. 어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. *job_id* 됩니다 **uniqueidentifier**, 기본값은 NULL입니다.  
  
`[ @error_flag = ] error_flag` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @server_name = ] 'server_name'` 대상 서버의 작업을 시작 합니다. *server_name* 은 **nvarchar (128)** , 기본값은 NULL입니다. *server_name* 작업은 현재 대상으로 하는 대상 서버 중 하나 여야 합니다.  
  
`[ @step_name = ] 'step_name'` 작업 실행을 시작 하는 단계의 이름입니다. 로컬 로그에만 적용됩니다. *step_name* 됩니다 **sysname**, 기본값은 NULL 사용 하 여  
  
`[ @output_flag = ] output_flag` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 이 저장된 프로시저에는 **msdb** 데이터베이스입니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 멤버인 **SQLAgentUserRole** 하 고 **SQLAgentReaderRole** 자신이 소유한 작업만 시작할 수 있습니다. 멤버인 **SQLAgentOperatorRole** 포함 하 여 다른 사용자가 소유 하는 모든 로컬 작업을 시작할 수 있습니다. 멤버인 **sysadmin** 모든 로컬 및 다중 서버 작업을 시작할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Weekly Sales Data Backup`라는 작업을 시작합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_delete_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_stop_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
