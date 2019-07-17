---
title: sp_add_agent_parameter (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_add_agent_parameter_TSQL
- sp_add_agent_parameter
helpviewer_keywords:
- sp_add_agent_parameter
ms.assetid: 055f4765-0574-47c3-bf7d-6ef6e9bd8b34
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: a61b85090dc88dddbb28c923f4acdc6e8fa07cb7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941804"
---
# <a name="spaddagentparameter-transact-sql"></a>sp_add_agent_parameter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  에이전트의 프로필에 새 매개 변수와 그 값을 추가합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_agent_parameter [ @profile_id = ] profile_id  
        , [ @parameter_name = ] 'parameter_name'   
        , [ @parameter_value = ] 'parameter_value'   
```  
  
## <a name="arguments"></a>인수  
`[ @profile_id = ] profile_id` 프로필의 id를 **MSagent_profiles** 테이블에 **msdb** 데이터베이스입니다. *profile_id* 됩니다 **int**, 기본값은 없습니다.  
  
 이 에이전트 유형을 확인 하려면 *profile_id* 나타내는 *profile_id* 에 [MSagent_profiles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) 테이블 및 참고는 *agent_type* 필드 값입니다. 값은 다음과 같습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|스냅샷 에이전트|  
|**2**|로그 판독기 에이전트|  
|**3**|배포 에이전트|  
|**4**|병합 에이전트|  
|**9**|큐 판독기 에이전트|  
  
`[ @parameter_name = ] 'parameter_name'` 매개 변수의 이름이입니다. *parameter_name* 됩니다 **sysname**, 기본값은 없습니다. 시스템 프로필에 이미 정의 된 매개 변수 목록을 참조 하세요 [복제 에이전트 프로필](../../relational-databases/replication/agents/replication-agent-profiles.md)합니다. 각 에이전트에 대해 유효한 매개 변수의 전체 목록은 다음 항목을 참조하십시오.  
  
-   [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
-   [복제 로그 판독기 에이전트](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [복제 병합 에이전트](../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [Replication Queue Reader Agent](../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
`[ @parameter_value = ] 'parameter_value'` 매개 변수에 할당할 값이입니다. *parameter_value* 됩니다 **nvarchar(255)** , 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_add_agent_parameter** 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_add_agent_parameter**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 에이전트 프로필 작업](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [복제 에이전트 프로필](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_profile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_change_agent_profile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_change_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [sp_drop_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)  
  
  
