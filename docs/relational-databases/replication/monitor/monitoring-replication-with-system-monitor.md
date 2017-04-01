---
title: "시스템 모니터로 복제 모니터링 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "성능 모니터링 [SQL Server 복제], 시스템 모니터"
  - "시스템 모니터 [SQL Server], 복제"
  - "성능 카운터 [SQL Server 복제]"
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# 시스템 모니터로 복제 모니터링
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 시스템 모니터를 사용 하면 그래프, 차트 및 보고서를 사용 하 여 사용자 컴퓨터의 효율성을 측정 하 고 파악 하 고 (예: 리소스 사용의 불균형된, 하드웨어 부족, 또는 잘못 된 프로그램 디자인) 문제를 해결 추가 하드웨어 요구 사항에 대 한 계획을 수 있습니다. 자세한 내용은 참조 [리소스 사용 모니터링 & #40; 시스템 모니터 & #41;](../../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)합니다.  
  
 시스템 모니터는 여러 가지 프로세스의 성능에 대한 정보를 제공하는 성능 개체 및 카운터를 사용합니다. 복제 에이전트와 관련된 카운터를 통해 복제 성능을 측정할 수 있습니다.  
  
|에이전트|성능 개체|카운터|설명|  
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
  
## 참고 항목  
 [모니터링 및 #40입니다. 복제 및 #41;](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  