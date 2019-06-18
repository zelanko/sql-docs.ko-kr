---
title: sys.dm_pdw_dms_workers (Transact-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 96fd36d1710a166285fecba092735c7d2495271e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690450"
---
# <a name="sysdmpdwdmsworkers-transact-sql"></a>sys.dm_pdw_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  DMS 단계를 완료 하는 모든 작업자에 대 한 정보를 보유 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 DMS 작업자의 일부인 쿼리입니다.<br /><br /> request_id, step_index, 및 dms_step_index이이 보기에 대 한 키를 구성합니다.|참조의 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다.|  
|step_index|**int**|이 DMS 작업자의 일부인 단계를 쿼리 합니다.<br /><br /> request_id, step_index, 및 dms_step_index이이 보기에 대 한 키를 구성합니다.|step_index를 참조 하세요 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)합니다.|  
|dms_step_index|**int**|이 작업 자가 실행 되는 DMS 계획의 단계입니다.<br /><br /> request_id, step_index, 및 dms_step_index이이 보기에 대 한 키를 구성합니다.||  
|pdw_node_id|**int**|작업자에서 실행 되는 노드.|에 대 한 node_id를 참조 하세요 [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)합니다.|  
|distribution_id|**정수**|있는 경우에 실행 되는 배포 합니다.|distribution_id를 참조 하세요 [sys.pdw_distributions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)합니다.|  
|유형|**nvarchar(32)**|이 항목을 나타내는 DMS 작업자 스레드의 유형입니다.|'DIRECT_CONVERTER', 'DIRECT_READER', 'FILE_READER', 'HASH_CONVERTER', 'HASH_READER', 'ROUNDROBIN_CONVERTER', 'EXPORT_READER', 'EXTERNAL_READER', 'EXTERNAL_WRITER', 'PARALLEL_COPY_READER', 'REJECT_WRITER', 'WRITER'|  
|상태|**nvarchar(32)**|DMS 작업자의 상태입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|bytes_per_sec|**bigint**|마지막 1 초에서 읽기 또는 쓰기 처리량입니다.|보다 크거나 0입니다. 쿼리 취소 되었거나 작업 자가 실행할 수 전에 실패 하는 경우 NULL입니다.|  
|bytes_processed|**bigint**|이 작업자에 의해 처리 된 총 바이트 수입니다.|보다 크거나 0입니다. 쿼리 취소 되었거나 작업 자가 실행할 수 전에 실패 하는 경우 NULL입니다.|  
|rows_processed|**bigint**|읽거나이 작업자에 대 한 기록 행 수입니다.|보다 크거나 0입니다. 쿼리 취소 되었거나 작업 자가 실행할 수 전에 실패 하는 경우 NULL입니다.|  
|start_time|**datetime**|이 작업 자가 실행 시작 된 시간입니다.|쿼리 단계가의 시작 시간 보다 크거나이 작업자에 속합니다. 참조 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)합니다.|  
|end_time|**datetime**|실행 종료, 실패 또는 취소 된 시간입니다.|진행 중이거나 큐에 대기 중인 작업자에 대 한 NULL입니다. 이 고, 그렇지 start_time 보다 큽니다.|  
|total_elapsed_time|**int**|밀리초 단위로 실행에 소요 된 총 시간입니다.|보다 크거나 0입니다.<br /><br /> 시스템 시작 되거나 다시 시작 이후 경과 된 총 시간입니다. Total_elapsed_time 정수 (밀리초 단위로 24.8 일)에 대 한 최대값을 초과 하는 경우 materialization 오류로 인해 오버플로를 발생 합니다.<br /><br /> 시간 (밀리초)의 최 댓 값 24.8 일 하는 것과 같습니다.|  
|cpu_time|**bigint**|CPU 시간 (밀리초)이이 작업자를 사용 합니다.|보다 크거나 0입니다.|  
|query_time|**int**|SQL 기간 밀리초에서 스레드로 행 반환을 시작 합니다.|보다 크거나 0입니다.|  
|buffers_available|**int**|사용 되지 않는 버퍼 수입니다.| 쿼리 취소 되었거나 작업 자가 실행할 수 전에 실패 하는 경우 NULL입니다.|  
|sql_spid|**int**|이 DMS 작업자에 대 한 작업을 수행 하는 SQL Server 인스턴스에서 세션 id입니다.||  
|dms_cpid|**int**|실행 중인 실제 스레드 프로세스 ID입니다.||  
|error_id|**nvarchar(36)**|있는 경우이 작업자를 실행 하는 동안 발생 한 오류의 고유 식별자입니다.|error_id를 참조 하세요 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)합니다.|  
|source_info|**nvarchar(4000)**|판독기 경우 원본 테이블 및 열 사양입니다.||  
|destination_info|**nvarchar(4000)**|작성기의 경우, 대상 테이블 사양입니다.||  
  
 이 보기에 의해 보존 된 최대 행에 대 한 내용은에서 메타 데이터 섹션을 참조 합니다 [용량 제한](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 항목...  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
