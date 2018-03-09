---
title: "Stretch Database 관리 및 문제 해결 | Microsoft 문서"
ms.custom: 
ms.date: 06/27/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, managing
- Stretch Database, troubleshooting
- managing Stretch Database
- troubleshooting Stretch Database
ms.assetid: 6334db3e-9297-44df-8d53-211187a95520
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 55c3cefee2008ed430e1af1fecc5162a3c165473
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="manage-and-troubleshoot-stretch-database"></a>Stretch Database 관리 및 문제 해결
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Stretch Database를 관리하고 문제를 해결하려면 이 문서에서 설명하는 도구와 방법을 사용하세요.  
## <a name="manage-local-data"></a>로컬 데이터 관리  
  
###  <a name="LocalInfo"></a> 스트레치 데이터베이스에 활성화된 로컬 데이터베이스 및 테이블에 대한 정보 얻기  
 카탈로그 뷰 **sys.databases** 및 **sys.tables** 를 열어 스트레치가 활성화된 SQL Server 데이터베이스 및 테이블에 대한 정보를 참조하세요. 자세한 내용은 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 및 [sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)를 참조하세요.  
 
 SQL Server에서 스트레치가 활성화된 테이블을 사용하는 공간을 확인하려면 다음 문을 실행합니다.
 
 ```sql
USE <Stretch-enabled database name>;
GO
EXEC sp_spaceused '<Stretch-enabled table name>', 'true', 'LOCAL_ONLY';
GO
 ```
   
## <a name="manage-data-migration"></a>데이터 마이그레이션 관리  
  
### <a name="check-the-filter-function-applied-to-a-table"></a>테이블에 적용된 필터 함수 확인  
 스트레치 데이터베이스에서 마이그레이션할 행을 선택하는 데 사용하는 함수를 식별하려면 **sys.remote_data_archive_tables** 카탈로그 뷰를 열고 **filter_predicate** 열의 값을 확인합니다. 값이 null이면 전체 테이블을 마이그레이션할 수 있습니다. 자세한 내용은 [sys.remote_data_archive_tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md) 및 [필터 함수를 사용하여 마이그레이션할 행 선택](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)을 참조하세요.  
  
