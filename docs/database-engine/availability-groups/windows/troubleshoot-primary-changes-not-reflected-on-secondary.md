---
title: '문제 해결: 보조 복제본에 반영되지 않는 주 복제본의 변경 내용(Always 가용성 그룹-SQL Server) | Microsoft Docs'
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c602fd39-db93-4717-8f3a-5a98b940f9cc
caps.latest.revision: 9
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b2d5d93ccd17abadaf702316fbad2a382ebc6495
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32867788"
---
# <a name="troubleshoot-changes-on-the-primary-replica-are-not-reflected-on-the-secondary-replica"></a>문제 해결: 보조 복제본에 반영되지 않은 주 복제본의 변경 내용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  클라이언트 응용 프로그램에서 주 복제본에 대한 업데이트를 성공적으로 완료하지만 보조 복제본 쿼리는 변경 내용이 반영되지 않았음을 보여줍니다. 이 경우 가용성에 정상 동기화 상태가 있음을 가정합니다. 대부분의 경우에서 이 동작은 몇 분 후 자체적으로 해결합니다.  
  
 변경 내용이 몇 분 후에도 보조 복제본에 여전히 반영되지 않는 경우 동기화 작업 흐름에 병목 상태가 있을 수 있습니다. 병목 상태의 위치는 보조 복제본이 동기 커밋 또는 비동기 커밋으로 설정되어 있는지 여부에 따라 달라집니다.  
  
 **동기 커밋**  
  
 주 복제본에서 각 성공적인 업데이트는 이미 보조 복제본으로 동기화되었거나 해당 로그 레코드가 보조 복제본에서 강화를 위해 플러시되었습니다. 따라서 병목 상태는 보조 복제본에서 로그가 플러시된 후 발생하는 다시 실행 프로세스에 있어야 합니다.  
  
 그러나 다시 실행을 따라 잡으면 보조 복제본에서 모든 읽기 작업은 스냅숏 격리입니다.  
  
  -   주 복제본에서 장기 실행 트랜잭션  
  
  -   보조 복제본에서 다시 실행  


**비동기 커밋**  
 
 비동기 커밋은 트랜잭션이 로컬 디스크로 플러시되자마자 승인하므로 병목 상태는 해당 시점 이후에 아무 곳이나 될 수 있습니다.  
 
  -   주 복제본에서 장기 실행 트랜잭션  
  
  -   네트워크 대기 시간 또는 처리량  
  
  -   보조 복제본에서 로그 확정  
  
  -   보조 복제본에서 다시 실행  


다음 섹션에서는 주 본제본의 변경 내용이 읽기 전용 쿼리에 대한 보조 복제본에 반영되지 않는 일반적인 원인을 설명합니다.  


##  <a name="BKMK_OLDTRANS"></a> 장기 실행 활성 트랜잭션  
 주 복제본에서 장기 실행 트랜잭션은 보조 복제본에서 업데이트를 읽지 못하도록 합니다.  
  
### <a name="explanation"></a>설명  
 보조 복제본에서 모든 읽기 작업은 스냅숏 격리 쿼리입니다. 스냅숏 격리에서 읽기 전용 클라이언트는 다시 실행된 로그에서 가장 오래된 활성 트랜잭션의 시작 지점의 보조 복제본에서 가용성 데이터베이스를 봅니다. 트랜잭션이 몇 시간 동안 커밋되지 않는 경우 열린 트랜잭션은 모든 읽기 전용 쿼리가 새로운 업데이트를 보지 못하도록 차단합니다.  
  
