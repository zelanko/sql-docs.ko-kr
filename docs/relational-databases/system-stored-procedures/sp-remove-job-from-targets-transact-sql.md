---
title: sp_remove_job_from_targets (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- sp_remove_job_from_targets_TSQL
- sp_remove_job_from_targets
dev_langs: TSQL
helpviewer_keywords: sp_remove_job_from_targets
ms.assetid: b8171fb1-c11d-4244-8618-a12e28a150ce
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8748e6968197faeb3809cf8adef59bc9b2452d57
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="spremovejobfromtargets-transact-sql"></a>sp_remove_job_from_targets(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 대상 서버 또는 대상 서버 그룹에서 지정한 작업을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_remove_job_from_targets [ @job_id = ] job_id   
     | [ @job_name = ] 'job_name'   
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@job_id =**] *job_id*  
 지정한 대상 서버 또는 대상 서버 그룹을 제거할 대상이 되는 작업의 ID입니다. 어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. *job_id* 은 **uniqueidentifier**, 기본값은 NULL입니다.  
  
 [  **@job_name =**] **'***job_name***'**  
 지정한 대상 서버 또는 대상 서버 그룹을 제거할 대상이 되는 작업 이름입니다. 어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. *job_name* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@target_server_groups =**] **'***target_server_groups***'**  
 지정된 작업에서 제거할 대상 서버 그룹의 쉼표로 구분된 목록입니다. *target_server_groups* 은 **nvarchar (1024)**, 기본값은 NULL입니다.  
  
 [  **@target_servers =**] **'***target_servers***'**  
 지정된 작업에서 제거할 대상 서버의 쉼표로 구분된 목록입니다. *target_servers* 은 **nvarchar (1024)**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="permissions"></a>Permissions  
 이 프로시저를 실행할 수 있는 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예  
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
  
## <a name="see-also"></a>관련 항목:  
 [sp_apply_job_to_targets &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_jobserver &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
