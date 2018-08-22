---
title: sp_delete_job (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_job
- sp_delete_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_job
ms.assetid: b85db6e4-623c-41f1-9643-07e5ea38db09
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b4f55f1c4dd0d83f7db9f92027f95bcfeea7ad7c
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395560"
---
# <a name="spdeletejob-transact-sql"></a>sp_delete_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  작업을 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_job { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
     [ , [ @originating_server = ] 'server' ]   
     [ , [ @delete_history = ] delete_history ]  
     [ , [ @delete_unused_schedule = ] delete_unused_schedule ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@job_id=** ] *job_id*  
 삭제할 작업의 ID입니다. *job_id* 됩니다 **uniqueidentifier**, 기본값은 NULL입니다.  
  
 [ **@job_name=** ] **'***job_name***'**  
 삭제할 작업의 이름입니다. *job_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  어느 *job_id* 하거나 *job_name*지정 해야 하며 둘 다 지정할 수 없습니다.  
  
 [ **@originating_server=** ] **'***server***'**  
 내부적으로만 사용할 수 있습니다.  
  
 [ **@delete_history=** ] *delete_history*  
 작업 기록 삭제 여부를 지정합니다. *delete_history* 됩니다 **비트**, 기본값은 **1**합니다. 때 *delete_history* 됩니다 **1**, 작업에 대 한 작업 기록이 삭제 됩니다. 때 *delete_history* 됩니다 **0**, 작업 기록 삭제 되지 않습니다.  
  
 작업이 삭제 된 기록을 삭제 되지 않습니다을 작업에 대 한 기록 정보는 표시 되지에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 그래픽 사용자 인터페이스 작업 기록 하지만 정보에 여전히에 상주할는 **sysjobhistory**테이블에 **msdb** 데이터베이스입니다.  
  
 [ **@delete_unused_schedule=** ] *delete_unused_schedule*  
 이 작업에 연결된 일정이 다른 작업에 연결되어 있지 않은 경우 해당 일정의 삭제 여부를 지정합니다. *delete_unused_schedule* 됩니다 **비트**, 기본값은 **1**합니다. 때 *delete_unused_schedule* 됩니다 **1**, 일정을 참조 하는 다른 작업이 없는 경우이 작업에 연결 된 일정이 삭제 됩니다. 때 *delete_unused_schedule* 됩니다 **0**, 일정은 삭제 되지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 합니다 **@originating_server** 인수는 내부 용도로 예약 되어 있습니다.  
  
 합니다 **@delete_unused_schedule** 인수는 자동으로 모든 작업에 연결 되어 있지 않은 일정을 제거 하 여 이전 버전의 SQL Server를 사용 하 여 이전 버전과 호환성을 제공 합니다. 이 매개 변수는 이전 버전과의 호환성 동작이 기본적으로 설정되어 있습니다. 작업에 연결 되어 있지 않은 일정을 유지 하기 위해 값을 제공 해야 합니다 **0** 으로 **@delete_unused_schedule** 인수입니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 작업 구조를 만들고 관리할 수 있는 바람직한 방법을 제공하는데 이는 그래픽을 사용하여 쉽게 작업을 관리할 수 있는 방법입니다.  
  
 이 저장 프로시저는 유지 관리 계획을 삭제할 수 없으며 유지 관리 계획의 일부인 작업도 삭제할 수 없습니다. 유지 관리 계획을 삭제하려면 대신 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하십시오.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **sysadmin** 고정 서버 역할의 멤버만 **sp_delete_job** 을 실행하여 모든 작업을 삭제할 수 있습니다. **sysadmin** 고정 서버 역할의 멤버가 아닌 사용자는 해당 사용자가 소유한 작업만 삭제할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `NightlyBackups` 작업을 삭제합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_add_job&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_help_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_update_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
