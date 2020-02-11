---
title: sp_set_session_context (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_set_session_context
- sp_set_session_context_TSQL
- sys.sp_set_session_context
- sys.sp_set_session_context_TSQL
helpviewer_keywords:
- sp_set_session_context
ms.assetid: 7a3a3b2a-1408-4767-a376-c690e3c1fc5b
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a57bf4acff6f8d0d08f86852de5ecc0411211c67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104390"
---
# <a name="sp_set_session_context-transact-sql"></a>sp_set_session_context (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

세션 컨텍스트에서 키-값 쌍을 설정 합니다.  
  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_set_session_context [ @key= ] N'key', [ @value= ] 'value'  
    [ , [ @read_only = ] { 0 | 1 } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 [ @key= ] N'key'  
 **Sysname**형식의 설정 되는 키입니다. 최대 키 크기는 128 바이트입니다.  
  
 [ @value= ] 기본값  
 **Sql_variant**형식의 지정 된 키에 대 한 값입니다. NULL 값을 설정 하면 메모리를 해제 합니다. 최대 크기는 8,000바이트입니다.  
  
 [ @read_only= ] {0 | 1}  
 **Bit**형식의 플래그입니다. 1 인 경우이 논리 연결에서 지정 된 키의 값을 다시 변경할 수 없습니다. 0 (기본값) 이면 값을 변경할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 모든 사용자는 세션에 대 한 세션 컨텍스트를 설정할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 다른 저장 프로시저와 마찬가지로 리터럴 및 변수 (식 또는 함수 호출 아님)만 매개 변수로 전달할 수 있습니다.  
  
 세션 컨텍스트의 총 크기는 1mb로 제한 됩니다. 이 제한을 초과 하는 값을 설정 하면 문이 실패 합니다. [Dm_os_memory_objects &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)에서 전체 메모리 사용량을 모니터링할 수 있습니다.  
  
 다음과 같이 [dm_os_memory_cache_counters &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md) 을 쿼리하여 전체 메모리 사용량을 모니터링할 수 있습니다.`SELECT * FROM sys.dm_os_memory_cache_counters WHERE type = 'CACHESTORE_SESSION_CONTEXT';`  
  
## <a name="examples"></a>예  
 다음 예에서는 값이 영어 인 세션 컨텍스트 키를 설정 하 고 반환 하는 방법을 보여 줍니다.  
  
```  
EXEC sys.sp_set_session_context @key = N'language', @value = 'English';  
SELECT SESSION_CONTEXT(N'language');  
```  
  
 다음 예제에서는 선택적 읽기 전용 플래그를 사용 하는 방법을 보여 줍니다.  
  
```  
EXEC sys.sp_set_session_context @key = N'user_id', @value = 4, @read_only = 1;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [Transact-sql&#41;SESSION_CONTEXT &#40;](../../t-sql/functions/session-context-transact-sql.md)   
 [행 수준 보안](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO  &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO&#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
