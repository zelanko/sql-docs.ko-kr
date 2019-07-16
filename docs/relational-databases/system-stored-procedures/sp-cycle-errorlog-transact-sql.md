---
title: sp_cycle_errorlog (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cycle_errorlog_TSQL
- sp_cycle_errorlog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cycle_errorlog
ms.assetid: 61a12cbf-78a3-4052-8604-3b29d07573fd
author: stevestein
ms.author: sstein
ms.openlocfilehash: c15a36678bf0bd1ff5fc933eb79bff96b6780b60
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108341"
---
# <a name="spcycleerrorlog-transact-sql"></a>sp_cycle_errorlog(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재의 오류 로그 파일을 닫고 서버를 다시 시작하는 것처럼 오류 로그 확장 번호를 순환시킵니다. 새 오류 로그는 버전, 저작권에 관한 정보 및 새 로그가 작성되었음을 표시하는 행을 포함합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cycle_errorlog  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시작 하 고, 현재 오류 로그로 바뀌었습니다 **errorlog.1')** ; **errorlog.1')** 됩니다 **errorlog.2**합니다 **errorlog.2** 됩니다 **errorlog.3**등입니다. **sp_cycle_errorlog** 중지 하 고 서버를 시작 하지 않고 오류 로그 파일을 순환 시킬 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 실행 권한은 **sp_cycle_errorlog** 의 멤버로 제한 되는 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그를 순환시킵니다.  
  
```  
EXEC sp_cycle_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cycle_agent_errorlog &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cycle-agent-errorlog-transact-sql.md)  
  
  
