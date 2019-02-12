---
title: sys.pdw_nodes_indexes (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c13e41abea44bdbe0f954518f42aab118360a155
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012384"
---
# <a name="syspdwnodesindexes-transact-sql"></a>sys.pdw_nodes_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  에 대 한 인덱스를 반환 합니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|이 인덱스가 속한 개체의 id입니다.||  
|NAME|**sysname**|인덱스의 이름입니다. 이름은 해당 개체 내 에서만 고유 합니다. NULL = 힙||  
|index_id|**int**|인덱스의 id입니다. index_id는 해당 개체 내 에서만 고유 합니다.<br /><br /> 0 = 힙<br /><br /> 1 = 클러스터형 인덱스<br /><br /> > 1 = 비클러스터형 인덱스||  
|유형|**tinyint**|인덱스의 유형입니다.<br /><br /> 0 = 힙<br /><br /> 1 = 클러스터형<br /><br /> 2 = 비클러스터형<br /><br /> 5 = 클러스터형 xVelocity 메모리 최적화 columnstore 인덱스|  
|type_desc|**nvarchar(60)**|인덱스 유형의 설명입니다.<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> 클러스터형된 COLUMNSTORE||  
|is_unique|**bit**|0 = 인덱스가 고유하지 않습니다.|항상 0입니다.|  
|data_space_id|**int**|이 인덱스에 대 한 데이터 공간의 id입니다. 데이터 공간은 파일 그룹 또는 파티션 구성표입니다.<br /><br /> 0 = object_id가 테이블 반환 함수입니다.||  
|ignore_dup_key|**bit**|0 = IGNORE_DUP_KEY가 OFF입니다.|항상 0입니다.|  
|is_primary_key|**bit**|1 = 인덱스가 PRIMARY KEY 제약 조건의 일부입니다.|항상 0입니다.|  
|is_unique_constraint|**bit**|1 = 인덱스가 UNIQUE 제약 조건의 일부입니다.|항상 0입니다.|  
|fill_factor|**tinyint**|> 0 = 인덱스가 생성 또는 다시 생성될 때 사용된 FILLFACTOR 백분율입니다.<br /><br /> 0 = 기본값|항상 0입니다.|  
|is_padded|**bit**|0 = PADINDEX가 OFF입니다.|항상 0입니다.|  
|is_disabled|**bit**|1 = 인덱스가 비활성화되었습니다.<br /><br /> 0 = 인덱스가 비활성화되지 않았습니다.||  
|is_hypothetical|**bit**|0 = 인덱스가 가상 인덱스입니다.|항상 0입니다.|  
|allow_row_locks|**bit**|1 = 인덱스에서 행 잠금을 허용합니다.|항상 1입니다.|  
|allow_page_locks|**bit**|1 = 인덱스에서 페이지 잠금을 허용합니다.|항상 1입니다.|  
|has_filter|**bit**|0 = 인덱스에 필터가 없습니다.|항상 0입니다.|  
|filter_definition|**nvarchar(max)**|필터링된 인덱스에 포함된 행 하위 집합에 대한 식입니다.|항상 NULL입니다.|  
|pdw_node_id|**int**|고유 식별자를 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 노드.|NOT NULL|  
  
## <a name="permissions"></a>사용 권한  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
