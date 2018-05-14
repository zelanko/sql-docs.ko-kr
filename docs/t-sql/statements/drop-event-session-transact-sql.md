---
title: DROP EVENT SESSION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP_EVENT_SESSION_TSQL
- DROP EVENT SESSION
dev_langs:
- TSQL
helpviewer_keywords:
- event sessions [SQL Server]
- DROP EVENT SESSION statement
ms.assetid: 92eabe4b-24e2-43b1-978c-31a199964b90
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 90e1c64844e16aea1b404c2356363337cb354725
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="drop-event-session-transact-sql"></a>DROP EVENT SESSION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이벤트 세션을 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP EVENT SESSION event_session_name  
ON SERVER  
```  
  
## <a name="arguments"></a>인수  
 *event_session_name*  
 기존 이벤트 세션의 이름입니다.  
  
## <a name="remarks"></a>Remarks  
 이벤트 세션을 삭제하면 대상 및 세션 매개 변수와 같은 모든 구성 정보가 완전히 제거됩니다.  
  
## <a name="permissions"></a>사용 권한  
 ALTER ANY EVENT SESSION 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이벤트 세션 삭제 방법을 보여 줍니다.  
  
```  
DROP EVENT SESSION evt_spin_lock_diagnosis  
ON SERVER;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [sys.server_event_sessions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)  
  
  
