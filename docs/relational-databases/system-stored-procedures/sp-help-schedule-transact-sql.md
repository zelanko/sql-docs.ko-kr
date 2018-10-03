---
title: sp_help_schedule (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 62a8246c6d694ae002a615e803c520127ab595c8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47630187"
---
# <a name="sphelpschedule-transact-sql"></a>sp_help_schedule(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  일정에 관한 정보를 나열합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_schedule   
     [ @schedule_id = ] id ,  
     [ @schedule_name = ] 'schedule_name'   
     [ , [ @attached_schedules_only = ] attached_schedules_only ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@schedule_id =** ] *id*  
 나열할 일정의 식별자입니다. *schedule_name* 됩니다 **int**, 기본값은 없습니다. 어느 *schedule_id* 하거나 *schedule_name* 지정할 수 있습니다.  
  
 [ **@schedule_name =** ] **'***schedule_name***'**  
 나열할 일정의 이름입니다. *schedule_name* 됩니다 **sysname**, 기본값은 없습니다. 어느 *schedule_id* 하거나 *schedule_name* 지정할 수 있습니다.  
  
 [ **@attached_schedules_only** =] *attached_schedules_only* ]  
 작업이 연결되어 있는 일정만 표시할지 여부를 지정합니다. *attached_schedules_only* 됩니다 **비트**, 기본값은 **0**합니다. 때 *attached_schedules_only* 됩니다 **0**, 모든 일정이 표시 됩니다. 때 *attached_schedules_only* 됩니다 **1**, 결과 집합은 작업에 연결 되어 있는 일정만 포함 합니다.  
  
 [ **@include_description** =] *include_description*  
 결과 집합에 설명을 포함할지 여부를 지정합니다. *include_description* 됩니다 **비트**, 기본값은 **0**합니다. 때 *include_description* 됩니다 **0**의 *schedule_description* 자리 표시자를 포함 하는 결과 집합의 열입니다. 때 *include_description* 됩니다 **1**에 일정 설명이 결과 집합에 포함 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 이 프로시저는 다음 결과 집합을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|일정 ID입니다.|  
|**schedule_uid**|**uniqueidentifier**|일정에 대한 식별자입니다.|  
|**schedule_name**|**sysname**|일정 이름입니다.|  
|**enabled**|**int**|일정을 사용할지 (**1**) 또는 사용 안 함 (**0**).|  
|**freq_type**|**int**|작업을 실행할 때를 지정하는 값입니다.<br /><br /> **1** = 1<br /><br /> **4** = 매일<br /><br /> **8** = 매주<br /><br /> **16** = 매월<br /><br /> **32** = 매월을 기준으로 **freq_interval**<br /><br /> **64** = SQLServerAgent 서비스를 시작할 때 실행 합니다.|  
|**freq_interval**|**int**|작업이 실행되는 요일입니다. 값의 값에 따라 달라 집니다 **freq_type**합니다. 자세한 내용은 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)합니다.|  
|**freq_subday_type**|**int**|에 대 한 단위 **freq_subday_interval**합니다. 자세한 내용은 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)합니다.|  
|**freq_subday_interval**|**int**|수가 **freq_subday_type** 작업의 각 실행 간에 발생 하는 기간. 자세한 내용은 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)합니다.|  
|**freq_relative_interval**|**int**|작업의 발생을 예약 합니다 **freq_interval** 매월에서 합니다. 자세한 내용은 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)합니다.|  
|**freq_recurrence_factor**|**int**|작업의 예정된 실행 간의 개월 수입니다.|  
|**active_start_date**|**int**|일정을 활성화하는 날짜입니다.|  
|**active_end_date**|**int**|일정을 종료하는 날짜입니다.|  
|**active_start_time**|**int**|일정을 시작하는 시간입니다.|  
|**active_end_time**|**int**|일정을 종료하는 시간입니다.|  
|**date_created**|**datetime**|일정을 만든 날짜입니다.|  
|**schedule_description**|**nvarchar(4000)**|일정에 관한 영어 설명입니다(요청된 경우에 한함).|  
|**job_count**|**int**|이 일정을 참조하는 작업 수를 반환합니다.|  
  
## <a name="remarks"></a>Remarks  
 매개 변수 없이 제공 하는 경우 **sp_help_schedule** 인스턴스의 모든 일정에 대 한 정보를 나열 합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 멤버인 **SQLAgentUserRole** 자신이 소유한 일정만 볼 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-information-for-all-schedules-in-the-instance"></a>1. 인스턴스의 모든 일정에 대한 정보 나열  
 다음 예에서는 인스턴스에 있는 모든 일정에 대한 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-schedule"></a>2. 특정 일정에 대한 정보 나열  
 다음 예에서는 `NightlyJobs`라는 일정에 대한 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
