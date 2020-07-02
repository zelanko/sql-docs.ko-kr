---
title: sp_remove_job_from_targets (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_remove_job_from_targets_TSQL
- sp_remove_job_from_targets
dev_langs:
- TSQL
helpviewer_keywords:
- sp_remove_job_from_targets
ms.assetid: b8171fb1-c11d-4244-8618-a12e28a150ce
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 033a2c950ec695a64aced30a383d25206e7f6d10
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751685"
---
# <a name="sp_remove_job_from_targets-transact-sql"></a>sp_remove_job_from_targets(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  지정한 대상 서버 또는 대상 서버 그룹에서 지정한 작업을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_remove_job_from_targets [ @job_id = ] job_id   
     | [ @job_name = ] 'job_name'   
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] job_id`지정 된 대상 서버 또는 대상 서버 그룹을 제거할 작업의 id입니다. *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다. *job_id* 은 **uniqueidentifier**이며 기본값은 NULL입니다.  
  
`[ @job_name = ] 'job_name'`지정 된 대상 서버 또는 대상 서버 그룹을 제거할 작업의 이름입니다. *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @target_server_groups = ] 'target_server_groups'`지정 된 작업에서 제거할 대상 서버 그룹의 쉼표로 구분 된 목록입니다. *target_server_groups* 는 **nvarchar (1024)** 이며 기본값은 NULL입니다.  
  
`[ @target_servers = ] 'target_servers'`지정 된 작업에서 제거할 대상 서버의 쉼표로 구분 된 목록입니다. *target_servers* 는 **nvarchar (1024)** 이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행할 수 있는 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `Weekly Sales Backups` 대상 서버 그룹, `Servers Processing Customer Orders` 및 `SEATTLE1` 서버에서 이전에 만든 `SEATTLE2` 작업을 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_remove_job_from_targets  
    @job_name = N'Weekly Sales Backups',  
    @target_server_groups = N'Servers Processing Customer Orders',   
    @target_servers = N'SEATTLE2,SEATTLE1' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_apply_job_to_targets &#40;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [Transact-sql&#41;sp_delete_jobserver &#40;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
