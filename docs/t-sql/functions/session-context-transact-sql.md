---
title: SESSION_CONTEXT (Transact SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 06/22/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SESSION_CONTEXT
- sys.SESSION_CONTEXT
- SESSION_CONTEXT_TSQL
- sys.SESSION_CONTEXT_TSQL
helpviewer_keywords:
- SESSION_CONTEXT function
ms.assetid: b6bdbc54-331a-43cc-ab3d-3872d6a12100
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 23eea4b51009272ae06987ee2e9c1730750b3d6d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="sessioncontext-transact-sql"></a>SESSION_CONTEXT (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  현재 세션 컨텍스트에서 지정된 된 키의 값을 반환합니다. 사용 하 여 설정 됩니다는 [sp_set_session_context &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md) 프로시저입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SESSION_CONTEXT(N'key')  
```  
  
## <a name="arguments"></a>인수  
 ' key'  
 검색 되는 값의 키 (sysname 형식)입니다.  
  
## <a name="return-type"></a>반환 형식  
 **sql_variant**  
  
## <a name="return-value"></a>반환 값  
 해당 키에 설정 된 값이 없는 경우 세션 컨텍스트 또는 NULL의 지정된 된 키와 연결 된 값입니다.  
  
## <a name="permissions"></a>Permissions  
 모든 사용자가 세션에 대 한 세션 컨텍스트를 읽을 수 있습니다.  
  
## <a name="remarks"></a>주의  
 SESSION_CONTEXT의 MARS 동작은 CONTEXT_INFO 유사 합니다. MARS 일괄 처리는 키-값 쌍을 설정한 경우 새 값이 되지 반환할 다른 MARS 일괄 처리에 같은 연결에서 시작 해야만 이러한 새 값을 설정 하는 일괄 처리 완료 후입니다. MARS 일괄 처리를 여러 연결에서 활성 상태인 경우 값 "read_only"로 설정할 수 없습니다. 이렇게 하면 경합 상태, "wins" 값에 대 한 비 결정성  
  
## <a name="examples"></a>예  
 키에 대 한 세션 컨텍스트 값을 설정 하는 다음의 간단한 예제 `user_id` 4, 사용 하 여 다음에 **SESSION_CONTEXT** 값을 검색 하는 함수입니다.  
  
```  
EXEC sp_set_session_context 'user_id', 4;  
SELECT SESSION_CONTEXT(N'user_id');  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_set_session_context&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [CURRENT_TRANSACTION_ID &#40; Transact SQL &#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [행 수준 보안](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO &#40; Transact SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40; Transact SQL &#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  

