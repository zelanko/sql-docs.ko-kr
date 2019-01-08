---
title: sp_update_agent_profile (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_update_agent_profile_TSQL
- sp_update_agent_profile
helpviewer_keywords:
- sp_update_agent_profile
ms.assetid: cc81f227-0df3-4151-bb4d-4f45ea997b71
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf8ec9183ce1bac5557040aa3256ef5e6499c0f5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52760135"
---
# <a name="spupdateagentprofile-transact-sql"></a>sp_update_agent_profile(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  복제 에이전트에서 사용하는 프로필을 업데이트합니다. 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_update_agent_profile [@agent_type=] agent_type, [ @agent_id= ] agent_id, [ @profile_id= ] profile_id  
```  
  
## <a name="arguments"></a>인수  
 [**@agent_type=**] **'***agent_type***'**  
 에이전트의 유형입니다. *agent_type* 됩니다 **int**이며 기본값은 없고 수 이러한 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|스냅숏 에이전트입니다.|  
|**2**|로그 판독기 에이전트입니다.|  
|**3**|배포 에이전트입니다.|  
|**4**|병합 에이전트입니다.|  
|**9**|큐 판독기 에이전트입니다.|  
  
 [**@agent_id=**] *agent_id*  
 에이전트의 ID입니다. *agent_id* 됩니다 **int**, 기본값은 없습니다.  
  
 [**@profile_id=**] *profile_id*  
 에이전트가 사용해야 하는 프로필의 ID입니다. *profile_id* 됩니다 **int**, 기본값은 없습니다. 각 에이전트에 대해 정의 된 프로필의 목록을 보려면 사용 하 여 [sp_help_agent_profile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)합니다. 시스템 프로필에 대 한 자세한 내용은 참조 하세요. [복제 에이전트 프로필](../../relational-databases/replication/agents/replication-agent-profiles.md)합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_update_agent_profile** 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_update_agent_profile**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 에이전트 프로필](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_change_agent_profile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_profile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
