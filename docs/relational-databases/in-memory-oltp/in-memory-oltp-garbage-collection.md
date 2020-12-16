---
title: 메모리 내 OLTP 가비지 수집 | Microsoft 문서
description: SQL Server에서 메모리 내 OLTP의 가비지 수집에 대해 알아봅니다. 더 이상 활성 상태가 아닌 트랜잭션이 행을 삭제하면 가비지 수집이 적용됩니다.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 940140a7-4785-46fc-8bf4-151435dccd3c
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b5b9060049965e9a826d3f9f22a1e6eb341ca0dc
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485295"
---
# <a name="in-memory-oltp-garbage-collection"></a>메모리 내 OLTP 가비지 수집
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  데이터 행은 더 이상 활성화되지 않는 트랜잭션에서 삭제된 경우 유효하지 않은 것으로 간주됩니다. 유효하지 않은 행에는 가비지 수집을 수행할 수 있습니다. [!INCLUDE[hek_2](../../includes/hek-2-md.md)]에서 가비지 수집의 특성은 다음과 같습니다.  
  
-   비중단. 가비지 수집은 시간이 지남에 따라 작업에 미치는 영향을 최소화하면서 배포됩니다.  
  
-   공동. 사용자 트랜잭션이 기본 가비지 수집 스레드와 함께 가비지 수집에 참여합니다.  
  
-   효율. 사용자 트랜잭션은 사용 중인 액세스 경로(인덱스)에서 유효하지 않은 행의 연결을 해제합니다. 이로 인해 행이 최종적으로 제거되면 필요한 작업을 축소합니다.  
  
-   응답. 메모리 가중에 따라 적극적인 가비지 수집을 수행합니다.  
  
-   확장 가능. 커밋 후 사용자 트랜잭션에서 가비지 수집 작업 중 일부를 수행합니다. 트랜잭션 활동이 많을수록 더 많은 트랜잭션에서 유효하지 않은 행의 연결을 해제합니다.  
  
 가비지 수집은 기본 가비지 수집 스레드에서 제어됩니다. 기본 가비지 수집 스레드는 매분 또는 커밋된 트랜잭션 수가 내부 임계값을 초과할 때 실행됩니다. 가비지 수집의 태스크는 다음을 수행하는 것입니다.  
  
-   행 집합을 삭제하거나 업데이트하는 트랜잭션 및 가장 오래된 활성 트랜잭션 전에 커밋된 트랜잭션을 식별합니다.  
  
-   이러한 이전 트랜잭션에서 생성된 행 버전을 식별합니다.  
  
-   각각 16행으로 구성된 하나 이상의 단위로 이전 행을 그룹화합니다. 이 작업은 가비지 수집기의 작업을 더 작은 단위로 분배하기 위해 수행됩니다.  
  
-   이러한 작업 단위를 각 스케줄러의 가비지 수집 큐로 이동합니다. 자세한 내용은 다음 가비지 수집기 DMV를 참조하세요. [sys.dm_xtp_gc_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-stats-transact-sql.md), [sys.dm_db_xtp_gc_cycle_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-gc-cycle-stats-transact-sql.md) 및 [sys.dm_xtp_gc_queue_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-queue-stats-transact-sql.md)  
  
 사용자 트랜잭션은 커밋 후 실행에 사용된 스케줄러와 연결된 큐에서 모든 큐 항목을 식별한 다음 메모리를 해제합니다. 스케줄러에서 가비지 수집 큐가 비어 있으면 현재 NUMA 노드에서 비어 있지 않은 큐를 검색합니다. 트랜잭션 활동이 적고 메모리 가중이 있는 경우 기본 가비지 수집기 스레드가 개입하여 어떤 큐에서든 행의 가비지 수집에 액세스할 수 있습니다. 예를 들어 많은 수의 행을 삭제한 후 트랜잭션 활동이 없고 메모리 가중이 없는 경우 트랜잭션 활동이 다시 시작되거나 메모리 가중이 있을 때까지 삭제된 행에서 가비지를 수집하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP의 메모리 관리](/previous-versions/sql/sql-server-2016/dn465872(v=sql.130))  
  
