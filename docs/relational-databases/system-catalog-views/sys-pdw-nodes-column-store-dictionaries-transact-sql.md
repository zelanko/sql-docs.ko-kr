---
description: sys.pdw_nodes_column_store_dictionaries (Transact-sql)
title: sys.pdw_nodes_column_store_dictionaries (Transact-sql)
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.custom: seo-dt-2019
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 7ae1c2e4-45c0-4880-a692-1f299fbcfd19
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: c64f087631b6104af14fc793c06946515220a51a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475164"
---
# <a name="syspdw_nodes_column_store_dictionaries-transact-sql"></a>sys.pdw_nodes_column_store_dictionaries (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Columnstore 인덱스에 사용 되는 각 사전에 대 한 행을 포함 합니다. 사전은 일부 데이터 형식을 인코딩하는 데 사용되므로 columnstore 인덱스의 일부 열에만 사전이 있습니다. 사전은 모든 세그먼트의 기본 사전으로 있을 수 있으며 열 세그먼트의 하위 집합에 사용되는 다른 보조 사전으로 있을 수도 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|파티션 ID를 나타냅니다. 데이터베이스 내에서 고유합니다.|  
|**hobt_id**|**bigint**|이 columnstore 인덱스가 있는 테이블에 대 한 힙 또는 B-트리 인덱스 (HoBT)의 ID입니다.|  
|**column_id**|**int**|Columnstore 열의 ID입니다.|  
|**dictionary_id**|**int**|사전의 ID입니다.|  
|**version**|**int**|사전 형식의 버전입니다.|  
|**type**|**int**|사전 종류입니다.<br /><br /> 1- **int** 값을 포함 하는 해시 사전<br /><br /> 2-사용 되지 않음<br /><br /> 3-문자열 값을 포함 하는 해시 사전<br /><br /> 4- **float** 값을 포함 하는 해시 사전|  
|**last_id**|**int**|사전의 마지막 데이터 ID입니다.|  
|**entry_count**|**bigint**|사전에 있는 항목의 개수입니다.|  
|**on_disc_size**|**bigint**|사전의 크기(바이트)입니다.|  
|**pdw_node_id**|**int**|노드의 고유 식별자 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 입니다.|  
  
## <a name="permissions"></a>사용 권한  
 `VIEW SERVER STATE` 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Azure Synapse Analytics 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [Transact-sql&#41;&#40;COLUMNSTORE 인덱스 만들기 ](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [Transact-sql&#41;sys.pdw_nodes_column_store_segments &#40;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [Transact-sql&#41;sys.pdw_nodes_column_store_row_groups &#40;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
  
  
