---
title: SQL Server:Buffer Node | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Buffer Node
- Buffer Node object
ms.assetid: fd3f9f0f-7c38-4cfd-a0c5-ee93dd52d9a5
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 9011394dccf472499c1c8a8bd1023b7c23009883
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67987216"
---
# <a name="sql-serverbuffer-node"></a>SQL Server:Buffer Node
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Buffer Node** 개체는 **Buffer Manager** 개체가 제공하는 카운터를 보완하는 카운터를 제공합니다. 이 카운터를 사용하여 각 NUMA(Non-Uniform Memory Access) 노드에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버퍼 풀 페이지 배포를 모니터링할 수 있습니다. 사용 중인 각 NUMA 노드에 대해 하나의 **Buffer Node** 개체 인스턴스가 있습니다. 비-NUMA 아키텍처에는 단일 **Buffer Node** 개체 인스턴스가 있습니다.  
  
## <a name="buffer-node-performance-objects"></a>Buffer Node 성능 개체  
 이 테이블에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Buffer Node** 성능 개체에 대해 설명합니다.  
  
|SQL Server Buffer Node 카운터|Description|  
|-------------------------------------|-----------------|  
|**Database pages**|이 노드의 버퍼 풀에서 데이터베이스 내용이 있는 페이지 수를 나타냅니다.|  
|**Page life expectancy**|페이지가 참조 없이 이 노드의 버퍼 풀에 남아 있는 최소 시간(초)을 나타냅니다.|  
|**Local Node page lookups/sec**|이 노드에서 충족된 조회 요청 수를 나타냅니다.|  
|**Remote Note page lookups/sec**|다른 노드에서 충족된 이 노드의 조회 요청 수를 나타냅니다.|  
  
 비-NUMA 하드웨어에서 SQL Server를 실행하는 경우 **Buffer Node** 및 **Buffer Manager** 개체의 카운터가 일치해야 합니다.  
  
 NUMA 하드웨어에서 모든 **Buffer Nodes** 의 각 카운터 합계는 **Buffer Manager**의 해당 합계와 일치해야 합니다.  
  
> [!NOTE]  
>  카운터의 동적 특성과 샘플링 정확도 때문에 카운터 값과 합계가 정확하게 일치하지 않을 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server, Buffer Manager 개체](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.dm_os_performance_counters&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  
