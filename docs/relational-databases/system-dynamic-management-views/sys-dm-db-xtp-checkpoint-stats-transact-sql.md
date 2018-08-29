---
title: sys.dm_db_xtp_checkpoint_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
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
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8b53431590bd6931873882f317fca608d510ecad
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43102344"
---
# <a name="sysdmdbxtpcheckpointstats-transact-sql"></a>sys.dm_db_xtp_checkpoint_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스의 메모리 내 OLTP 검사점 작업에 대한 통계를 반환합니다. 데이터베이스에 메모리 내 OLTP 개체가 없는 경우 빈 결과 집합을 반환합니다.  
  
 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
```  
SELECT * FROM db.sys.dm_db_xtp_checkpoint_stats;  
```  
  
**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 상당히 다른 보다 최신 버전 이며 낮은 항목에 설명 되어 [SQL Server 2014](#bkmk_2014)합니다.**
  
## <a name="includesssql15includessssql15-mdmd-and-later"></a>[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상  
 다음 표에서 열을 설명 `sys.dm_db_xtp_checkpoint_stats`부터 **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]** 합니다.  
  
|열 이름|형식|Description|  
|-----------------|----------|-----------------|  
|last_lsn_processed|**bigint**|컨트롤러에 의해 표시 된 마지막 LSN입니다.|  
|end_of_log_lsn|**numeric(38)**|로그 끝 LSN입니다.|  
|bytes_to_end_of_log|**bigint**|로그 바이트 사이의 바이트를 해당 컨트롤러에서 처리 되지 않은 `last_lsn_processed` 고 `end_of_log_lsn`입니다.|  
|log_consumption_rate|**bigint**|비율 (k B/초)에서 컨트롤러를 트랜잭션 로그 사용입니다.|  
|active_scan_time_in_ms|**bigint**|트랜잭션 로그 검색의 컨트롤러에서 소요 된 시간입니다.|  
|total_wait_time_in_ms|**bigint**|로그를 검사 하지 않는 하는 동안 컨트롤러에 대 한 누적 대기 시간입니다.|  
|waits_for_io|**bigint**|로그 IO 컨트롤러 스레드에서 발생 한 대기 수입니다.|  
|io_wait_time_in_ms|**bigint**|로그 IO 컨트롤러 스레드에서 기다리는 데 걸린 누적 시간입니다.|  
|waits_for_new_log_count|**bigint**|생성 될 새 로그에 대 한 컨트롤러 스레드에서 발생 한 대기 수입니다.|  
|new_log_wait_time_in_ms|**bigint**|새 로그 컨트롤러 스레드에서 기다리는 데 걸린 누적 시간입니다.|  
|idle_attempts_count|**bigint**|컨트롤러는 유휴 상태로 전환 횟수입니다.|  
|tx_segments_dispatched|**bigint**|컨트롤러에서 표시 하 고 직렬 변환기에 디스패치 세그먼트의 수입니다. 세그먼트는 serialization의 단위를 형성 하는 로그의 인접 한 일부입니다. 1MB로, 현재 크기가 않지만 나중에 변경할 수 있습니다.|  
|segment_bytes_dispatched|**bigint**|데이터베이스를 다시 시작한 이후 컨트롤러 serializer에 의해 반환 되는 바이트의 총 바이트 수입니다.|  
|bytes_serialized|**bigint**|데이터베이스를 다시 시작한 이후 직렬화 바이트의 총 수입니다.|  
|serializer_user_time_in_ms|**bigint**|사용자 모드에서 serializer에서 소요 된 시간입니다.|  
|serializer_kernel_time_in_ms|**bigint**|커널 모드에서 serializer에서 소요 된 시간입니다.|  
|xtp_log_bytes_consumed|**bigint**|데이터베이스 다시 시작 이후에 사용 된 로그 바이트의 총 수입니다.|  
|checkpoints_closed|**bigint**|데이터베이스를 다시 시작한 이후 닫힌 검사점의 수입니다.|  
|last_closed_checkpoint_ts|**bigint**|마지막으로 닫힌된 검사점의 타임 스탬프입니다.|  
|hardened_recovery_lsn|**numeric(38)**|복구는이 LSN에서 시작 됩니다.|  
|hardened_root_file_guid|**uniqueidentifier**|마지막으로 완료 된 검사점의 결과로 확정 루트 파일의 GUID입니다.|  
|hardened_root_file_watermark|**bigint**|**내부만**합니다. 얼마나 유효 최대 루트 파일을 읽는 데 (이 내부적으로 관련 형식에만 해당-BSN 호출).|  
|hardened_truncation_lsn|**numeric(38)**|잘림 지점의 LSN입니다.|  
|log_bytes_since_last_close|**bigint**|마지막 바이트를 현재 로그 끝을 닫습니다.|  
|time_since_last_close_in_ms|**bigint**|닫기 마지막 검사점 이후 시간입니다.|  
|current_checkpoint_id|**bigint**|현재 새 세그먼트가이 검사점에 할당 되 고 됩니다. 검사점 시스템이 파이프라인입니다. 현재 검사점은 로그에서 세그먼트에 할당 되는 것입니다. 제한에 도달 하면가 하는 컨트롤러와 새로 만든 최신 검사점 해제 됩니다.|  
|current_checkpoint_segment_count|**bigint**|현재 검사점의 세그먼트의 수입니다.|  
|recovery_lsn_candidate|**bigint**|**내부적으로**합니다. Current_checkpoint_id 닫으면 recoverylsn를 선택할 수에 대 한 후보입니다.|  
|outstanding_checkpoint_count|**bigint**|종료 대기 중인 파이프라인에서 검사점의 수입니다.|  
|closing_checkpoint_id|**bigint**|닫는 검사점의 ID입니다.<br /><br /> 병렬로 작업 하는 serializer 이므로 이러한 작업이 완료 되 면 다음 검사점 후보 닫기 스레드에서 닫아야 합니다. 닫기 스레드에서 한 번에 하나씩 닫을 수 있고 닫는 검사점 닫기 스레드에서 작업 하는 것 이므로 순서에 있어야 합니다.|  
|recovery_checkpoint_id|**bigint**|복구에 사용할 검사점의 ID입니다.|  
|recovery_checkpoint_ts|**bigint**|복구 검사점 타임 스탬프입니다.|  
|bootstrap_recovery_lsn|**numeric(38)**|부트스트랩에 대 한 복구 LSN입니다.|  
|bootstrap_root_file_guid|**uniqueidentifier**|부트스트랩에 대 한 루트 파일의 GUID입니다.|  
|internal_error_code|**bigint**|컨트롤러, serializer, close 및 병합 스레드 중 하나에서 표시 하는 데 오류가 발생 했습니다.|
|bytes_of_large_data_serialized|**bigint**|Serialize 된 데이터의 양입니다. |  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 다음 표에서 열을 설명 `sys.dm_db_xtp_checkpoint_stats`에 대 한 **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]** 합니다.  
  
|열 이름|형식|Description|  
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
  
## <a name="see-also"></a>관련 항목  
 [메모리 최적화 테이블 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