### <a name="diagnosis-and-resolution"></a>진단 및 해결  
 주 복제본에서 [DBCC OPENTRAN&#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-opentran-transact-sql.md)을 사용하여 가장 오래된 활성 트랜잭션을 보고 롤백할 수 있는지 확인합니다. 가장 오래된 활성 트랜잭션이 롤백되고 보조 복제본에 동기화되면 보조 복제본에서 읽기 작업은 가장 오래된 활성 트랜잭션의 시작 부분까지 가용성 데이터베이스의 업데이트를 확인할 수 있습니다.  
  
##  <a name="BKMK_LATENCY"></a> 높은 네트워크 대기 시간 또는 낮은 네트워크 처리량이 주 복제본에 로그 축적 유발  
 높은 네트워크 대기 시간 또는 낮은 처리량은 보조 복제본으로 로그가 충분히 빠르게 전송되는 것을 방지할 수 있습니다.  
  
### <a name="explanation"></a>설명  
 주 복제본은 보조 복제본으로 전송된 승인되지 않은 최대 허용 메시지 수를 초과하는 경우 로그 전송에 대한 흐름 제어를 활성화합니다. 이러한 메시지의 일부가 승인될 때까지 로그 블록이 보조 복제본으로 전송될 수 없습니다. 이 경우 RPO(복구 지점 목표)를 위협할 수 있는 잠재적 데이터 손실에 심각한 영향을 줄 수 있습니다.  
  
### <a name="diagnosis-and-resolution"></a>진단 및 해결  
 높은 DMV 값 [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)는 주 복제본에서 다시 보관되는 로그를 나타낼 수 있습니다. 이 값을 [log_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)로 나누면 데이터가 보조 복제본에서 얼마나 빨리 따라 잡힐 수 있는지에 대한 대략적인 예상 값을 제공할 수 있습니다.  
  
 또한 두 성능 개체 [SQL Server:가용성 복제본 > 흐름 제어 시간(ms/sec)](~/relational-databases/performance-monitor/sql-server-availability-replica.md) 및 [SQL Server:가용성 복제본 > 흐름 제어/초](~/relational-databases/performance-monitor/sql-server-availability-replica.md)를 확인하는 데 유용합니다. 이러한 두 값을 곱하면 흐름 제어가 해제될 때까지 대기하는 데 소비한 최종 시간이 나타납니다. 흐름 제어 대기 시간이 길수록 전송 속도가 더 느립니다.  
  
 아래는 네트워크 대기 시간 및 처리량 진단에 유용한 메트릭의 목록입니다. **ping.exe**와 같은 Windows 도구를 사용하여 네트워크 사용률을 평가할 수 있습니다.  
  
-   DMV [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
-   DMV [log_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
-   성능 카운터 `SQL Server:Database > Log Bytes Flushed/sec`  
  
-   성능 카운터 `SQL Server:Database Mirroring > Send/Receive Ack Time`  
  
-   성능 카운터 `SQL Server:Availability Replica > Bytes Sent to Replica/sec`  
  
-   성능 카운터 `SQL Server:Availability Replica > Bytes Sent to Transport/sec`  
  
-   성능 카운터 `SQL Server:Availability Replica > Flow Control Time (ms/sec)`  
  
-   성능 카운터 `SQL Server:Availability Replica > Flow Control/sec`  
  
-   성능 카운터 `SQL Server:Availability Replica > Resent Messages/sec`  
  
 이 문제를 해결하려면 네트워크 대역폭을 업그레이드하거나 불필요한 네트워크 트래픽을 제거하거나 줄여 보십시오.  
  
##  <a name="BKMK_REDOBLOCK"></a> 다시 실행 스레드의 실행을 차단하는 다른 워크로드 보고  
 보조 복제본의 다시 실행 스레드가 오래 실행 중인 읽기 전용 쿼리에 의해 DDL(데이터 정의 언어) 변경이 차단됩니다. 추가 업데이트를 읽기 작업에 사용할 수 있도록 다시 실행 스레드의 잠금을 해제해야 합니다.  
  
### <a name="explanation"></a>설명  
 보조 복제본에서 읽기 전용 쿼리는 스키마 안정성(`Sch-S`) 잠금을 수집합니다. 이러한 `Sch-S` 잠금은 다시 실행 스레드가 DDL을 변경하기 위해 스키마 수정(`Sch-M`) 잠금을 수집하는 것을 차단할 수 있습니다. 차단된 다시 실행 스레드는 차단 해제될 때까지 로그 기록을 적용할 수 없습니다.  
  
### <a name="diagnosis-and-resolution"></a>진단 및 해결  
 다시 실행 스레드가 차단된 경우 `sqlserver.lock_redo_blocked`라는 확장 이벤트가 생성됩니다. 또한 보조 복제본에 대해 DMV sys.dm_exec_request를 쿼리하여 다시 실행 스레드를 차단하는 세션을 알아낸 다음, 정정 작업을 실행할 수 있습니다. 다음 쿼리는 다시 실행 스레드를 차단하는 읽기 작업의 세션 ID를 반환합니다.  
  
```sql  
select session_id, command, blocking_session_id, wait_time, wait_type, wait_resource   
from sys.dm_exec_requests where command = 'DB STARTUP'  
```  
  
 다시 실행 스레드가 차단 해제된 보고 워크로드를 완료하도록 하거나 차단 세션 ID에 대해 [KILL&#40;Transact-SQL&#41;](~/t-sql/language-elements/kill-transact-sql.md) 명령을 실행하여 다시 실행 스레드를 즉시 차단 해제할 수 있습니다.  
  
##  <a name="BKMK_REDOBEHIND"></a> 리소스 경합으로 인한 다시 실행 스레드 뒤처짐  
 보조 복제본에 대한 큰 보고 워크로드 때문에 보조 복제본의 성능이 느려졌고 다시 실행 스레드가 뒤처졌습니다.  
  
### <a name="explanation"></a>설명  
 보조 복제본에 로그 기록을 적용할 때 다시 실행 스레드는 로그 디스크에서 로그 기록을 읽은 다음, 각 로그 기록에 대해 데이터 페이지에 접근하여 로그 기록을 적용합니다. 페이지 액세스는 페이지가 버퍼 풀에 아직 없는 경우 I/O 경계(물리적 디스크 액세스)일 수 있습니다. I/O 경계 보고 워크로드가 있는 경우 보고 워크로드가 다시 실행 스레드와 I/O 리소스를 경합하여 다시 실행 스레드가 느려질 수 있습니다. 이 경우는 업데이트된 데이터를 보는 다른 작업에 영향을 줄 뿐만 아니라 RTO에도 영향을 줍니다.  
  
### <a name="diagnosis-and-resolution"></a>진단 및 해결  
 다음 DMV 쿼리를 사용하여 `last_redone_lsn` 및 `last_received_lsn` 사이의 간격 차를 측정하면 다시 실행 스레드가 얼마나 뒤처졌는지 확인할 수 있습니다.  
  
```sql  
select recovery_lsn, truncation_lsn, last_hardened_lsn, last_received_lsn,   
   last_redone_lsn, last_redone_time  
from sys.dm_hadr_database_replica_states  
  
```  
  
 다시 실행 스레드가 실제로 뒤처진 경우 보조 복제본에 대해 성능 저하의 근본 원인을 조사해야 합니다. 보고 워크로드와의 I/O 경합이 있는 경우 [Resource Governor](~/relational-databases/resource-governor/resource-governor.md)를 사용하여 보고 워크로드가 실행되는 I/O 사이클을 간접적으로 제어하는 데 사용되는 CPU 사이클을 어느 정도 제어할 수 있습니다. 예를 들어 보고 워크로드가 CPU의 10%를 사용하지만 워크로드가 I/O 경계인 경우 Resource Governor를 사용하여 CPU 리소스 사용량을 5%로 제한하면 읽기 워크로드를 제한하여 I/O에 대한 영향을 최소화할 수 있습니다.  
  
## <a name="next-steps"></a>다음 단계  
 [SQL Server 2008의 성능 문제 해결](https://msdn.microsoft.com/library/dd672789(v=sql.100).aspx) 
  
  