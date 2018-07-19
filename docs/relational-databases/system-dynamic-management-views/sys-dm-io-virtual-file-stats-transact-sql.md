---
title: sys.dm_io_virtual_file_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_io_virtual_file_stats
- sys.dm_io_virtual_file_stats_TSQL
- sys.dm_io_virtual_file_stats
- dm_io_virtual_file_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_virtual_file_stats dynamic management function
ms.assetid: fa3e321f-6fe5-45ff-b397-02a0dd3d6b7d
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2720aba7dc9b3d8c1a6e34db5a588829245ed97a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38066834"
---
# <a name="sysdmiovirtualfilestats-transact-sql"></a>sys.dm_io_virtual_file_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  데이터 및 로그 파일에 대한 I/O 통계를 반환합니다. 이 동적 관리 뷰를 대체 합니다 [fn_virtualfilestats](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md) 함수입니다.  
  
> [!NOTE]  
>  이를 호출 하 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]에 이름을 사용 하 여 **sys.dm_pdw_nodes_io_virtual_file_stats**합니다. 

## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database

sys.dm_io_virtual_file_stats (   
    { database_id | NULL },  
    { file_id | NULL }  
)  
```  

```  
-- Syntax for Azure SQL Data Warehouse

sys.dm_pdw_nodes_io_virtual_file_stats
```
  
## <a name="arguments"></a>인수  


 *database_id* | NULL

 **적용 대상:** SQL Server(2008부터), Azure SQL Database

 데이터베이스의 ID입니다. *database_id* 은 int 이며 기본값은 없습니다. 올바른 입력은 데이터베이스의 ID 번호 또는 NULL입니다. NULL을 지정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 데이터베이스가 반환됩니다.  
  
 기본 제공 함수 [DB_ID](../../t-sql/functions/db-id-transact-sql.md) 지정할 수 있습니다.  
  
*file_id* | NULL

**적용 대상:** SQL Server(2008부터), Azure SQL Database
 
파일의 ID입니다. *file_id* 은 int 이며 기본값은 없습니다. 올바른 입력은 파일의 ID 번호 또는 NULL입니다. NULL을 지정하면 데이터베이스의 모든 파일이 반환됩니다.  
  
 기본 제공 함수 [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md) 를 지정할 수 있으며 현재 데이터베이스의 파일을 참조 합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|데이터베이스 이름입니다.</br></br>SQL Data Warehouse에 대 한 pdw_node_id 식별 된 노드에 저장 된 데이터베이스의 이름입니다. 각 노드 13 파일이 있는 한 tempdb 데이터베이스를 있습니다. 각 노드에 또한 배포당 하나의 데이터베이스에 있고 각 배포 데이터베이스 5 파일. 예를 들어, 각 노드 4 배포판에 있으면 결과 pdw_node_id 당 20 개의 배포 데이터베이스 파일을 보여줍니다. 
|**database_id**|**smallint**|데이터베이스의 ID입니다.|  
|**file_id**|**smallint**|파일의 ID입니다.|  
|**sample_ms**|**bigint**|컴퓨터가 시작된 이후로 경과한 시간(밀리초)입니다. 이 열은 이 함수의 다양한 출력을 비교하는 데 사용할 수 있습니다.</br></br>데이터 형식이 **int** 에 대 한 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|**num_of_reads**|**bigint**|파일에 대해 읽기가 실행된 횟수입니다.|  
|**num_of_bytes_read**|**bigint**|파일에 대해 실행된 읽기의 총 바이트 수입니다.|  
|**io_stall_read_ms**|**bigint**|사용자가 파일에 대한 읽기가 실행될 때까지 대기한 총 시간(밀리초)입니다.|  
|**num_of_writes**|**bigint**|파일에 대해 쓰기가 실행된 횟수입니다.|  
|**num_of_bytes_written**|**bigint**|파일에 대해 실행된 쓰기의 총 바이트 수입니다.|  
|**io_stall_write_ms**|**bigint**|사용자가 파일에 대한 쓰기가 완료될 때까지 대기한 총 시간(밀리초)입니다.|  
|**io_stall**|**bigint**|사용자가 파일에 대한 I/O가 완료될 때까지 대기한 총 시간(밀리초)입니다.|  
|**size_on_disk_bytes**|**bigint**|이 파일에 대해 디스크에서 사용된 바이트 수입니다. 스파스 파일의 경우 데이터베이스 스냅숏에 사용된 디스크의 실제 바이트 수입니다.|  
|**file_handle**|**varbinary**|이 파일에 대한 Windows 파일 핸들입니다.|  
|**io_stall_queued_read_ms**|**bigint**|**에 적용 되지 않습니다:**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)]합니다.<br /><br /> 읽기용 IO 리소스 관리에서 사용하는 총 IO 대시 시간입니다. Null을 허용하지 않습니다. 자세한 내용은 [sys.dm_resource_governor_resource_pools &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)합니다.|  
|**io_stall_queued_write_ms**|**bigint**|**에 적용 되지 않습니다:**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 를 통해 [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)]합니다.<br /><br />  쓰기용 IO 리소스 관리에서 사용하는 총 IO 대시 시간입니다. Null을 허용하지 않습니다.|
|**pdw_node_id**|**int**|**적용 대상:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]</br></br>배포에 대 한 노드의 식별자입니다.
 
  
## <a name="permissions"></a>사용 권한  
 VIEW SERVER STATE 권한이 필요합니다. 자세한 내용은 [동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)합니다.  
  
## <a name="examples"></a>예  

### <a name="a-return-statistics-for-a-log-file"></a>1. 로그 파일에 대 한 통계를 반환 합니다.

**적용 대상:** (2008부터 시작) 하는 SQL Server, Azure SQL Database

 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 로그 파일에 대한 통계를 반환합니다.  
  
```sql  
SELECT * FROM sys.dm_io_virtual_file_stats(DB_ID(N'AdventureWorks2012'), 2);  
GO  
```  
  
### <a name="b-return-statistics-for-file-in-tempdb"></a>2. Tempdb에서 파일에 대 한 통계를 반환 합니다.

**적용 대상:** Azure SQL Data Warehouse

```sql
SELECT * FROM sys.dm_pdw_nodes_io_virtual_file_stats 
WHERE database_name = ‘tempdb’ AND file_id = 2;

```

## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [I O 관련 동적 관리 뷰 및 함수 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  

