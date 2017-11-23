---
title: sp_apply_job_to_targets (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_apply_job_to_targets
- sp_apply_job_to_targets_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_apply_job_to_targets
ms.assetid: 4a3e9173-7e3c-4100-a9ac-2f5d2c60a8b0
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4f0c7c788370e25f3fe7000bc4481005f4224dda
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="spapplyjobtotargets-transact-sql"></a>sp_apply_job_to_targets(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  한 개 이상의 대상 서버 또는 한 개 이상의 대상 서버 그룹에 속하는 대상 서버에 작업을 적용합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_apply_job_to_targets { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]   
     [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>인수  
 [  **@job_id =**] *job_id*  
 지정한 대상 서버 또는 대상 서버 그룹에 적용할 작업의 ID입니다. *job_id* 은 **uniqueidentifier**, 기본값은 NULL입니다.  
  
 [  **@job_name =**] **'***job_name***'**  
 지정된 연결 대상 서버 또는 대상 서버 그룹에 적용할 작업의 이름입니다. *job_name* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
 [  **@target_server_groups =**] **'***target_server_groups***'**  
 지정된 작업을 적용할 대상 서버 그룹의 쉼표로 구분된 목록입니다. *target_server_groups* 은 **nvarchar (2048)**, 기본값은 NULL입니다.  
  
 [  **@target_servers=** ] **'***target_servers***'**  
 지정된 작업을 적용할 대상 서버의 쉼표로 구분된 목록입니다. *target_servers*은 **nvarchar (2048)**, 기본값은 NULL입니다.  
  
 [  **@operation=** ] **'***작업***'**  
 지정된 대상 서버 또는 대상 서버 그룹에서 지정된 작업을 적용할지 아니면 제거할지 여부를 나타냅니다. *작업*은 **varchar(7)**, 기본값은 APPLY입니다. 올바른 작업은 **적용** 및 **제거**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_apply_job_to_targets** 다중 대상 서버에서 적용 (또는 제거) 작업을 하는 쉬운 방법을 제공 하 고 호출 하는 대신 **sp_add_jobserver** (또는 **sp_delete_jobserver** ) 필요한 각 대상 서버에 대해 한 번씩입니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이전에 만든 `Backup Customer Information` 작업을 `Servers Maintaining Customer Information` 그룹의 모든 대상 서버에 적용합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_apply_job_to_targets  
    @job_name = N'Backup Customer Information',  
    @target_server_groups = N'Servers Maintaining Customer Information',   
    @operation = N'APPLY' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_add_jobserver &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_jobserver &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
