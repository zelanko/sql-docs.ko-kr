---
title: sp_delete_jobstep (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobstep
- sp_delete_jobstep_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobstep
ms.assetid: 421ede8e-ad57-474a-9fb9-92f70a3e77e3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 84b1e2840240d0d02a3193ecc592a13331719c7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62693826"
---
# <a name="spdeletejobstep-transact-sql"></a>sp_delete_jobstep(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  작업에서 작업 단계를 제거합니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_jobstep { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     [ @step_id = ] step_id   
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] job_id` 단계를 제거할 작업의 id. *job_id*됩니다 **uniqueidentifier**, 기본값은 NULL입니다.  
  
`[ @job_name = ] 'job_name'` 단계를 제거할 작업의 이름입니다. *job_name*됩니다 **sysname**, 기본값은 NULL입니다.  
  
> **참고:** 어느 *job_id* 하거나 *job_name* 지정 해야 하며 둘 다 지정할 수 없습니다.  
  
`[ @step_id = ] step_id` 제거할 단계의 id. *step_id*됩니다 **int**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 작업 단계를 제거하면 자동으로 삭제된 단계를 참조하는 다른 작업 단계가 업데이트됩니다.  
  
 특정 작업과 관련 된 단계에 대 한 자세한 내용은 실행 **sp_help_jobstep**합니다.  
  
> **참고:** 호출 **sp_delete_jobstep** 사용 하 여를 *step_id* 값이 0 이면 작업에 대 한 모든 작업 단계를 삭제 합니다.  
  
 Microsoft SQL Server Management Studio는 작업 인프라를 만들고 관리하는 데 권장되는 방법으로 그래픽을 사용하여 쉽게 작업을 관리할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 멤버만 **sysadmin** 다른 사용자가 소유한 작업 단계를 삭제할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `1` 작업에서 작업 단계 `Weekly Sales Data Backup`을 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [작업 보기 또는 수정](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_add_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_update_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
