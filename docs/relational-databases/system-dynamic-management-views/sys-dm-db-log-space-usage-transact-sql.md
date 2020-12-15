---
description: sys.dm_db_log_space_usage (Transact-sql)
title: sys.dm_db_log_space_usage (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_log_space_usage
- sys.dm_db_log_space_usage_TSQL
- dm_db_log_space_usage
- dm_db_log_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_space_usage dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a181be6b5a9fb7ce5d832e7270c662c875cc98c8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97444261"
---
# <a name="sysdm_db_log_space_usage-transact-sql"></a>sys.dm_db_log_space_usage (Transact-sql)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

트랜잭션 로그에 대 한 공간 사용량 정보를 반환 합니다. 
  
> [!NOTE]
> 모든 트랜잭션 로그 파일이 결합 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|데이터베이스 ID입니다.|  
|total_log_size_in_bytes |**bigint** |로그의 크기입니다.  |
|used_log_space_in_bytes |**bigint** |로그의 차지 하는 크기입니다.  |     
|used_log_space_in_percent |**real** |총 로그 크기의 백분율로 된 로그의 차지 하는 크기입니다. |
|log_space_in_bytes_since_last_backup |**bigint** |마지막 로그 백업 이후 사용 된 공간의 양입니다. <br />**적용 대상:** [!INCLUDE[sssql14-md](../../includes/sssql14-md.md)] 부터 [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)] ,  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] .|
    
  
## <a name="permissions"></a>사용 권한  

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   
  
## <a name="examples"></a>예  
  
### <a name="a-determine-the-amount-of-free-log-space-in-tempdb"></a>A. Tempdb에서 사용 가능한 로그 공간의 크기 확인   
다음 쿼리는 tempdb에서 사용할 수 있는 총 사용 가능한 로그 공간 (MB)을 반환 합니다.

```sql
USE tempdb;  
GO  

SELECT (total_log_size_in_bytes - used_log_space_in_bytes)*1.0/1024/1024 AS [free log space in MB]  
FROM sys.dm_db_log_space_usage;  
```
  
## <a name="see-also"></a>참고 항목  
[동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)    
[Transact-sql&#41;sys.dm_db_task_space_usage &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
[sys.dm_db_session_space_usage&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
[sys.dm_db_log_info&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys.dm_db_log_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md) 