###  <a name="Migration"></a> 데이터 마이그레이션 상태를 확인합니다.  
 Stretch Database 모니터에서 데이터 마이그레이션을 모니터링하려면 SQL Server Management Studio 데이터베이스에 대해 **작업 | 스트레치 | 모니터** 를 선택합니다. 자세한 내용은 [데이터 마이그레이션 모니터링 및 문제 해결&#40;스트레치 데이터베이스&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)를 참조하세요.  
  
 또는 마이그레이션된 데이터의 배치 및 행 수를 보려면 동적 관리 뷰 **sys.dm_db_rda_migration_status** 를 엽니다.  
  
###  <a name="Firewall"></a> 데이터 마이그레이션 문제 해결  
 문제 해결 제안 사항에 대해서는 [데이터 마이그레이션 모니터링 및 문제 해결&#40;스트레치 데이터베이스&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)를 참조하세요.  
  
## <a name="manage-remote-data"></a>원격 데이터 관리  
  
###  <a name="RemoteInfo"></a> 스트레치 데이터베이스에서 사용하는 원격 데이터베이스와 테이블에 대한 정보 얻기  
 마이그레이션된 데이터가 저장되는 원격 데이터베이스 및 테이블에 대한 정보를 보려면 카탈로그 뷰 **sys.remote_data_archive_databases** 및 **sys.remote_data_archive_tables** 를 엽니다. 자세한 내용은 [sys.remote_data_archive_databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-databases.md) 및 [sys.remote_data_archive_tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md)를 참조하세요.  
 
Azure에서 스트레치가 활성화된 테이블을 사용하는 공간을 확인하려면 다음 문을 실행합니다.
 
 ```sql
USE <Stretch-enabled database name>;
GO
EXEC sp_spaceused '<Stretch-enabled table name>', 'true', 'REMOTE_ONLY';
GO
 ```

### <a name="delete-migrated-data"></a>마이그레이션된 데이터 삭제  
Azure에 이미 마이그레이션된 데이터를 삭제하려는 경우 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)에 설명된 단계에 따릅니다.  
  
## <a name="manage-table-schema"></a>테이블 스키마 관리

### <a name="dont-change-the-schema-of-the-remote-table"></a>원격 테이블의 스키마를 변경하지 않음  
 스트레치 데이터베이스에 대해 구성된 SQL Server 테이블과 관련된 원격 Azure 테이블의 스키마를 변경하지 마십시오. 특히 열의 이름 또는 데이터 유형을 수정하지 마십시오. 스트레치 데이터베이스 기능에서는 SQL Server 테이블의 스키마와 관련하여 원격 테이블의 스키마에 대해 다양한 가정을 합니다. 원격 스키마를 변경하는 경우 Stretch Database이 변경된 테이블에 대한 작동을 중지합니다.  

### <a name="reconcile-table-columns"></a>테이블 열 조정  
원격 테이블의 열을 실수로 삭제한 경우 **sp_rda_reconcile_columns** 를 실행하여 원격 테이블이 아닌 스트레치가 활성화된 SQL Server 테이블에 있는 원격 테이블에 열을 추가합니다. 자세한 내용은 [sys.sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md)를 참조하세요.  
  
  > [!IMPORTANT]
  > **sp_rda_reconcile_columns** 가 원격 테이블에서 실수로 삭제한 열을 다시 만드는 경우 이전에 삭제된 열에 있었던 데이터를 복원하지 않습니다.
  
**sp_rda_reconcile_columns** 는 스트레치가 활성화된 SQL Server 테이블이 아닌 원격 테이블에 있는 원격 테이블의 열을 삭제하지 않습니다. 원격 Azure 테이블의 열이 스트레치가 활성화된 SQL Server 테이블에 더 이상 존재하지 않는 경우 이러한 추가 열이 있어도 스트레치 데이터베이스가 정상적으로 작동합니다. 필요에 따라 추가 열을 수동으로 제거할 수 있습니다.  
 
## <a name="manage-performance-and-costs"></a>성능 및 비용 관리  
  
### <a name="troubleshoot-query-performance"></a>쿼리 성능 문제 해결  
  스트레치가 설정된 테이블이 포함된 쿼리의 성능은 테이블에 스트레치가 설정되기 전보다 훨씬 느려집니다. 쿼리 성능이 크게 저하될 경우 다음과 같은 문제가 있는지 검토하십시오.  
  
-   Azure 서버가 SQL Server와 지리적으로 다른 지역에 있는 경우 Azure 서버를 SQL Server와 지리적으로 같은 지역에 구성하여 네트워크 대기 시간을 줄이십시오.  
  
-   네트워크 상태가 저하되었을 수 있습니다. 네트워크 관리자에게 최근 발생한 문제 또는 중단에 대해 문의하십시오.  
  
### <a name="increase-azure-performance-level-for-resource-intensive-operations-such-as-indexing"></a>인덱싱과 같이 리소스를 많이 사용하는 작업의 Azure 성능 수준 향상  
 스트레치 데이터베이스에 대해 구성된 대형 테이블에 인덱스를 빌드, 다시 빌드 또는 다시 구성하고 이 시간 동안 Azure에서 마이그레이션된 데이터의 쿼리가 많을 것으로 예상되는 경우, 작업 기간 동안 해당 원격 Azure 데이터베이스의 성능 수준을 높여 보세요. 성능 수준 및 가격에 대한 자세한 내용은 [SQL Server Stretch Database 가격](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)을 참조하세요.  
  
### <a name="you-cant-pause-the-sql-server-stretch-database-service-on-azure"></a>Azure의 SQL Server 스트레치 데이터베이스 서비스를 일시 중지할 수 없습니다.  
 적절한 성능 및 가격 수준을 선택하고 있는지 확인합니다. 리소스를 많이 사용하는 작업에 대해 일시적으로 성능 수준을 높인 경우 작업이 완료되면 이전 수준으로 복원하세요. 성능 수준 및 가격에 대한 자세한 내용은 [SQL Server 스트레치 데이터베이스 가격](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)을 참조하세요.  
   
 ## <a name="change-the-scope-of-queries"></a>쿼리의 범위 변경  
 스트레치 사용 테이블에 대한 쿼리는 기본적으로 로컬 및 원격 데이터를 반환합니다. 모든 사용자의 모든 쿼리에 대한 쿼리의 범위를 변경하거나 관리자의 단일 쿼리에 대해서만 변경할 수 있습니다.  
   
 ### <a name="change-the-scope-of-queries-for-all-queries-by-all-users"></a>모든 사용자의 모든 쿼리에 대한 쿼리 범위 변경  
 모든 사용자의 모든 쿼리의 범위를 변경하려면 저장 프로시저 **sys.sp_rda_set_query_mode**를 실행합니다. 로컬 데이터만 쿼리하는 범위를 줄이거나 모든 쿼리를 사용하지 않도록 설정하거나 기본 설정을 복원할 수 있습니다. 자세한 내용은 [sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)를 참조하세요.  
   
 ### <a name="queryHints"></a>관리자의 단일 쿼리에 대한 쿼리 범위 변경  
 db_owner 역할 멤버의 단일 쿼리 범위를 변경하려면 ***WITH ( REMOTE_DATA_ARCHIVE_OVERRIDE =* value** ) 쿼리 힌트를 SELECT 문에 추가합니다. REMOTE_DATA_ARCHIVE_OVERRIDE 쿼리 힌트는 다음 값을 가질 수 있습니다.  
 -   **LOCAL_ONLY** 로컬 데이터만 쿼리합니다.  
   
 -   **REMOTE_ONLY** 원격 데이터만 쿼리합니다.  
   
 -   **STAGE_ONLY** 스트레치 데이터베이스가 마이그레이션에 적합한 행을 준비하고 마이그레이션 후 특정 기간 동안 마이그레이션된 행을 유지하는 테이블의 데이터만 쿼리합니다. 이 쿼리 힌트는 준비 테이블을 쿼리하는 유일한 방법입니다.  
  
예를 들어 다음 쿼리는 로컬 결과만 반환합니다.  
  
 ```sql  
USE <Stretch-enabled database name>;
GO
SELECT * FROM <Stretch_enabled table name> WITH (REMOTE_DATA_ARCHIVE_OVERRIDE = LOCAL_ONLY) WHERE ... ;
GO
```  
   
 ## <a name="adminHints"></a>관리 업데이트 및 삭제 만들기  
 기본적으로 스트레치 사용 테이블에서 마이그레이션에 적합한 행 또는 이미 마이그레이션된 행을 업데이트 또는 삭제할 수 없습니다. 문제를 해결해야 할 경우 db_owner 역할의 멤버가 ***WITH ( REMOTE_DATA_ARCHIVE_OVERRIDE =* value** ) 쿼리 힌트를 문에 추가하여 UPDATE 또는 DELETE 작업을 실행할 수 있습니다. REMOTE_DATA_ARCHIVE_OVERRIDE 쿼리 힌트는 다음 값을 가질 수 있습니다.  
 -   **LOCAL_ONLY** 로컬 데이터만 업데이트하거나 삭제합니다.  
   
 -   **REMOTE_ONLY** 원격 데이터만 업데이트하거나 삭제합니다.  
   
 -   **STAGE_ONLY** 스트레치 데이터베이스가 마이그레이션에 적합한 행을 준비하고 마이그레이션 후 특정 기간 동안 마이그레이션된 행을 유지하는 테이블의 데이터만 업데이트하거나 삭제합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이그레이션 모니터링 및 문제 해결&#40;스트레치 데이터베이스&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)   
[스트레치 사용 데이터베이스 백업(스트레치 데이터베이스)](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
[스트레치 사용 데이터베이스 복원(스트레치 데이터베이스)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
  
