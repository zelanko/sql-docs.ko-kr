---
title: DROP MESSAGE TYPE (Transact SQL) | Microsoft Docs
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 859419b6809d1c44486130eadaf30c1411a03b97
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-message-type-transact-sql"></a>DROP MESSAGE TYPE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="permissions"></a>Permissions  
 메시지 유형 삭제 권한은 기본적으로 메시지 유형의 소유자, db_ddladmin 또는 db_owner 고정 데이터베이스 역할의 멤버 및 sysadmin 고정 서버 역할의 멤버로 설정됩니다.  
  
## <a name="remarks"></a>주의  
 계약이 메시지 유형을 참조하는 경우에는 메시지 유형을 삭제할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `//Adventure-Works.com/Expenses/SubmitExpense` 메시지 유형을 데이터베이스에서 삭제합니다.  
  
```  
DROP MESSAGE TYPE [//Adventure-Works.com/Expenses/SubmitExpense] ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER MESSAGE type&#40; Transact SQL &#41;](../../t-sql/statements/alter-message-type-transact-sql.md)   
 [메시지 유형 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
