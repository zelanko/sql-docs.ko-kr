---
description: sys.dm_exec_distributed_request_steps (Transact-sql)
title: sys.dm_exec_distributed_request_steps (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_distributed_request_steps
- sys.dm_exec_distributed_request_steps management view
ms.assetid: 1954541d-b716-4e03-8fcc-7022f428e01d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2edc50544c6a21b385544dd487f5202990ef331c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97411200"
---
# <a name="sysdm_exec_distributed_request_steps-transact-sql"></a>sys.dm_exec_distributed_request_steps (Transact-sql)
[!INCLUDE [sqlserver2016-asa-pdw](../../includes/applies-to-version/sqlserver2016-asa-pdw.md)]

  지정 된 PolyBase 요청 또는 쿼리를 구성 하는 모든 단계에 대 한 정보를 저장 합니다. 쿼리 단계 별로 하나의 행을 나열 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**int**|execution_id 및 step_index이 보기에 대 한 키를 구성 합니다. 요청과 연결 된 고유 숫자 id입니다.|[Sys.dm_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)에서 ID를 참조 하세요.|  
|step_index|**int**|요청을 구성 하는 단계 시퀀스에서이 단계를 수행 하는 위치입니다.|n 단계가 포함 된 요청의 경우 0 ~ (n-1)입니다.|  
|operation_type|**nvarchar(128)**|이 단계가 나타내는 작업의 유형입니다.|' MoveOperation ', ' OnOperation ', ' RandomIDOperation ', ' RemoteOperation ', ' ReturnOperation ', ' ShuffleMoveOperation ', ' Temptable Operation ', ' DropDiagnosticsNotifyOperation ', ' HadoopShuffleOperation ', ' HadoopBroadCastOperation ', ' HadoopRoundRobinOperation '|  
|distribution_type|**nvarchar(32)**|단계가 실행 되는 위치입니다.|' AllComputeNodes ', ' AllDistributions ', ' ComputeNode ', ' 분포 ', ' AllNodes ', ' SubsetNodes ', ' SubsetDistributions ', ' 지정 되지 않음 '.|  
|location_type|**nvarchar(32)**|단계가 실행 되는 위치입니다.|' Compute ', ' Head ' 또는 ' DMS '입니다. 모든 데이터 이동 단계는 ' DMS '를 표시 합니다.|  
|상태|**nvarchar(32)**|이 단계의 상태|' Pending ', ' Running ', ' Complete ', ' Failed ', ' 작업 취소 실패 ', ' PendingCancel ', ' 취소 됨 ', ' 실행 취소 됨 ', ' 중단 됨 '|  
|error_id|**nvarchar (36)**|이 단계와 연결 된 오류의 고유 id입니다 (있는 경우).|[Sys.dm_exec_compute_node_errors id &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)를 참조 하세요. 오류가 발생 하지 않은 경우 NULL입니다.|  
|start_time|**datetime**|단계가 실행을 시작한 시간입니다.|현재 시간 보다 작거나 같고이 단계가 속한 쿼리의 end_compile_time 보다 크거나 같습니다.|  
|end_time|**datetime**|이 단계가 실행을 완료 하거나 취소 했거나 실패 한 시간입니다.|현재 시간 보다 작거나 같고 start_time 보다 크거나 같은 경우 현재 실행 중이거나 큐에 대기 중인 단계에 대해 NULL로 설정 합니다.|  
|total_elapsed_time|**int**|쿼리 단계가 실행 된 총 시간 (밀리초)입니다.|0과 start_time 사이의 차이를 end_time 합니다. 대기 단계에 대해 0입니다.|  
|row_count|**bigint**|이 요청에서 변경 되거나 반환 된 총 행 수입니다.|0은 데이터를 변경 하거나 반환 하지 않은 단계의 경우에는 그렇지 않은 경우 영향을 받는 행 수입니다. DMS 단계에 대해-1로 설정 합니다.|  
|명령을 사용합니다.|nvarchar(4000)|이 단계의 명령에 대 한 전체 텍스트를 포함 합니다.|단계에 대 한 유효한 모든 요청 문자열입니다. 4000 자 보다 길면 잘립니다.|  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰를 사용한 PolyBase 문제 해결](/previous-versions/sql/sql-server-2016/mt146389(v=sql.130))   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
