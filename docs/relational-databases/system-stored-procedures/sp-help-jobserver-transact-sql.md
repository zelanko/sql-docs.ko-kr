---
title: sp_help_jobserver (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_jobserver
- sp_help_jobserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobserver
ms.assetid: 57971787-f9f5-4199-9f64-c2b61a308906
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5e1efcd128c2c77bcac729c7a529f9dc909457cc
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sphelpjobserver-transact-sql"></a>sp_help_jobserver(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  주어진 작업의 서버에 관한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_jobserver  
     { [ @job_id = ] job_id   
     | [ @job_name = ] 'job_name' }  
     [ , [ @show_last_run_details = ] show_last_run_details ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@job_id=** ] *job_id*  
 정보를 반환할 작업의 ID입니다. *job_id* 은 **uniqueidentifier**, 기본값은 NULL입니다.  
  
 [ **@job_name=** ] **'***job_name***'**  
 정보를 반환할 작업의 이름입니다. *job_name* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  어느 *job_id* 또는 *job_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
 [  **@show_last_run_details=** ] *show_last_run_details*  
 마지막 실행 정보가 결과 집합의 일부인지 여부입니다. *show_last_run_details* 은 **tinyint**, 기본값은 **0**합니다. **0** 마지막 실행 정보가 포함 되지 않은 및 **1** 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|대상 서버의 ID입니다.|  
|**server_name**|**nvarchar(30)**|대상 서버의 컴퓨터 이름입니다.|  
|**enlist_date**|**datetime**|대상 서버가 마스터 서버에 참여한 날짜입니다.|  
|**last_poll_date**|**datetime**|대상 서버가 마지막으로 마스터 서버를 폴링한 날짜입니다.|  
  
 경우 **sp_help_jobserver** 로 실행 되 *show_last_run_details* 로 설정 **1**, 결과 집합에 이러한 추가 열을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**last_run_date**|**int**|해당 대상 서버에서 작업이 마지막으로 실행을 시작한 날짜입니다.|  
|**last_run_time**|**int**|해당 서버에서 작업이 마지막으로 실행을 시작한 시간입니다.|  
|**last_run_duration**|**int**|해당 대상 서버에서 작업이 마지막으로 실행된 기간(초)입니다.|  
|**last_outcome_message**|**nvarchar(1024)**|작업의 마지막 결과에 대해 설명합니다.|  
|**last_run_outcome**|**int**|해당 서버에서 작업이 마지막으로 실행되었을 때의 결과입니다.<br /><br /> **0** = 실패<br /><br /> **1** = 성공<br /><br /> **3** = 취소<br /><br /> **5** = 알 수 없음|  
  
## <a name="permissions"></a>Permissions  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)을 참조하세요.  
  
 멤버 **SQLAgentUserRole** 자신이 소유한 작업에 대 한 정보를 보기만 할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 마지막 실행 정보를 포함하여 `NightlyBackups` 작업에 대한 정보를 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobserver  
    @job_name = N'NightlyBackups',  
    @show_last_run_details = 1 ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_add_jobserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_jobserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
