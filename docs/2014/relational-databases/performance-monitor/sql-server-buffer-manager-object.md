---
title: SQL Server, Buffer Manager 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Buffer Manager object
- SQLServer:Buffer Manager
ms.assetid: 9775ebde-111d-476c-9188-b77805f90e98
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ed9c8ff90798205f9db02ae4b4b47eb4310d4b06
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63250758"
---
# <a name="sql-server-buffer-manager-object"></a>SQL Server, Buffer Manager 개체
  **Buffer Manager** 개체는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 다음 항목을 어떻게 사용하는지 모니터링하는 카운터를 제공합니다.  
  
-   데이터 페이지를 저장하기 위한 메모리  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 데이터베이스 페이지를 읽고 쓸 때 실제 I/O를 모니터링하는 카운터  
  
-   SSD(솔리드 스테이트 드라이브)와 같은 빠른 비휘발성 스토리지를 사용하여 버퍼 캐시를 확장하는 버퍼 풀 확장  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용되는 메모리 및 카운터를 모니터링하면 다음 사항을 확인하는 데 도움이 됩니다.  
  
-   실제 메모리 부족으로 인해 병목 상태가 발생하는지 확인합니다. 캐시에서 자주 액세스하는 데이터를 저장할 수 없는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 디스크에서 데이터를 검색해야 합니다.  
  
-   메모리를 추가하거나 데이터 캐시 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 구조에 사용 가능한 메모리를 늘리면 쿼리 성능을 증가시킬 수 있는지 확인합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 디스크에서 데이터를 얼마나 자주 읽을 필요가 있는지 확인합니다. 실제 I/O는 메모리 액세스와 같은 다른 작업과 비교해서 시간이 더 오래 걸립니다. 실제 I/O를 최소화하면 쿼리 성능을 향상시킬 수 있습니다.  
  
## <a name="buffer-manager-performance-objects"></a>버퍼 관리자 성능 개체  
 이 테이블에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Buffer Manager** 성능 개체에 대해 설명합니다.  
  
|SQL Server Buffer Manager 카운터|Description|  
|----------------------------------------|-----------------|  
|**버퍼 캐시 적중률**|디스크에서 읽지 않고 버퍼 캐시에서 찾은 페이지 비율을 나타냅니다. 이 비율은 마지막 몇 천 페이지 액세스에 대한 총 캐시 조회 수로 나눈 총 캐시 적중 수입니다. 시간이 많이 지나면 이 비율은 일정해집니다. 캐시에서 읽는 것이 디스크에서 읽는 것보다 비용이 적게 들기 때문에 이 비율을 높이는 것이 좋습니다. 일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 사용할 수 있는 메모리 양을 늘리거나 버퍼 풀 확장 기능을 사용하여 buffer cache hit ratio를 높일 수 있습니다.|  
|**Checkpoint pages/sec**|모든 더티 페이지를 플러시해야 할 기타 작업이나 검사점에 의해 디스크에 플러시된 초당 페이지 수를 나타냅니다.|  
|**Database pages**|버퍼 풀에서 데이터베이스 내용이 있는 페이지 수를 나타냅니다.|  
|**Extension allocated pages**|버퍼 풀 확장 파일에서 이미 사용된 캐시 페이지의 총 수입니다.|  
|**Extension free pages**|버퍼 풀 확장 파일에서 사용되지 않은 캐시 페이지의 총 수입니다.|  
|**Extension in use as percentage**|버퍼 관리자 페이지가 차지하는 버퍼 풀 확장 페이징 파일의 비율입니다.|  
|**Extension outstanding IO counter**|버퍼 풀 확장 파일에 대한 I/O 큐 길이입니다.|  
|**Extension page evictions/sec**|초당 버퍼 풀 확장 파일에서 제거되는 페이지 수입니다.|  
|**Extension page reads/sec**|초당 버퍼 풀 확장 파일에서 읽어오는 페이지 수입니다.|  
|**Extension page unreferenced time**|페이지가 참조되지 않은 채 버퍼 풀 확장에 남아 있는 평균 시간(초)입니다.|  
|**Extension pages writes/sec**|초당 버퍼 풀 확장 파일에 쓰여지는 페이지 수입니다.|  
|**Free list stalls/sec**|사용 가능한 페이지를 기다린 초당 요청 수를 나타냅니다.|  
|**Lazy writes/sec**|버퍼 관리자의 지연 기록기가 기록한 초당 버퍼 수를 나타냅니다. *지연 기록기* 는 에이징된 더티 버퍼(다른 페이지에 버퍼를 다시 사용하려면 해당 변경 내용을 디스크에 다시 써야 하는 버퍼)의 일괄 처리를 플러시하는 시스템 프로세스이며 이러한 버퍼를 사용자 프로세스에 사용할 수 있게 합니다. 지연 기록기를 사용하면 사용 가능한 버퍼를 만들기 위해 자주 검사점을 수행할 필요가 없습니다.|  
|**Page life expectancy**|페이지가 참조 없이 버퍼 풀에 남아 있는 시간(초)을 나타냅니다.|  
|**Page lookups/sec**|버퍼 풀에서 페이지를 찾기 위한 초당 요청 수를 나타냅니다.|  
|**Page reads/sec**|실행한 물리적 데이터베이스 페이지 초당 읽기 수를 나타냅니다. 이 통계는 모든 데이터베이스에 걸친 총 실제 읽기 수를 나타냅니다. 실제 I/O는 비용이 많이 들기 때문에 용량이 큰 데이터 캐시나 인텔리전트 인덱스, 더 효율적인 쿼리를 사용하거나 데이터베이스 디자인을 바꾸면 비용을 최소화할 수 있습니다.|  
|**Page writes/sec**|실행한 물리적 데이터베이스 페이지 초당 쓰기 수를 나타냅니다.|  
|**Readahead pages/sec**|사용을 미리 예측하여 읽은 초당 페이지 수를 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server: Buffer 노드](sql-server-buffer-node.md)   
 [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [SQL Server, 계획 캐시 개체](sql-server-plan-cache-object.md)   
 [시스템 모니터 &#40;리소스 사용량 모니터링&#41;](monitor-resource-usage-system-monitor.md)   
 [dm_os_performance_counters &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)   
 [Buffer Pool Extension](../../database-engine/configure-windows/buffer-pool-extension.md)  
  
  
