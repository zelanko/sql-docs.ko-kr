---
title: 시스템 저장 프로시저 (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2016 CTP3)
f1_keywords:
- sql13.TSQLSysNoExpandPortal.f1
- sql13.TSQLSysNoExpandPortal.f1_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stored procedures [SQL Server]
- APIs [SQL Server]
- stored procedures [SQL Server], categories
- system stored procedures [SQL Server], categories
- system stored procedures [SQL Server]
ms.assetid: a5c4d5b8-5a24-4a2d-99b4-d003b546ee3a
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 481b0c451f5161231cf64402c5c758870a07be62
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979465"
---
# <a name="system-stored-procedures-transact-sql"></a>시스템 저장 프로시저(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 시스템 저장 프로시저를 통해 다양한 관리 및 정보 작업 수행할 수 있습니다. 시스템 저장 프로시저는 다음 표에 표시된 범주별로 그룹화됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|범주|Description|  
|--------------|-----------------|  
|[활성 지역 복제 저장 프로시저](http://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)|Azure SQL Database에서 활성 지역 복제 구성 관리를 관리 하는 데 사용|  
|[카탈로그 저장된 프로시저](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)|ODBC 데이터 사전 기능을 구현하고 ODBC 응용 프로그램을 원본 시스템 테이블 변경으로부터 격리합니다.|  
|[변경 데이터 캡처 저장된 프로시저](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)|변경 데이터 캡처 개체를 사용하도록 설정 또는 해제하거나 해당 개체에 대해 보고합니다.|  
|[커서 저장 프로시저](../../relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql.md)|커서 변수 기능을 구현합니다.|  
|[데이터 수집기 저장 프로시저](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)|데이터 수집기 및 컬렉션 집합, 컬렉션 항목, 컬렉션 유형과 같은 구성 요소 작업에 사용됩니다.|  
|[데이터베이스 엔진 저장 프로시저](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 일반적인 유지 관리를 수행합니다.|  
|[데이터베이스 메일 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 전자 메일 작업을 수행합니다.|  
|[데이터베이스 유지 관리 계획 저장 프로시저](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)|데이터베이스 성능을 관리하는 데 필요한 주요 유지 관리 태스크를 설정합니다.|  
|[분산된 쿼리 저장 프로시저](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)|분산 쿼리를 구현하고 관리합니다.|  
|[Filestream 및 FileTable 저장된 프로시저 &#40;TRANSACT-SQL&#41;](http://msdn.microsoft.com/library/54beca08-c012-4ebd-aa68-d8a10d221b64)|FILESTREAM 및 FileTable 기능을 구성하고 관리합니다.|  
|[방화벽 규칙 저장 프로시저 &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/firewall-rules-stored-procedures-azure-sql-database.md)|Azure SQL Database 방화벽을 구성 하는 데 사용 합니다.|  
|[전체 텍스트 검색 저장 프로시저](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)|전체 텍스트 인덱스를 구현하고 쿼리합니다.|  
|[일반 확장 저장된 프로시저](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)|다양한 유지 관리 작업을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 외부 프로그램으로의 인터페이스를 제공합니다.|  
|[로그 전달 저장 프로시저](../../relational-databases/system-stored-procedures/log-shipping-stored-procedures-transact-sql.md)|로그 전달 구성을 구성, 수정 및 모니터링합니다.|  
|[관리 데이터 웨어하우스 저장된 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql.md)|관리 데이터 웨어하우스를 구성 하는 데 사용 합니다.|  
|[OLE Automation 저장 프로시저](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)|표준 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리에서 표준 Automation 개체를 사용할 수 있도록 합니다.|  
|[정책 기반 관리 저장 프로시저](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)|정책 기반 관리에 사용됩니다.|  
|[PolyBase 저장 프로시저](http://msdn.microsoft.com/library/a522b303-bd1b-410b-92d1-29c950a15ede)|추가 또는 PolyBase 스케일 아웃 그룹에서 컴퓨터를 제거 합니다.|  
|[쿼리 저장소 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)|성능을 조정 하는 데 사용 합니다.|  
|[복제 저장 프로시저](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)|복제를 관리합니다.|  
|[보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)|보안을 관리합니다.|  
|[스냅숏된 백업 저장된 프로시저](http://msdn.microsoft.com/library/c278db87-5770-4037-a1e6-b9853a943339)|개별 백업 파일 스냅숏을 삭제 하거나 해당 스냅숏을 모두 함께 FILE_SNAPSHOT 백업을 삭제 하려면 사용 합니다.|  
|[공간 인덱스 저장 프로시저](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)|분석 하 고 공간 인덱스의 인덱싱 성능을 개선 하는 데 사용 합니다.|  
|[SQL Server 에이전트 저장 프로시저](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에서 성능 및 작업을 모니터링하는 데 사용합니다.|  
|[SQL Server Profiler 저장 프로시저](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 예약된 이벤트 기반 작업을 관리하는 데 사용합니다.|  
|[Stretch Database 저장 프로시저](../../relational-databases/system-stored-procedures/stretch-database-extended-stored-procedures-transact-sql.md)|Stretch database를 관리 하는 데 사용 합니다.|  
|[Temporal 테이블에 대 한 프로시저 정보](http://msdn.microsoft.com/library/f28ca74e-7876-4592-b794-e78e3690fff6)|Temporal 테이블에 대해 사용|  
|[XML 저장 프로시저](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)|XML 텍스트 관리에 사용합니다.|  
  
> [!NOTE]  
>  특별히 지정되지 않는 한 모든 시스템 저장 프로시저는 성공을 의미하는 값 0을 반환합니다. 실패에 대해서는 0이 아닌 값을 반환합니다.  
  
## <a name="api-system-stored-procedures"></a>API 시스템 저장 프로시저  
 ADO, OLE DB 및 ODBC 응용 프로그램에 대해 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 실행하는 사용자는 이러한 응용 프로그램이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 참조에서 다루지 않는 시스템 저장 프로시저를 사용한다는 사실을 알 수 있습니다. 이러한 저장된 프로시저에서 사용 되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 데이터베이스 API의 기능을 구현 합니다. 이러한 저장 프로시저는 사용자 요청을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 전달하기 위해 공급자 또는 드라이버가 사용하는 메커니즘으로 공급자 또는 드라이버에서 내부적으로만 사용하도록 되어 있습니다. 명시적으로 호출을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-기반된 응용 프로그램 지원 되지 않습니다.  
  
 Sp_createorphan 및 sp_droporphans 저장 프로시저는 ODBC를 사용 **ntext**를 **텍스트**, 및 **이미지** 처리 합니다.  
  
 sp_reset_connection 저장 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 트랜잭션의 원격 저장 프로시저 호출을 지원하는 데 사용됩니다. 이 저장 프로시저는 연결 풀에서 연결이 다시 사용될 때 Audit Login 및 Audit Logout 이벤트도 실행합니다.  
  
 다음 표에 있는 시스템 저장 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내부 또는 클라이언트 API를 통해서만 사용되며 일반적인 용도로는 사용되지 않습니다. 시스템 기본 테이블은 변경될 수 있으며 호환성이 보장되지 않습니다.  
  
 다음 저장 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에 문서화되어 있습니다.  
  
|||  
|-|-|  
|sp_catalogs|sp_column_privileges|  
|sp_column_privileges_ex|sp_columns|  
|sp_columns_ex|sp_databases|  
|sp_cursor|sp_cursorclose|  
|sp_cursorexecute|sp_cursorfetch|  
|sp_cursoroption|sp_cursoropen|  
|sp_cursorprepare|sp_cursorprepexec|  
|sp_cursorunprepare|sp_execute|  
|sp_datatype_info|sp_fkeys|  
|sp_foreignkeys|sp_indexes|  
|sp_pkeys|sp_primarykeys|  
|sp_prepare|sp_prepexec|  
|sp_prepexecrpc|sp_unprepare|  
|sp_server_info|sp_special_columns|  
|sp_sproc_columns|sp_statistics|  
|sp_table_privileges|sp_table_privileges_ex|  
|sp_tables|sp_tables_ex|  
  
 다음 저장 프로시저는 문서화되어 있지 않습니다.  
  
|||  
|-|-|  
|sp_assemblies_rowset|sp_assemblies_rowset_rmt|  
|sp_assemblies_rowset2|sp_assembly_dependencies_rowset|  
|sp_assembly_dependencies_rowset_rmt|sp_assembly_dependencies_rowset2|  
|sp_bcp_dbcmptlevel|sp_catalogs_rowset|  
|sp_catalogs_rowset;2|sp_catalogs_rowset;5|  
|sp_catalogs_rowset_rmt|sp_catalogs_rowset2|  
|sp_check_constbytable_rowset|sp_check_constbytable_rowset;2|  
|sp_check_constbytable_rowset2|sp_check_constraints_rowset|  
|sp_check_constraints_rowset;2|sp_check_constraints_rowset2|  
|sp_column_privileges_rowset|sp_column_privileges_rowset;2|  
|sp_column_privileges_rowset;5|sp_column_privileges_rowset_rmt|  
|sp_column_privileges_rowset2|sp_columns_90|  
|sp_columns_90_rowset|sp_columns_90_rowset_rmt|  
|sp_columns_90_rowset2|sp_columns_ex_90|  
|sp_columns_rowset|sp_columns_rowset;2|  
|sp_columns_rowset;5|sp_columns_rowset_rmt|  
|sp_columns_rowset2|sp_constr_col_usage_rowset|  
|sp_datatype_info_90|sp_ddopen;1|  
|sp_ddopen;10|sp_ddopen;11|  
|sp_ddopen;12|sp_ddopen;13|  
|sp_ddopen;2|sp_ddopen;3|  
|sp_ddopen;4|sp_ddopen;5|  
|sp_ddopen;6|sp_ddopen;7|  
|sp_ddopen;8|sp_ddopen;9|  
|sp_foreign_keys_rowset|sp_foreign_keys_rowset;2|  
|sp_foreign_keys_rowset;3|sp_foreign_keys_rowset;5|  
|sp_foreign_keys_rowset_rmt|sp_foreign_keys_rowset2|  
|sp_foreign_keys_rowset3|sp_indexes_90_rowset|  
|sp_indexes_90_rowset_rmt|sp_indexes_90_rowset2|  
|sp_indexes_rowset|sp_indexes_rowset;2|  
|sp_indexes_rowset;5|sp_indexes_rowset_rmt|  
|sp_indexes_rowset2|sp_linkedservers_rowset|  
|sp_linkedservers_rowset;2|sp_linkedservers_rowset2|  
|sp_oledb_database|sp_oledb_defdb|  
|sp_oledb_deflang|sp_oledb_language|  
|sp_oledb_ro_usrname|sp_primary_keys_rowset|  
|sp_primary_keys_rowset;2|sp_primary_keys_rowset;3|  
|sp_primary_keys_rowset;5|sp_primary_keys_rowset_rmt|  
|sp_primary_keys_rowset2|sp_procedure_params_90_rowset|  
|sp_procedure_params_90_rowset2|sp_procedure_params_rowset|  
|sp_procedure_params_rowset;2|sp_procedure_params_rowset2|  
|sp_procedures_rowset|sp_procedures_rowset;2|  
|sp_procedures_rowset2|sp_provider_types_90_rowset|  
|sp_provider_types_rowset|sp_schemata_rowset|  
|sp_schemata_rowset;3|sp_special_columns_90|  
|sp_sproc_columns_90|sp_statistics_rowset|  
|sp_statistics_rowset;2|sp_statistics_rowset2|  
|sp_stored_procedures|sp_table_constraints_rowset|  
|sp_table_constraints_rowset;2|sp_table_constraints_rowset2|  
|sp_table_privileges_rowset|sp_table_privileges_rowset;2|  
|sp_table_privileges_rowset;5|sp_table_privileges_rowset_rmt|  
|sp_table_privileges_rowset2|sp_table_statistics_rowset|  
|sp_table_statistics_rowset;2|sp_table_statistics2_rowset|  
|sp_tablecollations|sp_tablecollations_90|  
|sp_tables_info_90_rowset|sp_tables_info_90_rowset_64|  
|sp_tables_info_90_rowset2|sp_tables_info_90_rowset2_64|  
|sp_tables_info_rowset|sp_tables_info_rowset;2|  
|sp_tables_info_rowset_64|sp_tables_info_rowset_64;2|  
|sp_tables_info_rowset2|sp_tables_info_rowset2_64|  
|sp_tables_rowset;2|sp_tables_rowset;5|  
|sp_tables_rowset_rmt|sp_tables_rowset2|  
|sp_usertypes_rowset|sp_usertypes_rowset_rmt|  
|sp_usertypes_rowset2|sp_views_rowset|  
|sp_views_rowset2|sp_xml_schema_rowset|  
|sp_xml_schema_rowset2||  
  
## <a name="see-also"></a>관련 항목  
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [저장 프로시저&#40;데이터베이스 엔진&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [저장된 프로시저를 실행 &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/stored-procedures-running.md)   
 [저장된 프로시저 실행](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [저장 프로시저 실행](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
