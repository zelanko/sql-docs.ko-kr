---
title: sys.dm_pdw_request_steps (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/01/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: dmv's
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: cc563e88-0d34-436e-b914-b60d6ee0d50b
caps.latest.revision: "10"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 846806609d926aef8bfc7f9c15238dfec069727c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwrequeststeps-transact-sql"></a>sys.dm_pdw_request_steps (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  지정된 된 요청을 작성 하거나에 쿼리 하는 모든 단계에 대 한 정보를 보관 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다. 각 쿼리 단계에 대해 행을 나열합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar (32)**|request_id 및 step_index이이 보기에 대 한 키를 구성 합니다.<br /><br /> 이 요청과 관련 된 고유 숫자 id입니다.|참조에서 request_id [sys.dm_pdw_exec_requests &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|request_id 및 step_index이이 보기에 대 한 키를 구성 합니다.<br /><br /> 이 단계의 요청 구성 하는 단계 시퀀스의 위치입니다.|0 (n-1)에 n 단계를 포함 한 요청입니다.|  
|operation_type|**nvarchar(35)**|이 단계에서 나타내는 작업의 형식입니다.|**DMS 쿼리 계획 작업:** 'ReturnOperation', 'PartitionMoveOperation', 'MoveOperation', 'BroadcastMoveOperation', 'ShuffleMoveOperation', 'TrimMoveOperation', 'CopyOperation', 'DistributeReplicatedTableMoveOperation'<br /><br /> **SQL 쿼리 계획 작업:** 'OnOperation', 'RemoteOperation'<br /><br /> **다른 쿼리 계획 작업:** 'MetaDataCreateOperation', 'RandomIDOperation'<br /><br /> **읽기에 대 한 외부 작업:** 'HadoopShuffleOperation', 'HadoopRoundRobinOperation', 'HadoopBroadcastOperation'<br /><br /> **MapReduce에 대 한 외부 작업:** 'HadoopJobOperation', 'HdfsDeleteOperation'<br /><br /> **쓰기 작업에 대해 외부 작업:** 'ExternalExportDistributedOperation', 'ExternalExportReplicatedOperation', 'ExternalExportControlOperation'<br /><br /> 자세한 내용은 "이해 쿼리 계획"의 참조는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.|  
|distribution_type|**nvarchar (32)**|이 단계를 진행 합니다 배포의 유형입니다.|'AllNodes', 'AllDistributions', 'AllComputeNodes', 'ComputeNode', 'Distribution', 'SubsetNodes', '지정 되지 않은' ' SubsetDistributions'|  
|location_type|**nvarchar (32)**|단계가 실행 되는 위치입니다.|' Compute', '제어', 'DMS'|  
|상태|**nvarchar (32)**|이 단계는 상태입니다.|보류 중, 실행 중, 완료, 실패, UndoFailed, PendingCancel, 취소, 실행 취소, 중단|  
|error_id|**nvarchar(36)**|있는 경우이 단계와 관련 된 오류의 고유 id입니다.|참조의 error_id [sys.dm_pdw_errors &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). 오류가 발생 하지 않은 경우 NULL입니다.|  
|start_time|**datetime**|단계는 실행을 시작 시간입니다.|더 작은 또는 현재 시간 및 크거나 end_compile_time이이 단계 속해 있는 쿼리 합니다. 쿼리에 대 한 자세한 내용은 참조 하십시오. [sys.dm_pdw_exec_requests &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|end_time|**datetime**|이 단계 실행을 완료, 취소 되었거나 실패 시간입니다.|더 작은 또는 현재 시간 및 크거나 start_time 합니다. 실행의 현재 단계에 대 한 NULL로 설정 하거나 큐에 대기 합니다.|  
|total_elapsed_time|**int**|총 시간 (밀리초)에는 쿼리 단계 실행입니다.|0 사이의 start_time 및 end_time 간의 차이입니다. 큐에 대기 중인된 단계에 대 한 0입니다.<br /><br /> Total_elapsed_time 정수에 대 한 최대값을 초과 하면 total_elapsed_time 최대 값으로 계속 됩니다. 이 조건에는 "최 댓 값 초과 했습니다." 경고가 생성 됩니다.<br /><br /> 밀리초의 최대값 24.8 일 하는 것과 같습니다.|  
|row_count|**bigint**|총 행 수는 변경 되거나이 요청에서 반환 합니다.|데이터를 반환 하거나 변경 하지 않았는지 여부를 지정 하는 단계에 대 한 0입니다. 그렇지 않으면 영향을 받는 행 수입니다.|  
|command|**nvarchar(4000)**|이 단계의 명령의 전체 텍스트를 포함합니다.|단계에 대해 유효한 요청 문자열입니다. 작업 MetaDataCreateOperation 유형인 경우 NULL입니다. 4000 자 보다 긴 경우 잘립니다.|  
  
 이 보기에 의해 보존 된 최대 행에 대 한 내용은 "최소 및 최대 값에" 최대 시스템 뷰의 값 섹션을 참조는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
