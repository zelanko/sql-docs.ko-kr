---
title: sys.pdw_replicated_table_cache_state (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 4ab853993091b5a8893dc23387a336a9944bd774
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001104"
---
# <a name="syspdwreplicatedtablecachestate-transact-sql"></a>sys.pdw_replicated_table_cache_state (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  복제 된 테이블을 사용 하 여 연결 된 캐시의 상태를 반환 **object_id**합니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|테이블에 대 한 개체 ID입니다. 참조 [sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)합니다.<br /><br /> **object_id** 는이 보기에 대 한 키입니다.||  
|state|**nvarchar(40)**|이 테이블에 대 한 복제 된 테이블 캐시 상태입니다.|'NotReady','Ready'|  
  
## <a name="example"></a>예제
이 예에서는 테이블 이름 및 복제 된 테이블 캐시의 상태를 검색할 sys.tables 사용 하 여 sys.pdw_replicated_table_cache_state를 조인 합니다.

```sql
SELECT t.[name], p.[object_id], p.[state]
  FROM sys.pdw_replicated_table_cache_state p 
  JOIN sys.tables t ON t.object_id = p.object_id
```



## <a name="next-steps"></a>다음 단계  
 SQL Data Warehouse 및 병렬 데이터 웨어하우스에 대 한 모든 카탈로그 뷰 목록을 참조 하세요 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)합니다.   
  
