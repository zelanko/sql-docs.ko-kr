---
title: sp_update_jobschedule (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_jobschedule_TSQL
- sp_update_jobschedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_jobschedule
ms.assetid: 4df02594-4cd1-49a9-8d97-37c44e4d5423
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5a526a5a304d790cfa0bd373f6c9f7225ffe3d2f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891335"
---
# <a name="sp_update_jobschedule-transact-sql"></a>sp_update_jobschedule(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  지정한 작업에 대한 일정 설정을 변경합니다.  
  
 **sp_update_jobschedule** 은 이전 버전과의 호환성을 위해서만 제공 됩니다.  
  
> [!IMPORTANT]
>  이전 버전의 Microsoft SQL Server에서 사용 된 구문에 대 한 자세한 내용은 Microsoft SQL Server 2000에 대 한 Transact-sql Referencefor 참조 하십시오 *.*  
  
## <a name="remarks"></a>설명  
 이제 작업 일정을 작업과 독립적으로 관리할 수 있습니다. 일정을 업데이트 하려면 **sp_update_schedule**을 사용 합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 **Sysadmin** 의 멤버만이 저장 프로시저를 사용 하 여 다른 사용자가 소유한 작업 일정을 업데이트할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 SQL Server 에이전트](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_update_schedule &#40;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)  
  
  
