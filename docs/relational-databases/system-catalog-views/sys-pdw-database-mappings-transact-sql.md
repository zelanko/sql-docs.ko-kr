---
title: sys. pdw_database_mappings (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 4ae2c71e-dd56-41ea-a16b-64936175b459
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5a5f3e4f421fbe169d5acb049e5a91ce5ffa3612
ms.sourcegitcommit: 1be90e93980a8e92275b5cc072b12b9e68a3bb9a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84627544"
---
# <a name="syspdw_database_mappings-transact-sql"></a>sys. pdw_database_mappings (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  는 데이터베이스의 **database_id**를 계산 노드에 사용 되는 실제 이름에 매핑하고 시스템에서 데이터베이스 소유자의 **보안 주체 id** 를 제공 합니다. **Pdw_database_mappings** 를 **sys** . **pdw_nodes_pdw_physical_databases**에 조인 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|physical_name|**nvarchar (36)**|계산 노드에 있는 데이터베이스의 물리적 이름입니다.<br /><br /> **physical_name** 및 **database_id** 이 보기의 키를 구성 합니다.||  
|database_id|**int**|데이터베이스의 개체 ID입니다. [&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)를 참조 하세요.<br /><br /> **physical_name** 및 **database_id** 이 보기의 키를 구성 합니다.||  
  
## <a name="examples-sspdw"></a>예제: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 다른 시스템 테이블에 pdw_database_mappings를 조인 하 여 데이터베이스가 매핑되는 방법을 보여 줍니다.  
  
```  
SELECT DB.database_id, DB.name, Map.*, Phys.*   
FROM sys.databases AS DB  
JOIN sys.pdw_database_mappings AS Map  
    ON DB.database_id = Map.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS Phys  
    ON Map.physical_name = Phys.physical_name  
ORDER BY DB.database_id, Phys.pdw_node_id;  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [pdw_index_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)   
 [pdw_table_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)   
 [pdw_nodes_pdw_physical_databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-pdw-physical-databases-transact-sql.md)  
  
  

