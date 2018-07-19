---
title: sys.dm_pdw_request_steps (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.suite: sql
ms.component: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cc563e88-0d34-436e-b914-b60d6ee0d50b
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5a6fbf843d3a9aca9172a5ab6ea828a0c0b0a40a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38060295"
---
# <a name="sysdmpdwrequeststeps-transact-sql"></a>sys.dm_pdw_request_steps (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  지정된 된 요청을 작성 하거나 쿼리 하는 모든 단계에 대 한 정보를 보유 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]합니다. 쿼리 단계 마다 하나의 행을 나열합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|request_id 및 step_index이이 보기에 대 한 키를 구성 합니다.<br /><br /> 요청과 연결 된 고유 숫자 id입니다.|참조의 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다.|  
|step_index|**int**|request_id 및 step_index이이 보기에 대 한 키를 구성 합니다.<br /><br /> 요청을 구성 하는 단계의 순서에서이 단계의 위치입니다.|0 (n-1)를 n 단계를 사용 하 여 요청입니다.|  
|operation_type|**nvarchar(35)**|이 단계에서 표시 하는 작업의 형식입니다.|**DMS 쿼리 계획 작업:** 'ReturnOperation', 'PartitionMoveOperation', 'MoveOperation', 'BroadcastMoveOperation', 'ShuffleMoveOperation', 'TrimMoveOperation', 'CopyOperation', 'DistributeReplicatedTableMoveOperation'<br /><br /> **SQL 쿼리 계획 작업:** 'OnOperation', 'RemoteOperation'<br /><br /> **다른 쿼리 계획 작업:** 'MetaDataCreateOperation', 'RandomIDOperation'<br /><br /> **읽기에 대 한 외부 작업:** 'HadoopShuffleOperation', 'HadoopRoundRobinOperation', 'HadoopBroadcastOperation'<br /><br /> **MapReduce에 대 한 외부 작업:** 'HadoopJobOperation', 'HdfsDeleteOperation'<br /><br /> **쓰기에 대 한 외부 작업:** 'ExternalExportDistributedOperation', 'ExternalExportReplicatedOperation', 'ExternalExportControlOperation'<br /><br /> 자세한 내용은 "쿼리 계획 이해"에서 참조 된 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.|  
|distribution_type|**nvarchar(32)**|이 단계를 진행 하는 배포의 형식입니다.|'AllNodes', 'AllDistributions', 'AllComputeNodes', 'ComputeNode', 'Distribution', 'SubsetNodes', 'SubsetDistributions', 'Unspecified'|  
|location_type|**nvarchar(32)**|위치 단계는 실행 중입니다.|' 계산 ', 'Control', 'DMS'|  
|상태|**nvarchar(32)**|이 단계의 상태입니다.|보류 중, 실행 중, 완료, 실패, UndoFailed PendingCancel, 취소, 취소, 중단|  
|error_id|**nvarchar(36)**|있는 경우이 단계와 관련 된 오류의 고유 id입니다.|참조의 error_id [sys.dm_pdw_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)합니다. 오류가 발생 하지 않은 경우 NULL입니다.|  
|start_time|**datetime**|단계 실행 시작 된 시간입니다.|더 작은 또는 현재 같음 및 크거나 end_compile_time이이 단계 속해 있는 쿼리. 쿼리에 대 한 자세한 내용은 참조 하세요. [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다.|  
|end_time|**datetime**|이 단계 실행이 완료, 취소 되었거나 실패 한 시간입니다.|더 작은 또는 현재 같음 및 크거나 start_time 합니다. 실행의 현재 단계에 대 한 NULL로 설정 하거나 큐에 대기 합니다.|  
|total_elapsed_time|**int**|총 시간 (밀리초) 쿼리 단계가 실행 합니다.|0 사이의 start_time 및 end_time 간의 차이입니다. 큐에 대기 중인된 단계에 대 한 0입니다.<br /><br /> Total_elapsed_time 정수에 대 한 최대값을 초과 하면 total_elapsed_time 최대 값으로 계속 됩니다. 이 조건이 "최대 값을 초과 했습니다." 경고 생성<br /><br /> 시간 (밀리초)의 최 댓 값 24.8 일 하는 것과 같습니다.|  
|row_count|**bigint**|총 행 변경 하거나이 요청에서 반환 합니다.|변경 하거나 데이터를 반환 하지 않은 단계에 대 한 0입니다. 영향을 받는 행의 수가 고, 그렇지입니다.|  
|command|**nvarchar(4000)**|이 단계의 명령의 전체 텍스트를 포함합니다.|단계에 대 한 모든 요청이 유효한 문자열입니다. 작업 MetaDataCreateOperation 형식의 경우 NULL입니다. 4000 자 보다 긴 경우 잘립니다.|  
  
 이 보기에 의해 보존 된 최대 행에 대 한 내용은의 "최소 및 최대 값" 최대 시스템 뷰의 값 섹션을 참조 합니다 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
