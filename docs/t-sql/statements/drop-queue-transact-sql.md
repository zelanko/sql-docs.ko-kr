---
title: DROP QUEUE (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP QUEUE
- DROP_QUEUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping queues
- queues [Service Broker], removing
- deleting queues
- DROP QUEUE statement
- removing queues
ms.assetid: fd866520-ca00-477d-b2e9-0110e9610ed4
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51920e14a3a24f9bfb48f11c07414812da1694b9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-queue-transact-sql"></a>DROP QUEUE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 큐를 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP QUEUE <object>  
[ ; ]  
  
<object> ::=  
{  
    [ database_name . [ schema_name ] . | schema_name . ]  
        queue_name  
}  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 삭제할 큐가 있는 데이터베이스의 이름입니다. No *database_name* 제공 되는 현재 데이터베이스에 대 한 기본값입니다.  
  
 *schema_name (개체)*  
 삭제할 큐를 소유하는 스키마의 이름입니다. No *schema_name* 제공 되는 현재 사용자의 기본 스키마는 기본값입니다.  
  
 *queue_name*  
 삭제할 큐의 이름입니다.  
  
## <a name="remarks"></a>주의  
 서비스에서 참조하는 큐는 삭제할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 큐 삭제 권한은 기본적으로 큐의 구성원의 소유자는 **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할의 멤버는 **sysadmin** 고정 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 삭제는 **ExpenseQueue** 현재 데이터베이스의 큐입니다.  
  
```  
DROP QUEUE ExpenseQueue ;  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE QUEUE&#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER queue&#40; Transact SQL &#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

