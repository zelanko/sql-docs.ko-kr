---
title: DROP BROKER PRIORITY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_BROKER_PRIORITY_TSQL
- DROP BROKER PRIORITY
dev_langs:
- TSQL
helpviewer_keywords:
- DROP BROKER PRIORITY statement
ms.assetid: 09ee6c5b-af94-4a4b-a0e2-f9eac50e43aa
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 254914f3b92289faf19a37b4651e7c95804ac791
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-broker-priority-transact-sql"></a>DROP BROKER PRIORITY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에서 대화 우선 순위를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP BROKER PRIORITY ConversationPriorityName  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *ConversationPriorityName*  
 제거할 대화 우선 순위의 이름을 지정합니다.  
  
## <a name="remarks"></a>주의  
 대화 우선 순위를 삭제해도 기존의 모든 대화는 대화 우선 순위에 할당된 우선 순위 수준대로 계속 작동합니다.  
  
## <a name="permissions"></a>Permissions  
 대화 우선 순위를 만들 수 있는 권한은 기본적으로 db_ddladmin 또는 db_owner 고정 데이터베이스 역할 및 sysadmin 고정 서버 역할의 멤버에게 있습니다. 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `InitiatorAToTargetPriority`라는 대화 우선 순위를 삭제합니다.  
  
```  
DROP BROKER PRIORITY InitiatorAToTargetPriority;  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER BROKER PRIORITY &#40; Transact SQL &#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [BROKER 우선 순위 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [sys.conversation_priorities &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  

