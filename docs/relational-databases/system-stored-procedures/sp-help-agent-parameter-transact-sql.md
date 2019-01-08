---
title: sp_help_agent_parameter (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_parameter
- sp_help_agent_parameter_TSQL
helpviewer_keywords:
- sp_help_agent_parameter
ms.assetid: 8fb4a9c3-19af-4a34-8004-572729ba3d15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7c9120872253706d45c813f78b8c437b3ff0484
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52786235"
---
# <a name="sphelpagentparameter-transact-sql"></a>sp_help_agent_parameter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  프로필의 모든 매개 변수를 반환 합니다 [MSagent_parameters &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) 시스템 테이블입니다. 이 저장 프로시저는 에이전트가 실행되고 있는 모든 데이터베이스의 배포자에서 실행될 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_agent_parameter [ [ @profile_id = ] profile_id ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@profile_id=**] *profile_id*  
 프로필의 id를 [MSagent_parameters &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msagent-parameters-transact-sql.md) 테이블입니다. *profile_id* 됩니다 **int**, 기본값은 **-1**, 모든 매개 변수를 반환 하는 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|에이전트 프로필의 ID입니다.|  
|**parameter_name**|**sysname**|매개 변수의 이름입니다.|  
|**value**|**nvarchar(255)**|매개 변수의 값입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_help_agent_parameter** 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **replmonitor** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_help_agent_parameter**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 에이전트 프로필 작업](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [sp_add_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_drop_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
