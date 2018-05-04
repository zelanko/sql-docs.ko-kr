---
title: sys.pdw_loader_backup_runs (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5bc01ddf16335530f8ad5984e6194874d0a1980c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="syspdwloaderbackupruns-transact-sql"></a>sys.pdw_loader_backup_runs (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  진행 중인 시간 및 완료 된 백업 및 복원 작업에 대 한 정보가 들어 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], 및 지속적인 시간 및 완료 된 백업, 복원 및 로드 작업에서 하는 방법에 대 한 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다. 이 정보는 시스템을 다시 시작해도 유지됩니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|특정 백업, 복원 또는 부하 실행에 대 한 고유 식별자입니다.<br /><br /> 이 보기에 대 한 키입니다.||  
|name|**nvarchar(255)**|부하에 대 한 null입니다. 백업 또는 복원에 대 한 선택적 이름입니다.||  
|submit_time|**datetime**|요청이 제출 된 시간입니다.||  
|start_time|**datetime**|작업이 시작된 시간입니다.||  
|end_time|**datetime**|시간 작업 완료, 실패 또는 취소 되었습니다.||  
|total_elapsed_time|**int**|경과 된 총 시간 start_time 및 end_time 간이나 start_time 및 현재 시간 사이의 완료, 취소 됨 또는 실패 상태로 실행 됩니다.|Total_elapsed_time 정수 (밀리초에서 24.8 일)에 대 한 최대값을 초과 하면 오버플로 materialization 오류로 인해 발생 합니다.<br /><br /> 밀리초의 최대값 24.8 일 하는 것과 같습니다.|  
|operation_type|**nvarchar(16)**|부하 유형입니다.|' 백업 ', '로드', 'RESTORE'|  
|mode|**nvarchar(16)**|실행된 형식 내에서 사용 되는 모드입니다.|Operation_type = **백업**<br />**차등**<br />**FULL**<br /><br /> Operation_type = **부하**<br />**추가**<br />**다시 로드**<br />**UPSERT**<br /><br /> Operation_type = **복원**<br />**DATABASE**<br />**HEADER_ONLY**|  
|database_name|**nvarchar(255)**|이 작업의 컨텍스트는 데이터베이스의 이름||  
|table_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|작업을 요청 하는 사용자의 ID입니다.||  
|session_id|**nvarchar(32)**|작업을 수행 하는 세션의 ID입니다.|세션 id를 참조 하십시오. [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)합니다.|  
|request_id|**nvarchar(32)**|작업을 수행 하는 요청의 ID입니다. 로드에 대 한이 부하와 관련 된 현재 또는 마지막 요청입니다.|참조에서 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)합니다.|  
|상태|**nvarchar(16)**|실행의 상태입니다.|'취소',' 완료 ', '실패', '대기', '실행 중|  
|진행 중|**int**|완료율입니다.|0에서 100|  
|command|**nvarchar(4000)**|전체 텍스트 사용자가 제출한 명령입니다.|한 (개 공백) 4000 자 보다 긴 경우 잘립니다.|  
|rows_processed|**bigint**|이 작업의 일부로 처리 된 행의 수입니다.||  
|rows_rejected|**bigint**|이 작업의 일환으로 거부 하는 행 수입니다.||  
|rows_inserted|**bigint**|이 작업의 일환으로 데이터베이스 테이블에 삽입 된 행 수입니다.||  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
