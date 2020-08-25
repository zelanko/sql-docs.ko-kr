---
description: CURRENT_TRANSACTION_ID(Transact_SQL)
title: CURRENT_TRANSACTION_ID(Transact_SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 80ef65ccfbd26b74c31ed36adc95730315d2943a
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645968"
---
# <a name="current_transaction_id-transact-sql"></a>CURRENT_TRANSACTION_ID(Transact_SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

이 함수는 현재 세션에서 현재 트랜잭션의 트랜잭션 ID를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
CURRENT_TRANSACTION_ID( )  
  
```  

## <a name="return-types"></a>반환 형식

**bigint**
  
## <a name="return-value"></a>Return Value  
[sys.dm_tran_current_transaction&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-current-transaction-transact-sql.md)에서 가져온 현재 세션에서 현재 트랜잭션의 트랜잭션 ID입니다.
  
## <a name="permissions"></a>사용 권한  
모든 사용자는 현재 세션의 트랜잭션 ID를 반환할 수 있습니다.
  
## <a name="examples"></a>예제  
이 예에서는 현재 세션의 트랜잭션 ID를 반환합니다.
  
```sql
SELECT CURRENT_TRANSACTION_ID();  
```  
  
## <a name="see-also"></a>참고 항목
[sp_set_session_context&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)  
[SESSION_CONTEXT&#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)  
[행 수준 보안](../../relational-databases/security/row-level-security.md)  
[CONTEXT_INFO  &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)  
[SET CONTEXT_INFO&#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  
