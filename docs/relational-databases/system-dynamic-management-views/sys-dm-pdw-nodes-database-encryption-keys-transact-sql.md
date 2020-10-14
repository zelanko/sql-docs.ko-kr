---
description: sys.dm_pdw_nodes_database_encryption_keys (Transact-sql)
title: sys.dm_pdw_nodes_database_encryption_keys (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e7fd02b2-5d7e-4816-a0af-b58ae2ac3f7a
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5e8a399d58c4ffa4f61e9509bd243f7e9c71275e
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037726"
---
# <a name="sysdm_pdw_nodes_database_encryption_keys-transact-sql"></a>sys.dm_pdw_nodes_database_encryption_keys (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  연결된 데이터베이스 암호화 키 및 데이터베이스의 암호화 상태에 대한 정보를 반환합니다. **sys.dm_pdw_nodes_database_encryption_keys** 는 각 노드에 대해이 정보를 제공 합니다. 데이터베이스 암호화에 대 한 자세한 내용은 [투명한 데이터 암호화 (SQL Server PDW)](../../analytics-platform-system/transparent-data-encryption.md)를 참조 하세요.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|database_id|**int**|각 노드에 있는 물리적 데이터베이스의 ID입니다.|  
|encryption_state|**int**|이 노드의 데이터베이스가 암호화 되었는지 아니면 암호화 되지 않는지를 나타냅니다.<br /><br /> 0 = 데이터베이스 암호화 키가 없고 암호화되지 않음<br /><br /> 1 = 암호화되지 않음<br /><br /> 2 = 암호화 진행 중<br /><br /> 3 = 암호화됨<br /><br /> 4 = 키 변경 진행 중<br /><br /> 5 = 해독 진행 중<br /><br /> 6 = 보호 변경 진행 중 (데이터베이스 암호화 키를 암호화 하는 인증서를 변경 하는 중)|  
|create_date|**datetime**|암호화 키를 만든 날짜를 표시합니다.|  
|regenerate_date|**datetime**|암호화 키를 다시 생성한 날짜를 표시합니다.|  
|modify_date|**datetime**|암호화 키를 수정한 날짜를 표시합니다.|  
|set_date|**datetime**|암호화 키가 데이터베이스에 적용된 날짜를 표시합니다.|  
|opened_date|**datetime**|데이터베이스 키가 마지막으로 열린 시간을 표시합니다.|  
|key_algorithm|**varchar (?)**|키에 사용된 알고리즘을 표시합니다.|  
|key_length|**int**|키의 길이를 표시합니다.|  
|encryptor_thumbprint|**varbin**|암호기의 손도장을 표시합니다.|  
|percent_complete|**real**|데이터베이스 암호화 상태 변경의 완료 비율입니다. 상태 변경이 없으면 0이 됩니다.|  
|node_id|**int**|노드와 연결 된 고유 숫자 id입니다.|  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 `sys.dm_pdw_nodes_database_encryption_keys` 다른 시스템 테이블에 조인 하 여 TDE로 보호 되는 데이터베이스의 각 노드에 대 한 암호화 상태를 표시 합니다.  
  
```  
SELECT D.database_id AS DBIDinMaster, D.name AS UserDatabaseName,   
PD.pdw_node_id AS NodeID, DM.physical_name AS PhysDBName,   
keys.encryption_state  
FROM sys.dm_pdw_nodes_database_encryption_keys AS keys  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON keys.database_id = PD.database_id AND keys.pdw_node_id = PD.pdw_node_id  
JOIN sys.pdw_database_mappings AS DM  
    ON DM.physical_name = PD.physical_name  
JOIN sys.databases AS D  
    ON D.database_id = DM.database_id  
ORDER BY D.database_id, PD.pdw_node_ID;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  

