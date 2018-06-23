---
title: 시스템 모니터로 복제 모니터링 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- monitoring performance [SQL Server replication], System Monitor
- System Monitor [SQL Server], replication
- performance counters [SQL Server replication]
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
caps.latest.revision: 29
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 27a07add39848ff1ca4294fb3cd4bac3c067c0ac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172862"
---
# <a name="monitoring-replication-with-system-monitor"></a>시스템 모니터로 복제 모니터링
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 시스템 모니터를 사용하면 그래프, 차트 및 보고서를 통해 컴퓨터의 효율성을 측정하고, 발생할 수 있는 문제(리소스 사용의 불균형, 하드웨어 부족, 잘못된 프로그램 디자인 등)를 식별하고 해결하며, 그 밖의 하드웨어 요구에 대한 계획을 수립할 수 있습니다. 자세한 내용은 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../performance-monitor/monitor-resource-usage-system-monitor.md)을 참조하세요.  
  
 시스템 모니터는 여러 가지 프로세스의 성능에 대한 정보를 제공하는 성능 개체 및 카운터를 사용합니다. 복제 에이전트와 관련된 카운터를 통해 복제 성능을 측정할 수 있습니다.  
  
|에이전트|성능 개체|카운터|Description|  
|-----------|------------------------|-------------|-----------------|  
|모든 에이전트|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: 복제 에이전트|실행 중|현재 실행 중인 복제 에이전트 수입니다.|  
|스냅숏 에이전트|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Snapshot|스냅숏: Delivered Cmds/sec|배포자로 배달된 초당 명령 수입니다.|  
|스냅숏 에이전트|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Snapshot|스냅숏: Delivered Trans/sec|배포자로 배달된 초당 트랜잭션 수입니다.|  
|로그 판독기 에이전트|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Logreader|Logreader: Delivered Cmds/sec|배포자로 배달된 초당 명령 수입니다.|  
|로그 판독기 에이전트|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Logreader|Logreader: Delivered Trans/sec|배포자로 배달된 초당 트랜잭션 수입니다.|  
|로그 판독기 에이전트|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Logreader|Logreader: Delivery Latency|트랜잭션이 게시자에 적용되었다가 배포자로 배달되기까지 경과한 현재 시간(밀리초)입니다.|  
|배포 에이전트|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Dist.|Dist: Delivered Cmds/sec|구독자로 배달된 초당 명령 수입니다.|  
|배포 에이전트|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Dist.|Dist: Delivered Trans/sec|구독자로 배달된 초당 트랜잭션 수입니다.|  
|배포 에이전트|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Dist.|Dist: Delivery Latency|트랜잭션이 배포자로 배달되었다가 구독자에 적용되기까지 경과한 현재 시간(밀리초)입니다.|  
|병합 에이전트|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Merge|Conflicts/sec|병합 프로세스 중 발생하는 초당 충돌 수입니다.|  
|병합 에이전트|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Merge|Downloaded Changes/sec|게시자에서 구독자로 복제된 초당 행 수입니다.|  
|병합 에이전트|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication Merge|Uploaded Changes/sec|구독자에서 게시자로 복제된 초당 행 수입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [모니터링&#40;복제&#41;](../monitoring-replication.md)  
  
  