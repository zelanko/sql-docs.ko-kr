---
title: sp_drop_agent_parameter (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ce01a218fd2185c5904baf41014bc0c7caa5ec25
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830215"
---
# <a name="sp_drop_agent_parameter-transact-sql"></a>sp_drop_agent_parameter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSagent_parameters** 테이블의 프로필에서 매개 변수를 하나 또는 모두 삭제 합니다. 이 저장 프로시저는 에이전트가 실행되고 있는 모든 데이터베이스의 배포자에서 실행될 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_drop_agent_parameter [ @profile_id = ] profile_id  
    [ , [ @parameter_name = ] 'parameter_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @profile_id = ] profile_id`매개 변수를 삭제할 프로필의 ID입니다. *profile_id* 는 **int**이며 기본값은 없습니다.  
  
`[ @parameter_name = ] 'parameter_name'`삭제할 매개 변수의 이름입니다. *parameter_name* 는 **sysname**이며 기본값은 **%** 입니다. 인 경우 **%** 지정 된 프로필에 대 한 모든 매개 변수가 삭제 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_drop_agent_parameter** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_drop_agent_parameter**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_agent_parameter &#40;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [Transact-sql&#41;sp_help_agent_parameter &#40;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
