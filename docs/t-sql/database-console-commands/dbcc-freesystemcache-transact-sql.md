---
title: DBCC FREESYSTEMCACHE(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d5c6924da3ef9ac85683c857c786337b9d9b978b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-freesystemcache-transact-sql"></a>DBCC FREESYSTEMCACHE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

모든 캐시의 사용하지 않는 캐시 항목을 모두 해제합니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 현재 항목에 필요한 메모리 확보를 위해 사용하지 않는 캐시 항목을 백그라운드에서 미리 정리합니다. 그러나 이 명령으로 모든 캐시나 지정된 리소스 관리자 풀 캐시에서 사용하지 않는 항목을 수동으로 제거할 수 있습니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
```sql
DBCC FREESYSTEMCACHE   
    ( 'ALL' [, pool_name ] )   
    [WITH   
    { [ MARK_IN_USE_FOR_REMOVAL ] , [ NO_INFOMSGS ]  }  
    ]  
```  
  
## <a name="arguments"></a>인수  
 ( 'ALL' [,*pool_name* ] )  
 ALL은 지원되는 모든 캐시를 지정합니다.  
 *pool_name*은 Resource Governor 풀 캐시를 지정합니다. 이 풀과 연결된 항목만 삭제할 수 있습니다.  
  
 MARK_IN_USE_FOR_REMOVAL  
 현재 사용 중인 항목을 더 이상 사용하지 않게 되면 각 캐시에서 비동기적으로 삭제합니다. DBCC FREESYSTEMCACHE WITH MARK_IN_USE_FOR_REMOVAL이 실행된 후 캐시에 작성된 새 항목은 영향을 받지 않습니다.  
  
 NO_INFOMSGS  
 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="remarks"></a>Remarks  
DBCC FREESYSTEMCACHE를 실행하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 계획 캐시가 삭제됩니다. 계획 캐시를 삭제하면 모든 후속 실행 계획이 다시 컴파일되며 일시적으로 갑자기 쿼리 성능이 저하될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 "'DBCC FREEPROCCACHE' 또는 'DBCC FREESYSTEMCACHE' 작업으로 인해 '%s' 캐시스토어(계획 캐시의 일부)에 대한 캐시스토어 플러시가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 %d번 발견되었습니다"라는 계획 캐시의 삭제된 각 캐시스토어에 대한 정보 메시지가 있습니다. 이 메시지는 캐시가 해당 시간 간격 내에 플러시되는 동안 5분마다 기록됩니다.

## <a name="result-sets"></a>결과 집합  
DBCC FREESYSTEMCACHE는 다음을 반환합니다. “DBCC 실행이 완료되었습니다. DBCC에서 오류 메시지를 출력하면 시스템 관리자에게 문의하세요."
  
## <a name="permissions"></a>사용 권한  
서버에 대한 ALTER SERVER STATE 권한이 필요합니다.
  
## <a name="examples"></a>예  
  
### <a name="a-releasing-unused-cache-entries-from-a-resource-governor-pool-cache"></a>1. 리소스 관리자 풀 캐시에서 사용하지 않는 캐시 항목 해제  
다음 예에서는 지정된 리소스 관리자 리소스 풀에만 사용되는 캐시를 정리하는 방법을 설명합니다.
  
```sql
-- Clean all the caches with entries specific to the resource pool named "default".  
DBCC FREESYSTEMCACHE ('ALL', default);  
```  
  
### <a name="b-releasing-entries-from-their-respective-caches-after-they-become-unused"></a>2. 캐시에서 더 이상 사용되지 않는 항목 해제  
다음 예에서는 MARK_IN_USE_FOR_REMOVAL 절을 사용하여 모든 현재 캐시에서 더 이상 사용되지 않는 항목을 해제합니다.
  
```sql
DBCC FREESYSTEMCACHE ('ALL') WITH MARK_IN_USE_FOR_REMOVAL;  
```  
  
## <a name="see-also"></a>참고 항목  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC FREEPROCCACHE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)  
[DBCC FREESESSIONCACHE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)  
[리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)
  
  
