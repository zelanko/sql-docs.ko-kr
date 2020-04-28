---
title: sp_change_agent_profile (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_change_agent_profile
- sp_change_agent_profile_TSQL
helpviewer_keywords:
- sp_change_agent_profile
ms.assetid: e73acf8d-0be8-4197-ba11-fe798d0e2820
author: stevestein
ms.author: sstein
ms.openlocfilehash: c49a710b25bad0cf36115afadc439cbe793981c3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68768917"
---
# <a name="sp_change_agent_profile-transact-sql"></a>sp_change_agent_profile(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [MSagent_profiles &#40;transact-sql&#41;](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) 테이블에 저장 된 복제 에이전트 프로필의 매개 변수를 변경 합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_change_agent_profile [ @profile_id = ] profile_id   
        , [ @property = ] 'property'   
        , [ @value = ] 'value'   
```  
  
## <a name="arguments"></a>인수  
`[ @profile_id = ] profile_id`프로필의 ID입니다. *profile_id* 는 **int**이며 기본값은 없습니다.  
  
`[ @property = ] 'property'`속성의 이름입니다. *속성* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @value = ] 'value'`속성의 새 값입니다. *value* 는 **nvarchar (3000)** 이며 기본값은 없습니다.  
  
 이 표에서는 변경할 수 있는 프로필 속성에 대해 설명합니다.  
  
|속성|설명|  
|--------------|-----------------|  
|**한**|프로필에 관한 설명입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_change_agent_profile** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_change_agent_profile**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_agent_profile &#40;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [Transact-sql&#41;sp_drop_agent_profile &#40;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [Transact-sql&#41;sp_help_agent_profile &#40;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
