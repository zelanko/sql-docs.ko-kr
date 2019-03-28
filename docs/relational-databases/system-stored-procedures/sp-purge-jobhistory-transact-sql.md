---
title: sp_purge_jobhistory (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_purge_jobhistory_TSQL
- sp_purge_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_jobhistory
ms.assetid: 237f9bad-636d-4262-9bfb-66c034a43e88
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ab2f2fcb07fb181fd32d5a60f9fd2d8f25725f96
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535685"
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
`[ @job_name = ] 'job_name'` 기록 레코드를 삭제 하는 작업의 이름입니다. *job_name*됩니다 **sysname**, 기본값은 NULL입니다. 어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
> [!NOTE]  
>  멤버는 **sysadmin** 고정 서버 역할의 멤버는 **SQLAgentOperatorRole** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_purge_jobhistory** 를지정하지않고*job_name* 하거나 *job_id*합니다. 때 **sysadmin** 사용자가 이러한 인수를 지정 하지 않으면, 지정 된 시간 내 모든 로컬 및 다중 서버 작업에 대 한 작업 기록이 삭제 됩니다 *oldest_date*합니다. 때 **SQLAgentOperatorRole** 사용자가 이러한 인수를 지정 하지 않으면, 지정 된 시간 내 모든 로컬 작업에 대 한 작업 기록이 삭제 됩니다 *oldest_date*합니다.  
  
`[ @job_id = ] job_id` 삭제할 레코드에 대 한 작업의 작업 id. *job_id*됩니다 **uniqueidentifier**, 기본값은 NULL입니다. 어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. 에 대 한 설명을 참조 하십시오 **@job_name** 방법은 **sysadmin** 하거나 **SQLAgentOperatorRole** 사용자는이 인수를 사용할 수 있습니다.  
  
`[ @oldest_date = ] oldest_date` 기록에 보존할 가장 오래 된 레코드입니다. *oldest_date* 됩니다 **datetime**, 기본값은 NULL입니다. 때 *oldest_date* 를 지정 하면 **sp_purge_jobhistory** 만 지정 된 값 보다 오래 된 레코드를 제거 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 때 **sp_purge_jobhistory** 완료 되 면 메시지가 반환 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로의 멤버만 합니다 **sysadmin** 고정된 서버 역할 또는 **SQLAgentOperatorRole** 고정된 데이터베이스 역할에서이 저장된 프로시저를 실행할 수 있습니다. 멤버인 **sysadmin** 모든 로컬 및 다중 서버 작업에 대 한 작업 기록을 제거할 수 있습니다. 멤버인 **SQLAgentOperatorRole** 만으로 모든 로컬 작업에 대 한 작업 기록을 제거할 수 있습니다.  
  
 멤버를 포함 한 다른 사용자 **SQLAgentUserRole** 회원과 **SQLAgentReaderRole**, 명시적으로 권한을 부여 해야 합니다 EXECUTE에 **sp_purge_jobhistory**. 이러한 사용자는 이 저장 프로시저에 대해 EXECUTE 권한을 부여 받은 다음에도 각자 소유한 작업에 대한 기록만 제거할 수 있습니다.  
  
 합니다 **SQLAgentUserRole**를 **SQLAgentReaderRole**, 및 **SQLAgentOperatorRole** 고정된 데이터베이스 역할에는 **msdb** 데이터베이스입니다. 해당 사용 권한에 대 한 자세한 내용은 참조 하세요 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)입니다.  
  
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
>  구성원만 합니다 **sysadmin** 고정 서버 역할의 멤버 및 합니다 **SQLAgentOperatorRole** 모든 작업에 대 한 기록을 제거할 수 있습니다. 때 **sysadmin** 매개 변수 없이이 저장된 프로시저를 실행 하는 사용자, 모든 로컬 및 다중 서버 작업에 대 한 작업 기록을 제거 됩니다. 때 **SQLAgentOperatorRole** 매개 변수 없이이 저장된 프로시저를 실행 하는 사용자, 모든 로컬 작업에 대 한 작업 기록만 제거 됩니다.  
  
 다음 예에서는 매개 변수 없이 프로시저를 실행하여 모든 기록 레코드를 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_help_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobhistory &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [GRANT 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
  
