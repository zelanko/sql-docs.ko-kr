---
title: Stretch Database용 확장 이벤트 | Microsoft 문서
ms.custom: ''
ms.date: 06/14/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: stretch-database
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 70485e74-2e25-4e7e-be6c-9dd1780a42e3
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 47948ec945b63772d84713df08c6a54175ead166
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="extended-events-for-stretch-database"></a>Stretch Database용 확장 이벤트
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


스트레치 데이터베이스는 문제 해결을 위해 몇 가지 확장 이벤트를 제공합니다.  
  
자세한 내용은 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)를 참조하세요. 문제 해결을 위해 확장 이벤트 세션을 시작하는 방법은 [확장 이벤트 세션 만들기](http://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74)를 참조하세요.  
  
## <a name="list-of-extended-events-for-stretch-database"></a>스트레치 데이터베이스용 확장 이벤트 목록  
  
이벤트 이름|이벤트 설명   
---------|---------  
remote_data_archive_db_ddl|데이터를 확장하기 위한 데이터베이스 T-SQL ddl이 처리될 때 발생합니다.  
remote_data_archive_provision_operation|프로비전 작업이 시작 또는 끝날 때 발생합니다.  
remote_data_archive_query_rewrite|확장을 위한 쿼리 다시 쓰기 중에 RelOp_Get이 바뀌면 발생합니다.  
remote_data_archive_table_ddl|데이터를 확장하기 위한 테이블 T-SQL ddl이 처리될 때 발생합니다.  
remote_data_archive_telemetry|온-프레미스 시스템이 Azure DB로 원격 분석 이벤트를 전송할 때마다 발생합니다.  
remote_data_archive_telemetry_rejected|AzureDB Stretch 원격 분석 이벤트가 거부될 때마다 발생합니다.  
repopulate_stretch_schema_task_queue_complete|늘이기 스키마 태스크 큐 다시 채우기 완료를 보고합니다.  
repopulate_stretch_schema_task_queue_start|늘이기 스키마 태스크 큐를 다시 채우는 태스크가 시작되었음을 보고합니다.  
stretch_codegen_errorlog|코드 생성기의 출력을 보고합니다.  
stretch_codegen_start|늘이기 코드 생성 시작을 보고합니다.  
stretch_create_remote_table_start|원격 테이블 만들기의 시작을 보고합니다.  
stretch_database_disable_completed|ALTER DATABASE SET REMOTE_DATA_ARCHIVE OFF 명령의 완료를 보고합니다.  
stretch_database_enable_completed|ALTER DATABASE SET REMOTE_DATA_ARCHIVE ON 명령 완료를 보고합니다.  
stretch_database_reauthorize_completed|sp_rda_reauthorize_db spec proc의 완료를 보고합니다.  
stretch_index_reconciliation_codegen_completed|늘이기 원격 인덱스 작업에 대한 코드 생성 완료를 보고합니다.  
stretch_index_update_step_completed|늘어난 인덱스 업데이트 작업의 기간을 보고합니다.  
stretch_migration_debug_trace|마이그레이션 확대 동작에 대한 디버그 추적입니다.  
stretch_migration_dequeue_migration|데이터베이스에 대한 늘이기 마이그레이션 태스크가 큐에서 제거되면 이벤트가 발생합니다.  
stretch_migration_queue_migration|데이터베이스 및 개체의 마이그레이션을 시작하기 위해 패킷을 큐 대기합니다.  
stretch_migration_requeue_migration|늘이기 마이그레이션 태스크 패킷이 다시 대기하면 이벤트가 발생합니다.  
stretch_migration_start_migration|데이터베이스 및 개체의 마이그레이션을 시작합니다.  
stretch_migration_start_unmigration|데이터베이스 및 개체에 대한 마이그레이션 해제를 시작합니다.  
stretch_remote_column_execution_completed|늘어난 열에 대해 생성된 코드의 원격 실행 완료를 보고합니다.  
stretch_remote_column_reconciliation_codegen_completed|확장 원격 열 조정에 대한 코드 생성 완료를 보고합니다.  
stretch_remote_index_execution_completed|늘어난 인덱스에 대해 생성된 코드의 원격 실행 완료를 보고합니다.  
stretch_schema_queue_task|데이터베이스 및 개체에 대해 스키마 태스크를 처리하는 동안 패킷이 대기열 목록에 추가되려고 하는 시기를 보고합니다.  
stretch_schema_script_execution_completed|늘이기 스키마 태스크 처리 중 확대 스크립트 실행 완료를 보고합니다.  
stretch_schema_script_execution_skipped|늘이기 스키마 태스크 처리 중 확대 스크립트 실행 건너뛰기를 보고합니다.  
stretch_schema_script_execution_start|늘이기 스키마 태스크 처리 중 확대 스크립트 실행이 시작되었음을 보고합니다.  
stretch_schema_task_failed|늘이기 스키마 태스크 중 확대 스키마 함수의 오류를 보고합니다.  
stretch_schema_task_skipped|확장 스키마 기능 중 확장 스키마 태스크를 건너뛰었음을 보고합니다.  
stretch_schema_task_start|늘이기 스키마 태스크 중 늘이기 스키마 함수 시작을 보고합니다.  
stretch_schema_task_succeeded|늘이기 스키마 태스크 중 확대 스키마 함수의 정상적 완료를 보고합니다.  
stretch_sp_migration_get_batch_id|sp_stretch_get_batch_id를 호출합니다.  
stretch_sync_metadata_start|마이그레이션 태스크 중 메타데이터 확인의 시작을 보고합니다.  
stretch_table_codegen_completed|늘이기한 테이블에 대한 코드 생성 완료를 보고합니다.  
stretch_table_complete_data_reconciliation|데이터베이스 및 개체의 데이터 조정을 완료합니다.  
stretch_table_data_reconciliation_event|행 일괄 처리의 데이터 조정 완료를 보고합니다.  
stretch_table_data_reconciliation_results_event|여러 행 일괄 처리의 성공적 데이터 조정 완료 또는 오류를 보고합니다.  
stretch_table_hinted_admin_delete_event|관리자 힌트를 사용하는 삭제 DML 작업 실행을 보고합니다.  
stretch_table_hinted_admin_update_event|관리자 힌트를 사용하는 확장 업데이트 DML 작업 실행을 보고합니다.  
stretch_table_provisioning_step_completed|늘어난 테이블 프로비저닝 작업의 기간을 보고합니다.  
stretch_table_query_error|늘이기 쿼리를 다시 쓰는 동안 발생한 오류를 보고합니다.  
stretch_table_remote_creation_completed|늘어난 테이블에 대해 생성된 코드의 원격 실행 완료를 보고합니다.  
stretch_table_row_migration_event|행 일괄 처리의 마이그레이션 완료를 보고합니다.  
stretch_table_row_migration_results_event|여러 행 일괄 처리의 성공적 마이그레이션 완료 또는 오류를 보고합니다.  
stretch_table_row_unmigration_event|행 일괄 처리의 마이그레이션 해제 완료를 보고합니다.  
stretch_table_row_unmigration_results_event|여러 행 일괄 처리의 성공적 마이그레이션 해제 완료 또는 오류를 보고합니다.  
stretch_table_start_data_reconciliation|데이터베이스 및 개체의 데이터 조정을 시작합니다.  
stretch_table_unprovision_completed|늘어나지 않은 테이블에 대한 로컬 리소스 제거 완료를 보고합니다.  
stretch_table_validation_error|사용자가 늘이기를 사용하도록 설정하는 경우 테이블에 대한 유효성 검사 완료를 보고합니다.  
stretch_unprovision_table_start|늘이기 테이블 프로비전 해제 시작을 보고합니다.  
  
## <a name="see-also"></a>참고 항목  
[스트레치 데이터베이스 관리 및 문제 해결](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  

