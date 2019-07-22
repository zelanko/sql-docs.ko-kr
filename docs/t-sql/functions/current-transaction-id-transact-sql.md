---
title: CURRENT_TRANSACTION_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CURRENT_TRANSACTION_ID
- CURRENT_TRANSACTION_ID_TSQL
- sys.CURRENT_TRANSACTION_ID
- sys.CURRENT_TRANSACTION_ID_TSQL
helpviewer_keywords:
- CURRENT_TRANSACTION_ID function
ms.assetid: 82cd9f92-d935-45a0-a433-620d6e15b467
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6bd6cbe675fa5e9aba72fc545d1108c3aad6f930
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026339"
---
# <a name="currenttransactionid-transact-sql"></a>CURRENT_TRANSACTION_ID(Transact_SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

이 함수는 현재 세션에서 현재 트랜잭션의 트랜잭션 ID를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CURRENT_TRANSACTION_ID( )  
  
```  
  
## <a name="return-types"></a>반환 형식
**bigint**
  
## <a name="return-value"></a>반환 값  
[sys.dm_tran_current_transaction&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-current-transaction-transact-sql.md)에서 가져온 현재 세션에서 현재 트랜잭션의 트랜잭션 ID입니다.
  
## <a name="permissions"></a>사용 권한  
모든 사용자는 현재 세션의 트랜잭션 ID를 반환할 수 있습니다.
  
## <a name="examples"></a>예  
이 예에서는 현재 세션의 트랜잭션 ID를 반환합니다.
  
```sql
SELECT CURRENT_TRANSACTION_ID();  
```  
  
## <a name="see-also"></a>관련 항목:
[sp_set_session_context&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)  
[SESSION_CONTEXT&#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)  
[행 수준 보안](../../relational-databases/security/row-level-security.md)  
[CONTEXT_INFO&#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)  
[SET CONTEXT_INFO&#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  
