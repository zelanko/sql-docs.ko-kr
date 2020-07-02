---
title: sp_detach_schedule (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_detach_schedule
- sp_detach_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_schedule
ms.assetid: 9a1fc335-1bef-4638-a33a-771c54a5dd19
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b183a121981cc32ca7cdd3857c4e9ee10fa7f83e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717350"
---
# <a name="sp_detach_schedule-transact-sql"></a>sp_detach_schedule(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  일정과 작업 간 연결을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_detach_schedule   
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
       { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @delete_unused_schedule = ] delete_unused_schedule   
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] job_id`일정을 제거할 작업의 id입니다. *job_id* 은 **uniqueidentifier**이며 기본값은 NULL입니다.  
  
`[ @job_name = ] 'job_name'`일정을 제거할 작업의 이름입니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다.  
  
`[ @schedule_id = ] schedule_id`작업에서 제거할 일정의 일정 id입니다. *schedule_id* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @schedule_name = ] 'schedule_name'`작업에서 제거할 일정의 이름입니다. *schedule_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *Schedule_id* 또는 *schedule_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다.  
  
`[ @delete_unused_schedule = ] delete_unused_schedule`사용 하지 않는 작업 일정을 삭제할지 여부를 지정 합니다. *delete_unused_schedule* 은 **bit**이며 기본값은 **0**입니다. 즉, 모든 일정을 참조 하는 작업이 없는 경우에도 모든 일정이 유지 됩니다. **1**로 설정 되 면 작업을 참조 하지 않는 경우 사용 하지 않는 작업 일정이 삭제 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 작업 소유자는 일정 소유자가 아니어도 작업을 일정에 연결하고 일정에서 작업을 분리할 수 있습니다. 하지만 호출자가 일정 소유자가 아닌 한 분리를 통해 일정에 남은 작업이 없도록 일정을 삭제할 수 없습니다.  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자가 일정을 소유하는지 여부를 확인합니다. **Sysadmin** 고정 서버 역할의 멤버만 다른 사용자가 소유한 작업의 일정을 분리할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `'NightlyJobs'` 일정과 `'BackupDatabase'` 작업 간 연결을 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_detach_schedule  
    @job_name = 'BackupDatabase',  
    @schedule_name = 'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_schedule &#40;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_attach_schedule &#40;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_delete_schedule &#40;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
