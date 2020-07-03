---
title: sp_delete_jobschedule (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobschedule
- sp_delete_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobschedule
ms.assetid: 82fbb48b-603a-4016-a7fb-1ce17fb76919
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8a74d7235b1faa80c1fe65f80717c39e7944f343
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85864267"
---
# <a name="sp_delete_jobschedule-transact-sql"></a>sp_delete_jobschedule(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  작업의 일정을 삭제합니다.  
  
 **sp_delete_jobschedule** 은 이전 버전과의 호환성을 위해서만 제공 됩니다.  
  
  
## <a name="remarks"></a>설명  
 이제 작업 일정을 작업과 독립적으로 관리할 수 있습니다. 작업에서 일정을 제거 하려면 **sp_detach_schedule**을 사용 합니다. 일정을 삭제 하려면 **sp_delete_schedule**을 사용 합니다.  
  
> **참고: sp_delete_jobschedule** 는 여러 작업에 연결 된 일정을 지원 하지 않습니다. 기존 스크립트에서 **sp_delete_jobschedule** 를 호출 하 여 둘 이상의 작업에 연결 된 일정을 제거 하는 경우 프로시저에서 오류를 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **Sysadmin** 역할의 멤버는 작업 일정을 삭제할 수 있습니다. **Sysadmin** 역할의 멤버가 아닌 사용자는 자신이 소유한 작업 일정만 삭제할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_delete_schedule &#40;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_detach_schedule &#40;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)   
 [작업 보기 또는 수정](../../ssms/agent/view-or-modify-jobs.md)   
 [Transact-sql&#41;sp_add_schedule &#40;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [Transact-sql&#41;sp_help_jobschedule &#40;](../../relational-databases/system-stored-procedures/sp-help-jobschedule-transact-sql.md)   
 [Transact-sql&#41;sp_update_jobschedule &#40;](../../relational-databases/system-stored-procedures/sp-update-jobschedule-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
