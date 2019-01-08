---
title: sp_drop_agent_parameter (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_drop_agent_parameter_TSQL
- sp_drop_agent_parameter
helpviewer_keywords:
- sp_drop_agent_parameter
ms.assetid: b99e65ff-9cca-4dce-a2ce-2968de23a76a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bd8c367f3fecd0c9951b577fdcdf31cf77ac589e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52821947"
---
# <a name="spdropagentparameter-transact-sql"></a>sp_drop_agent_parameter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  프로필에서 하나 또는 모든 매개 변수를 삭제 합니다 **MSagent_parameters** 테이블입니다. 이 저장 프로시저는 에이전트가 실행되고 있는 모든 데이터베이스의 배포자에서 실행될 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_drop_agent_parameter [ @profile_id = ] profile_id  
    [ , [ @parameter_name = ] 'parameter_name' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@profile_id=**] *profile_id*  
 매개 변수를 삭제할 프로필의 ID입니다. *profile_id* 됩니다 **int**, 기본값은 없습니다.  
  
 [  **@parameter_name=**] **'***parameter_name***'**  
 삭제할 매개 변수의 이름입니다. *parameter_name* 됩니다 **sysname**, 기본값은 **%** 합니다. 하는 경우 **%**, 지정된 된 프로필에 대 한 모든 매개 변수가 삭제 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_drop_agent_parameter** 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_drop_agent_parameter**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_add_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
