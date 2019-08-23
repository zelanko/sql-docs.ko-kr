---
title: sp_add_agent_profile (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_add_agent_profile
- sp_add_agent_profile_TSQL
helpviewer_keywords:
- sp_add_agent_profile
ms.assetid: 5c246a33-2c21-4a77-9c2a-a2c9f0c5dda1
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 24a900409ae5979c13bdbff0d67d9d2670059208
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770850"
---
# <a name="sp_add_agent_profile-transact-sql"></a>sp_add_agent_profile(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  복제 에이전트용 새 프로필을 작성합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_agent_profile [ [ @profile_id= ] profile_id OUTPUT ]  
        , [ @profile_name= ] 'profile_name'   
        , [ @agent_type= ] 'agent_type' ]   
    [ , [ @profile_type= ] profile_type ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @default= ] default ]  
```  
  
## <a name="arguments"></a>인수  
`[ @profile_id = ] profile_id`새로 삽입 된 프로필과 연결 된 ID입니다. *profile_id* 은 **INT** 이며 선택적 출력 매개 변수입니다. 지정한 경우 값이 새 프로필 ID로 설정됩니다.  
  
`[ @profile_name = ] 'profile_name'`프로필의 이름입니다. *profile_name* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @agent_type = ] 'agent_type'`복제 에이전트의 유형입니다. *agent_type* 은 **int**이며 기본값은 없고 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|스냅숏 에이전트|  
|**2**|로그 판독기 에이전트|  
|**3**|배포 에이전트|  
|**4**|병합 에이전트|  
|**9**|큐 판독기 에이전트|  
  
`[ @profile_type = ] profile_type`프로필의 유형입니다. *profile_type* 은 **int**이며 기본값은 **1**입니다.  
  
 **0** 은 시스템 프로필을 나타냅니다. **1** 은 사용자 지정 프로필을 나타냅니다. 이 저장 프로시저를 사용 하 여 사용자 지정 프로필을 만들 수 있습니다. 따라서 유일 하 게 유효한 값은 **1**입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 시스템 프로필만 만듭니다.[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
`[ @description = ] 'description'`프로필에 대 한 설명입니다. *description* 은 **nvarchar (3000)** 이며 기본값은 없습니다.  
  
`[ @default = ] default`프로필이 *agent_type * ** 에 대 한 기본값 인지 여부를 나타냅니다. *기본값* 은 **bit**이며 기본값은 **0**입니다. **1** 은 추가 중인 프로필이 *agent_type*에서 지정한 에이전트의 새 기본 프로필이 됨을 나타냅니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_add_agent_profile** 는 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
 사용자 지정 에이전트 프로필은 에이전트 매개 변수의 기본값으로 추가됩니다. [ &#40;Sp_change_agent_parameter transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md) 을 사용 하 여 이러한 기본값을 변경 하거나 [sp_add_agent_parameter &#40;&#41; ](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md) 를 사용 하 여 추가 매개 변수를 추가 합니다.  
  
 **Sp_add_agent_profile** 가 실행 되 면 [ &#40;MSagent_profiles transact-sql&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) 테이블에 새 사용자 지정 프로필에 대 한 행이 추가 되 고이 프로필에 대 한 연결 된 기본 매개 변수가 MSagent_parameters에 추가 됩니다. [ &#40;Transact-sql 테이블&#41; ](../../relational-databases/system-tables/msagent-parameters-transact-sql.md)  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_add_agent_profile**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 에이전트 프로필 작업](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [복제 에이전트 프로필](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_parameter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_change_agent_parameter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [sp_change_agent_profile &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_drop_agent_parameter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_drop_agent_profile &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [sp_help_agent_profile &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)  
  
  
