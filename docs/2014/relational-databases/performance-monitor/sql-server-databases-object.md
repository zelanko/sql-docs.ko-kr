---
title: SQL Server, Databases 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Databases object
- SQLServer:Databases
- Availability Groups [SQL Server], performance counters
ms.assetid: a7f9e7d4-fff4-4c72-8b3e-3f18dffc8919
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b4c0c7a5626f3eb48509d7a4cfbf239f7cb931da
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52776425"
---
# <a name="sql-server-databases-object"></a>SQL Server, Databases 개체
  SQL Server의 **SQLServer:Databases** 개체는 대량 복사 작업, 백업 및 복원 처리량, 트랜잭션 로그 동작을 모니터링하기 위해 카운터를 제공합니다. 트랜잭션 및 트랜잭션 로그를 모니터링하면 데이터베이스에서 사용자 작업이 일어나는 횟수와 트랜잭션 로그가 얼마나 기록되었는지 확인할 수 있습니다. 사용자 작업의 양은 데이터베이스의 성능을 결정하고 로그 크기, 잠금 및 복제에 영향을 줍니다. 낮은 수준의 로그 작업을 모니터링하여 사용자 작업 및 리소스 사용을 측정하면 성능 병목 상태를 분석할 때 유용합니다.  
  
 개별 데이터베이스를 나타내는 **Databases** 개체의 여러 가지 인스턴스를 동시에 모니터링할 수도 있습니다.  
  
 이 표에서는 SQL Server **Databases** 카운터를 설명합니다.  
  
|SQL Server Databases 카운터|Description|  
|-----------------------------------|-----------------|  
|**Active Transactions**|데이터베이스에 대한 활성 트랜잭션 수입니다.|  
|**Backup/Restore Throughput/sec**|데이터베이스 백업 및 복원 작업에 대한 초당 읽기/쓰기 처리량입니다. 예를 들어 백업 디바이스를 병렬로 추가해 사용하거나 속도가 더 빠른 디바이스를 사용할 때 데이터베이스 백업 성능이 어떻게 변하는지 측정할 수 있습니다. 데이터베이스 백업 및 복원 작업의 처리량으로 사용자의 백업 및 복원 작업의 진행 상태와 성능을 확인할 수 있습니다.|  
|**Bulk Copy Rows/sec**|초당 대량 복사되는 행 수입니다.|  
|**Bulk Copy Throughput/sec**|초당 대량 복사되는 데이터 양(KB)입니다.|  
|**Commit table entries**|데이터베이스의 커밋 테이블에 대한 메모리 내 부분의 크기입니다. 자세한 내용은 [sys.dm_tran_commit_table&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table)을 참조하세요.|  
|**Data File(s) Size (KB)**|모든 자동 증가를 포함한 데이터베이스에 있는 모든 데이터 파일의 총 크기(KB)입니다. 이 카운터를 모니터링하면 **tempdb**의 크기 등을 확인할 때 유용합니다.|  
|**DBCC Logical Scan Bytes/sec**|DBCC(데이터베이스 콘솔 명령)의 초당 논리적 읽기 검색 바이트 수입니다.|  
|**Log Cache Hit Ratio**|로그 캐시에서 충족된 로그 캐시 읽기 비율입니다.|  
|**Log Cache Reads/sec**|로그 관리자 캐시를 통해 수행된 초당 읽기입니다.|  
|**Log File(s) Size (KB)**|데이터베이스에 있는 모든 트랜잭션 로그 파일의 총 크기(KB)입니다.|  
|**Log File(s) Used Size (KB)**|데이터베이스에서 사용된 모든 로그 파일의 총 크기입니다.|  
|**Log Flush Wait Time**|로그를 플러시하는 총 대기 시간(밀리초)입니다. AlwaysOn 보조 데이터베이스에서 이 값은 로그 레코드가 디스크에 확정될 때까지의 대기 시간을 나타냅니다.|  
|**Log Flush Waits/sec**|로그 플러시를 기다리는 초당 커밋 수입니다.|  
|**Log Flush Write Time (ms)**|마지막 1초 동안 완료된 로그 플러시의 쓰기를 수행하는 데 소요된 시간(밀리초)입니다.|  
|**Log Flushes/sec**|초당 로그 플러시 수입니다.|  
|**Log Growths**|데이터베이스에 대한 트랜잭션 로그가 확장된 총 횟수입니다.|  
|**Log Shrinks**|데이터베이스에 대한 트랜잭션 로그가 축소된 총 횟수입니다.|  
|**Log Pool Cache Misses/sec**|로그 풀에서 로그 블록을 사용할 수 없었던 요청 수입니다. *로그 풀* 은 트랜잭션 로그의 메모리 내 캐시입니다. 이 캐시는 복구, 트랜잭션 복제, 롤백 및 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]용 로그 읽기를 최적화하는 데 사용됩니다.|  
|**Log Pool Disk Reads/sec**|논리 블록을 인출하기 위해 로그 풀에서 실행한 디스크 읽기 수입니다.|  
|**Log Pool Requests/sec**|로그 풀에서 처리된 로그 블록 요청 수입니다.|  
|**Log Truncations**|트랜잭션 로그가 축소된 횟수입니다.|  
|**Percent Log Used**|사용 중인 로그에 있는 공백의 비율입니다.|  
|**Repl. Pending Xacts**|복제하도록 표시되었지만 배포 데이터베이스에는 아직 배달되지 않은 게시 데이터베이스의 트랜잭션 로그에 있는 트랜잭션 수입니다.|  
|**Repl. Trans. Rate**|게시 데이터베이스의 트랜잭션 로그에서 읽어서 배포 데이터베이스로 배달된 트랜잭션 수입니다.|  
|**Shrink Data Movement Bytes/sec**|자동 축소 작업이나 DBCC SHRINKDATABASE 또는 DBCC SHRINKFILE 문에 의해 이동된 초당 데이터 양입니다.|  
|**Tracked transactions/sec**|데이터베이스의 커밋 테이블에 기록된 커밋된 트랜잭션의 수입니다.|  
|**Transactions/sec**|데이터베이스에 대해 시작된 초당 트랜잭션 수입니다.<br /><br /> **Transactions/sec** 는 XTP 전용 트랜잭션(고유하게 컴파일된 저장 프로시저를 통해 시작된 트랜잭션)을 계산하지 않습니다.|  
|**Write Transactions/sec**|마지막 1초 동안 데이터베이스에 쓰고 커밋된 트랜잭션 수입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Serve, 데이터베이스 복제본](sql-server-database-replica.md)  
  
  
