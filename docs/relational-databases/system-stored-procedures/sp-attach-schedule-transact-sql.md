---
description: sp_attach_schedule(Transact-SQL)
title: sp_attach_schedule (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_attach_schedule_TSQL
- sp_attach_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_schedule
ms.assetid: 80c80eaf-cf23-4ed8-b8dd-65fe59830dd1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8108bdad26c02b02ae2e88b1780fada126e2c797
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464492"
---
# <a name="sp_attach_schedule-transact-sql"></a>sp_attach_schedule(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  작업의 일정을 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_attach_schedule  
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     { [ @schedule_id = ] schedule_id   
     | [ @schedule_name = ] 'schedule_name' }  
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] job_id` 일정이 추가 된 작업의 id입니다. *job_id*은 **uniqueidentifier**이며 기본값은 NULL입니다.  
  
`[ @job_name = ] 'job_name'` 일정을 추가할 작업의 이름입니다. *job_name*는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *Job_id* 또는 *job_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다.  
  
`[ @schedule_id = ] schedule_id` 작업에 대해 설정할 일정의 일정 id입니다. *schedule_id*은 **int**이며 기본값은 NULL입니다.  
  
`[ @schedule_name = ] 'schedule_name'` 작업에 대해 설정할 일정의 이름입니다. *schedule_name*는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *Schedule_id* 또는 *schedule_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다.  
  
## <a name="remarks"></a>설명  
 일정과 작업의 소유자는 같아야 합니다.  
  
 일정은 둘 이상의 작업에 대해 설정할 수 있습니다. 작업은 둘 이상의 일정으로 실행할 수 있습니다.  
  
 이 저장 프로시저는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 작업 소유자는 일정 소유자가 아니어도 작업을 일정에 연결하고 일정에서 작업을 분리할 수 있습니다. 하지만 호출자가 일정 소유자가 아닌 한 분리를 통해 일정에 남은 작업이 없도록 일정을 삭제할 수 없습니다.  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 사용자가 작업과 일정을 둘 다 소유하고 있는지 확인합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `NightlyJobs`라는 일정을 만듭니다. 서버 시간이 `01:00`일 때 이 일정을 사용하는 작업이 매일 실행됩니다. 이 예에서는 `BackupDatabase` 작업과 `RunReports` 작업에 일정을 연결합니다.  
  
> [!NOTE]  
>  이 예에서는 `BackupDatabase` 작업 및 `RunReports` 작업이 이미 있다고 가정합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_add_schedule  
    @schedule_name = N'NightlyJobs' ,  
    @freq_type = 4,  
    @freq_interval = 1,  
    @active_start_time = 010000 ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'BackupDatabase',  
   @schedule_name = N'NightlyJobs' ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'RunReports',  
   @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [Transact-sql&#41;sp_add_schedule &#40;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_detach_schedule &#40;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_delete_schedule &#40;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
