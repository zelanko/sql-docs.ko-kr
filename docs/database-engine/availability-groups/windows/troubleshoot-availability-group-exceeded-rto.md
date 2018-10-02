---
title: '문제 해결: 가용성 그룹 초과 RTO(SQL Server) | Microsoft Docs'
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: e83e4ef8-92f0-406f-bd0b-dc48dc210517
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8b3a2b9208900d89a56f3a49b5dd1cf1aa0e04d2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724221"
---
# <a name="troubleshoot-availability-group-exceeded-rto"></a>문제 해결: 가용성 그룹 초과 RTO
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  가용성 그룹에 데이터 손실 없이 자동 장애 조치(failover) 또는 계획된 수동 장애 조치(failover) 후 장애 조치 시간이 RTO(복구 시간 목표)를 초과하는 것을 발견할 수 있습니다. 또는 [Always On 가용성 그룹에 대한 성능 모니터링](monitor-performance-for-always-on-availability-groups.md)의 방법을 사용하여 동기 커밋 보조 복제본(예: 자동 장애 조치(failover) 파트너)의 장애 조치 시간을 예상할 때 RTO 초과를 발견할 수 있습니다.  
  
 자동 장애 조치가 아직 완료되지 않은 경우 [SQL Server 2012 Always On 환경에서 자동 장애 조치(failover) 문제 해결](http://support.microsoft.com/kb/2833707)을 참조하세요.  
  
 다음 섹션에서는 RTO를 초과하는 장애 조치 시간에 대한 일반적인 원인을 설명합니다.  
  
1.  [다시 실행 스레드의 실행을 차단하는 워크로드 보고](#BKMK_REDOBLOCK)  
  
2.  [리소스 경합으로 인한 다시 실행 스레드 뒤처짐](#BKMK_CONTENTION)  
  
##  <a name="BKMK_REDOBLOCK"></a> 다시 실행 스레드의 실행을 차단하는 워크로드 보고  
 보조 복제본의 다시 실행 스레드가 오래 실행 중인 읽기 전용 쿼리에 의해 DDL(데이터 정의 언어) 변경이 차단됩니다.  
  
### <a name="explanation"></a>설명  
 보조 복제본에서 읽기 전용 쿼리는 스키마 안정성(`Sch-S`) 잠금을 수집합니다. 이러한 `Sch-S` 잠금은 다시 실행 스레드가 DDL을 변경하기 위해 스키마 수정(`Sch-M`) 잠금을 수집하는 것을 차단할 수 있습니다. 차단된 다시 실행 스레드는 차단 해제될 때까지 로그 기록을 적용할 수 없습니다. 차단 해제된 후에는 로그의 끝까지 계속 캐치업하고 이후 실행 취소 및 장애 조치(failover) 프로세스가 진행되도록 할 수 있습니다.  
  
### <a name="diagnosis-and-resolution"></a>진단 및 해결  
 다시 실행 스레드가 차단된 경우 `sqlserver.lock_redo_blocked`라는 확장 이벤트가 생성됩니다. 또한 보조 복제본에 대해 DMV sys.dm_exec_request를 쿼리하여 다시 실행 스레드를 차단하는 세션을 알아낸 다음, 정정 작업을 실행할 수 있습니다. 다음 쿼리는 다시 실행 스레드를 차단하는 읽기 전용 쿼리의 세션 ID를 반환합니다.  
  
```sql  
select session_id, command, blocking_session_id, wait_time, wait_type, wait_resource   
from sys.dm_exec_requests where command = 'DB STARTUP'  
```  
  
 다시 실행 스레드가 차단 해제된 보고 워크로드를 완료하도록 하거나 차단 세션 ID에 대해 [KILL &#40;Transact-SQL&#41;](~/t-sql/language-elements/kill-transact-sql.md) 명령을 실행하여 다시 실행 스레드를 즉시 차단 해제할 수 있습니다.  
  
##  <a name="BKMK_CONTENTION"></a> 리소스 경합으로 인한 다시 실행 스레드 뒤처짐  
 보조 복제본에 대한 큰 보고 워크로드 때문에 보조 복제본의 성능이 느려졌고 다시 실행 스레드가 뒤처졌습니다.  
  
### <a name="explanation"></a>설명  
 보조 복제본에 로그 기록을 적용할 때 다시 실행 스레드는 로그 디스크에서 로그 기록을 읽은 다음, 각 로그 기록에 대해 데이터 페이지에 접근하여 로그 기록을 적용합니다. 페이지 액세스는 페이지가 버퍼 풀에 아직 없는 경우 I/O 경계(물리적 디스크 액세스)일 수 있습니다. I/O 경계 보고 워크로드가 있는 경우 보고 워크로드가 다시 실행 스레드와 I/O 리소스를 경합하여 다시 실행 스레드가 느려질 수 있습니다.  
  
### <a name="diagnosis-and-resolution"></a>진단 및 해결  
 다음 DMV 쿼리를 사용하여 `last_redone_lsn` 및 `last_received_lsn` 사이의 간격 차를 측정하면 다시 실행 스레드가 얼마나 뒤처졌는지 확인할 수 있습니다.  
  
```sql  
select recovery_lsn, truncation_lsn, last_hardened_lsn, last_received_lsn,   
   last_redone_lsn, last_redone_time  
from sys.dm_hadr_database_replica_states  
  
```  
  
 다시 실행 스레드가 실제로 뒤처진 경우 보조 복제본에 대해 성능 저하의 근본 원인을 조사해야 합니다. 보고 워크로드와의 I/O 경합이 있는 경우 [Resource Governor](~/relational-databases/resource-governor/resource-governor.md)를 사용하여 보고 워크로드가 실행되는 I/O 사이클을 간접적으로 제어하는 데 사용되는 CPU 사이클을 어느 정도 제어할 수 있습니다. 예를 들어 보고 워크로드가 CPU의 10%를 사용하지만 워크로드가 I/O 경계인 경우 Resource Governor를 사용하여 CPU 리소스 사용량을 5%로 제한하면 읽기 워크로드를 제한하여 I/O에 대한 영향을 최소화할 수 있습니다.  
  
## <a name="next-steps"></a>다음 단계  
 [SQL Server의 성능 문제 해결(SQL Server 2012에 적용)](http://msdn.microsoft.com/library/dd672789(v=SQL.100).aspx)  
  
  
