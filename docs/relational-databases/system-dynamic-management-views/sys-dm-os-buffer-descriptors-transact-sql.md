---
description: sys.dm_os_buffer_descriptors(Transact-SQL)
title: sys. dm_os_buffer_descriptors (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_buffer_descriptors_TSQL
- dm_os_buffer_descriptors_TSQL
- sys.dm_os_buffer_descriptors
- dm_os_buffer_descriptors
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_buffer_descriptors dynamic management view
ms.assetid: 012aab95-8888-4f35-9ea3-b5dff6e3f60f
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fe2641c33169e094b5e3cf5ae49a36508f5d4d00
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539404"
---
# <a name="sysdm_os_buffer_descriptors-transact-sql"></a>sys.dm_os_buffer_descriptors(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버퍼 풀에 있는 모든 데이터 페이지에 대한 정보를 반환합니다. 데이터베이스, 개체 또는 유형에 따라 버퍼 풀에서 데이터베이스 페이지를 배포하는 방식을 결정하는 데 이 뷰의 결과를 사용할 수 있습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 이 동적 관리 뷰는 버퍼 풀 확장 파일에서 데이터 페이지에 대한 정보를 반환합니다. 자세한 내용은 [Buffer Pool Extension](../../database-engine/configure-windows/buffer-pool-extension.md)을 참조 하세요.  
  
 데이터 페이지를 디스크에서 읽으면 해당 페이지가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버퍼 풀에 복사되며 다시 사용할 수 있도록 캐싱됩니다. 각 캐시된 데이터 페이지에는 하나의 버퍼 설명자가 있습니다. 버퍼 설명자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 현재 캐시된 각 데이터 페이지를 고유하게 식별합니다. sys.dm_os_buffer_descriptors는 모든 사용자 및 시스템 데이터베이스에 대해 캐시된 페이지를 반환합니다. 여기에는 Resource 데이터베이스와 연결된 페이지가 포함됩니다.  
  
> **참고:** 또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_os_buffer_descriptors**을 사용 합니다.  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|버퍼 풀에 있는 페이지와 연결된 데이터베이스의 ID입니다. Null을 허용합니다.|  
|file_id|**int**|페이지의 지속형 이미지를 저장하는 파일의 ID입니다. Null을 허용합니다.|  
|page_id|**int**|파일 내 페이지의 ID입니다. Null을 허용합니다.|  
|page_level|**int**|페이지의 인덱스 수준입니다. Null을 허용합니다.|  
|allocation_unit_id|**bigint**|페이지 할당 단위의 ID입니다. 이 값은 sys.allocation_units를 조인하는 데 사용할 수 있습니다. Null을 허용합니다.|  
|page_type|**nvarchar(60)**|페이지의 유형입니다 (예: 데이터 페이지 또는 인덱스 페이지). Null을 허용합니다.|  
|row_count|**int**|페이지의 행 수입니다. Null을 허용합니다.|  
|free_space_in_bytes|**int**|페이지의 사용 가능한 공간(바이트)입니다. Null을 허용합니다.|  
|is_modified|**bit**|1 = 디스크에서 읽은 후 페이지가 수정되었습니다. Null을 허용합니다.|  
|numa_node|**int**|버퍼에 대한 Nonuniform Memory Access 노드입니다. Null을 허용합니다.|  
|read_microsec|**bigint**|페이지를 버퍼로 읽어 오는 데 필요한 실제 시간(밀리초)입니다 이 값은 버퍼를 다시 사용하면 다시 설정됩니다. Null을 허용합니다.|  
|is_in_bpool_extension|**bit**|1 = 페이지가 버퍼 풀 확장에 있습니다. Null을 허용합니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
   
## <a name="remarks"></a>설명  
 dm_os_buffer_descriptors는 리소스 데이터베이스에서 사용 중인 페이지를 반환 합니다. dm_os_buffer_descriptors은 사용 가능한 페이지 또는 도난당 한 페이지에 대 한 정보 또는 읽을 때 오류가 발생 한 페이지에 대 한 정보를 반환 하지 않습니다.  
  
|시작|대상|켜기|관계|  
|----------|--------|--------|------------------|  
|sys.dm_os_buffer_descriptors|sys.databases|database_id|다 대 일|  
|sys.dm_os_buffer_descriptors|\<userdb>.sys. allocation_units|allocation_unit_id|다 대 일|  
|sys.dm_os_buffer_descriptors|\<userdb>.sys. database_files|file_id|다 대 일|  
|sys.dm_os_buffer_descriptors|sys.dm_os_buffer_pool_extension_configuration|file_id|다 대 일|  
  
## <a name="examples"></a>예제  
  
### <a name="a-returning-cached-page-count-for-each-database"></a>A. 각 데이터베이스에 대해 캐시된 페이지 수 반환  
 다음 예에서는 각 데이터베이스에 대해 로드된 페이지 수를 반환합니다.  
  
```  
SELECT COUNT(*)AS cached_pages_count  
    ,CASE database_id   
        WHEN 32767 THEN 'ResourceDb'   
        ELSE db_name(database_id)   
        END AS database_name  
FROM sys.dm_os_buffer_descriptors  
GROUP BY DB_NAME(database_id) ,database_id  
ORDER BY cached_pages_count DESC;  
```  
  
### <a name="b-returning-cached-page-count-for-each-object-in-the-current-database"></a>B. 현재 데이터베이스의 각 개체에 대해 캐시된 페이지 수 반환  
 다음 예에서는 현재 데이터베이스의 각 개체에 대해 로드된 페이지 수를 반환합니다.  
  
```  
SELECT COUNT(*)AS cached_pages_count   
    ,name ,index_id   
FROM sys.dm_os_buffer_descriptors AS bd   
    INNER JOIN   
    (  
        SELECT object_name(object_id) AS name   
            ,index_id ,allocation_unit_id  
        FROM sys.allocation_units AS au  
            INNER JOIN sys.partitions AS p   
                ON au.container_id = p.hobt_id   
                    AND (au.type = 1 OR au.type = 3)  
        UNION ALL  
        SELECT object_name(object_id) AS name     
            ,index_id, allocation_unit_id  
        FROM sys.allocation_units AS au  
            INNER JOIN sys.partitions AS p   
                ON au.container_id = p.partition_id   
                    AND au.type = 2  
    ) AS obj   
        ON bd.allocation_unit_id = obj.allocation_unit_id  
WHERE database_id = DB_ID()  
GROUP BY name, index_id   
ORDER BY cached_pages_count DESC;  
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.allocation_units&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 
 [Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Resource 데이터베이스](../../relational-databases/databases/resource-database.md)   
 [sys.dm_os_buffer_pool_extension_configuration&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql.md)  
  
  


