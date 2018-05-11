---
title: DROP MESSAGE TYPE(Transact-SQL) | Microsoft Docs
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
- DROP_MESSAGE_TYPE_TSQL
- DROP MESSAGE TYPE
dev_langs:
- TSQL
helpviewer_keywords:
- message types [Service Broker], removing
- deleting message types
- dropping message types
- DROP MESSAGE TYPE statement
- removing message types
ms.assetid: 805e8ad5-8a93-49f0-88e5-e6fca8814dd5
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8745d96c94ac804982a5230b371059c19bdbfa1e
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="drop-message-type-transact-sql"></a>DROP MESSAGE TYPE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 메시지 유형을 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP MESSAGE TYPE message_type_name  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *message_type_name*  
 삭제할 메시지 유형의 이름입니다. 서버, 데이터베이스 및 스키마 이름은 지정될 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 메시지 유형 삭제 권한은 기본적으로 메시지 유형의 소유자, db_ddladmin 또는 db_owner 고정 데이터베이스 역할의 멤버 및 sysadmin 고정 서버 역할의 멤버로 설정됩니다.  
  
## <a name="remarks"></a>Remarks  
 계약이 메시지 유형을 참조하는 경우에는 메시지 유형을 삭제할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `//Adventure-Works.com/Expenses/SubmitExpense` 메시지 유형을 데이터베이스에서 삭제합니다.  
  
```  
DROP MESSAGE TYPE [//Adventure-Works.com/Expenses/SubmitExpense] ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER MESSAGE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-message-type-transact-sql.md)   
 [CREATE MESSAGE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
