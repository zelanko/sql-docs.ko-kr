---
title: sys.pdw_database_mappings (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 4ae2c71e-dd56-41ea-a16b-64936175b459
caps.latest.revision: 9
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f1455d25c0a3ea344c5104053358b2d4fed0c65b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38058071"
---
# <a name="syspdwdatabasemappings-transact-sql"></a>sys.pdw_database_mappings (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Maps는 **database_id**물리적 이름으로 데이터베이스의 계산 노드를 사용 하 고 제공 합니다 **보안 주체 id** 시스템의 데이터베이스 소유자의 합니다. 조인 **sys.pdw_database_mappings** 하 **sys.databases** 하 고 **sys.pdw_nodes_pdw_physical_databases**합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|physical_name|**nvarchar(36)**|계산 노드에서 데이터베이스에 대 한 물리적 이름입니다.<br /><br /> **physical_name** 하 고 **database_id** 이 보기에 대 한 키를 형성 합니다.||  
|database_id|**int**|데이터베이스에 대 한 개체 ID입니다. 참조 [sys.databases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)합니다.<br /><br /> **physical_name** 하 고 **database_id** 이 보기에 대 한 키를 형성 합니다.||  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]   
 다음 예제에서는 sys.pdw_database_mappings 데이터베이스 매핑되는 방식을 표시할 다른 시스템 테이블에 조인 됩니다.  
  
```  
SELECT DB.database_id, DB.name, Map.*, Phys.*   
FROM sys.databases AS DB  
JOIN sys.pdw_database_mappings AS Map  
    ON DB.database_id = Map.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS Phys  
    ON Map.physical_name = Phys.physical_name  
ORDER BY DB.database_id, Phys.pdw_node_id;  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.pdw_index_mappings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)   
 [sys.pdw_table_mappings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)   
 [sys.pdw_nodes_pdw_physical_databases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-pdw-physical-databases-transact-sql.md)  
  
  

