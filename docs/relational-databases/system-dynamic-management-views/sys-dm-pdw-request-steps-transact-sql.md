---
title: sys. dm_pdw_request_steps (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cc563e88-0d34-436e-b914-b60d6ee0d50b
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 260b822d111f94fc567704cd908cb5632e3bdcaf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73240778"
---
# <a name="sysdm_pdw_request_steps-transact-sql"></a>sys. dm_pdw_request_steps (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  에서 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]지정 된 요청 또는 쿼리를 구성 하는 모든 단계에 대 한 정보를 저장 합니다. 쿼리 단계 별로 하나의 행을 나열 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar (32)**|request_id 및 step_index이 보기에 대 한 키를 구성 합니다.<br /><br /> 요청과 연결 된 고유 숫자 id입니다.|[Dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)에서 request_id를 참조 하세요.|  
|step_index|**int**|request_id 및 step_index이 보기에 대 한 키를 구성 합니다.<br /><br /> 요청을 구성 하는 단계 시퀀스에서이 단계를 수행 하는 위치입니다.|n 단계가 포함 된 요청의 경우 0 ~ (n-1)입니다.|  
|operation_type|**nvarchar (35)**|이 단계가 나타내는 작업의 유형입니다.|**DMS 쿼리 계획 작업:** ' ReturnOperation ', ' 파티션 Moveoperation ', ' MoveOperation ', ' BroadcastMoveOperation ', ' ShuffleMoveOperation ', ' TrimMoveOperation ', ' CopyOperation ', ' DistributeReplicatedTableMoveOperation '<br /><br /> **SQL 쿼리 계획 작업:** ' OnOperation ', ' RemoteOperation '<br /><br /> **다른 쿼리 계획 작업:** 'MetaDataCreateOperation', 'RandomIDOperation'<br /><br /> **읽기의 외부 작업:** 'HadoopShuffleOperation', 'HadoopRoundRobinOperation', 'HadoopBroadcastOperation'<br /><br /> **MapReduce에 대 한 외부 작업:** 'HadoopJobOperation', 'HdfsDeleteOperation'<br /><br /> **쓰기에 대 한 외부 작업:** 'ExternalExportDistributedOperation', 'ExternalExportReplicatedOperation', 'ExternalExportControlOperation'<br /><br /> 자세한 내용은에서 "쿼리 계획 이해"를 참조 하십시오 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]. <br /><br />  또한 데이터베이스 설정에 따라 쿼리 계획이 영향을 받을 수 있습니다.  자세한 내용은 [ALTER DATABASE SET 옵션](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-set-options?toc=/azure/sql-data-warehouse/toc.json&bc=/azure/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest) 을 확인 하세요.|  
|distribution_type|**nvarchar (32)**|배포 유형이 단계를 수행 합니다.|' AllNodes ', ' AllDistributions ', ' AllComputeNodes ', ' ComputeNode ', ' 분포 ', ' SubsetNodes ', ' SubsetDistributions ', ' 지정 되지 않음 '|  
|location_type|**nvarchar (32)**|단계가 실행 되는 위치입니다.|' Compute ', ' Control ', ' DMS '|  
|상태|**nvarchar (32)**|이 단계의 상태입니다.|보류 중, 실행 중, 완료, 실패, 작업 취소 실패, PendingCancel, 취소 됨, 취소 됨, 중단 됨|  
|error_id|**nvarchar (36)**|이 단계와 연결 된 오류의 고유 id입니다 (있는 경우).|[Transact-sql&#41;&#40;dm_pdw_errors ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)error_id을 참조 하세요. 오류가 발생 하지 않은 경우 NULL입니다.|  
|start_time|**datetime**|단계가 실행을 시작한 시간입니다.|현재 시간 보다 작거나 같고이 단계가 속한 쿼리의 end_compile_time 보다 크거나 같습니다. 쿼리에 대 한 자세한 내용은 [dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)을 참조 하십시오.|  
|end_time|**datetime**|이 단계가 실행을 완료 하거나 취소 했거나 실패 한 시간입니다.|현재 시간 보다 작거나 같고 start_time 보다 크거나 같습니다. 현재 실행 중이거나 큐에 대기 중인 단계에 대해서는 NULL로 설정 합니다.|  
|total_elapsed_time|**int**|쿼리 단계가 실행 된 총 시간 (밀리초)입니다.|0과 start_time 사이의 차이를 end_time 합니다. 대기 단계에 대해 0입니다.<br /><br /> Total_elapsed_time 정수에 대 한 최대값을 초과 하는 경우 total_elapsed_time는 최대 값으로 계속 됩니다. 이 경우 "최 댓 값이 초과 되었습니다." 라는 경고가 생성 됩니다.<br /><br /> 최대 값 (밀리초)은 24.8 일에 해당 합니다.|  
|row_count|**bigint**|이 요청에서 변경 되거나 반환 된 총 행 수입니다.|데이터를 변경 하거나 반환 하지 않은 단계의 경우 0입니다. 그렇지 않으면 영향을 받는 행의 수입니다.|  
|command|**nvarchar(4000)**|이 단계의 명령에 대 한 전체 텍스트를 포함 합니다.|단계에 대 한 유효한 모든 요청 문자열입니다. 작업이 MetaDataCreateOperation 형식인 경우 NULL입니다. 4000 자 보다 길면 잘립니다.|  
  
 이 뷰에서 유지 되는 최대 행에 대 한 자세한 내용은의 "최소 및 최대 값"의 최대 시스템 뷰 값 섹션을 참조 하십시오 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
