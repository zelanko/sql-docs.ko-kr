---
description: sys.pdw_replicated_table_cache_state(Transact-SQL)
title: sys.pdw_replicated_table_cache_state(Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 07/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest
ms.openlocfilehash: 76b5f9ec684b4733934a8cdd703942f12cf1b541
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97404488"
---
# <a name="syspdw_replicated_table_cache_state-transact-sql"></a>sys.pdw_replicated_table_cache_state(Transact-SQL)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

  **Object_id** 여 복제 된 테이블과 연결 된 캐시의 상태를 반환 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|테이블의 개체 ID입니다. [Sys.debug &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조 하세요.<br /><br /> **object_id** 는이 뷰의 키입니다.||  
|state|**nvarchar(40)**|이 테이블에 대 한 복제 된 테이블 캐시 상태입니다.|' NotReady ', ' Ready '|  
  
## <a name="example"></a>예
이 예에서는 테이블 이름 및 복제 된 테이블 캐시의 상태를 검색 하기 위해 sys.pdw_replicated_table_cache_state를 sys. tables와 조인 합니다.

```sql
SELECT t.[name], p.[object_id], p.[state]
  FROM sys.pdw_replicated_table_cache_state p 
  JOIN sys.tables t ON t.object_id = p.object_id
```



## <a name="next-steps"></a>다음 단계  
 Azure Synapse Analytics 및 병렬 데이터 웨어하우스의 모든 카탈로그 뷰 목록은 [Azure Synapse 분석 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)를 참조 하세요.   
  
