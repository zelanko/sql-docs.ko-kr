---
title: sys.dm_exec_distributed_request_steps (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ec49f2b0db65c57b69e721f569fccfe32e861e8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618461"
---
# <a name="sysdmexecdistributedrequeststeps-transact-sql"></a>sys.dm_exec_distributed_request_steps (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  지정 된 PolyBase 요청 또는 쿼리를 작성 하는 모든 단계에 대 한 정보를 보유 합니다. 쿼리 단계 마다 하나의 행을 나열합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**int**|execution_id 및 step_index이이 보기에 대 한 키를 구성 합니다. 요청과 연결 된 고유 숫자 id입니다.|ID를 참조 하세요 [sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)합니다.|  
|step_index|**int**|요청을 구성 하는 단계의 순서에서이 단계의 위치입니다.|0 (n-1)를 n 단계를 사용 하 여 요청입니다.|  
|operation_type|**nvarchar(128)**|이 단계에서 표시 된 작업의 형식입니다.|'MoveOperation','OnOperation','RandomIDOperation','RemoteOperation','ReturnOperation','ShuffleMoveOperation','TempTablePropertiesOperation','DropDiagnosticsNotifyOperation', ‘HadoopShuffleOperation', ‘HadoopBroadCastOperation', ‘HadoopRoundRobinOperation'|  
|distribution_type|**nvarchar(32)**|위치 단계는 실행 중입니다.|‘AllComputeNodes','AllDistributions','ComputeNode','Distribution','AllNodes','SubsetNodes','SubsetDistributions','Unspecified'.|  
|location_type|**nvarchar(32)**|위치 단계는 실행 중입니다.|'계산', 'Head' 또는 'DMS'. 모든 데이터 이동 단계에는 'DMS' 보여 줍니다.|  
|상태|**nvarchar(32)**|이 단계는 상태|‘Pending', ‘Running', ‘Complete', ‘Failed', ‘UndoFailed', ‘PendingCancel', ‘Cancelled', ‘Undone', ‘Aborted'|  
|error_id|**nvarchar(36)**|있는 경우이 단계와 관련 된 오류의 고유 id|id를 참조 하세요 [sys.dm_exec_compute_node_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)이 고, 오류가 발생 하지 않은 경우 NULL입니다.|  
|start_time|**datetime**|단계 실행 시작 된 시간|더 작은 또는 현재 같음 및 크거나 end_compile_time이이 단계 속해 있는 쿼리.|  
|end_time|**datetime**|이 단계 실행이 완료, 취소 되었거나 실패 한 시간입니다.|더 작은 또는 현재 같음 및 크거나 start_time, 큐에 대기 또는 실행의 현재 단계에 대 한 NULL로 설정 합니다.|  
|total_elapsed_time|**int**|총 쿼리 단계가 실행 된를 밀리초 단위로 시간|0 사이의 start_time 및 end_time 간의 차이입니다. 큐에 대기 중인된 단계에 대 한 0입니다.|  
|row_count|**bigint**|변경 또는이 요청에서 반환한 행의 총 수|변경 하지 않았거나 데이터, 그렇지 않으면 영향을 받는 행 수를 반환 하는 단계에 대 한 0입니다. DMS 단계에 대 한-1로 설정 합니다.|  
|command|nvarchar(4000)|이 단계의 명령의 전체 텍스트를 포함합니다.|단계에 대 한 모든 요청이 유효한 문자열입니다. 4000 자 보다 긴 경우 잘립니다.|  
  
## <a name="see-also"></a>관련 항목  
 [PolyBase 동적 관리 뷰를 사용 하 여 문제 해결](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
