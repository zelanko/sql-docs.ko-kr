---
title: sp_start_job (Transact-sql) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68032834"
---
# <a name="sp_start_job-transact-sql"></a>sp_start_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 즉시 작업을 실행하도록 지시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @job_name = ] 'job_name'`시작할 작업의 이름입니다. *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @job_id = ] job_id`시작할 작업의 id입니다. *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다. *job_id* 은 **uniqueidentifier**이며 기본값은 NULL입니다.  
  
`[ @error_flag = ] error_flag` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @server_name = ] 'server_name'`작업을 시작할 대상 서버입니다. *server_name* 은 **nvarchar (128)** 이며 기본값은 NULL입니다. *server_name* 은 현재 작업 대상인 대상 서버 중 하나 여야 합니다.  
  
`[ @step_name = ] 'step_name'`작업 실행을 시작할 단계의 이름입니다. 로컬 로그에만 적용됩니다. *step_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @output_flag = ] output_flag` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 이 저장 프로시저는 **msdb** 데이터베이스에 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **SQLAgentUserRole** 및 **SQLAgentReaderRole** 의 멤버는 자신이 소유한 작업만 시작할 수 있습니다. **SQLAgentOperatorRole** 의 멤버는 다른 사용자가 소유 하는 작업을 포함 하 여 모든 로컬 작업을 시작할 수 있습니다. **Sysadmin** 의 멤버는 모든 로컬 및 다중 서버 작업을 시작할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Weekly Sales Data Backup`라는 작업을 시작합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_delete_job &#40;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [Transact-sql&#41;sp_help_job &#40;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [Transact-sql&#41;sp_stop_job &#40;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [Transact-sql&#41;sp_update_job &#40;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
