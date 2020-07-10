---
title: sys. pdw_loader_backup_runs (Transact-sql) | Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6ca5fc44e34153411e32a890b509d86caacbd9db
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196989"
---
# <a name="syspdw_loader_backup_runs-transact-sql"></a>sys. pdw_loader_backup_runs (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  에서 진행 중이 고 완료 된 백업 및 복원 작업과의 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 지속적인 백업, 복원 및 로드 작업에 대 한 정보를 포함 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 합니다. 이 정보는 시스템을 다시 시작해도 유지됩니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|특정 백업, 복원 또는 로드 실행에 대 한 고유 식별자입니다.<br /><br /> 이 보기의 키입니다.||  
|이름|**nvarchar(255)**|로드의 경우 Null입니다. 백업 또는 복원에 대 한 선택적 이름입니다.||  
|submit_time|**datetime**|요청이 제출 된 시간입니다.||  
|start_time|**datetime**|작업이 시작된 시간입니다.||  
|end_time|**datetime**|작업이 완료, 실패 또는 취소 된 시간입니다.||  
|total_elapsed_time|**int**|완료, 취소 또는 실패 한 실행에 대 한 start_time와 현재 시간 사이 또는 start_time와 end_time 간에 경과 된 총 시간입니다.|Total_elapsed_time 정수 24.8 (밀리초)의 최대값을 초과 하는 경우 오버플로로 인 한 구체화 실패가 발생 합니다.<br /><br /> 최대 값 (밀리초)은 24.8 일에 해당 합니다.|  
|operation_type|**nvarchar (16)**|로드 형식입니다.|' 백업 ', ' 로드 ', ' 복원 '|  
|mode|**nvarchar (16)**|실행 형식 내의 모드입니다.|Operation_type = **백업**<br />**큰**<br />**FULL**<br /><br /> Operation_type = **로드**<br />**추가할**<br />**로딩**<br />**UPSERT**<br /><br /> Operation_type = **복원**<br />**데이터**<br />**HEADER_ONLY**|  
|database_name|**nvarchar(255)**|이 작업의 컨텍스트인 데이터베이스의 이름입니다.||  
|table_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|작업을 요청 하는 사용자의 ID입니다.||  
|session_id|**nvarchar(32)**|작업을 수행 하는 세션의 ID입니다.|[Dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)에서 session_id를 참조 하세요.|  
|request_id|**nvarchar(32)**|작업을 수행 하는 요청의 ID입니다. 로드의 경우이 로드와 연결 된 현재 또는 마지막 요청입니다.|[Dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)에서 request_id를 참조 하세요.|  
|상태|**nvarchar (16)**|실행의 상태입니다.|' 취소 됨 ', ' 완료 됨 ', ' 실패 ', ' 대기 중 ', ' 실행 중 '|  
|progress|**int**|완료 비율입니다.|0~100|  
|명령을 사용합니다.|**nvarchar(4000)**|사용자가 제출한 명령의 전체 텍스트입니다.|는 4000 자 (공백 수) 보다 길면 잘립니다.|  
|rows_processed|**bigint**|이 작업의 일부로 처리 된 행 수입니다.||  
|rows_rejected|**bigint**|이 작업의 일부로 거부 된 행 수입니다.||  
|rows_inserted|**bigint**|이 작업의 일부로 데이터베이스 테이블에 삽입 된 행 수입니다.||  
  
## <a name="see-also"></a>참고 항목  
 [SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
