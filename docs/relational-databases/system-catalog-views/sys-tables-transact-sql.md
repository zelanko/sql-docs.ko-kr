---
title: sys.tables (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- tables_TSQL
- sys.tables_TSQL
- sys.tables
- tables
dev_langs:
- TSQL
helpviewer_keywords:
- sys.tables catalog view
ms.assetid: 8c42eba1-c19f-4045-ac82-b97a5e994090
caps.latest.revision: 70
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e3daf28a4bdb50de899de32b4f60f82112dec8c2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="systables-transact-sql"></a>sys.tables(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 각 사용자 테이블마다 하나의 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|\<열을 상속 >||이 뷰가 상속 하는 열 목록은 참조 [sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)합니다.|  
|lob_data_space_id|**int**|0이 아닌 값은 이 테이블의 BLOB(Binary Large Object) 데이터를 보관하는 데이터 공간(파일 그룹 또는 파티션 구성표)의 ID입니다. LOB 데이터 형식의 예로 **varbinary (max)**, **varchar (max)**, **geography**, 또는 **xml**합니다.<br /><br /> 0 = 테이블에 LOB 데이터가 없습니다.|  
|filestream_data_space_id|**int**|FILESTREAM 파일 그룹 또는 FILESTREAM 파일 그룹으로 구성된 파티션 구성표의 데이터 공간 ID입니다.<br /><br /> FILESTREAM 파일 그룹의 이름을 보고 하려면 쿼리를 실행 `SELECT FILEGROUP_NAME (filestream_data_space_id) FROM sys.tables`합니다.<br /><br /> sys.tables는 filestream_data_space_id = data_space_id에서 다음과 같은 뷰에 조인할 수 있습니다.<br /><br /> -sys.filegroups<br /><br /> -sys.partition_schemes<br /><br /> -sys.indexes<br /><br /> -sys.allocation_units<br /><br /> -sys.fulltext_catalogs<br /><br /> -sys.data_spaces<br /><br /> -sys.destination_data_spaces<br /><br /> -sys.master_files<br /><br /> -sys.database_files<br /><br /> -backupfilegroup (filegroup_id에 조인)|  
|max_column_id_used|**int**|이 테이블에 사용된 최대 열 ID입니다.|  
|lock_on_bulk_load|**bit**|대량 로드 시 테이블이 잠깁니다. 자세한 내용은 [sp_tableoption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)을 참조하세요.|  
|uses_ansi_nulls|**bit**|테이블이 SET ANSI_NULLS 데이터베이스 옵션을 ON으로 설정하여 생성되었습니다.|  
|is_replicated|**bit**|1 = 테이블이 스냅숏 복제 또는 트랜잭션 복제를 사용하여 게시됩니다.|  
|has_replication_filter|**bit**|1 = 테이블에 복제 필터가 있습니다.|  
|is_merge_published|**bit**|1 = 테이블이 병합 복제를 사용하여 게시됩니다.|  
|is_sync_tran_subscribed|**bit**|1 = 테이블이 즉시 업데이트 구독을 사용하여 구독됩니다.|  
|has_unchecked_assembly_data|**bit**|1 = 테이블은 마지막 ALTER ASSEMBLY를 수행하는 동안 정의가 변경된 어셈블리에 종속되어 있는 데이터를 포함합니다. 다음 번 DBCC CHECKDB 또는 DBCC CHECKTABLE이 성공적으로 수행된 후에 다시 0으로 설정됩니다.|  
|text_in_row_limit|**int**|행의 텍스트에 허용된 최대 바이트입니다.<br /><br /> 0 = text in row 옵션이 설정되지 않았습니다. 자세한 내용은 [sp_tableoption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)을 참조하세요.|  
|large_value_types_out_of_row|**bit**|1 = 큰 값 유형은 행 밖에 저장됩니다. 자세한 내용은 [sp_tableoption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)을 참조하세요.|  
|is_tracked_by_cdc|**bit**|1 = 테이블에 변경 데이터 캡처가 설정되어 있습니다. 자세한 내용은 참조 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)합니다.|  
|lock_escalation|**tinyint**|테이블에 대한 LOCK_ESCALATION 옵션의 값입니다.<br /><br /> 0 = TABLE<br /><br /> 1 = DISABLE<br /><br /> 2 = AUTO|  
|lock_escalation_desc|**nvarchar(60)**|테이블에 대한 lock_escalation 옵션의 텍스트 설명입니다. 가능한 값은 TABLE, AUTO 및 DISABLE입니다.|  
|is_filetable|**bit**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]까지<br /><br /> 1 = 테이블이 FileTable입니다.<br /><br /> FileTables 기능에 대한 자세한 내용은 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)를 참조하세요.|  
|durability|**tinyint**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]까지<br /><br /> 다음은 가능한 값입니다.<br /><br /> 0 = SCHEMA_AND_DATA<br /><br /> 1 = SCHEMA_ONLY<br /><br /> 0 값은 기본값입니다.|  
|durability_desc|**nvarchar(60)**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]까지<br /><br /> 가능한 값은 다음과 같습니다.<br /><br /> SCHEMA_ONLY<br /><br /> SCHEMA_AND_DATA<br /><br /> SCHEMA_AND_DATA 값은 테이블이 메모리 내 영구 테이블임을 나타냅니다. SCHEMA_AND_DATA는 메모리 액세스에 최적화된 테이블에 대한 기본값입니다. SCHEMA_ONLY 값은 메모리 액세스에 최적화된 개체가 포함된 데이터베이스를 다시 시작할 때 테이블 데이터가 저장되지 않음을 나타냅니다.|  
|is_memory_optimized|**bit**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]까지<br /><br /> 가능한 값은 다음과 같습니다.<br /><br /> 0 = 메모리 액세스에 최적화가 아닙니다.<br /><br /> 1 = 메모리 액세스에 최적화입니다.<br /><br /> 0 값은 기본값입니다.<br /><br /> 메모리 액세스에 최적화된 테이블은 메모리 내 사용자 테이블입니다. 디스크에 저장된 스키마는 다른 사용자 테이블과 비슷합니다. 메모리 액세스에 최적화된 테이블은 고유하게 컴파일된 저장 프로시저에서 액세스할 수 있습니다.|  
|temporal_type|**tinyint**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]까지<br /><br /> 테이블의 형식을 나타내는 숫자 값입니다.<br /><br /> 0 = NON_TEMPORAL_TABLE<br /><br /> 1 = HISTORY_TABLE<br /><br /> 2 = SYSTEM_VERSIONED_TEMPORAL_TABLE|  
|temporal_type_desc|**nvarchar(60)**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]까지<br /><br /> 유형의 테이블의 텍스트 설명:<br /><br /> NON_TEMPORAL_TABLE<br /><br /> HISTORY_TABLE<br /><br /> SYSTEM_VERSIONED_TEMPORAL_TABLE|  
|history_table_id|**int**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]까지<br /><br /> 때 temporal_type IN (2, 4) 기록 데이터를 유지 하는 테이블의 object_id 반환 그렇지 않으면 NULL을 반환 합니다.|  
|is_remote_data_archive_enabled|**bit**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]<br /><br /> 스트레치 사용 테이블 인지를 나타냅니다.<br /><br /> 0 = 테이블은 스트레치 지원 하지 않습니다.<br /><br /> 1 = 테이블은 스트레치 사용 합니다.<br /><br /> 자세한 내용은 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하십시오.|  
|is_external|**bit**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)], 및 [!INCLUDE[sssdwfull](../../includes/sssdwfull-md.md)]합니다.<br /><br /> 테이블은 외부 테이블을 나타냅니다.<br /><br /> 0 = 테이블이 외부 테이블 아닙니다.<br /><br /> 1 = 테이블이 외부 테이블입니다.| 
|history_retention_period|**int**|**적용 대상**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]. <br/><br/>History_retention_period_unit으로 지정 된 값에서 임시 기록 보존 기간의 지속 시간을 나타내는 숫자 값입니다. |  
|history_retention_period_unit|**int**|**적용 대상**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]. <br/><br/>임시 기록 보존 기간 단위의 형식을 나타내는 숫자 값입니다. <br /><br />-1: 무한 <br /><br />3: 일 <br /><br />4: 주 <br /><br />5: 월 <br /><br />6: 연도 |  
|history_retention_period_unit_desc|**nvarchar(10)**|**적용 대상**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]. <br/><br/>임시 기록 보존 기간 단위 유형의의 텍스트 설명입니다. <br /><br />INFINITE <br /><br />DAY <br /><br />WEEK <br /><br />MONTH <br /><br />YEAR |  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 기본 키가 없는 모든 사용자 테이블을 반환합니다.  
  
```  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasPrimaryKey') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
다음 예제에서는 어떻게 관련된 임시 데이터 노출 될 수 있습니다.  
   
**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]까지
  
```  
SELECT T1.object_id, T1.name as TemporalTableName, SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,  
T2.name as HistoryTableName, SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,  
T1.temporal_type_desc  
FROM sys.tables T1  
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id  
ORDER BY T1.temporal_type desc  
```  

다음 예에서는 임시 기록 보존 하는 방법은 수 노출 하는 방법을 보여 줍니다.  

**적용 대상**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].  
  
```  
SELECT DB.is_temporal_history_retention_enabled, SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema, 
T1.name as TemporalTableName, SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema, T2.name as HistoryTableName,
T1.history_retention_period, T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases where name = DB_NAME()) DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2 
```  
  
## <a name="see-also"></a>관련 항목:  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [DBCC checkdb& #40; Transact SQL & #41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKTABLE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [SQL Server 시스템 카탈로그 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
