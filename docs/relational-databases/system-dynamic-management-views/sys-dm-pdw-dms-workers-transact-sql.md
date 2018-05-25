---
title: sys.dm_pdw_dms_workers (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0a284d18-3c46-4ffa-bcc9-689e660ee8b4
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 68d4b12395172f8ea5c820e745abf2a3f5f4c7c8
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmpdwdmsworkers-transact-sql"></a>sys.dm_pdw_dms_workers (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  DMS 단계를 완료 하는 모든 작업자에 대 한 정보를 보유 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|이 DMS 작업자의 일부 인지를 쿼리 합니다.<br /><br /> request_id, step_index, 및 dms_step_index이이 보기에 대 한 키를 형성합니다.|참조에서 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다.|  
|step_index|**int**|이 DMS 작업자의 일부인 단계를 쿼리 합니다.<br /><br /> request_id, step_index, 및 dms_step_index이이 보기에 대 한 키를 형성합니다.|step_index 참조 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)합니다.|  
|dms_step_index|**int**|이 작업 자가 실행 되는 DMS 계획의 단계입니다.<br /><br /> request_id, step_index, 및 dms_step_index이이 보기에 대 한 키를 형성합니다.||  
|pdw_node_id|**int**|작업자에서 실행 되는 노드.|참조에 대 한 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)합니다.|  
|distribution_id|**Int**|있는 경우 작업 자가에서 실행 되는 배포 합니다.|distribution_id 참조 [sys.pdw_distributions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)합니다.|  
|유형|**nvarchar(32)**|DMS 작업자 스레드를이 항목의 형식입니다.|'DIRECT_CONVERTER', 'DIRECT_READER', 'FILE_READER', 'HASH_CONVERTER', 'HASH_READER', 'ROUNDROBIN_CONVERTER', 'EXPORT_READER', 'EXTERNAL_READER', 'EXTERNAL_WRITER', 'PARALLEL_COPY_READER', 'REJECT_WRITER', 'WRITER'|  
|상태|**nvarchar(32)**|DMS 작업자의 상태입니다.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|bytes_per_sec|**bigint**|마지막 1 초 동안에서 읽기 또는 쓰기 처리량입니다.|보다 크거나 0입니다. 쿼리 취소 되었거나 작업 자가 실행할 수 전에 실패 하는 경우 NULL입니다.|  
|bytes_processed|**bigint**|이 작업자에 의해 처리 된 총 바이트 수입니다.|보다 크거나 0입니다. 쿼리 취소 되었거나 작업 자가 실행할 수 전에 실패 하는 경우 NULL입니다.|  
|rows_processed|**bigint**|읽거나이 작업자에 대 한 기록 행 수입니다.|보다 크거나 0입니다. 쿼리 취소 되었거나 작업 자가 실행할 수 전에 실패 하는 경우 NULL입니다.|  
|start_time|**datetime**|이 작업자의 실행 시작 시간입니다.|쿼리 단계의 시작 시간 보다 크거나이 작업자에 속해 있습니다. 참조 [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)합니다.|  
|end_time|**datetime**|시간을 실행 종료, 실패 또는 취소 되었습니다.|진행 중이거나 대기 중인 작업자에 대 한 NULL입니다. 그 외, start_time 보다 큽니다.|  
|total_elapsed_time|**int**|실행 시간 (밀리초)에에서 소요 된 총 시간입니다.|보다 크거나 0입니다.<br /><br /> 시스템 시작 또는 다시 시작 이후 경과 하는 총 시간입니다. Total_elapsed_time 정수 (밀리초에서 24.8 일)에 대 한 최대값을 초과 하면 오버플로 materialization 오류로 인해 발생 합니다.<br /><br /> 밀리초의 최대값 24.8 일 하는 것과 같습니다.|  
|cpu_time|**bigint**|밀리초 단위로이 작업자에 사용 된 CPU 시간입니다.|보다 크거나 0입니다.|  
|query_time|**int**|SQL 전에 기간을 밀리초 단위로 스레드에 행을 반환을 시작 합니다.|보다 크거나 0입니다.|  
|buffers_available|**int**|사용 되지 않는 버퍼 수입니다.| 쿼리 취소 되었거나 작업 자가 실행할 수 전에 실패 하는 경우 NULL입니다.|  
|sql_spid|**int**|이 DMS 작업자에 대 한 작업을 수행 하는 SQL Server 인스턴스에 세션 id입니다.||  
|dms_cpid|**int**|실행 하는 실제 스레드에의 프로세스 ID입니다.||  
|error_id|**nvarchar(36)**|있는 경우이 작업 자가 실행 하는 동안 발생 한 오류의 고유 식별자입니다.|참조에서 error_id [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)합니다.|  
|source_info|**nvarchar(4000)**|판독기, 원본 테이블 및 열 사양입니다.||  
|destination_info|**nvarchar(4000)**|에 대 한 기록기 대상 테이블 사양입니다.||  
  
 이 보기에 의해 보존 된 최대 행에 대 한 정보를 참조 하십시오. [최대 시스템 뷰의 값](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
