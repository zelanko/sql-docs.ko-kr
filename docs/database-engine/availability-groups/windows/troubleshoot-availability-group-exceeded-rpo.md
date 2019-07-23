---
title: '문제 해결: 가용성 그룹 초과 RPO(SQL Server) | Microsoft Docs'
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 38de1841-9c99-435a-998d-df81c7ca0f1e
author: rothja
ms.author: jroth
ms.openlocfilehash: ef5ec5b9bd72fbda8c5a57547c1e1b74f9538a6a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013742"
---
# <a name="troubleshoot-availability-group-exceeded-rpo"></a>문제 해결: 가용성 그룹 초과 RPO
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  비동기 커밋 보조 복제본에 대한 가용성 그룹에 강제 수동 장애 조치(failover)를 수행한 후 데이터 손실이 RPO(복구 지점 목표)보다 많은 것을 발견할 수 있습니다. 또는 [Always On 가용성 그룹에 대한 성능 모니터링](monitor-performance-for-always-on-availability-groups.md)의 방법을 사용하여 비동기 커밋 보조 복제본의 잠재적 데이터 손실을 계산할 때 RPO 초과를 발견할 수 있습니다.  
  
 동기 커밋 보조 복제본은 데이터 손실 없음을 보증하지만 비동기 커밋 보조 복제본의 잠재적 데이터 손실은 보조 복제본에 확정되어 아직 대기 중인 로그의 양에 따라 달라집니다.  
  
 다음 섹션에서는 서버 인스턴스에 가용성 그룹과 무관한 시스템 성능 문제가 없다고 가정하고 비동기 커밋 보조 복제본의 높은 잠재적 데이터 손실의 일반적인 원인을 설명합니다.  
  
