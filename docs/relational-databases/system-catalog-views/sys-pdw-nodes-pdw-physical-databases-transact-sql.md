---
title: sys. pdw_nodes_pdw_physical_databases (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 03/09/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 70e0939d-4d97-4ae0-ba16-934e0a80e718
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 64d74d28c4b99e75c114effdf651a58d01a614d6
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394048"
---
# <a name="syspdw_nodes_pdw_physical_databases-transact-sql"></a>sys. pdw_nodes_pdw_physical_databases (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  계산 노드의 각 물리적 데이터베이스에 대 한 행을 포함 합니다. 데이터베이스에 대 한 자세한 정보를 얻기 위해 실제 데이터베이스 정보를 집계 합니다. 정보를 결합 하려면 `sys.pdw_nodes_pdw_physical_databases` 및 테이블에를 조인 합니다 `sys.pdw_database_mappings` `sys.databases` .  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|database_id|**int**|데이터베이스의 개체 ID입니다. 이 값은 [&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 뷰의 database_id와 동일 하지 않습니다.|  
|physical_name|**sysname**|셸/계산 노드에 있는 데이터베이스의 물리적 이름입니다. 이 값은 [pdw_database_mappings &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md) 뷰의 physical_name 열에 있는 값과 동일 합니다.|  
|pdw_node_id|**int**|노드와 연결 된 고유 숫자 id입니다.|  
  
## <a name="examples-sspdw"></a>예제: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-returning"></a>A. 복귀  
 다음 쿼리는 master에 있는 각 데이터베이스의 이름과 ID를 반환 하 고 각 계산 노드에 해당 하는 데이터베이스 이름을 반환 합니다.  
  
```  
SELECT D.database_id AS DBID_in_master, D.name AS UserDatabaseName,   
PD.pdw_node_id AS NodeID, DM.physical_name AS PhysDBName   
FROM sys.databases AS D  
JOIN sys.pdw_database_mappings AS DM  
    ON D.database_id = DM.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON DM.physical_name = PD.physical_name  
ORDER BY D.database_id, PD.pdw_node_ID;  
```  
  
### <a name="b-using-syspdw_nodes_pdw_physical_databases-to-gather-detailed-object-information"></a>B. Sys. pdw_nodes_pdw_physical_databases를 사용 하 여 자세한 개체 정보 수집  
 다음 쿼리는 인덱스에 대 한 정보를 표시 하 고 개체가 데이터베이스의 개체에 속하는 데이터베이스에 대 한 유용한 정보를 포함 합니다.  
  
```  
SELECT D.name AS UserDatabaseName, D.database_id AS DBIDinMaster,  
DM.physical_name AS PhysDBName, PD.pdw_node_id AS NodeID,   
IU.object_id, IU.index_id, IU.user_seeks, IU.user_scans, IU.user_lookups, IU.user_updates  
FROM sys.databases AS D  
JOIN sys.pdw_database_mappings AS DM  
    ON D.database_id = DM.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON DM.physical_name = PD.physical_name  
JOIN sys.dm_pdw_nodes_db_index_usage_stats AS IU  
    ON PD.database_id = IU.database_id  
ORDER BY D.database_id, IU.object_id, IU.index_id, PD.pdw_node_ID;  
```  
  
### <a name="c-using-syspdw_nodes_pdw_physical_databases-to-determine-the-encryption-state"></a>C. Pdw_nodes_pdw_physical_databases를 사용 하 여 암호화 상태 확인  
 다음 쿼리는 AdventureWorksPDW2012 데이터베이스의 암호화 상태를 제공 합니다.  
  
```  
WITH dek_encryption_state AS   
(  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id, encryption_state  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
        INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
            ON dek.database_id = node_db_map.database_id AND dek.pdw_node_id = node_db_map.pdw_node_id  
        LEFT JOIN sys.pdw_database_mappings AS db_map  
            ON node_db_map .physical_name = db_map.physical_name  
        INNER JOIN sys.dm_pdw_nodes AS nodes  
            ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
)  
SELECT TOP 1 encryption_state  
       FROM  dek_encryption_state  
       WHERE dek_encryption_state.database_id = DB_ID('AdventureWorksPDW2012 ')  
       ORDER BY (CASE encryption_state WHEN 3 THEN -1 ELSE encryption_state END) DESC;  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [pdw_database_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  

