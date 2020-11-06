---
description: DBCC FREESYSTEMCACHE(Transact-SQL)
title: DBCC FREESYSTEMCACHE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FREESYSTEMCACHE_TSQL
- DBCC_FREESYSTEMCACHE_TSQL
- DBCC FREESYSTEMCACHE
- FREESYSTEMCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- clearing unused cache entries
- DBCC FREESYSTEMCACHE statement
- unused cache entries
- releasing unused cache entries
- freeing unused cache entries
- cleaning unused cache entries
ms.assetid: 4b5c460b-e4ad-404a-b4ca-d65aba38ebbb
author: pmasl
ms.author: umajay
ms.openlocfilehash: 0069e1fc2a6991df71291fd377aaa76e10f23256
ms.sourcegitcommit: b09f069c6bef0655b47e9953a4385f1b52bada2b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92734633"
---
# <a name="dbcc-freesystemcache-transact-sql"></a>DBCC FREESYSTEMCACHE(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

모든 캐시의 사용하지 않는 캐시 항목을 모두 해제합니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 현재 항목에 필요한 메모리 확보를 위해 사용하지 않는 캐시 항목을 백그라운드에서 미리 정리합니다. 그러나 이 명령으로 모든 캐시나 지정된 Resource Governor 풀 캐시에서 사용하지 않는 항목을 수동으로 제거할 수 있습니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
```syntaxsql
DBCC FREESYSTEMCACHE   
    ( 'ALL' [, pool_name ] )   
    [WITH   
    { [ MARK_IN_USE_FOR_REMOVAL ] , [ NO_INFOMSGS ]  }  
    ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
( 'ALL' [, _pool\_name_ ] )  
ALL은 지원되는 모든 캐시를 지정합니다.  
_pool\_name_ 은 Resource Governor 풀 캐시를 지정합니다. 이 풀과 연결된 항목만 해제됩니다. 사용 가능한 풀 이름을 나열하려면 다음을 실행합니다.

```sql
SELECT name FROM sys.dm_os_memory_clerks
```

이 명령을 사용하여 대부분의(전부는 아님) 캐시를 개별적으로 해제할 수 있습니다.
  
MARK_IN_USE_FOR_REMOVAL  
현재 사용 중인 항목을 더 이상 사용하지 않게 되면 각 캐시에서 비동기적으로 해제합니다. DBCC FREESYSTEMCACHE WITH MARK_IN_USE_FOR_REMOVAL이 실행된 후 캐시에 만들어진 새 항목은 영향을 받지 않습니다.  
  
NO_INFOMSGS  
모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="remarks"></a>설명  
DBCC FREESYSTEMCACHE를 실행하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 계획 캐시가 삭제됩니다. 계획 캐시를 삭제하면 모든 예정된 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. 계획 캐시의 삭제된 각 캐시 저장소에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 다음과 같은 정보 메시지가 있습니다.

>`SQL Server has encountered %d occurrence(s) of cachestore flush for the '%s' cachestore (part of plan cache) due to 'DBCC FREEPROCCACHE' or 'DBCC FREESYSTEMCACHE' operations.`

 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.

## <a name="result-sets"></a>결과 집합  
DBCC FREESYSTEMCACHE는 다음을 반환합니다. “DBCC 실행이 완료되었습니다. DBCC에서 오류 메시지를 출력하면 시스템 관리자에게 문의하세요."
  
## <a name="permissions"></a>사용 권한  
서버에 대한 ALTER SERVER STATE 권한이 필요합니다.
  
## <a name="examples"></a>예제  
  
### <a name="a-releasing-unused-cache-entries-from-a-resource-governor-pool-cache"></a>A. 리소스 관리자 풀 캐시에서 사용하지 않는 캐시 항목 해제  
다음 예에서는 지정된 리소스 관리자 리소스 풀에만 사용되는 캐시를 정리하는 방법을 설명합니다.
  
```sql
-- Clean all the caches with entries specific to the resource pool named "default".  
DBCC FREESYSTEMCACHE ('ALL', default);  
```  
  
### <a name="b-releasing-entries-from-their-respective-caches-after-they-become-unused"></a>B. 캐시에서 더 이상 사용되지 않는 항목 해제  
다음 예에서는 MARK_IN_USE_FOR_REMOVAL 절을 사용하여 모든 현재 캐시에서 더 이상 사용되지 않는 항목을 해제합니다.
  
```sql
DBCC FREESYSTEMCACHE ('ALL') WITH MARK_IN_USE_FOR_REMOVAL;  
```  
  
## <a name="see-also"></a>참고 항목  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)  
[DBCC FREESESSIONCACHE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)  
[리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)
  
  
