---
title: "SQL Server XTP 데이터베이스 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server 2016 XTP Databases
ms.assetid: 488ff55e-173f-43f6-9bdb-67b35e7cebfe
caps.latest.revision: 3
author: dagiro
ms.author: v-dagir
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e2839d276956db1b82bf6b1f236ceae74b973477
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-xtp-databases"></a>SQL Server XTP 데이터베이스
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

**SQL Server XTP 데이터베이스** 성능 개체는 메모리 내 OLTP 데이터베이스 관련 카운터를 제공합니다.

> [!NOTE]
>  SQL Server XTP 데이터베이스 카운터는 현재 sys.dm_os_performance_counters에서 표시되지 않습니다.  카운터는 [시스템 모니터](../../relational-databases/performance/start-system-monitor-windows.md)에서 볼 수 있습니다.

이 표에서는 **SQL Server XTP Databases** 카운터를 설명합니다.

|카운터|Description| 
|-------------|-----------------|  
|**Avg Transaction Segment Large Data Size**|트랜잭션 세그먼트 대규모 데이터 페이로드의 평균 크기입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**Avg Transaction Segment Size**|트랜잭션 세그먼트 페이로드의 평균 크기입니다. 이 값이 0이 되면 백엔드 할당자로부터 더 많은 페이지가 할당됩니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**Flush Thread 256K Queue Depth**|256K IO 요청 수에 대한 플러시 스레드 큐 크기입니다.|
|**Flush Thread 4K Queue Depth**|4K IO 요청 수에 대한 플러시 스레드 큐 크기입니다.|
|**Flush Thread 64K Queue Depth**|64K IO 요청 수에 대한 플러시 스레드 큐 크기입니다.|
|**Flush Thread Frozen IOs/sec (256K)**|플러시 페이지 처리 중 고정 임계값보다 높아 수행할 수 없다고 발견된 256K IO 요청 수입니다.|
|**Flush Thread Frozen IOs/sec (4K)**|플러시 페이지 처리 중 고정 임계값보다 높아 수행할 수 없다고 발견된 4K IO 요청 수입니다.|
|**Flush Thread Frozen IOs/sec (64K)**|플러시 페이지 처리 중 고정 임계값보다 높아 수행할 수 없다고 발견된 64K IO 요청 수입니다.|
|**IoPagePool256K Free List Count**|256K IO 페이지 풀 사용 가능 목록의 페이지 수입니다. 이 값이 0이 되면 백엔드 할당자로부터 더 많은 페이지가 할당됩니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**IoPagePool256K Total Allocated**|백엔드 할당자로부터 256K IO 페이지 풀에서 할당되고 유지되는 총 페이지 수입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**IoPagePool4K Free List Count**|4K IO 페이지 풀 사용 가능 목록의 페이지 수입니다. 이 값이 0이 되면 백엔드 할당자로부터 더 많은 페이지가 할당됩니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**IoPagePool4K Total Allocated**|백엔드 할당자로부터 4K IO 페이지 풀에서 할당되고 유지되는 총 페이지 수입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**IoPagePool64K Free List Count**|64K IO 페이지 풀 사용 가능 목록의 페이지 수입니다. 이 값이 0이 되면 백엔드 할당자로부터 더 많은 페이지가 할당됩니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**IoPagePool64K Total Allocated**|백엔드 할당자로부터 64K IO 페이지 풀에서 할당되고 유지되는 총 페이지 수입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**MtLog 256K Expand Count**|256K MtLog가 확장된 횟수입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**MtLog 256K IOs Outstanding**|MtLog에서 수행하여 처리 중인 256K IO 요청 수입니다.|
|**MtLog 256K Page Fill %/Page Flushed**|플러시된 각 256K MtLog 페이지의 평균 채우기 비율입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**MtLog 256K Write Bytes/sec**|256K MtLog 개체에서 초당 쓰기 바이트 수입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**MtLog 4K Expand Count**|4K MtLog가 확장된 횟수입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**MtLog 4K IOs Outstanding**|MtLog에서 수행하여 처리 중인 4K IO 요청 수입니다.|
|**MtLog 4K Page Fill %/Page Flushed**|플러시된 각 4K MtLog 페이지의 평균 채우기 비율입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**MtLog 4K Write Bytes/sec**|4K MtLog 개체에서 초당 쓰기 바이트 수입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**MtLog 64K Expand Count**|64K MtLog가 확장된 횟수입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**MtLog 64K IOs Outstanding**|MtLog에서 수행하여 처리 중인 64K IO 요청 수입니다.|
|**MtLog 64K Page Fill %/Page Flushed**|플러시된 각 64K MtLog 페이지의 평균 채우기 비율입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**MtLog 64K Write Bytes/sec**|64K MtLog 개체에서 초당 쓰기 바이트 수입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**Num Merges**|플라이트의 병합 수입니다.|
|**Num Merges/sec**|초당 생성된 병합 수입니다(평균).|
|**Num Serializations**|플라이트의 직렬화 수입니다.|
|**Num Serializations/sec**|초당 생성된 직렬화 수입니다(평균).|
|**Tail Cache Page Count**|비상 캐시에 할당된 페이지 수입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|
|**Tail Cache Page Count Peak**|비상 캐시에 할당된 최대 페이지 수입니다. 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|


## <a name="see-also"></a>관련 항목:  
[SQL Server XTP&#40;메모리 내 OLTP&#41; 성능 카운터](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)

