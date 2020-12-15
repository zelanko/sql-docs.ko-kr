---
description: sys.dm_os_memory_cache_hash_tables(Transact-SQL)
title: sys.dm_os_memory_cache_hash_tables (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_hash_tables_TSQL
- sys.dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_hash_tables dynamic management view
ms.assetid: 68b94f35-8f80-4d2b-bcde-7a21934219af
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 60be80590eb91b0bdfe2f6f2e3864a4f5b3f4fad
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464594"
---
# <a name="sysdm_os_memory_cache_hash_tables-transact-sql"></a>sys.dm_os_memory_cache_hash_tables(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 각 활성 캐시에 대해 하나의 행을 반환합니다.  
  
> [!NOTE]  
>  또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **sys.dm_pdw_nodes_os_memory_cache_hash_tables** 이름을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|캐시 항목의 주소(기본 키)입니다. Null을 허용하지 않습니다.|  
|**name**|**nvarchar(256)**|캐시의 이름입니다. Null을 허용하지 않습니다.|  
|**type**|**nvarchar(60)**|캐시 유형입니다. Null을 허용하지 않습니다.|  
|**table_level**|**int**|해시 테이블 번호입니다. 특정 캐시에는 다양한 해시 함수에 해당하는 여러 개의 해시 테이블이 포함될 수도 있습니다. Null을 허용하지 않습니다.|  
|**buckets_count**|**int**|해시 테이블의 버킷 수입니다. Null을 허용하지 않습니다.|  
|**buckets_in_use_count**|**int**|현재 사용 중인 버킷 수입니다. Null을 허용하지 않습니다.|  
|**buckets_min_length**|**int**|버킷의 최소 캐시 항목 수입니다. Null을 허용하지 않습니다.|  
|**buckets_max_length**|**int**|버킷의 최대 캐시 항목 수입니다. Null을 허용하지 않습니다.|  
|**buckets_avg_length**|**int**|각 버킷의 평균 캐시 항목 수입니다. Null을 허용하지 않습니다.|  
|**buckets_max_length_ever**|**int**|서버를 시작한 이후 이 해시 테이블의 해시 버킷에 캐시된 항목의 최대 수입니다. Null을 허용하지 않습니다.|  
|**hits_count**|**bigint**|캐시 적중 수입니다. Null을 허용하지 않습니다.|  
|**misses_count**|**bigint**|캐시 누락 수입니다. Null을 허용하지 않습니다.|  
|**buckets_avg_scan_hit_length**|**int**|검색한 항목을 찾기 전에 버킷에서 조사된 평균 항목 수입니다. Null을 허용하지 않습니다.|  
|**buckets_avg_scan_miss_length**|**int**|검색이 실패로 끝나기 전에 버킷에서 조사된 평균 항목 수입니다. Null을 허용하지 않습니다.|  
|**pdw_node_id**|**int**|이 배포가 설정 된 노드의 식별자입니다.<br /><br /> **적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>사용 권한 

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   

## <a name="see-also"></a>참고 항목  
 
  [Transact-sql&#41;&#40;운영 체제 관련 동적 관리 뷰 SQL Server ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


