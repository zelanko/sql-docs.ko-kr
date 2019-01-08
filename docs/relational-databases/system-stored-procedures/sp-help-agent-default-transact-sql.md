---
title: sp_help_agent_default (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_default
- sp_help_agent_default_TSQL
helpviewer_keywords:
- sp_help_agent_default
ms.assetid: 7ba55e39-05dd-43c7-b5da-b268ed8426dd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9ee9596b578396786da8562f2ecf73c3b85f0241
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588037"
---
# <a name="sphelpagentdefault-transact-sql"></a>sp_help_agent_default(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  매개 변수로 전달된 에이전트 유형에 대한 기본 구성 ID를 검색합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행될 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_agent_default [ @profile_id= ] profile_id OUTPUT   
        , [ @agent_type = ] agent_type  
```  
  
## <a name="arguments"></a>인수  
 [  **@profile_id=**] _profile_id_**출력**  
 에이전트 유형에 대한 기본 구성 ID입니다. *profile_id* 됩니다 **int**, 기본값은 없습니다. *profile_id* 도 출력 매개 변수 이며 에이전트 유형에 대 한 기본 구성의 ID를 반환 합니다.  
  
 [  **@agent_type=**] **'**_agent_type_**'**  
 에이전트의 유형입니다. *agent_type* 됩니다 **int**이며 기본값은 없고 수 이러한 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|스냅숏 에이전트입니다.|  
|**2**|로그 판독기 에이전트입니다.|  
|**3**|배포 에이전트입니다.|  
|**4**|병합 에이전트입니다.|  
|**9**|큐 판독기 에이전트|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_help_agent_default** 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **replmonitor** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_help_agent_default**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
