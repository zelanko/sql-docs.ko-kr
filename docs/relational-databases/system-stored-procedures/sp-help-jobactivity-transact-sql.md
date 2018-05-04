---
title: sp_help_jobactivity (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_jobactivity_TSQL
- sp_help_jobactivity
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobactivity
ms.assetid: d344864f-b4d3-46b1-8933-b81dec71f511
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1bb61b773fe36078c35c1638e038d7bed4c1ad4c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpjobactivity-transact-sql"></a>sp_help_jobactivity(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업의 런타임 상태에 대한 정보를 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_jobactivity { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @session_id = ] session_id ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@job_id =**] *job_id*  
 작업 ID입니다. *job_id*은 **uniqueidentifier**, 기본값은 NULL입니다.  
  
 [ **@job_name =**] **'***job_name***'**  
 작업의 이름입니다. *job_name*은 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
 [ **@session_id** = ] *session_id*  
 정보를 보고할 세션 ID입니다. *session_id* 은 **int**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 다음 결과 집합을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|에이전트 세션 ID입니다.|  
|**job_id**|**uniqueidentifier**|작업의 ID입니다.|  
|**job_name**|**sysname**|작업의 이름입니다.|  
|**run_requested_date**|**datetime**|작업 실행을 요청한 날짜입니다.|  
|**run_requested_source**|**sysname**|작업 실행을 요청한 원본입니다. 다음 중 하나입니다.<br /><br /> **1** = 일정에 따라 실행<br /><br /> **2** = 경고에 대 한 응답으로 실행<br /><br /> **3** = 시작 시 실행<br /><br /> **4** = 사용자가 실행<br /><br /> **6** = CPU 유휴 일정에 실행|  
|**queued_date**|**datetime**|요청이 대기한 날짜입니다. 작업을 직접 실행한 경우 NULL입니다.|  
|**start_execution_date**|**datetime**|실행 가능한 스레드에 작업이 할당된 날짜입니다.|  
|**last_executed_step_id**|**int**|최근에 실행한 작업 단계의 단계 ID입니다.|  
|**last_exectued_step_date**|**datetime**|최근에 실행한 작업 단계를 실행하기 시작한 시간입니다.|  
|**stop_execution_date**|**datetime**|작업 실행이 중지된 시간입니다.|  
|**next_scheduled_run_date**|**datetime**|작업을 실행하도록 예약된 날짜입니다.|  
|**job_history_id**|**int**|작업 기록 테이블에서 작업 기록의 ID입니다.|  
|**message**|**nvarchar(1024)**|작업을 마지막으로 실행하는 동안 생성되는 메시지입니다.|  
|**run_status**|**int**|작업을 마지막으로 실행했을 때 반환되는 상태입니다. 다음 중 하나입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **3** = 취소<br /><br /> **5** = 알 수 없는 상태|  
|**operator_id_emailed**|**int**|작업이 완료되었을 때 전자 메일을 통해 알림을 받는 운영자의 ID입니다.|  
|**operator_id_netsent**|**int**|통해 알림을 받는 운영자의 ID 번호 **net send** 에서 작업을 완료 합니다.|  
|**operator_id_paged**|**int**|작업이 완료되었을 때 호출기를 통해 알림을 받는 운영자의 ID입니다.|  
  
## <a name="remarks"></a>주의  
 이 프로시저는 작업의 현재 상태에 대한 스냅숏을 제공합니다. 반환된 결과는 요청을 처리하는 당시의 정보를 나타냅니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서는 에이전트 서비스가 시작될 때마다 세션 ID를 만듭니다. 세션 id는 테이블에 저장 되어 **msdb.dbo.syssessions**합니다.  
  
 No *session_id* 제공, 가장 최근의 세션에 대 한 정보를 나열 합니다.  
  
 No *job_name* 또는 *job_id* 제공, 모든 작업에 대 한 정보를 나열 합니다.  
  
## <a name="permissions"></a>Permissions  
 기본적으로의 멤버는 **sysadmin** 고정된 서버 역할에서이 저장된 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)을 참조하세요.  
  
 구성원만 **sysadmin** 다른 사용자가 소유한 작업에 대 한 활동을 볼 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 사용자가 볼 수 있는 권한을 가진 모든 작업의 동작을 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobactivity ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 에이전트 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
