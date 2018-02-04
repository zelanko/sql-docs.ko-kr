---
title: sp_purge_jobhistory (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_purge_jobhistory_TSQL
- sp_purge_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_jobhistory
ms.assetid: 237f9bad-636d-4262-9bfb-66c034a43e88
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7f50228e089d71a6cf3a8d74225e1e26f42844fd
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sppurgejobhistory-transact-sql"></a>sp_purge_jobhistory(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  작업에 대한 기록 레코드를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_purge_jobhistory   
   {   [ @job_name = ] 'job_name' |   
     | [ @job_id = ] job_id }  
   [ , [ @oldest_date = ] oldest_date ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@job_name=** ] **'***job_name***'**  
 기록 레코드를 삭제할 작업의 이름입니다. *job_name*은 **sysname**, 기본값은 NULL입니다. 어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
> [!NOTE]  
>  멤버는 **sysadmin** 고정 서버 역할의 멤버 또는 **SQLAgentOperatorRole** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_purge_jobhistory** 는 지정하지않고*job_name* 또는 *job_id*합니다. 때 **sysadmin** 사용자가 이러한 인수를 지정 하지 않으면, 지정 된 시간 내에서 모든 로컬 및 다중 서버 작업에 대 한 작업 기록이 삭제 됩니다 *oldest_date*합니다. 때 **SQLAgentOperatorRole** 사용자가 이러한 인수를 지정 하지 않으면, 지정 된 시간 내에서 모든 로컬 작업에 대 한 작업 기록이 삭제 됩니다 *oldest_date*합니다.  
  
 [ **@job_id=** ] *job_id*  
 레코드를 삭제할 작업의 ID입니다. *job_id*은 **uniqueidentifier**, 기본값은 NULL입니다. 어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. 에 대 한 설명에 나와 있는 참고를 참조 하십시오.  **@job_name**  방법에 대 한 정보에 대 한 **sysadmin** 또는 **SQLAgentOperatorRole** 사용자는이 인수를 사용할 수 있습니다.  
  
 [ **@oldest_date** = ] *oldest_date*  
 기록에 보존할 가장 오래된 레코드입니다. *oldest_date* 은 **datetime**, 기본값은 NULL입니다. 때 *oldest_date* 지정 된 **sp_purge_jobhistory** 만 지정 된 값 보다 오래 된 레코드를 제거 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 때 **sp_purge_jobhistory** 완료 되 면 메시지가 반환 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만 기본적으로는 **sysadmin** 고정된 서버 역할 또는 **SQLAgentOperatorRole** 고정된 데이터베이스 역할에서이 저장된 프로시저를 실행할 수 있습니다. 멤버 **sysadmin** 모든 로컬 및 다중 서버 작업에 대 한 작업 기록을 제거할 수 있습니다. 멤버 **SQLAgentOperatorRole** 만으로 모든 로컬 작업에 대 한 작업 기록을 제거할 수 있습니다.  
  
 멤버를 포함 하 여 다른 사용자가 **SQLAgentUserRole** 의 구성원과 **SQLAgentReaderRole**, 명시적으로 권한을 부여 해야는 EXECUTE에 **sp_purge_jobhistory**. 이러한 사용자는 이 저장 프로시저에 대해 EXECUTE 권한을 부여 받은 다음에도 각자 소유한 작업에 대한 기록만 제거할 수 있습니다.  
  
 **SQLAgentUserRole**, **SQLAgentReaderRole**, 및 **SQLAgentOperatorRole** 고정된 데이터베이스 역할은는 **msdb** 데이터베이스입니다. 해당 사용 권한에 대 한 세부 정보를 참조 하십시오. [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-remove-history-for-a-specific-job"></a>1. 특정 작업의 기록 제거  
 다음 예에서는 `NightlyBackups`이라는 작업의 기록을 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-remove-history-for-all-jobs"></a>2. 모든 작업의 기록 제거  
  
> [!NOTE]  
>  구성원만는 **sysadmin** 고정 서버 역할의 멤버는 **SQLAgentOperatorRole** 모든 작업에 대 한 기록을 제거할 수 있습니다. 때 **sysadmin** 매개 변수 없이이 저장된 프로시저를 실행 하는 사용자, 모든 로컬 및 다중 서버 작업에 대 한 작업 기록을 제거 됩니다. 때 **SQLAgentOperatorRole** 매개 변수 없이이 저장된 프로시저를 실행 하는 사용자, 모든 로컬 작업에 대 한 작업 기록만 제거 됩니다.  
  
 다음 예에서는 매개 변수 없이 프로시저를 실행하여 모든 기록 레코드를 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_help_job&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobhistory &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [GRANT 개체 사용 권한 &#40; Transact SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
  
