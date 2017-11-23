---
title: sys.pdw_nodes_pdw_physical_databases (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 70e0939d-4d97-4ae0-ba16-934e0a80e718
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f54cc6c6d5de9559ed53e5762ecc471ea303f559
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwnodespdwphysicaldatabases-transact-sql"></a>sys.pdw_nodes_pdw_physical_databases (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  계산 노드의 각 물리적 데이터베이스에 대 한 행을 포함합니다. 데이터베이스에 대 한 자세한 정보를 보려면 물리적 데이터베이스 정보를 집계 합니다. 조인 정보를 결합 하는 `sys.pdw_nodes_pdw_physical_databases` 에 `sys.pdw_database_mappings` 및 `sys.databases` 테이블입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|데이터베이스에 대 한 개체 ID입니다. 이 값은에서 database_id와 동일 하지는 [sys.databases&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 보기.|  
|physical_name|**sysname**|셸/계산 노드의 데이터베이스에 대 한 물리적 이름입니다. 이 값은 physical_name 열에 있는 값과 같으며는 [sys.pdw_database_mappings &#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md) 보기.|  
|pdw_node_id|**int**|노드와 연결 된 고유 숫자 id입니다.|  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-returning"></a>1. 반환  
 다음 쿼리는 각 계산 노드에 마스터 및 해당 데이터베이스 이름에서 이름 및 각 데이터베이스의 ID를 반환합니다.  
  
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
  
### <a name="b-using-syspdwnodespdwphysicaldatabases-to-gather-detailed-object-information"></a>2. 세부 개체 정보를 수집할 sys.pdw_nodes_pdw_physical_databases를 사용 하 여  
 다음 쿼리에서 인덱스에 대 한 정보를 표시 및 개체는 데이터베이스의 개체에 속한 데이터베이스에 대 한 유용한 정보를 포함 합니다.  
  
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
  
### <a name="c-using-syspdwnodespdwphysicaldatabases-to-determine-the-encryption-state"></a>3. Sys.pdw_nodes_pdw_physical_databases를 사용 하 여 암호화 상태를 확인 합니다.  
 다음 쿼리는 AdventureWorksPDW2012 데이터베이스의 암호화 상태를 제공합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.pdw_database_mappings &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  

