---
title: sys. dm_hadr_database_replica_states (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_database_states_TSQL
- sys.dm_hadr_database_states
- dm_hadr_database_states
- dm_hadr_database_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_database_replica_states dynamic management view
ms.assetid: 1a17b0c9-2535-4f3d-8013-cd0a6d08f773
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 83b3c369add51a853078dd64a8861d633ac330ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73982274"
---
# <a name="sysdm_hadr_database_replica_states-transact-sql"></a>sys.dm_hadr_database_replica_states(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로컬 인스턴스에서 가용성 복제본을 호스팅하는 Always On 가용성 그룹에 참여 하는 각 데이터베이스에 대해 하나의 행을 반환 합니다. 이 동적 관리 뷰는 주 복제본과 보조 복제본 모두에 대한 상태 정보를 표시합니다. 보조 복제본에서 이 뷰는 서버 인스턴스에 있는 모든 보조 데이터베이스에 대해 하나의 행을 반환합니다. 주 복제본에서 이 뷰는 각 주 데이터베이스에 대해 하나의 행과 해당 보조 데이터베이스에 대해 하나의 행을 반환합니다.  
  
> [!IMPORTANT]
> 동작과 상위 수준의 상태에 따라 데이터베이스 상태 정보가 사용할 수 없거나 만료될 수 있습니다. 또한 값은 로컬 관련성만 가집니다. 예를 들어 주 복제본에서 **last_hardened_lsn** 열의 값은 보조 복제본이 현재 보유 하 고 있을 수 있는 실제 확정 된 lsn 값이 아니라 주 복제본에서 현재 사용할 수 있는 지정 된 보조 데이터베이스에 대 한 정보를 반영 합니다.  
   
|열 이름|데이터 형식|주 복제본에 대한 설명|  
|-----------------|---------------|----------------------------------------|  
|**database_id**|**int**|SQL Server 내에서 고유한 데이터베이스의 식별자입니다. 이 값은 [sys. 데이터베이스](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰에 표시 된 것과 동일한 값입니다.|  
|**group_id**|**uniqueidentifier**|데이터베이스가 속한 가용성 그룹의 식별자입니다.|  
|**replica_id**|**uniqueidentifier**|가용성 그룹 내 가용성 복제본의 식별자입니다.|  
|**group_database_id**|**uniqueidentifier**|가용성 그룹 내 데이터베이스의 식별자입니다. 이 식별자는 이 데이터베이스가 조인되는 모든 복제본에서 동일합니다.|  
|**is_local**|**bit**|가용성 데이터베이스가 로컬인지 여부를 나타나며 다음 중 하나입니다.<br /><br /> 0 = 데이터베이스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 로컬이 아닙니다.<br /><br /> 1 = 데이터베이스가 서버 인스턴스에 로컬입니다.|  
|**is_primary_replica**|**bit**|복제본이 기본이면 1을, 보조 복제본이면 0을 반환합니다.<br /><br />**적용 대상:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상.|  
|**synchronization_state**|**tinyint**|데이터 이동 상태 이며 다음 값 중 하나입니다.<br /><br /> 0 = 동기화 중이 아닙니다. 주 데이터베이스의 경우 데이터베이스에서 트랜잭션 로그를 해당 보조 데이터베이스와 동기화할 준비가 되지 않았음을 나타냅니다. 보조 데이터베이스의 경우 데이터베이스에서 연결 문제로 인해 로그 동기화를 시작하지 않았거나 데이터베이스가 일시 중지되었거나, 시작 중에 전환 상태를 진행하고 있거나 역할 전환 중임을 나타냅니다.<br /><br /> 1 = 동기화 중입니다. 주 데이터베이스의 경우 해당 데이터베이스가 보조 데이터베이스의 검색 요청을 받을 준비가 되었음을 나타냅니다. 보조 데이터베이스의 경우 데이터베이스에 대한 활성 데이터 이동이 수행되고 있음을 나타냅니다.<br /><br /> 2 = 동기화 됨 주 데이터베이스는 동기화 중 대신 동기화됨으로 표시됩니다. 동기 커밋 보조 데이터베이스는 로컬 캐시에 데이터베이스가 장애 조치(failover) 준비되고 동기화 중일 때 동기화됨으로 표시됩니다.<br /><br /> 3 = 되돌리기 보조 데이터베이스가 주 데이터베이스에서 페이지 가져오기를 현재 진행 중인 경우의 실행 취소 프로세스의 단계를 나타냅니다.<br />**주의:** 보조 복제본의 데이터베이스가 되돌리기 상태에 있는 경우 보조 복제본에 대 한 장애 조치를 강제로 실행 하면 데이터베이스가 주 데이터베이스로 시작 될 수 없는 상태로 유지 됩니다. 데이터베이스를 보조 데이터베이스로 다시 연결하거나 로그 백업에서 새 로그 레코드를 적용해야 합니다.<br /><br /> 4 = 초기화 하 고 있습니다. 보조 데이터베이스에서 실행 취소 LSN을 catch하는 데 필요한 트랜잭션 로그가 보조 복제본에서 제공되고 확정 중인 경우의 실행 취소 단계를 나타냅니다.<br />**주의:** 보조 복제본의 데이터베이스가 초기화 중 상태에 있는 경우 보조 복제본에 대 한 장애 조치를 강제로 실행 하면 데이터베이스가 주 데이터베이스로 시작 될 수 없는 상태로 유지 됩니다. 데이터베이스를 보조 데이터베이스로 다시 연결하거나 로그 백업에서 새 로그 레코드를 적용해야 합니다.|  
|**synchronization_state_desc**|**nvarchar (60)**|데이터 이동 상태에 대한 설명이며 다음 중 하나입니다.<br /><br /> NOT SYNCHRONIZING<br /><br /> SYNCHRONIZING<br /><br /> SYNCHRONIZED<br /><br /> REVERTING<br /><br /> INITIALIZING|  
|**is_commit_participant**|**bit**|0 = 트랜잭션 커밋이 이 데이터베이스에 대해 동기화되어 있지 않습니다.<br /><br /> 1 = 트랜잭션 커밋이 이 데이터베이스에 대해 동기화되어 있습니다.<br /><br /> 비동기 커밋 가용성 복제본의 데이터베이스에 대해서는 이 값이 항상 0입니다.<br /><br /> 동기 커밋 가용성 복제본의 데이터베이스에 대해서는 이 값이 주 데이터베이스에서만 정확합니다.|  
|**synchronization_health**|**tinyint**|가용성 복제본의 가용성 그룹에 조인 된 데이터베이스의 동기화 상태와 가용성 복제본의 가용성 모드 (동기 커밋 또는 비동기 커밋 모드)의 교차를 반영 하며, 다음 중 하나입니다. 다음 값<br /><br /> 0 = 비정상 상태입니다. 데이터베이스의 **synchronization_state** 은 (동기화 하지 않음) 0입니다.<br /><br /> 1 = 부분 정상입니다. 동기 커밋 가용성 복제본의 데이터베이스는 **synchronization_state** 1 (동기화 중) 인 경우 부분적으로 정상으로 간주 됩니다.<br /><br /> 2 = 정상 동기 커밋 가용성 복제본의 데이터베이스는 **synchronization_state** 2 (SYNCHRONIZED) 인 경우 정상으로 간주 되 고 비동기 커밋 가용성 복제본의 데이터베이스는 **SYNCHRONIZATION_STATE** 1 (동기화 중) 인 경우 정상으로 간주 됩니다.|  
|**synchronization_health_desc**|**nvarchar (60)**|가용성 데이터베이스의 **synchronization_health** 에 대 한 설명입니다.<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**database_state**|**tinyint**|0 = 온라인<br /><br /> 1 = 복원 중<br /><br /> 2 = 복구 중<br /><br /> 3 = 복구 보류 중<br /><br /> 4 = 주의 대상<br /><br /> 5 = 응급<br /><br /> 6 = 오프라인<br /><br /> **참고:** Sys. 데이터베이스의 **상태** 열과 동일 합니다.|  
|**database_state_desc**|**nvarchar (60)**|가용성 복제본의 **database_state** 에 대 한 설명입니다.<br /><br /> ONLINE<br /><br /> RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT<br /><br /> EMERGENCY<br /><br /> OFFLINE<br /><br /> **참고:** Sys. 데이터베이스의 **state_desc** 열과 동일 합니다.|  
|**is_suspended**|**bit**|데이터베이스 상태이며 다음 중 하나입니다.<br /><br /> 0 = 다시 시작됨<br /><br /> 1 = 일시 중지됨|  
|**suspend_reason**|**tinyint**|데이터베이스가 일시 중지된 경우 일시 중지된 상태의 원인이며 다음 중 하나입니다.<br /><br /> 0 = 사용자 동작<br /><br /> 1 = 파트너가 일시 중지<br /><br /> 2 = 다시 실행<br /><br /> 3 = 캡처<br /><br /> 4 = 적용<br /><br /> 5 = 다시 시작<br /><br /> 6 = 실행 취소<br /><br /> 7 = 유효성 재검사<br /><br /> 8 = 보조 복제본 동기화 지점 계산에서 오류 발생|  
|**suspend_reason_desc**|**nvarchar (60)**|데이터베이스가 일시 중지된 이유에 대한 설명이며 다음 중 하나입니다.<br /><br /> SUSPEND_FROM_USER = 사용자가 데이터 이동을 수동으로 일시 중지했습니다.<br /><br /> SUSPEND_FROM_PARTNER = 강제 장애 조치(Failover) 후 데이터베이스 복제본이 일시 중지되었습니다.<br /><br /> SUSPEND_FROM_REDO = 다시 실행 단계 중에 오류가 발생했습니다.<br /><br /> SUSPEND_FROM_APPLY = 로그를 파일에 쓰는 동안 오류가 발생했습니다(오류 로그 참조).<br /><br /> SUSPEND_FROM_CAPTURE = 로그를 주 복제본에 캡처하는 동안 오류가 발생했습니다.<br /><br /> SUSPEND_FROM_RESTART = 데이터베이스가 다시 시작하기 전에 데이터베이스 복제본이 일시 중지되었습니다(오류 로그 참조).<br /><br /> SUSPEND_FROM_UNDO = 다시 실행 단계 중에 오류가 발생했습니다(오류 로그 참조).<br /><br /> SUSPEND_FROM_REVALIDATION = 재연결 시 로그 변경 사항 불일치가 검색되었습니다(오류 로그 참조).<br /><br /> SUSPEND_FROM_XRF_UPDATE = 공통 로그 지점을 찾을 수 없습니다(오류 로그 참조).|  
|**recovery_lsn**|**숫자 (25, 0)**|주 복제본에서 주 데이터베이스가 복구 또는 장애 조치(failover) 후 새 로그 레코드를 쓰기 전의 트랜잭션 로그 끝입니다. 지정된 보조 데이터베이스에 대해 이 값이 현재 확정된 LSN(last_hardened_lsn)보다 작으면 recovery_lsn은 이 보조 데이터베이스에서 다시 동기화(즉, 되돌려서 다시 초기화)해야 하는 값입니다. 이 값이 현재 확정된 LSN보다 크거나 같으면 다시 동기화가 필요하지 않으며 발생하지 않습니다.<br /><br /> **recovery_lsn** 는 0으로 채워진 로그-블록 ID를 반영 합니다. 실제 LSN(로그 시퀀스 번호)이 아닙니다. 이 값이 파생 되는 방법에 대 한 자세한 내용은이 항목의 뒷부분에 나오는 [LSN 열 값 이해](#LSNcolumns)를 참조 하세요.|  
|**truncation_lsn**|**숫자 (25, 0)**|주 복제본의 주 데이터베이스의 경우 모든 해당 보조 데이터베이스에 최소 로그 잘림 LSN을 반영합니다. 백업 작업 등에 의해 로컬 로그 잘림이 차단되는 경우 이 LSN이 로컬 잘림 LSN보다 클 수 있습니다.<br /><br /> 지정된 보조 데이터베이스의 경우 해당 데이터베이스의 잘림 지점을 반영합니다.<br /><br /> **truncation_lsn** 는 0으로 채워진 로그-블록 ID를 반영 합니다. 실제 로그 시퀀스 번호가 아닙니다.|  
|**last_sent_lsn**|**숫자 (25, 0)**|모든 로그 블록이 주 복제본에 의해 전송된 지점을 나타내는 로그 블록 식별자입니다. 가장 최근에 전송된 로그 블록의 ID가 아니라 전송될 다음 로그 블록의 ID입니다.<br /><br /> **last_sent_lsn** 은 0으로 채워진 로그-블록 ID를 반영 하며 실제 로그 시퀀스 번호가 아닙니다.|  
|**last_sent_time**|**datetime**|마지막 로그 블록이 전송된 시간입니다.|  
|**last_received_lsn**|**숫자 (25, 0)**|이 보조 데이터베이스를 호스팅하는 보조 복제본이 모든 로그 블록을 받은 지점을 식별하는 로그 블록 ID입니다.<br /><br /> **last_received_lsn** 는 0으로 채워진 로그-블록 ID를 반영 합니다. 실제 로그 시퀀스 번호가 아닙니다.|  
|**last_received_time**|**datetime**|보조 복제본에서 마지막으로 수신된 메시지의 로그 블록 ID를 읽은 시간입니다.|  
|**last_hardened_lsn**|**숫자 (25, 0)**|보조 데이터베이스에서 마지막으로 확정된 LSN의 로그 레코드를 포함하는 로그 블록의 시작입니다.<br /><br /> 현재 정책이 "지연"인 동기 커밋 데이터베이스 또는 비동기 커밋 주 데이터베이스에서 이 값은 NULL입니다. 다른 동기 커밋 주 데이터베이스의 경우 **last_hardened_lsn** 는 모든 보조 데이터베이스에 대해 확정 된 lsn의 최소값을 나타냅니다.<br /><br /> **참고: last_hardened_lsn** 은 0으로 채워진 로그-블록 ID를 반영 합니다. 실제 로그 시퀀스 번호가 아닙니다. 자세한 내용은이 항목의 뒷부분에 나오는 [LSN 열 값 이해](#LSNcolumns)를 참조 하세요.|  
|**last_hardened_time**|**datetime**|보조 데이터베이스에서 마지막으로 확정 된 LSN (**last_hardened_lsn**)에 대 한 로그 블록 식별자의 시간입니다. 주 데이터베이스에서 확정된 최소 LSN에 해당하는 시간을 반영합니다.|  
|**last_redone_lsn**|**숫자 (25, 0)**|보조 데이터베이스에서 마지막으로 다시 실행된 로그 레코드의 실제 로그 시퀀스 번호입니다. **last_redone_lsn** 은 항상 **last_hardened_lsn**보다 낮습니다.|  
|**last_redone_time**|**datetime**|보조 데이터베이스에서 마지막 로그 레코드가 다시 실행된 시간입니다.|  
|**log_send_queue_size**|**bigint**|주 데이터베이스의 로그 레코드 중 보조 데이터베이스로 전송되지 않은 레코드의 양(KB)입니다.|  
|**log_send_rate**|**bigint**|주 복제본 인스턴스가 마지막 활성 기간 동안 데이터를 전송 하는 평균 속도 (KB)입니다.|  
|**redo_queue_size**|**bigint**|보조 복제본의 로그 파일에 있는 로그 레코드 중 아직 다시 실행되지 않은 로그 레코드의 양(KB)입니다.|  
|**redo_rate**|**bigint**|지정 된 보조 데이터베이스에서 로그 레코드가 다시 실행 되는 평균 속도 (kb)입니다.|  
|**filestream_send_rate**|**bigint**|FILESTREAM 파일이 보조 복제본으로 전송되는 속도(KB/초)입니다.|  
|**end_of_log_lsn**|**숫자 (25, 0)**|로그 LSN의 로컬 끝입니다. 주 데이터베이스와 보조 데이터베이스의 로그 캐시에 있는 마지막 로그 레코드에 해당하는 실제 LSN입니다. 기본 복제본에서 보조 행은 보조 복제본이 주 복제본에 전송한 최근 진행 메시지의 로그 LSN의 끝을 반영합니다.<br /><br /> **end_of_log_lsn** 는 0으로 채워진 로그-블록 ID를 반영 합니다. 실제 로그 시퀀스 번호가 아닙니다. 자세한 내용은이 항목의 뒷부분에 나오는 [LSN 열 값 이해](#LSNcolumns)를 참조 하세요.|  
|**last_commit_lsn**|**숫자 (25, 0)**|트랜잭션 로그의 마지막 커밋 레코드에 해당하는 실제 로그 시퀀스 번호입니다.<br /><br /> 주 데이터베이스에서 처리된 마지막 커밋 레코드에 해당합니다. 보조 데이터베이스에 대한 행에 보조 복제본이 주 복제본에 전송한 로그 시퀀스 번호가 표시됩니다.<br /><br /> 보조 데이터베이스에서 다시 실행된 마지막 커밋 레코드입니다.|  
|**last_commit_time**|**datetime**|마지막 커밋 레코드에 해당하는 시간입니다.<br /><br /> 보조 데이터베이스에서 이 시간은 주 데이터베이스의 시간과 동일합니다.<br /><br /> 주 복제본에서 각 보조 데이터베이스 행에는 해당 보조 데이터베이스를 호스팅하는 보조 복제본이 주 복제본에 다시 보고된 시간이 표시됩니다. 주 데이터베이스 행과 지정 된 보조 데이터베이스 행 간의 시간 차이는 다시 실행 프로세스가 catch 되 고 진행률이 주 복제본에 다시 보고 된 것으로 가정 하 여 대략 RPO (복구 지점 목표)를 나타냅니다. 보조 복제본을 기준으로 합니다.|  
|**low_water_mark_for_ghosts**|**bigint**|주 데이터베이스에서 고스트 정리에 사용되는 하위 워터마크를 나타내는 데이터베이스에 대한 일정하게 증가하는 번호입니다. 시간이 지나도 이 번호가 증가하지 않으면 고스트 정리가 수행되지 않은 것을 의미합니다. 정리할 고스트 행을 결정하기 위해 주 복제본은 주 복제본을 포함한 모든 가용성 복제본에서 이 데이터베이스에 대한 이 열의 최소값을 사용합니다.|  
|**secondary_lag_seconds**|**bigint**|동기화 중에 보조 복제본이 주 복제본의 뒤에 있는 시간 (초)입니다.<br /><br />**적용 대상:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상.|  
  
##  <a name="LSNcolumns"></a>LSN 열 값 이해  
 **End_of_log_lsn**, **last_hardened_lsn**, **last_received_lsn**, **last_sent_lsn**, **recovery_lsn**및 **truncation_lsn** 열의 값은 실제 lsn (로그 시퀀스 번호)이 아닙니다. 각 값은 0으로 채워진 로그-블록 ID를 반영합니다.  
  
 **end_of_log_lsn**, **last_hardened_lsn**및 **recovery_lsn** 는 플러시 lsn입니다. 예를 들어 **last_hardened_lsn** 은 이미 디스크에 있는 블록을 지난 다음 블록의 시작을 나타냅니다.  따라서 **last_hardened_lsn** 값 < 모든 LSN은 디스크에 있습니다.  이 값에 >= 인 LSN은 플러시되지 않습니다.  
  
 **Dm_hadr_database_replica_states**에서 반환 된 lsn 값 중 **LAST_REDONE_LSN** 는 실제 lsn입니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
