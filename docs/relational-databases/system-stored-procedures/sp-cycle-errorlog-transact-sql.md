---
description: sp_cycle_errorlog(Transact-SQL)
title: sp_cycle_errorlog (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 433accd75ac9bf5c5f2e390aa1bcbf0a1c5e0a6e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549921"
---
# <a name="sp_cycle_errorlog-transact-sql"></a>sp_cycle_errorlog(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재의 오류 로그 파일을 닫고 서버를 다시 시작하는 것처럼 오류 로그 확장 번호를 순환시킵니다. 새 오류 로그는 버전, 저작권에 관한 정보 및 새 로그가 작성되었음을 표시하는 행을 포함합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_cycle_errorlog  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이 시작 될 때마다 현재 오류 로그의 이름이 오류 로그로 바뀝니다 **. 1**; **오류 로그 1** 은 **오류 로그 2**, **오류 로그 2** 는 **오류 로그 3**등이 됩니다. **sp_cycle_errorlog** 를 사용 하면 서버를 중지 하 고 시작 하지 않고 오류 로그 파일을 순환할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sp_cycle_errorlog** 에 대 한 실행 권한은 **sysadmin** 고정 서버 역할의 멤버로 제한 됩니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그를 순환시킵니다.  
  
```  
EXEC sp_cycle_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_cycle_agent_errorlog &#40;](../../relational-databases/system-stored-procedures/sp-cycle-agent-errorlog-transact-sql.md)  
  
  
