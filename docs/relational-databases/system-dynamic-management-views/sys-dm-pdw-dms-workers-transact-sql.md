---
title: sys. dm_pdw_dms_workers (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0a284d18-3c46-4ffa-bcc9-689e660ee8b4
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6e5f295637db0e138caf324e3126707b9e0ea774
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67899497"
---
# <a name="sysdm_pdw_dms_workers-transact-sql"></a>sys. dm_pdw_dms_workers (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  DMS 단계를 완료 하는 모든 작업자에 대 한 정보를 저장 합니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 DMS 작업자를 포함 하는 쿼리입니다.<br /><br /> 이 보기의 키를 request_id, step_index 및 dms_step_index 구성 합니다.|[Dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)에서 request_id를 참조 하세요.|  
|step_index|**int**|이 DMS 작업자의 일부인 쿼리 단계입니다.<br /><br /> 이 보기의 키를 request_id, step_index 및 dms_step_index 구성 합니다.|[Dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)에서 step_index를 참조 하세요.|  
|dms_step_index|**int**|이 작업자를 실행 하는 DMS 계획의 단계입니다.<br /><br /> 이 보기의 키를 request_id, step_index 및 dms_step_index 구성 합니다.||  
|pdw_node_id|**int**|Worker가 실행 되는 노드입니다.|[Dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)에서 node_id를 참조 하세요.|  
|distribution_id|**정수**|작업자 (있는 경우)가 실행 되 고 있는 배포입니다.|[Pdw_distributions &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)에서 distribution_id를 참조 하세요.|  
|형식(type)|**nvarchar(32)**|이 항목이 나타내는 DMS 작업자 스레드의 형식입니다.|' DIRECT_CONVERTER ', ' DIRECT_READER ', ' FILE_READER ', ' HASH_CONVERTER ', ' HASH_READER ', ' ROUNDROBIN_CONVERTER ', ' EXPORT_READER ', ' EXTERNAL_READER ', ' EXTERNAL_WRITER ', ' PARALLEL_COPY_READER ', ' REJECT_WRITER ', ' WRITER '|  
|상태|**nvarchar(32)**|DMS 작업자의 상태입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|bytes_per_sec|**bigint**|마지막 1 초 동안 읽기 또는 쓰기 처리량입니다.|0 보다 크거나 같습니다. Worker가 실행 되기 전에 쿼리가 취소 되거나 실패 한 경우 NULL입니다.|  
|bytes_processed|**bigint**|이 작업자에서 처리 한 총 바이트 수입니다.|0 보다 크거나 같습니다. Worker가 실행 되기 전에 쿼리가 취소 되거나 실패 한 경우 NULL입니다.|  
|rows_processed|**bigint**|이 작업자에 대해 읽거나 쓴 행 수입니다.|0 보다 크거나 같습니다. Worker가 실행 되기 전에 쿼리가 취소 되거나 실패 한 경우 NULL입니다.|  
|start_time|**datetime**|이 작업자의 실행이 시작 된 시간입니다.|이 작업자가 속한 쿼리 단계의 시작 시간 보다 크거나 같습니다. [Dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)을 참조 하십시오.|  
|end_time|**datetime**|실행이 종료, 실패 또는 취소 된 시간입니다.|진행 중이거나 지연 된 작업자의 경우 NULL입니다. 그렇지 않으면 start_time 보다 큽니다.|  
|total_elapsed_time|**int**|실행에 소요 된 총 시간 (밀리초)입니다.|0 보다 크거나 같습니다.<br /><br /> 시스템을 시작 하거나 다시 시작한 이후 경과 된 총 시간입니다. Total_elapsed_time 정수 24.8 (밀리초)의 최대값을 초과 하는 경우 오버플로로 인 한 구체화 실패가 발생 합니다.<br /><br /> 최대 값 (밀리초)은 24.8 일에 해당 합니다.|  
|cpu_time|**bigint**|이 작업자에 사용 된 CPU 시간 (밀리초)입니다.|0 보다 크거나 같습니다.|  
|query_time|**int**|SQL에서 스레드에 행 반환을 시작 하기 전 까지의 시간 (밀리초)입니다.|0 보다 크거나 같습니다.|  
|buffers_available|**int**|사용 하지 않는 버퍼 수입니다.| Worker가 실행 되기 전에 쿼리가 취소 되거나 실패 한 경우 NULL입니다.|  
|sql_spid|**int**|이 DMS 작업자에 대해 작업을 수행 하는 SQL Server 인스턴스의 세션 id입니다.||  
|dms_cpid|**int**|실행 중인 실제 스레드의 프로세스 ID입니다.||  
|error_id|**nvarchar (36)**|이 작업자를 실행 하는 동안 발생 한 오류의 고유 식별자입니다 (있는 경우).|[Dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)에서 error_id를 참조 하세요.|  
|source_info|**nvarchar(4000)**|판독기의 경우 원본 테이블 및 열을 지정 합니다.||  
|destination_info|**nvarchar(4000)**|작성기의 경우 대상 테이블의 사양입니다.||  
  
 이 뷰에서 유지 되는 최대 행에 대 한 자세한 내용은 [용량 제한](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 항목에서 메타 데이터 섹션을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
