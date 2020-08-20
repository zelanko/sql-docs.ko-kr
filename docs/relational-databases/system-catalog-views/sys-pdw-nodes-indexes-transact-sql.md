---
description: sys. pdw_nodes_indexes (Transact-sql)
title: sys. pdw_nodes_indexes (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 261bcb7f-a906-4979-b274-bc5f1aa66426
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f6c518d53122015af3e86350b0037e1b88604543
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490264"
---
# <a name="syspdw_nodes_indexes-transact-sql"></a>sys. pdw_nodes_indexes (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  에 대 한 인덱스를 반환 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|이 인덱스가 속한 개체의 id입니다.||  
|name|**sysname**|인덱스의 이름입니다. 이름은 개체 내 에서만 고유 합니다. NULL = 힙||  
|index_id|**int**|인덱스의 id입니다. index_id는 해당 개체 내에서만 고유합니다.<br /><br /> 0 = 힙<br /><br /> 1 = 클러스터형 인덱스<br /><br /> > 1 = 비클러스터형 인덱스||  
|type|**tinyint**|인덱스의 유형입니다.<br /><br /> 0 = 힙<br /><br /> 1 = 클러스터형<br /><br /> 2 = 비클러스터형<br /><br /> 5 = 클러스터 된 xVelocity 메모리 액세스에 최적화 된 columnstore 인덱스|  
|type_desc|**nvarchar(60)**|인덱스 유형의 설명입니다.<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> 클러스터형 COLUMNSTORE||  
|is_unique|**bit**|0 = 인덱스가 고유하지 않습니다.|항상 0입니다.|  
|data_space_id|**int**|이 인덱스에 대 한 데이터 공간의 id입니다. 데이터 공간은 파일 그룹 또는 파티션 구성표입니다.<br /><br /> 0 = object_id는 테이블 반환 함수입니다.||  
|ignore_dup_key|**bit**|0 = IGNORE_DUP_KEY가 OFF입니다.|항상 0입니다.|  
|is_primary_key|**bit**|1 = 인덱스가 PRIMARY KEY 제약 조건의 일부입니다.|항상 0입니다.|  
|is_unique_constraint|**bit**|1 = 인덱스가 UNIQUE 제약 조건의 일부입니다.|항상 0입니다.|  
|fill_factor|**tinyint**|> 0 = 인덱스를 만들거나 다시 작성할 때 사용 되는 FILLFACTOR 백분율입니다.<br /><br /> 0 = 기본값|항상 0입니다.|  
|is_padded|**bit**|0 = PADINDEX가 OFF입니다.|항상 0입니다.|  
|is_disabled|**bit**|1 = 인덱스가 비활성화되었습니다.<br /><br /> 0 = 인덱스가 비활성화되지 않았습니다.||  
|is_hypothetical|**bit**|0 = 인덱스가 가상 인덱스입니다.|항상 0입니다.|  
|allow_row_locks|**bit**|1 = 인덱스에서 행 잠금을 허용합니다.|항상 1입니다.|  
|allow_page_locks|**bit**|1 = 인덱스에서 페이지 잠금을 허용합니다.|항상 1입니다.|  
|has_filter|**bit**|0 = 인덱스에 필터가 없습니다.|항상 0입니다.|  
|filter_definition|**nvarchar(max)**|필터링된 인덱스에 포함된 행 하위 집합에 대한 식입니다.|항상 NULL입니다.|  
|pdw_node_id|**int**|노드의 고유 식별자 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 입니다.|NOT NULL|  
  
## <a name="permissions"></a>사용 권한  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
