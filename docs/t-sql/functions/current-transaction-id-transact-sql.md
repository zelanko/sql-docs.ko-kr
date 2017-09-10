---
title: CURRENT_TRANSACTION_ID (Transact SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CURRENT_TRANSACTION_ID
- CURRENT_TRANSACTION_ID_TSQL
- sys.CURRENT_TRANSACTION_ID
- sys.CURRENT_TRANSACTION_ID_TSQL
helpviewer_keywords:
- CURRENT_TRANSACTION_ID function
ms.assetid: 82cd9f92-d935-45a0-a433-620d6e15b467
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6716663ea2e54fdeb372b2a1ce2aa3e206f785ac
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="currenttransactionid-transact-sql"></a>CURRENT_TRANSACTION_ID (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

현재 세션의 현재 트랜잭션의 트랜잭션 ID를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CURRENT_TRANSACTION_ID( )  
  
```  
  
## <a name="return-types"></a>반환 형식
**bigint**
  
## <a name="return-value"></a>반환 값  
현재 트랜잭션의 현재 세션에서에서 가져온 트랜잭션 ID [sys.dm_tran_current_transaction &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-current-transaction-transact-sql.md).
  
## <a name="permissions"></a>Permissions  
모든 사용자는 현재 세션의 트랜잭션 ID를 반환할 수 있습니다.
  
## <a name="examples"></a>예  
다음 예에서는 현재 세션의 트랜잭션 ID를 반환합니다.
  
```sql
SELECT CURRENT_TRANSACTION_ID();  
```  
  
## <a name="see-also"></a>참고 항목
[sp_set_session_context&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)  
[Session_context&#40; Transact SQL &#41;](../../t-sql/functions/session-context-transact-sql.md)  
[행 수준 보안](../../relational-databases/security/row-level-security.md)  
[CONTEXT_INFO &#40; Transact SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)  
[SET CONTEXT_INFO &#40; Transact SQL &#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  

