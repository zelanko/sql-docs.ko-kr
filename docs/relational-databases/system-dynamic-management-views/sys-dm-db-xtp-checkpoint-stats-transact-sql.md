---
title: sys. dm_db_xtp_checkpoint_stats (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_stats
- dm_db_xtp_checkpoint_stats_TSQL
- sys.dm_db_xtp_checkpoint_stats
- sys.dm_db_xtp_checkpoint_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_stats dynamic management view
ms.assetid: 8d0b18ca-db4d-4376-9905-3e4457727c46
author: CarlRabeler
ms.author: carlrab
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c93cc5f34d86e15645b4d53c02244e2705bbeda5
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830837"
---
# <a name="sysdm_db_xtp_checkpoint_stats-transact-sql"></a>sys.dm_db_xtp_checkpoint_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스의 메모리 내 OLTP 검사점 작업에 대한 통계를 반환합니다. 데이터베이스에 메모리 내 OLTP 개체가 없는 경우 빈 결과 집합을 반환합니다.  
  
 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
```  
USE In_Memory_db_name
SELECT * FROM sys.dm_db_xtp_checkpoint_stats;  
```  
  
**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]는 최신 버전과 상당히 다르며 [SQL Server 2014](#bkmk_2014)의 항목에서 더 자세히 설명 합니다.**
  
## <a name="sssql15-and-later"></a>[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상.  
 다음 표에서는부터 시작 하 여의 열에 대해 설명 합니다 `sys.dm_db_xtp_checkpoint_stats` **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]** .  
  
|열 이름|형식|설명|  
|-----------------|----------|-----------------|  
|last_lsn_processed|**bigint**|컨트롤러에서 표시 한 마지막 LSN입니다.|  
|end_of_log_lsn|**numeric (38)**|로그 끝의 LSN입니다.|  
|bytes_to_end_of_log|**bigint**|및 사이의 바이트에 해당 하는 컨트롤러에서 처리 되지 않은 로그 바이트 수 `last_lsn_processed` `end_of_log_lsn` 입니다.|  
|log_consumption_rate|**bigint**|컨트롤러의 트랜잭션 로그 사용 률 (k b/초)입니다.|  
|active_scan_time_in_ms|**bigint**|컨트롤러에서 트랜잭션 로그를 적극적으로 검사 하는 데 걸린 시간입니다.|  
|total_wait_time_in_ms|**bigint**|로그를 검사 하지 않는 동안 컨트롤러의 누적 대기 시간입니다.|  
|waits_for_io|**bigint**|컨트롤러 스레드에서 발생 한 로그 IO의 대기 수입니다.|  
|io_wait_time_in_ms|**bigint**|컨트롤러 스레드에서 로그 IO를 대기 하는 데 걸린 누적 시간입니다.|  
|waits_for_new_log_count|**bigint**|새 로그가 생성 될 때까지 컨트롤러 스레드에서 발생 한 대기 수입니다.|  
|new_log_wait_time_in_ms|**bigint**|컨트롤러 스레드에서 새 로그를 대기 하는 데 걸린 누적 시간입니다.|  
|idle_attempts_count|**bigint**|컨트롤러가 유휴 상태로 전환 된 횟수입니다.|  
|tx_segments_dispatched|**bigint**|컨트롤러에서 표시 되 고 serializer에 디스패치 된 세그먼트 수입니다. 세그먼트는 직렬화 단위를 형성 하는 로그의 인접 한 부분입니다. 현재는 1MB로 크기 조정 되지만 나중에 변경 될 수 있습니다.|  
|segment_bytes_dispatched|**bigint**|데이터베이스가 다시 시작 된 이후 컨트롤러에서 serializer로 디스패치 된 바이트의 총 바이트 수입니다.|  
|bytes_serialized|**bigint**|데이터베이스 다시 시작 이후 직렬화 된 총 바이트 수입니다.|  
|serializer_user_time_in_ms|**bigint**|사용자 모드에서 serializer에 소요 된 시간입니다.|  
|serializer_kernel_time_in_ms|**bigint**|커널 모드에서 serializer에 소요 된 시간입니다.|  
|xtp_log_bytes_consumed|**bigint**|데이터베이스를 다시 시작한 이후 사용 된 총 로그 바이트 수입니다.|  
|checkpoints_closed|**bigint**|데이터베이스를 다시 시작한 이후 닫힌 검사점 수입니다.|  
|last_closed_checkpoint_ts|**bigint**|마지막으로 닫힌 검사점의 타임 스탬프입니다.|  
|hardened_recovery_lsn|**numeric (38)**|이 LSN에서 복구가 시작 됩니다.|  
|hardened_root_file_guid|**uniqueidentifier**|마지막으로 완료 된 검사점의 결과로 확정 된 루트 파일의 GUID입니다.|  
|hardened_root_file_watermark|**bigint**|**내부 전용**입니다. 최대 루트 파일을 읽을 수 있는 정도입니다 (내부적으로는 BSN 이라고 함).|  
|hardened_truncation_lsn|**numeric (38)**|잘림 지점의 LSN입니다.|  
|log_bytes_since_last_close|**bigint**|마지막으로 가까운 로그 끝에 있는 바이트입니다.|  
|time_since_last_close_in_ms|**bigint**|검사점을 마지막으로 닫은 후의 시간입니다.|  
|current_checkpoint_id|**bigint**|현재 새 세그먼트를이 검사점에 할당 하는 중입니다. 검사점 시스템이 파이프라인입니다. 현재 검사점은 로그에서 세그먼트가 할당 되는 세그먼트입니다. 한도에 도달 하면 컨트롤러에서 검사점을 해제 하 고 현재로 만든 새 컨트롤러를 만듭니다.|  
|current_checkpoint_segment_count|**bigint**|현재 검사점의 세그먼트 수입니다.|  
|recovery_lsn_candidate|**bigint**|**내부적 으로만**입니다. Current_checkpoint_id 닫힐 때 recoverylsn으로 선택할 후보입니다.|  
|outstanding_checkpoint_count|**bigint**|파이프라인에서 종결 되기를 기다리는 검사점의 수입니다.|  
|closing_checkpoint_id|**bigint**|닫는 검사점의 ID입니다.<br /><br /> Serializer가 병렬로 작동 하 고 있으므로 완료 된 후에는 종료 스레드를 사용 하 여 검사점을 닫아야 합니다. 그러나 close 스레드는 한 번에 하나만 닫을 수 있으며 순서 대로 되어 있어야 합니다. 따라서 닫는 스레드가 작업 중인 종료 검사점입니다.|  
|recovery_checkpoint_id|**bigint**|복구에 사용할 검사점의 ID입니다.|  
|recovery_checkpoint_ts|**bigint**|복구 검사점의 타임 스탬프입니다.|  
|bootstrap_recovery_lsn|**numeric (38)**|부트스트랩에 대 한 복구 LSN입니다.|  
|bootstrap_root_file_guid|**uniqueidentifier**|부트스트랩에 대 한 루트 파일의 GUID입니다.|  
|internal_error_code|**bigint**|컨트롤러, serializer, 닫기 및 병합 스레드에 의해 오류가 발생 했습니다.|
|bytes_of_large_data_serialized|**bigint**|Serialize 된 데이터의 양입니다. |  
  
