---
title: sp_delete_jobstep (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_delete_jobstep
- sp_delete_jobstep_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_delete_jobstep
ms.assetid: 421ede8e-ad57-474a-9fb9-92f70a3e77e3
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9134c1f50a3ce1e9aaee8456db4f076193271ca9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
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
 [  **@job_id=** ] *job_id*  
 단계를 제거할 작업의 ID입니다. *job_id*은 **uniqueidentifier**, 기본값은 NULL입니다.  
  
 [  **@job_name=** ] **'***job_name***'**  
 단계를 제거할 작업의 이름입니다. *job_name*은 **sysname**, 기본값은 NULL입니다.  
  
> **참고:** 어느 *job_id* 또는 *job_name* 지정 해야 하며 둘 다 지정할 수 없습니다.  
  
 [  **@step_id=** ] *step_id*  
 제거할 단계의 ID입니다. *step_id*은 **int**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>주의  
 작업 단계를 제거하면 자동으로 삭제된 단계를 참조하는 다른 작업 단계가 업데이트됩니다.  
  
 관련 된 특정 작업 단계에 대 한 자세한 내용은 실행 **sp_help_jobstep**합니다.  
  
> **참고:** 호출 **sp_delete_jobstep** 와 *step_id* 값이 0 이면 작업에 대 한 모든 작업 단계를 삭제 합니다.  
  
 Microsoft SQL Server Management Studio는 작업 인프라를 만들고 관리하는 데 권장되는 방법으로 그래픽을 사용하여 쉽게 작업을 관리할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)을 참조하세요.  
  
 구성원만 **sysadmin** 다른 사용자가 소유 하는 작업 단계를 삭제할 수 있습니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [작업 보기 또는 수정](http://msdn.microsoft.com/library/57f649b8-190c-4304-abd7-7ca5297deab7)   
 [sp_add_jobstep&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_update_jobstep &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
