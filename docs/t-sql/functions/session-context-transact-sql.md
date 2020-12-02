---
description: SESSION_CONTEXT (Transact-SQL)
title: SESSION_CONTEXT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SESSION_CONTEXT
- sys.SESSION_CONTEXT
- SESSION_CONTEXT_TSQL
- sys.SESSION_CONTEXT_TSQL
helpviewer_keywords:
- SESSION_CONTEXT function
ms.assetid: b6bdbc54-331a-43cc-ab3d-3872d6a12100
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: eb971143c7de2bdbf683b24f81162e088ffd2a8e
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91378838"
---
# <a name="session_context-transact-sql"></a>SESSION_CONTEXT (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  현재 세션 컨텍스트에서 지정된 키의 값을 반환합니다. 이 값은 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md) 프로시저를 사용하여 설정됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
SESSION_CONTEXT(N'key')  
```  
  
## <a name="arguments"></a>인수
 'key'  
 검색되는 값의 키(sysname 형식)입니다.  
  
## <a name="return-type"></a>반환 형식  
 **sql_variant**  
  
## <a name="return-value"></a>Return Value  
 세션 컨텍스트에서 지정된 키와 연관된 값이거나 해당 키에 값이 설정되지 않은 경우 NULL입니다.  
  
## <a name="permissions"></a>사용 권한  
 모든 사용자는 해당 세션에 대한 세션 컨텍스트를 읽을 수 있습니다.  
  
## <a name="remarks"></a>설명  
 SESSION_CONTEXT의 MARS 동작은 CONTEXT_INFO의 그것과 유사합니다. MARS 일괄 처리가 키-값 쌍을 설정하는 경우 새 값을 완료로 설정하는 일괄 처리를 시작하지 않았다면 동일한 연결의 다른 MARS 일괄 처리에서 새 값을 반환하지 않습니다. 다중 MARS 일괄 처리가 연결에서 활성 상태인 경우 값을 "read_only"로 설정할 수 없습니다. 이렇게 하면 어떤 값이 "이길지"에 관한 경쟁 조건 및 비결정론이 방지됩니다.  
  
## <a name="examples"></a>예제  
 다음 간단한 예에서는 키 `user_id`의 세션 컨텍스트 값을 4로 설정한 다음, **SESSION_CONTEXT** 함수를 사용하여 값을 검색합니다.  
  
```sql  
EXEC sp_set_session_context 'user_id', 4;  
SELECT SESSION_CONTEXT(N'user_id');  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_set_session_context&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [행 수준 보안](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO  &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO&#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