##  <a name="sssql14"></a><a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 다음 표에서는의 열에 대해 설명 합니다 `sys.dm_db_xtp_checkpoint_stats` **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]** .  
  
|열 이름|형식|설명|  
|-----------------|----------|-----------------|  
|log_to_process_in_bytes|**bigint**|스레드의 현재 LSN(로그 시퀀스 번호) 및 로그 끝 사이의 로그 바이트 수입니다.|  
|total_log_blocks_processed|**bigint**|서버 시작 후 처리된 총 로그 블록 수입니다.|  
|total_log_records_processed|**bigint**|서버 시작 후 처리된 총 로그 레코드 수입니다.|  
|xtp_log_records_processed|**bigint**|서버 시작 후 처리된 총 메모리 OLTP 로그 레코드 수입니다.|  
|total_wait_time_in_ms|**bigint**|누적 대기 시간(밀리초)입니다.|  
|waits_for_io|**bigint**|로그 IO에 대한 대기 수입니다.|  
|io_wait_time_in_ms|**bigint**|로그 ID를 대기하는 데 걸린 누적 시간입니다.|  
|waits_for_new_log|**bigint**|새 로그 생성을 위한 대기 수입니다.|  
|new_log_wait_time_in_ms|**bigint**|새 로그에서 대기하는 데 걸린 누적 시간입니다.|  
|log_generated_since_last_checkpoint_in_bytes|**bigint**|마지막 메모리 OLTP 검사점 이후 생성된 로그의 양입니다.|  
|ms_since_last_checkpoint|**bigint**|마지막 메모리 OLTP 검사점 이후 시간(밀리초)입니다.|  
|checkpoint_lsn|**숫자 (38)**|마지막으로 완료된 메모리 내 OLTP 검사점과 연결된 복구 LSN(로그 시퀀스 번호)입니다.|  
|current_lsn|**숫자 (38)**|현재 처리 중인 로그 레코드의 LSN입니다.|  
|end_of_log_lsn|**숫자 (38)**|로그 끝의 LSN입니다.|  
|task_address|**varbinary(8)**|SOS_Task의 주소입니다. sys.dm_os_tasks에 조인해서 추가 정보를 찾을 수 있습니다.|  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 `VIEW DATABASE STATE` 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 최적화 테이블 동적 관리 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
