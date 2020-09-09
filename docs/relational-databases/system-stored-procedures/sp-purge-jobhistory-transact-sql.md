---
description: sp_purge_jobhistory(Transact-SQL)
title: sp_purge_jobhistory (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c804e5fbeb61a62ae7a615d09085e0dea8ee61d0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535040"
---
# <a name="sp_purge_jobhistory-transact-sql"></a>sp_purge_jobhistory(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  작업에 대한 기록 레코드를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_purge_jobhistory   
   {   [ @job_name = ] 'job_name' |   
     | [ @job_id = ] job_id }  
   [ , [ @oldest_date = ] oldest_date ]  
```  
  
## <a name="arguments"></a>인수  
`[ @job_name = ] 'job_name'` 기록 레코드를 삭제할 작업의 이름입니다. *job_name*는 **sysname**이며 기본값은 NULL입니다. *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다.  
  
> [!NOTE]  
>  **Sysadmin** 고정 서버 역할의 멤버 또는 **SQLAgentOperatorRole** 고정 데이터베이스 역할의 멤버는 *job_name* 또는 *job_id*를 지정 하지 않고 **sp_purge_jobhistory** 을 실행할 수 있습니다. **Sysadmin** 사용자가 이러한 인수를 지정 하지 않으면 *oldest_date*에 지정 된 시간 내에 모든 로컬 및 다중 서버 작업에 대 한 작업 기록이 삭제 됩니다. **SQLAgentOperatorRole** 사용자가 이러한 인수를 지정 하지 않으면 *oldest_date*에 지정 된 시간 내에 모든 로컬 작업에 대 한 작업 기록이 삭제 됩니다.  
  
`[ @job_id = ] job_id` 삭제할 레코드에 대 한 작업의 id입니다. *job_id* 은 **uniqueidentifier**이며 기본값은 NULL입니다. *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다. **Sysadmin** 또는 **SQLAgentOperatorRole** 사용자가이 인수를 사용할 수 있는 방법에 대 한 자세한 내용은 ** \@ job_name** 설명의 참고를 참조 하세요.  
  
`[ @oldest_date = ] oldest_date` 기록에 보존할 가장 오래 된 레코드입니다. *oldest_date* 은 **datetime**이며 기본값은 NULL입니다. *Oldest_date* 지정 된 경우 **sp_purge_jobhistory** 는 지정 된 값 보다 오래 된 레코드만 제거 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **Sp_purge_jobhistory** 성공적으로 완료 되 면 메시지가 반환 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할 또는 **SQLAgentOperatorRole** 고정 데이터베이스 역할의 멤버만이 저장 프로시저를 실행할 수 있습니다. **Sysadmin** 의 멤버는 모든 로컬 및 다중 서버 작업에 대 한 작업 기록을 제거할 수 있습니다. **SQLAgentOperatorRole** 의 멤버는 모든 로컬 작업에 대 한 작업 기록만 제거할 수 있습니다.  
  
 **SQLAgentUserRole** 멤버 및 **SQLAgentReaderRole**멤버를 비롯 한 다른 사용자는 **sp_purge_jobhistory**에 대 한 EXECUTE 권한을 명시적으로 부여 해야 합니다. 이러한 사용자는 이 저장 프로시저에 대해 EXECUTE 권한을 부여 받은 다음에도 각자 소유한 작업에 대한 기록만 제거할 수 있습니다.  
  
 **SQLAgentUserRole**, **SQLAgentReaderRole**및 **SQLAgentOperatorRole** 고정 데이터베이스 역할은 **msdb** 데이터베이스에 있습니다. 사용 권한에 대 한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조 하세요.  
  
## <a name="examples"></a>예제  
  
### <a name="a-remove-history-for-a-specific-job"></a>A. 특정 작업의 기록 제거  
 다음 예에서는 `NightlyBackups`이라는 작업의 기록을 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-remove-history-for-all-jobs"></a>B. 모든 작업의 기록 제거  
  
> [!NOTE]  
>  **Sysadmin** 고정 서버 역할의 멤버 및 **SQLAgentOperatorRole** 의 멤버만 모든 작업에 대 한 기록을 제거할 수 있습니다. **Sysadmin** 사용자가 매개 변수 없이이 저장 프로시저를 실행 하면 모든 로컬 및 다중 서버 작업에 대 한 작업 기록이 제거 됩니다. **SQLAgentOperatorRole** 사용자가 매개 변수 없이이 저장 프로시저를 실행 하면 모든 로컬 작업에 대 한 작업 기록도 제거 됩니다.  
  
 다음 예에서는 매개 변수 없이 프로시저를 실행하여 모든 기록 레코드를 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_help_job &#40;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [Transact-sql&#41;sp_help_jobhistory &#40;](../../relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [GRANT 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
  
