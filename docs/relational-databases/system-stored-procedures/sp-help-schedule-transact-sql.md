---
title: sp_help_schedule (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_schedule
- sp_help_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_schedule
ms.assetid: b2fc4ce1-0a8e-44d2-b206-7dc7b258d8c9
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 59223cb9ba6fd0a7129966fa49aef4d8e7e67eb3
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
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
 나열할 일정의 식별자입니다. *schedule_name* 은 **int**, 기본값은 없습니다. 어느 *schedule_id* 또는 *schedule_name* 지정할 수 있습니다.  
  
 [ **@schedule_name =** ] **'***schedule_name***'**  
 나열할 일정의 이름입니다. *schedule_name* 은 **sysname**, 기본값은 없습니다. 어느 *schedule_id* 또는 *schedule_name* 지정할 수 있습니다.  
  
 [ **@attached_schedules_only** = ] *attached_schedules_only* ]  
 작업이 연결되어 있는 일정만 표시할지 여부를 지정합니다. *attached_schedules_only* 은 **비트**, 기본값은 **0**합니다. 때 *attached_schedules_only* 은 **0**, 모든 일정이 표시 됩니다. 때 *attached_schedules_only* 은 **1**, 결과 집합을 작업에 연결 되어 있는 일정만 포함 합니다.  
  
 [ **@include_description** = ] *include_description*  
 결과 집합에 설명을 포함할지 여부를 지정합니다. *include_description* 은 **비트**, 기본값은 **0**합니다. 때 *include_description* 은 **0**, *schedule_description* 자리 표시자를 포함 하는 결과 집합의 열입니다. 때 *include_description* 은 **1**는 일정 설명이 결과 집합에 포함 됩니다.  
  
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
|**freq_type**|**int**|작업을 실행할 때를 지정하는 값입니다.<br /><br /> **1** = Once<br /><br /> **4** = 매일<br /><br /> **8** = 매주<br /><br /> **16** = 매월<br /><br /> **32** 기준으로 = 매월는 **freq_interval**<br /><br /> **64** = SQLServerAgent 서비스를 시작할 때 실행 됩니다.|  
|**freq_interval**|**int**|작업이 실행되는 요일입니다. 값의 값에 따라 **freq_type**합니다. 자세한 내용은 참조 [sp_add_schedule &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_type**|**int**|에 대 한 단위 **freq_subday_interval**합니다. 자세한 내용은 참조 [sp_add_schedule &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_interval**|**int**|수가 **freq_subday_type** 작업의 실행 사이 발생 하는 기간. 자세한 내용은 참조 [sp_add_schedule &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_relative_interval**|**int**|작업 발생 횟수의 예약 된 **freq_interval** 각 월에 합니다. 자세한 내용은 참조 [sp_add_schedule &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_recurrence_factor**|**int**|작업의 예정된 실행 간의 개월 수입니다.|  
|**active_start_date**|**int**|일정을 활성화하는 날짜입니다.|  
|**active_end_date**|**int**|일정을 종료하는 날짜입니다.|  
|**active_start_time**|**int**|일정을 시작하는 시간입니다.|  
|**active_end_time**|**int**|일정을 종료하는 시간입니다.|  
|**date_created**|**datetime**|일정을 만든 날짜입니다.|  
|**schedule_description**|**nvarchar(4000)**|일정에 관한 영어 설명입니다(요청된 경우에 한함).|  
|**job_count**|**int**|이 일정을 참조하는 작업 수를 반환합니다.|  
  
## <a name="remarks"></a>주의  
 매개 변수를 제공 **sp_help_schedule** 인스턴스에 있는 모든 일정에 대 한 정보를 나열 합니다.  
  
## <a name="permissions"></a>Permissions  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)을 참조하세요.  
  
 멤버 **SQLAgentUserRole** 는 각자 소유한 일정만 볼 수 있습니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [sp_add_schedule&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
