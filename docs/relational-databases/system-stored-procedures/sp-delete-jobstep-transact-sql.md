---
description: sp_delete_jobstep(Transact-SQL)
title: sp_delete_jobstep (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7fc21ae11a1ade4780b99a86d03b7c9948c05663
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489427"
---
# <a name="sp_delete_jobstep-transact-sql"></a>sp_delete_jobstep(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  작업에서 작업 단계를 제거합니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_jobstep { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     [ @step_id = ] step_id   
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] job_id` 단계를 제거할 작업의 id입니다. *job_id*은 **uniqueidentifier**이며 기본값은 NULL입니다.  
  
`[ @job_name = ] 'job_name'` 단계를 제거할 작업의 이름입니다. *job_name*는 **sysname**이며 기본값은 NULL입니다.  
  
> **참고:** *Job_id* 또는 *job_name* 를 지정 해야 합니다. 둘 다 지정할 수 없습니다.  
  
`[ @step_id = ] step_id` 제거 되는 단계의 id입니다. *step_id*는 **int**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 작업 단계를 제거하면 자동으로 삭제된 단계를 참조하는 다른 작업 단계가 업데이트됩니다.  
  
 특정 작업과 관련 된 단계에 대 한 자세한 내용을 보려면 **sp_help_jobstep**를 실행 하십시오.  
  
> **참고:** *Step_id* 값이 0 인 **sp_delete_jobstep** 를 호출 하면 작업의 모든 작업 단계가 삭제 됩니다.  
  
 Microsoft SQL Server Management Studio는 작업 인프라를 만들고 관리하는 데 권장되는 방법으로 그래픽을 사용하여 쉽게 작업을 관리할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **Sysadmin** 의 멤버만 다른 사용자가 소유한 작업 단계를 삭제할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `1` 작업에서 작업 단계 `Weekly Sales Data Backup`을 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [작업 보기 또는 수정](../../ssms/agent/view-or-modify-jobs.md)   
 [Transact-sql&#41;sp_add_jobstep &#40;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [Transact-sql&#41;sp_update_jobstep &#40;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [Transact-sql&#41;sp_help_jobstep &#40;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
