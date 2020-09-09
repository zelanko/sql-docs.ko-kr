---
description: sp_drop_agent_profile(Transact-SQL)
title: sp_drop_agent_profile (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_drop_agent_profile
- sp_drop_agent_profile_TSQL
helpviewer_keywords:
- sp_drop_agent_profile
ms.assetid: b884f9ef-ae89-4cbc-a917-532c3ff6ed41
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6a3864e61e681ad6465295b1fb43011e8d9f9b19
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549820"
---
# <a name="sp_drop_agent_profile-transact-sql"></a>sp_drop_agent_profile(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSagent_profiles** 테이블에서 프로필을 삭제 합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_drop_agent_profile [ @profile_id = ] profile_id  
```  
  
## <a name="arguments"></a>인수  
`[ @profile_id = ] profile_id` 삭제할 프로필의 ID입니다. *profile_id* 는 **int**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_drop_agent_profile** 은 모든 유형의 복제에 사용 됩니다.  
  
 지정 된 프로필의 매개 변수도 **MSagent_parameters** 테이블에서 삭제 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_drop_agent_profile**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_agent_profile &#40;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [Transact-sql&#41;sp_change_agent_profile &#40;](../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)   
 [Transact-sql&#41;sp_help_agent_profile &#40;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
