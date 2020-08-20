---
description: DROP QUEUE(Transact-SQL)
title: DROP QUEUE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 28269fcc3c3b4e43e1343bb13abb72d1716a5b0a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478808"
---
# <a name="drop-queue-transact-sql"></a>DROP QUEUE(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  기존 큐를 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
DROP QUEUE <object>  
[ ; ]  
  
<object> ::=  
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *database_name*  
 삭제할 큐가 있는 데이터베이스의 이름입니다. *database_name*을 제공하지 않으면 기본값은 현재 데이터베이스입니다.  
  
 *schema_name (object)*  
 삭제할 큐를 소유하는 스키마의 이름입니다. *schema_name*을 제공하지 않으면 기본값은 현재 사용자의 기본 스키마입니다.  
  
 *queue_name*  
 삭제할 큐의 이름입니다.  
  
## <a name="remarks"></a>설명  
 서비스에서 참조하는 큐는 삭제할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 큐를 삭제할 수 있는 권한은 기본적으로 큐의 소유자, **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할의 멤버 및 **sysadmin** 고정 서버 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 현재 데이터베이스에서 **ExpenseQueue** 큐를 삭제합니다.  
  
```  
DROP QUEUE ExpenseQueue ;  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE QUEUE&#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER QUEUE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
