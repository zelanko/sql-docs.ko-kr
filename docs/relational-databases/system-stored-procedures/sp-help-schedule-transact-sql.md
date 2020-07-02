---
title: sp_help_schedule (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_schedule
- sp_help_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_schedule
ms.assetid: b2fc4ce1-0a8e-44d2-b206-7dc7b258d8c9
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2b14900e32c32a5de50998580a8d0de9ed7eacfb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720306"
---
# <a name="sp_help_schedule-transact-sql"></a>sp_help_schedule(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  일정에 관한 정보를 나열합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_schedule   
     [ @schedule_id = ] id ,  
     [ @schedule_name = ] 'schedule_name'   
     [ , [ @attached_schedules_only = ] attached_schedules_only ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>인수  
`[ @schedule_id = ] id`나열할 일정의 식별자입니다. *schedule_name* 는 **int**이며 기본값은 없습니다. *Schedule_id* 또는 *schedule_name* 를 지정할 수 있습니다.  
  
`[ @schedule_name = ] 'schedule_name'`나열할 일정의 이름입니다. *schedule_name* 는 **sysname**이며 기본값은 없습니다. *Schedule_id* 또는 *schedule_name* 를 지정할 수 있습니다.  
  
`[ @attached_schedules_only = ] attached_schedules_only ]`작업이 연결 된 일정만 표시할지 여부를 지정 합니다. *attached_schedules_only* 은 **bit**이며 기본값은 **0**입니다. *Attached_schedules_only* **0**이면 모든 일정이 표시 됩니다. *Attached_schedules_only* **1**이면 결과 집합에는 작업에 연결 된 일정만 포함 됩니다.  
  
`[ @include_description = ] include_description`결과 집합에 설명을 포함할지 여부를 지정 합니다. *include_description* 은 **bit**이며 기본값은 **0**입니다. *Include_description* 가 **0**이면 결과 집합의 *schedule_description* 열에 자리 표시 자가 포함 됩니다. *Include_description* **1**이면 일정에 대 한 설명이 결과 집합에 포함 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 이 프로시저는 다음 결과 집합을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|일정 ID입니다.|  
|**schedule_uid**|**uniqueidentifier**|일정에 대한 식별자입니다.|  
|**schedule_name**|**sysname**|일정 이름입니다.|  
|**사용**|**int**|일정 사용 (**1**) 또는 사용 안 함 (**0**)을 지정 합니다.|  
|**freq_type**|**int**|작업을 실행할 때를 지정하는 값입니다.<br /><br /> **1** = 한 번<br /><br /> **4** = 매일<br /><br /> **8** = 매주<br /><br /> **16** = 매월<br /><br /> **32** = 매월, **freq_interval** 기준<br /><br /> **64** = SQLServerAgent 서비스를 시작할 때 실행 합니다.|  
|**freq_interval**|**int**|작업이 실행되는 요일입니다. 값은 **freq_type**값에 따라 달라 집니다. 자세한 내용은 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)를 참조 하세요.|  
|**freq_subday_type**|**int**|**Freq_subday_interval**단위입니다. 자세한 내용은 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)를 참조 하세요.|  
|**freq_subday_interval**|**int**|각 작업 실행 사이에 발생 하는 **freq_subday_type** 기간 수입니다. 자세한 내용은 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)를 참조 하세요.|  
|**freq_relative_interval**|**int**|매월 **freq_interval** 예약 된 작업의 발생입니다. 자세한 내용은 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)를 참조 하세요.|  
|**freq_recurrence_factor**|**int**|작업의 예정된 실행 간의 개월 수입니다.|  
|**active_start_date**|**int**|일정을 활성화하는 날짜입니다.|  
|**active_end_date**|**int**|일정을 종료하는 날짜입니다.|  
|**active_start_time**|**int**|일정을 시작하는 시간입니다.|  
|**active_end_time**|**int**|일정을 종료하는 시간입니다.|  
|**date_created**|**datetime**|일정을 만든 날짜입니다.|  
|**schedule_description**|**nvarchar(4000)**|일정에 관한 영어 설명입니다(요청된 경우에 한함).|  
|**job_count**|**int**|이 일정을 참조하는 작업 수를 반환합니다.|  
  
## <a name="remarks"></a>설명  
 매개 변수를 제공 하지 않으면 **sp_help_schedule** 는 인스턴스의 모든 일정에 대 한 정보를 나열 합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **SQLAgentUserRole** 의 멤버는 자신이 소유한 일정만 볼 수 있습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-listing-information-for-all-schedules-in-the-instance"></a>A. 인스턴스의 모든 일정에 대한 정보 나열  
 다음 예에서는 인스턴스에 있는 모든 일정에 대한 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-schedule"></a>B. 특정 일정에 대한 정보 나열  
 다음 예에서는 `NightlyJobs`라는 일정에 대한 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_schedule &#40;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_attach_schedule &#40;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_delete_schedule &#40;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_detach_schedule &#40;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
