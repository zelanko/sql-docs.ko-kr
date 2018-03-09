---
title: sp_set_session_context (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- sp_set_session_context
- sp_set_session_context_TSQL
- sys.sp_set_session_context
- sys.sp_set_session_context_TSQL
helpviewer_keywords:
- sp_set_session_context
ms.assetid: 7a3a3b2a-1408-4767-a376-c690e3c1fc5b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a55ee31e1f4d9f5f98766550f60a16d3dd56843c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spsetsessioncontext-transact-sql"></a>sp_set_session_context (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

세션 컨텍스트에서 키-값 쌍을 설정합니다.  
  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_set_session_context [ @key= ] 'key', [ @value= ] 'value'  
    [ , [ @read_only = ] { 0 | 1 } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 [ @key=] 'key'  
 설정 되는 형식의 키 **sysname**합니다. 최대 키 크기가 128 바이트입니다.  
  
 [ @value=] 'value'  
 형식의 지정된 된 키에 대 한 값 **sql_variant**합니다. NULL 값을 설정 하는 메모리를 해제 합니다. 최대 크기는 8,000바이트입니다.  
  
 [ @read_only= ] { 0 | 1 }  
 형식의 플래그가 **비트**합니다. 1 인 경우, 다음 지정된 된 키에 대 한 값에서 변경할 수 없습니다 다시이 논리적 연결 합니다. 경우 0 (기본값) 다음 값을 변경할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 모든 사용자가 세션에 대 한 세션 컨텍스트를 설정할 수 있습니다.  
  
## <a name="remarks"></a>주의  
 다른 저장된 프로시저와 같은 리터럴 및 변수 (not 식 또는 함수 호출)만 매개 변수로 전달할 수 있습니다.  
  
 세션 컨텍스트의 총 크기는 256kb로 제한 합니다. 이 제한을 초과할 발생 하는 값 집합에는 문이 실패 합니다. 전체 메모리 사용량을 모니터링할 수 있습니다 [sys.dm_os_memory_objects &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).  
  
 쿼리하여 메모리의 전반적인 사용량을 모니터링할 수 있습니다 [sys.dm_os_memory_cache_counters &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md) 다음과 같습니다.`SELECT * FROM sys.dm_os_memory_cache_counters WHERE type = 'CACHESTORE_SESSION_CONTEXT';`  
  
## <a name="examples"></a>예  
 다음 예제에서는 설정 하 고 다음 값이 영어 언어 세션 컨텍스트 키를 반환 하는 방법을 보여 줍니다.  
  
```  
EXEC sp_set_session_context 'language', 'English';  
SELECT SESSION_CONTEXT(N'language');  
```  
  
 다음 예제에서는 선택적 읽기 전용 플래그의 사용을 보여 줍니다.  
  
```  
EXEC sp_set_session_context 'user_id', 4, @read_only = 1;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CURRENT_TRANSACTION_ID &#40; Transact SQL &#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [SESSION_CONTEXT&#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)   
 [행 수준 보안](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO &#40; Transact SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40; Transact SQL &#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
