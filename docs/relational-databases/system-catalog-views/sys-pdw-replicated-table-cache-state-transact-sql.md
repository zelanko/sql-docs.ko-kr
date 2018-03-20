---
title: sys.pdw_replicated_table_cache_state (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: barbkess
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5efc510645a6a5648c4d1e2c6e2c05567159e6e2
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="syspdwreplicatedtablecachestate-transact-sql"></a>sys.pdw_replicated_table_cache_state (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  복제 된 테이블에 연결 된 캐시의 상태를 반환 **object_id**합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|테이블에 대 한 개체 ID입니다. 참조 [sys.objects &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)합니다.<br /><br /> **object_id** 이 보기에 대 한 키입니다.||  
|state|**nvarchar(40)**|이 테이블에 대 한 복제 테이블 캐시 상태입니다.|'NotReady','Ready'|  
  
## <a name="example"></a>예제
이 예에서는 테이블 이름 및 복제 테이블 캐시의 상태를 검색 하는 sys.tables와 sys.pdw_replicated_table_cache_state를 조인 합니다.

```sql
SELECT t.[name], p.[object_id], p.[state]
  FROM sys.pdw_replicated_table_cache_state p 
  JOIN sys.tables t ON t.object_id = p.object_id
```



## <a name="next-steps"></a>다음 단계  
 SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스에 대 한 모든 카탈로그 뷰 목록, 참조 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)합니다.   
  
