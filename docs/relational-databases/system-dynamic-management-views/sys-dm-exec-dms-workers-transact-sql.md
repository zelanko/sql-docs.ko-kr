---
description: sys. dm_exec_dms_workers (Transact-sql)
title: sys. dm_exec_dms_workers (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_dms_workers management view
- sys.dm_exec_dms_workers management view
ms.assetid: f468da29-78c3-4f10-8a3c-17905bbf46f2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 677ad00bd29d3f689c1722e1fc1abd65374426a5
ms.sourcegitcommit: c4d6804bde7eaf72d9233d6d43f77d77d1b17c4e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2020
ms.locfileid: "91624780"
---
# <a name="sysdm_exec_dms_workers-transact-sql"></a>sys. dm_exec_dms_workers (Transact-sql)
[!INCLUDE [sqlserver2016-asa-pdw](../../includes/applies-to-version/sqlserver2016-asa-pdw.md)]

  DMS 단계를 완료 하는 모든 작업자에 대 한 정보를 저장 합니다.  
  
 이 보기는 최근 1000 요청 및 활성 요청에 대 한 데이터를 표시 합니다. 활성 요청은 항상이 뷰에 있는 데이터를 가집니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|`nvarchar(32)`|이 DMS 작업자를 포함 하는 쿼리입니다. <br /><br /> 이 보기의 키를 execution_id, step_index 및 dms_step_index 구성 합니다.||  
|step_index|`int`|이 DMS 작업자의 일부인 쿼리 단계입니다.|[Dm_exec_distributed_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)에서 단계 인덱스를 참조 하십시오.|  
|dms_step_index|`int`|이 작업자를 실행 하는 DMS 계획의 단계입니다.|[Dm_exec_dms_workers (transact-sql)을](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md) 참조 하세요.|  
|compute_node_id|`int`|Worker가 실행 되는 노드입니다.|[Dm_exec_compute_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)을 참조 하십시오.|  
|distribution_id|`int`|||  
|형식|`nvarchar(32)`|이 항목이 나타내는 DMS 작업자 스레드의 형식입니다.|' DIRECT_CONVERTER ', ' DIRECT_READER ', ' FILE_READER ', ' HASH_CONVERTER ', ' HASH_READER ', ' ROUNDROBIN_CONVERTER ', ' EXPORT_READER ', ' EXTERNAL_READER ', ' EXTERNAL_WRITER ', ' PARALLEL_COPY_READER ', ' REJECT_WRITER ', ' WRITER '|  
|상태|`nvarchar(32)`|이 단계의 상태|' Pending ', ' Running ', ' Complete ', ' Failed ', ' 작업 취소 실패 ', ' PendingCancel ', ' 취소 됨 ', ' 실행 취소 됨 ', ' 중단 됨 '|  
|bytes_per_sec|`bigint`|||  
|bytes_processed|`bigint`|||  
|rows_processed|`bigint`|||  
|start_time|`datetime`|단계가 실행을 시작한 시간입니다.|현재 시간 보다 작거나 같고이 단계가 속한 쿼리의 end_compile_time 보다 크거나 같습니다.|  
|end_time|`datetime`|이 단계가 실행을 완료 하거나 취소 했거나 실패 한 시간입니다.|현재 시간 보다 작거나 같고 start_time 보다 크거나 같은 경우 현재 실행 중이거나 큐에 대기 중인 단계에 대해 NULL로 설정 합니다.|  
|total_elapsed_time|`int`|쿼리 단계가 실행 된 총 시간 (밀리초)입니다.|0과 start_time 사이의 차이를 end_time 합니다. 대기 단계에 대해 0입니다.|  
|cpu_time|`bigint`|||  
|query_time|`int`|||  
|buffers_available|`int`|||  
|dms_cpid|`int`|||  
|sql_spid|`int`|||  
|error_id|`nvarchar(36)`|||  
|source_info|`nvarchar(4000)`|||  
|destination_info|`nvarchar(4000)`|||  
|명령을 사용합니다.|`nvarchar(4000)`|||
|compute_pool_id|`int`|풀에 대 한 고유 식별자입니다.|

## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰를 사용한 PolyBase 문제 해결](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
