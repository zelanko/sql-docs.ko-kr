---
title: sp_add_agent_profile (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_add_agent_profile
- sp_add_agent_profile_TSQL
helpviewer_keywords:
- sp_add_agent_profile
ms.assetid: 5c246a33-2c21-4a77-9c2a-a2c9f0c5dda1
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 75184f18fafc70f4e88a4ee8b250c8d9eb80fbc9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32990158"
---
# <a name="spaddagentprofile-transact-sql"></a>sp_add_agent_profile(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [ **@profile_id=** ] *profile_id*  
 새로 삽입된 프로필과 연결된 ID입니다. *profile_id* 은 **int** 이며 선택적 출력 매개 변수입니다. 지정한 경우 값이 새 프로필 ID로 설정됩니다.  
  
 [ **@profile_name=** ] **'***profile_name***'**  
 프로필 이름입니다. *profile_name* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@agent_type=** ] **'***agent_type***'**  
 복제 에이전트 유형입니다. *agent_type* 은 **int**이며 기본값은 없고 수 있습니다 이러한 값 중 하나 여야 합니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**1**|스냅숏 에이전트|  
|**2**|로그 판독기 에이전트|  
|**3**|배포 에이전트|  
|**4**|병합 에이전트|  
|**9**|큐 판독기 에이전트|  
  
 [  **@profile_type=** ] *profile_type*  
 프로필의 유형이입니다. *profile_type* 은 **int**, 기본값은 **1**합니다.  
  
 **0** 시스템 프로필을 나타냅니다. **1** 사용자 지정 프로필을 나타냅니다. 이 저장된 프로시저를 사용 하 여만 사용자 지정 프로필을 만들 수 있습니다. 따라서 유일한 유효 값은 **1**합니다. 만 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 프로필을 만듭니다.  
  
 [  **@description=** ] **'***설명***'**  
 프로필에 대한 설명입니다. *설명* 은 **nvarchar (3000)**, 기본값은 없습니다.  
  
 [  **@default=** ] *기본값*  
 프로필에 대 한 기본값 인지를 나타내는 *agent_type * *입니다.* *기본* 은 **비트**, 기본값은 **0**합니다. **1** 추가한으로 지정 된 에이전트에 대 한 새 기본 프로필이 됩니다 있게 나타냅니다 *agent_type*합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_add_agent_profile** 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
 사용자 지정 에이전트 프로필은 에이전트 매개 변수의 기본값으로 추가됩니다. 사용 하 여 [sp_change_agent_parameter &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md) 이러한 기본값을 변경 하려면 또는 [sp_add_agent_parameter &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md) 추가 매개 변수를 추가 합니다.  
  
 때 **sp_add_agent_profile** 은 실행에서 새 사용자 지정 프로필에 대 한 행이 추가 됩니다는 [MSagent_profiles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) 테이블 및이 대 한 연결 된 기본 매개 변수 프로필에 추가 되 고 [MSagent_parameters &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) 테이블입니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_add_agent_profile**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 에이전트 프로필 작업](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [복제 에이전트 프로필](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [sp_add_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_change_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md)   
 [sp_change_agent_profile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [sp_drop_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_drop_agent_profile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [sp_help_agent_profile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)  
  
  
