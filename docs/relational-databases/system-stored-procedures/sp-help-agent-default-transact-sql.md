---
title: sp_help_agent_default (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: c0797b8fe4a2ba496b28f0c347eb5349e77e91e0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68762759"
---
# <a name="sp_help_agent_default-transact-sql"></a>sp_help_agent_default(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  매개 변수로 전달된 에이전트 유형에 대한 기본 구성 ID를 검색합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행될 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_agent_default [ @profile_id= ] profile_id OUTPUT   
        , [ @agent_type = ] agent_type  
```  
  
## <a name="arguments"></a>인수  
`[ @profile_id = ] _profile_idOUTPUT`에이전트 유형에 대 한 기본 구성의 ID입니다. *profile_id* 는 **int**이며 기본값은 없습니다. 또한 *profile_id* 는 출력 매개 변수 이며 에이전트 유형에 대 한 기본 구성의 id를 반환 합니다.  
  
`[ @agent_type = ] 'agent_type'`에이전트의 유형입니다. *agent_type* 은 **int**이며 기본값은 없고 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|스냅샷 에이전트입니다.|  
|**2**|로그 판독기 에이전트입니다.|  
|**3**|배포 에이전트입니다.|  
|**4**|병합 에이전트입니다.|  
|**9**|큐 판독기 에이전트|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_help_agent_default** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **replmonitor** 고정 데이터베이스 역할의 멤버만 **sp_help_agent_default**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
