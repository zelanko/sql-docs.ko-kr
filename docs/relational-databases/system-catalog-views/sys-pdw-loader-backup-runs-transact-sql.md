---
title: sys.pdw_loader_backup_runs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 067a39c807b546bc8364bab05d0423f86407a625
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56014514"
---
# <a name="syspdwloaderbackupruns-transact-sql"></a>sys.pdw_loader_backup_runs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  진행 중인 및 완료 된 백업 및 복원 작업에 대 한 정보가 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], 및 지속적인 및 완료 된 백업, 복원 및 로드 작업에서 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다. 이 정보는 시스템을 다시 시작해도 유지됩니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|특정 백업, 복원 또는 부하 실행에 대 한 고유 식별자입니다.<br /><br /> 이 보기에 대 한 키입니다.||  
|NAME|**nvarchar(255)**|부하에 대 한 null입니다. 백업 또는 복원에 대 한 선택적 이름입니다.||  
|submit_time|**datetime**|요청이 제출 된 시간입니다.||  
|start_time|**datetime**|작업이 시작된 시간입니다.||  
|end_time|**datetime**|작업 완료, 실패 또는 취소 된 시간입니다.||  
|total_elapsed_time|**int**|총 경과 start_time와 현재 시간 또는 start_time 및 end_time 간에 완료, 취소 되었거나 실패 한 실행에 대 한 합니다.|Total_elapsed_time 정수 (밀리초 단위로 24.8 일)에 대 한 최대값을 초과 하는 경우 materialization 오류로 인해 오버플로를 발생 합니다.<br /><br /> 시간 (밀리초)의 최 댓 값 24.8 일 하는 것과 같습니다.|  
|operation_type|**nvarchar(16)**|부하 형식입니다.|'백업', 'LOAD', ' RESTORE'|  
|mode|**nvarchar(16)**|실행된 형식 내에서 사용 되는 모드입니다.|Operation_type = **백업**<br />**차등**<br />**FULL**<br /><br /> Operation_type = **부하**<br />**추가**<br />**RELOAD**<br />**UPSERT**<br /><br /> Operation_type = **복원**<br />**DATABASE**<br />**HEADER_ONLY**|  
|database_name|**nvarchar(255)**|이 작업의 컨텍스트는 데이터베이스의 이름||  
|table_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|작업을 요청 하는 사용자의 ID입니다.||  
|session_id|**nvarchar(32)**|작업을 수행 하는 세션 ID입니다.|Session_id를 참조 하세요 [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)합니다.|  
|request_id|**nvarchar(32)**|작업을 수행 하는 요청의 ID입니다. 로드에 대 한이 부하와 관련 된 현재 또는 마지막 요청입니다...|참조의 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다.|  
|상태|**nvarchar(16)**|실행의 상태입니다.|'CANCELLED','COMPLETED','FAILED','QUEUED','RUNNING'|  
|진행률|**int**|완료 비율입니다.|0에서 100 사이의|  
|command|**nvarchar(4000)**|전체 텍스트는 사용자가 제출한 명령입니다.|(공백을 계산) 4000 자 보다 긴 경우 잘립니다.|  
|rows_processed|**bigint**|이 작업의 일부로 처리 하는 행 수입니다.||  
|rows_rejected|**bigint**|이 작업의 일환으로 거부 하는 행 수입니다.||  
|rows_inserted|**bigint**|이 작업의 일환으로 데이터베이스 테이블에 삽입 된 행의 수입니다.||  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
