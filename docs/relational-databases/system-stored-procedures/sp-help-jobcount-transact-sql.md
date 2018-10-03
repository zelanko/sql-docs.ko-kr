---
title: sp_help_jobcount (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobcount
- sp_help_jobcount_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobcount
ms.assetid: ae8ef851-646c-4889-bc11-c8ec78762572
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0274c825b18e1377e337b614068db7fc75c7a917
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47732031"
---
# <a name="sphelpjobcount-transact-sql"></a>sp_help_jobcount(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  일정이 연결된 작업 수를 제공합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_jobcount   
     [ @schedule_name = ] 'schedule_name' ,  
     [ @schedule_id = ] schedule_id   
```  
  
## <a name="arguments"></a>인수  
 [ **@schedule_id=** ] *schedule_id*  
 나열할 일정의 식별자입니다. *schedule_id* 됩니다 **int**, 기본값은 없습니다. 어느 *schedule_id* 하거나 *schedule_name* 지정할 수 있습니다.  
  
 [ **@schedule_name=** ]  **'***schedule_name***'**  
 나열할 일정의 이름입니다. *schedule_name* 됩니다 **sysname**, 기본값은 없습니다. 어느 *schedule_id* 하거나 *schedule_name* 지정할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 다음 결과 집합을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**JobCount**|**int**|지정한 일정에 대한 작업 수입니다.|  
  
## <a name="remarks"></a>Remarks  
 이 프로시저는 지정한 일정에 연결된 작업 수를 나열합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 멤버만 **sysadmin** 다른 사용자가 소유한 작업의 개수를 볼 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `NightlyJobs` 일정에 연결된 작업 수를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_jobcount  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
