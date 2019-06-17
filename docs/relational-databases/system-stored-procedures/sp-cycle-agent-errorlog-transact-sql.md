---
title: sp_cycle_agent_errorlog (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cycle_agent_errorlog
- sp_cycle_agent_errorlog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cycle_agent_errorlog
ms.assetid: 8aa96182-60b7-4d7b-b2a7-ccce70378c6e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dfb1f3ef9dc8bdac81ed7c3a3a490ca91f73ff23
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62507189"
---
# <a name="spcycleagenterrorlog-transact-sql"></a>sp_cycle_agent_errorlog(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 오류 로그 파일을 닫고 서버를 다시 시작하는 것처럼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 오류 로그 확장 번호를 순환시킵니다. 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 오류 로그에는 새 로그가 생성되었음을 나타내는 줄이 포함됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cycle_agent_errorlog  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 시작 하 고, 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 오류 로그로 바뀌었습니다 **SQLAgent.1**; **SQLAgent.1** 됩니다 **SQLAgent.2**합니다 **SQLAgent.2** 됩니다 **SQLAgent.3**등입니다. **sp_cycle_agent_errorlog** 중지 하 고 서버를 시작 하지 않고 오류 로그 파일을 순환 시킬 수 있습니다.  
  
 이 저장된 프로시저에서 실행 되어야 합니다는 **msdb** 데이터베이스입니다.  
  
## <a name="permissions"></a>사용 권한  
 실행 권한은 **sp_cycle_agent_errorlog** 의 멤버로 제한 되는 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 오류 로그를 순환시킵니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_cycle_agent_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_cycle_errorlog &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md)  
  
  
