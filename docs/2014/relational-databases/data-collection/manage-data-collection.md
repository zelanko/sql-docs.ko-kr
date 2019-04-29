---
title: 데이터 컬렉션 관리 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collection [SQL Server]
- data collector [SQL Server], Transact-SQL
- data collector [SQL Server], SQL Server Management Studio
ms.assetid: bc137daa-9f37-4c01-9766-8b7350c75af8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 543f972f5c5805bb1508b6a256f7a7ed3a2aaa3b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62918595"
---
# <a name="manage-data-collection"></a>데이터 컬렉션 관리
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저 및 함수를 사용하여 데이터 컬렉션 활성화 또는 비활성화, 컬렉션 집합 구성 변경, 관리 데이터 웨어하우스에서 데이터 보기와 같은 데이터 컬렉션의 다양한 기능을 관리할 수 있습니다.  
  
## <a name="manage-data-collection-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 데이터 컬렉션 관리  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 사용하여 다음과 같은 데이터 수집기 관련 태스크를 수행할 수 있습니다.  
  
-   [관리 데이터 웨어하우스 구성&#40;SQL Server Management Studio&#41;](configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
-   [데이터 수집기의 속성 구성](configure-properties-of-a-data-collector.md)  
  
-   [데이터 컬렉션 설정 또는 해제](data-collection.md)  
  
-   [컬렉션 집합 시작 또는 중지](start-or-stop-a-collection-set.md)  
  
-   [SQL Server Profiler를 사용하여 SQL 추적 컬렉션 집합 만들기&#40;SQL Server Management Studio&#41;](use-sql-server-profiler-to-create-a-sql-trace-collection-set.md)  
  
-   [컬렉션 집합 로그 보기&#40;SQL Server Management Studio&#41;](view-collection-set-logs-sql-server-management-studio.md)  
  
-   [컬렉션 집합 일정 보기 또는 변경&#40;SQL Server Management Studio&#41;](view-or-change-collection-set-schedules-sql-server-management-studio.md)  
  
-   [컬렉션 집합 보고서 보기&#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)  
  
## <a name="manage-data-collection-by-using-transact-sql"></a>Transact-SQL을 사용하여 데이터 컬렉션 관리  
 데이터 수집기는 데이터 수집기 관련 태스크를 수행하는 데 사용할 수 있는 광범위한 저장 프로시저 컬렉션을 제공합니다. 예를 들어 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 다음과 같은 태스크를 수행할 수 있습니다.  
  
-   [데이터 컬렉션 매개 변수 구성&#40;Transact-SQL&#41;](configure-data-collection-parameters-transact-sql.md)  
  
-   [데이터 컬렉션 설정 또는 해제](data-collection.md)  
  
-   [컬렉션 집합 시작 또는 중지](start-or-stop-a-collection-set.md)  
  
-   [일반 T-SQL 쿼리 수집기 유형을 사용하는 사용자 지정 컬렉션 집합 만들기&#40;Transact-SQL&#41;](create-custom-collection-set-generic-t-sql-query-collector-type.md)  
  
-   [컬렉션 집합에 컬렉션 항목 추가&#40;Transact-SQL&#41;](add-a-collection-item-to-a-collection-set-transact-sql.md)  
  
 또한 msdb 및 관리 데이터 웨어하우스 데이터베이스에 대한 구성 데이터, 실행 로그 데이터 및 관리 데이터 웨어하우스에 저장된 데이터를 가져오는 데 사용할 수 있는 함수 및 뷰도 제공합니다.  
  
 사용자만의 종단 간 데이터 컬렉션 시나리오를 만들 수 있도록 제공되는 저장 프로시저, 함수 및 뷰를 사용할 수 있습니다.  
  
> [!IMPORTANT]  
>  일반적인 저장 프로시저와 달리 데이터 수집기 저장 프로시저는 정확하게 입력된 매개 변수를 사용하며 데이터 형식 자동 변환을 지원하지 않습니다. 이러한 매개 변수를 인수 설명에 지정된 올바른 입력 매개 변수 데이터 형식으로 호출하지 않으면 저장 프로시저가 오류를 반환합니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 제공된 코드 예제를 만들고 실행할 수 있습니다. 자세한 내용은 [개체 탐색기](../../ssms/object/object-explorer.md)를 참조하세요. 임의의 편집기에서 쿼리를 만들어 이를 확장명이 .sql인 텍스트 파일에 저장할 수도 있습니다. Windows 명령 프롬프트에서 `sqlcmd` 유틸리티를 사용하여 쿼리를 실행할 수 있습니다. 자세한 내용은 [sqlcmd 유틸리티 사용](../scripting/sqlcmd-use-the-utility.md)을 참조하세요.  
  
### <a name="stored-procedures-and-views"></a>저장 프로시저 및 뷰  
 **데이터 수집기 작업**  
  
 다음 표에서는 데이터 수집기 작업에 사용할 수 있는 저장 프로시저에 대해 설명합니다.  
  
|프로시저 이름|Description|  
|--------------------|-----------------|  
|[sp_syscollector_enable_collector](/sql/relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql)|데이터 수집기를 활성화합니다.|  
|[sp_syscollector_disable_collector](/sql/relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql)|데이터 수집기를 비활성화합니다.|  
  
 **컬렉션 집합 작업**  
  
 다음 표에서는 컬렉션 집합 작업에 사용할 수 있는 저장 프로시저에 대해 설명합니다.  
  
|프로시저 이름|Description|  
|--------------------|-----------------|  
|[sp_syscollector_run_collection_set&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql)|요청 시 컬렉션 집합을 실행합니다.|  
|[sp_syscollector_start_collection_set&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql)|컬렉션 집합을 시작합니다.|  
|[sp_syscollector_stop_collection_set&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql)|컬렉션 집합을 중지합니다.|  
|[sp_syscollector_create_collection_set&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql)|컬렉션 집합을 만듭니다.|  
|[sp_syscollector_delete_collection_set&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-collection-set-transact-sql)|컬렉션 집합을 삭제합니다.|  
|[sp_syscollector_update_collection_set&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-update-collection-set-transact-sql)|컬렉션 집합 구성을 변경합니다.|  
|[sp_syscollector_upload_collection_set&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-upload-collection-set-transact-sql)|컬렉션 집합 데이터를 관리 데이터 웨어하우스에 업로드합니다. 이는 사실상 요청 시 업로드입니다.|  
  
 **컬렉션 항목 작업**  
  
 다음 표에서는 컬렉션 집합 항목에 사용할 수 있는 저장 프로시저에 대해 설명합니다.  
  
|프로시저 이름|Description|  
|--------------------|-----------------|  
|[sp_syscollector_create_collection_item&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql)|컬렉션 항목을 만듭니다.|  
|[sp_syscollector_delete_collection_item&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql)|컬렉션 항목을 삭제합니다.|  
|[sp_syscollector_update_collection_item&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql)|컬렉션 항목을 업데이트합니다.|  
  
 **수집기 유형 작업**  
  
 다음 표에서는 수집기 유형 작업에 사용할 수 있는 저장 프로시저에 대해 설명합니다.  
  
|프로시저 이름|Description|  
|--------------------|-----------------|  
|[sp_syscollector_create_collector_type&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-create-collector-type-transact-sql)|수집기 유형을 만듭니다.|  
|[sp_syscollector_update_collector_type&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-update-collector-type-transact-sql)|수집기 유형을 업데이트합니다.|  
|[sp_syscollector_delete_collector_type&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-collector-type-transact-sql)|수집기 유형을 삭제합니다.|  
  
 **구성 정보 가져오기**  
  
 다음 표에서는 구성 정보와 실행 로그 데이터를 가져오는 데 사용할 수 있는 뷰에 대해 설명합니다.  
  
|뷰 이름|Description|  
|---------------|-----------------|  
|[syscollector_config_store&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syscollector-config-store-transact-sql)|데이터 수집기 구성을 가져옵니다.|  
|[syscollector_collection_items&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syscollector-collection-items-transact-sql)|컬렉션 항목 정보를 가져옵니다.|  
|[syscollector_collection_sets&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql)|컬렉션 집합 정보를 가져옵니다.|  
|[syscollector_collector_types&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syscollector-collector-types-transact-sql)|수집기 유형 정보를 가져옵니다.|  
|[syscollector_execution_log&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syscollector-execution-log-transact-sql)|컬렉션 집합 및 패키지 실행에 대한 정보를 가져옵니다.|  
|[syscollector_execution_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql)|태스크 실행에 대한 정보를 가져옵니다.|  
|[syscollector_execution_log_full&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql)|실행 로그가 꽉 찬 경우 정보를 가져옵니다.|  
  
 **관리 데이터 웨어하우스에 대한 액세스 구성**  
  
 다음 표에서는 관리 데이터 웨어하우스에 대한 액세스를 구성하는 데 사용할 수 있는 저장 프로시저에 대해 설명합니다.  
  
|프로시저 이름|Description|  
|--------------------|-----------------|  
|[sp_syscollector_set_warehouse_database_name&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql)|관리 데이터 웨어하우스에 대한 연결 문자열에 정의된 데이터베이스 이름을 지정합니다.|  
|[sp_syscollector_set_warehouse_instance_name&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql)|관리 데이터 웨어하우스에 대한 연결 문자열에 정의된 인스턴스를 지정합니다.|  
  
 **관리 데이터 웨어하우스 구성**  
  
 다음 표에서는 관리 데이터 웨어하우스 구성 작업에 사용할 수 있는 저장 프로시저에 대해 설명합니다.  
  
|프로시저 이름|Description|  
|--------------------|-----------------|  
|[core.sp_create_snapshot&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-create-snapshot-transact-sql)|관리 데이터 웨어하우스에 컬렉션 스냅숏을 만듭니다.|  
|[core.sp_update_data_source&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-update-data-source-transact-sql)|데이터 컬렉션의 데이터 원본을 업데이트합니다.|  
|[core.sp_add_collector_type&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-add-collector-type-transact-sql)|관리 데이터 웨어하우스에 수집기 유형을 추가합니다.|  
|[core.sp_remove_collector_type&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-remove-collector-type-transact-sql)|관리 데이터 웨어하우스에서 수집기 유형을 제거합니다.|  
|[core.sp_purge_data&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-purge-data-transact-sql)|관리 데이터 웨어하우스에서 데이터를 삭제합니다.|  
  
 **업로드 패키지 작업**  
  
 다음 표에서는 업로드 패키지에 사용할 수 있는 저장 프로시저에 대해 설명합니다.  
  
|프로시저 이름|Description|  
|--------------------|-----------------|  
|[sp_syscollector_set_cache_window&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql)|데이터 업로드 다시 시도 횟수를 구성합니다.|  
|[sp_syscollector_set_cache_directory&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql)|업로드 다시 시도 사이에 데이터를 저장할 임시 스토리지를 지정합니다.|  
  
 **데이터 컬렉션 실행 로그 작업**  
  
 다음 표에서는 데이터 컬렉션 실행 로그 작업에 사용할 수 있는 저장 프로시저에 대해 설명합니다.  
  
|프로시저 이름|Description|  
|--------------------|-----------------|  
|[sp_syscollector_delete_execution_log_tree&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-execution-log-tree-transact-sql)|실행 로그에서 컬렉션 집합 항목을 삭제합니다.|  
  
### <a name="functions"></a>함수  
 다음 표에서는 실행 및 정보 추적에 사용할 수 있는 함수에 대해 설명합니다.  
  
|함수 이름|Description|  
|-------------------|-----------------|  
|[fn_syscollector_get_execution_details&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql)|특정 패키지에 대한 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 실행 로그 데이터를 가져옵니다.|  
|[fn_syscollector_get_execution_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/fn-syscollector-get-execution-stats-transact-sql)|컬렉션 집합 또는 패키지에 대한 실행 통계를 가져옵니다. 이 정보에는 기록된 오류가 포함됩니다.|  
|[snapshots.fn_trace_getdata&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/snapshots-fn-trace-getdata-transact-sql)|일반 SQL 추적 수집기 유형을 사용하여 데이터를 수집할 때 기록된 이벤트를 가져옵니다.|  
  
## <a name="see-also"></a>관련 항목  
 [저장 프로시저 실행](../stored-procedures/execute-a-stored-procedure.md)   
 [SQL Server Management Studio 사용](../../database-engine/use-sql-server-management-studio.md)   
 [데이터 컬렉션](data-collection.md)  
  
  
