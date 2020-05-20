---
title: sp_help_agent_profile (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_profile
- sp_help_agent_profile_TSQL
helpviewer_keywords:
- sp_help_agent_profile
ms.assetid: 5637b671-4aa3-497e-9a1c-c99798a1afb4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ae3e555f48958aec87ed012244fae9775fae1619
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826108"
---
# <a name="sp_help_agent_profile-transact-sql"></a>sp_help_agent_profile(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  지정된 에이전트의 프로필을 표시합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_agent_profile [ [ @agent_type = ] agent_type ]   
    [ , [ @profile_id = ] profile_id ]  
```  
  
## <a name="arguments"></a>인수  
`[ @agent_type = ] agent_type`에이전트의 유형입니다. *agent_type* 은 **int**이며 기본값은 **0**이 고 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1**|스냅샷 에이전트|  
|**2**|로그 판독기 에이전트|  
|**3**|배포 에이전트|  
|**4**|병합 에이전트|  
|**9**|큐 판독기 에이전트|  
  
`[ @profile_id = ] profile_id`표시할 프로필의 ID입니다. *profile_id* 는 **int**이며 기본값은 **MSagent_profiles** 테이블의 모든 프로필을 반환 하는 **-1**입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|프로필의 ID입니다.|  
|**profile_name**|**sysname**|에이전트 유형에 대해 고유합니다.|  
|**agent_type**|**int**|**1** = 스냅숏 에이전트<br /><br /> **2** = 로그 판독기 에이전트<br /><br /> **3** = 배포 에이전트<br /><br /> **4** = 병합 에이전트<br /><br /> **9** = 큐 판독기 에이전트|  
|**Type**|**int**|**0** = 시스템<br /><br /> **1** = 사용자 지정|  
|**한**|**varchar (3000)**|프로필에 관한 설명입니다.|  
|**def_profile**|**bit**|해당 프로필이 해당 에이전트 유형에 대한 기본값인지 여부를 지정합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_help_agent_profile** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>권한  
 **Sysadmin** 고정 서버 역할 또는 **replmonitor** 고정 데이터베이스 역할의 멤버만 **sp_help_agent_profile**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 에이전트 프로필 작업](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Transact-sql&#41;sp_add_agent_profile &#40;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [Transact-sql&#41;sp_drop_agent_profile &#40;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [Transact-sql&#41;sp_help_agent_parameter &#40;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)  
  
  
