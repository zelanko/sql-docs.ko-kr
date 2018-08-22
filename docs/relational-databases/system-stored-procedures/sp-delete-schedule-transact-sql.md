---
title: sp_delete_schedule (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_schedule
- sp_delete_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_schedule
ms.assetid: 18b2c985-47b8-49c8-82d1-8a4af3d7d33a
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0a531b3673320e3c1e521e68c511e21b7976d1af
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392402"
---
# <a name="spdeleteschedule-transact-sql"></a>sp_delete_schedule(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  일정을 삭제합니다.  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_schedule { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @force_delete = ] force_delete  
```  
  
## <a name="arguments"></a>인수  
 [ **@schedule_id=** ] *schedule_id*  
 삭제할 일정의 ID입니다. *schedule_id* 됩니다 **int**, 기본값은 NULL입니다.  
  
> **참고:** 중 하나 *schedule_id* 하거나 *schedule_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
 [ **@schedule_name=** ] **'***schedule_name***'**  
 삭제할 일정의 이름입니다. *schedule_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> **참고:** 중 하나 *schedule_id* 하거나 *schedule_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
 [ **@force_delete** =] *force_delete*  
 일정을 작업에 연결할 경우 프로시저의 실패 여부를 지정합니다. *Force_delete* 는 bit 이며 기본값은 **0**합니다. 때 *force_delete* 됩니다 **0**, 일정을 작업에 연결 되어 있으면 저장된 프로시저가 실패 합니다. 때 *force_delete* 됩니다 **1**, 작업에 일정 연결 되었는지 여부에 관계 없이 일정이 삭제 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 기본적으로 작업에 연결된 일정은 삭제할 수 없습니다. 작업에 연결 된 일정을 삭제 하려면 값을 지정 **1** 에 대 한 *force_delete*합니다. 일정을 삭제해도 현재 실행 중인 작업은 중지되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 작업 소유자는 일정 소유자가 아니어도 작업을 일정에 연결하고 일정에서 작업을 분리할 수 있습니다. 하지만 호출자가 일정 소유자가 아닌 한 분리를 통해 일정에 남은 작업이 없도록 일정을 삭제할 수 없습니다.  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 멤버는 **sysadmin** 역할에는 다른 사용자가 소유한 작업 일정을 삭제할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-deleting-a-schedule"></a>1. 일정 삭제  
 다음 예에서는 `NightlyJobs`이라는 일정을 삭제합니다. 이 예에서는 작업에 연결된 일정을 삭제하지 않습니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="b-deleting-a-schedule-attached-to-a-job"></a>2. 작업에 연결된 일정 삭제  
 다음은 일정이 작업에 연결되었는지 여부에 관계없이 `RunOnce`라는 일정을 삭제하는 예입니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_schedule  
    @schedule_name = 'RunOnce',  
    @force_delete = 1;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [작업 구현](../../ssms/agent/implement-jobs.md)   
 [sp_add_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)  
  
  
