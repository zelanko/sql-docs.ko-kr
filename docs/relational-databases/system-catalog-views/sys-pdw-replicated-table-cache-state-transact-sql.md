---
title: sys.pdw_replicated_table_cache_state (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.service: sql-data-warehouse
ms.component: system-objects
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 8d78a537bb2de2ee880551afd3667f308b49ce83
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37985109"
---
# <a name="syspdwreplicatedtablecachestate-transact-sql"></a>sys.pdw_replicated_table_cache_state (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  복제 된 테이블을 사용 하 여 연결 된 캐시의 상태를 반환 **object_id**합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|테이블에 대 한 개체 ID입니다. 참조 [sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)합니다.<br /><br /> **object_id** 는이 보기에 대 한 키입니다.||  
|state|**nvarchar(40)**|이 테이블에 대 한 복제 된 테이블 캐시 상태입니다.|' NotReady', '준비'|  
  
## <a name="example"></a>예제
이 예에서는 테이블 이름 및 복제 된 테이블 캐시의 상태를 검색할 sys.tables 사용 하 여 sys.pdw_replicated_table_cache_state를 조인 합니다.

```sql
SELECT t.[name], p.[object_id], p.[state]
  FROM sys.pdw_replicated_table_cache_state p 
  JOIN sys.tables t ON t.object_id = p.object_id
```



## <a name="next-steps"></a>다음 단계  
 SQL Data Warehouse 및 병렬 데이터 웨어하우스에 대 한 모든 카탈로그 뷰 목록을 참조 하세요 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)합니다.   
  