1.  [높은 네트워크 대기 시간 또는 낮은 네트워크 처리량이 주 복제본에 로그 축적 유발](#BKMK_LATENCY)  
  
2.  [디스크 I/O 병목 상태로 보조 복제본에 확정된 로그 속도 저하](#BKMK_IO_BOTTLENECK)  
  
##  <a name="BKMK_LATENCY"></a> 높은 네트워크 대기 시간 또는 낮은 네트워크 처리량이 주 복제본에 로그 축적 유발  
 자체의 RPO를 초과하는 데이터베이스의 가장 일반적인 원인은 보조 복제본으로 충분히 빠르게 전송될 수 없기 때문입니다.  
  
### <a name="explanation"></a>설명  
 주 복제본은 보조 복제본으로 전송된 승인되지 않은 최대 허용 메시지 수를 초과하는 경우 로그 전송에 대한 흐름 제어를 활성화합니다. 이러한 메시지의 일부가 승인될 때까지 로그 블록이 보조 복제본으로 전송될 수 없습니다. 데이터 손실은 보조 복제본에서 확정된 경우에만 방지할 수 있으므로 전송되지 않은 로그 메시지가 축적되면 잠재적 데이터 손실이 증가합니다.  
  
### <a name="diagnosis-and-resolution"></a>진단 및 해결  
 보조 복제본으로 다시 전송된 메시지 수가 많은 것은 높은 네트워크 대기 시간 및 네트워크 노이즈를 나타낼 수 있습니다. 또한 DMV 값 **log_send_rate**를 성능 개체의 초당 플러시된 로그 바이트 수(Log Bytes Flushed/sec)와 비교할 수 있습니다. 로그가 전송되는 것보다 더 빠르게 디스크로 플러시되면 잠재적 데이터 손실이 무한히 증가할 수 있습니다.  
  
 또한 두 성능 개체 `SQL Server:Availability Replica > Flow Control Time (ms/sec)` 및 `SQL Server:Availability Replica > Flow Control/sec`를 확인하는 것도 유용합니다. 이러한 두 값을 곱하면 흐름 제어가 해제될 때까지 대기하는 데 소비한 최종 시간이 나타납니다. 흐름 제어 대기 시간이 길수록 전송 속도가 더 느립니다.  
  
 다음 메트릭은 네트워크 대기 시간 및 처리량 진단에 유용합니다. **ping.exe** 및 [네트워크 모니터](https://www.microsoft.com/download/details.aspx?id=4865) 등 다른 Windows 도구를 사용하여 대기 시간 및 네트워크 사용률을 평가할 수 있습니다.  
  
-   DMV `sys.dm_hadr_database_replica_states, log_send_queue_size`  
  
-   DMV `sys.dm_hadr_database_replica_states, log_send_rate`  
  
-   성능 카운터 `SQL Server:Database > Log Bytes Flushed/sec`  
  
-   성능 카운터 `SQL Server:Database Mirroring > Send/Receive Ack Time`  
  
-   성능 카운터 `SQL Server:Availability Replica > Bytes Sent to Replica/sec`  
  
-   성능 카운터 `SQL Server:Availability Replica > Bytes Sent to Transport/sec`  
  
-   성능 카운터 `SQL Server:Availability Replica > Flow Control Time (ms/sec)`  
  
-   성능 카운터 `SQL Server:Availability Replica > Flow Control/sec`  
  
-   성능 카운터 `SQL Server:Availability Replica > Resent Messages/sec`  

이 문제를 해결하려면 네트워크 대역폭을 업그레이드하거나 불필요한 네트워크 트래픽을 제거하거나 줄여 보십시오.  


##  <a name="BKMK_IO_BOTTLENECK"></a> 디스크 I/O 병목 상태로 보조 복제본에 확정된 로그 속도 저하  
 데이터베이스 파일 배포에 따라 로그 확정은 보고 워크로드와의 I/O 경합 때문에 느려질 수 있습니다.  
  
### <a name="explanation"></a>설명  
 로그 블록이 로그 파일에서 확정되자마자 데이터 손실이 방지됩니다. 그러므로 로그 파일을 데이터 파일에서 격리하는 것이 중요합니다. 로그 파일 및 데이터 파일이 모두 같은 하드 디스크로 매핑된 경우 데이터 파일에 대한 읽기 횟수가 많은 보고 워크로드는 로그 확정 작업에 필요한 것과 같은 I/O 리소스를 사용합니다. 로그 확정이 느리면 주 복제본에 대한 승인이 느려져서 흐름 제어의 과도한 활성화 및 긴 흐름 제어 대기 시간을 유발할 수 있습니다.  
  
### <a name="diagnosis-and-resolution"></a>진단 및 해결  
 네트워크가 높은 대기 시간 또는 낮은 처리량을 겪지 않는 것을 확인했으면 보조 복제본에 대해 I/O 경합을 조사해야 합니다. [SQL Server: 디스크 I/O 최소화](https://technet.microsoft.com/magazine/jj643251.aspx)의 쿼리는 경합 식별에 유용합니다. 해당 문서의 예제를 편의상 아래에 인용합니다.  
  
 다음 스크립트를 사용하여 SQL Server의 모든 인스턴스에서 실행 중인 모든 가용성 데이터베이스의 각 데이터 및 로그 파일에 대한 읽기 및 쓰기 횟수를 볼 수 있습니다. 이는 평균 I/O 정지 시간(밀리초) 기준으로 정렬됩니다. 참고로 숫자는 서버 인스턴스가 시작된 마지막 시간부터 누적되었습니다. 그러므로 어느 정도 시간이 경과한 후 두 측정값 간의 차를 가져와야 합니다.  
  
```sql  
SELECT DB_NAME(database_id) AS   
   [Database Name] ,   
   file_id ,   
   io_stall_read_ms ,   
   num_of_reads ,   
   CAST(io_stall_read_ms / ( 1.0 + num_of_reads ) AS NUMERIC(10, 1)) AS [avg_read_stall_ms] ,   
   io_stall_write_ms ,   
   num_of_writes ,  
   CAST(io_stall_write_ms / ( 1.0 + num_of_writes ) AS NUMERIC(10, 1)) AS [avg_write_stall_ms] ,   
   io_stall_read_ms + io_stall_write_ms AS [io_stalls] ,   
   num_of_reads + num_of_writes AS [total_io] ,   
   CAST(( io_stall_read_ms + io_stall_write_ms ) / ( 1.0 + num_of_reads  
+ num_of_writes) AS NUMERIC(10,1)) AS [avg_io_stall_ms]  
FROM sys.dm_io_virtual_file_stats(NULL, NULL)  
WHERE DB_NAME(database_id) IN (SELECT DISTINCT database_name FROM sys.dm_hadr_database_replica_cluster_states)  
ORDER BY avg_io_stall_ms DESC;  
```  
  
 이러한 다음 쿼리는 시스템에 보류 중인 I/O 요청의 지정 시간(누적이 아닌) 스냅샷을 제공합니다.  
  
```sql  
SELECT DB_NAME(mf.database_id) AS [Database] ,   
   mf.physical_name ,  
   r.io_pending ,   
   r.io_pending_ms_ticks ,   
   r.io_type ,   
   fs.num_of_reads ,   
   fs.num_of_writes  
FROM sys.dm_io_pending_io_requests AS r   
INNER JOIN sys.dm_io_virtual_file_stats(NULL, NULL) AS fs ON r.io_handle = fs.file_handle   
INNER JOIN sys.master_files AS mf ON fs.database_id = mf.database_id  
AND fs.file_id = mf.file_id  
ORDER BY r.io_pending , r.io_pending_ms_ticks DESC;  
```  
  
 읽기 I/O 및 쓰기 I/O가 서로 일치하는 방법을 비교하여 I/O 경합을 식별할 수 있습니다.  
  
 다음은 I/O 병목 상태를 진단하는 데 도움이 될 수 있는 몇 가지 다른 성능 카운터입니다.  
  
-   **물리적 디스크: 모든 카운터**  
  
-   **물리적 디스크: Avg. Disk sec/Transfer**  
  
-   **SQL Server: 데이터베이스 > 로그 플러시 대기 시간**  
  
-   **SQL Server: 데이터베이스 > 로그 플러시 대기/초**  
  
-   **SQL Server: 데이터베이스 > 로그 풀 디스크 읽기 횟수/초**  
  
 I/O 병목 상태를 식별하고 로그 파일 및 데이터 파일을 같은 하드 디스크에 저장한 경우 가장 먼저 수행해야 할 일은 데이터 파일 및 로그 파일을 서로 다른 디스크에 저장하는 것입니다. 이 모범 사례는 보고 워크로드가 주 복제본에서 로그 버퍼까지의 로그 전송 경로 및 보조 복제본에서의 트랜잭션을 확정하는 기능을 방해하지 않도록 합니다.  
  
## <a name="next-steps"></a>다음 단계  
 [SQL Server의 성능 문제 해결(SQL Server 2012에 적용)](https://msdn.microsoft.com/library/dd672789(v=SQL.100).aspx)  
  
  
