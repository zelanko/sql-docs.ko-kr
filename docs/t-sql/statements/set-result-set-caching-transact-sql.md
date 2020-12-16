---
description: SET RESULT_SET_CACHING(Transact-SQL)
title: SET RESULT_SET_CACHING(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest
ms.openlocfilehash: 01636cde074298c3c503e65f55b60595e44a6416
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471814"
---
# <a name="set-result-set-caching-transact-sql"></a>SET RESULT SET CACHING (Transact-SQL) 

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

현재 클라이언트 세션에 대한 결과 집합 동작을 제어합니다.  

[!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]에 적용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문

```syntaxsql
SET RESULT_SET_CACHING { ON | OFF };
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="remarks"></a>설명  

result_set_caching 설정을 구성하려는 사용자 데이터베이스에 연결된 상태에서 이 명령을 실행합니다.

**ON**   
현재 클라이언트 세션에 대한 결과 집합 캐싱을 설정합니다.  데이터베이스 수준에서 결과 집합 캐싱이 OFF인 경우 세션에서 ON으로 설정할 수 없습니다.

**OFF**   
현재 클라이언트 세션에 대한 결과 집합 캐싱을 사용하지 않도록 설정합니다.

## <a name="examples"></a>예제

쿼리의 request_id로 [sys.dm_pdw_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)의 result_cache_hit 열을 쿼리하여 이 쿼리가 결과 캐시 적중 또는 결과 캐시 누락 중 어떤 상태로 실행되었는지 확인합니다.

```sql
SELECT result_cache_hit
FROM sys.dm_pdw_exec_requests
WHERE request_id = 'QID58286'
```

## <a name="permissions"></a>사용 권한

public 역할의 멤버 자격이 필요

## <a name="see-also"></a>참고 항목

- [결과 집합 캐싱을 사용한 성능 조정](/azure/sql-data-warehouse/performance-tuning-result-set-caching)
- [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](./alter-database-transact-sql-set-options.md?preserve-view=true&view=azure-sqldw-latest)
- [ALTER DATABASE&#40;Transact-SQL&#41;](./alter-database-transact-sql.md?preserve-view=true&view=azure-sqldw-latest)
- [DBCC SHOWRESULTCACHESPACEUSED(Transact-SQL)](../database-console-commands/dbcc-showresultcachespaceused-transact-sql.md)
- [DBCC DROPRESULTSETCACHE (Transact-SQL)](../database-console-commands/dbcc-dropresultsetcache-transact-sql.md)