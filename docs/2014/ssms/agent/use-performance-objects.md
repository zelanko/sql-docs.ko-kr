---
title: 성능 개체 사용 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 724d921aaabafbe17adb96f48e679485247f8e92
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37301433"
---
# <a name="use-performance-objects"></a>성능 개체 사용
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에는 서비스 수행 방법을 모니터링하는 성능 개체와 카운터가 포함됩니다. 이러한 성능 개체를 사용하면 Windows 도구인 성능 모니터를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 백그라운드에서 수행하는 작업을 식별할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 현재 실행 중인 활성 작업 수를 확인하여 차단된 작업을 식별할 수 있습니다.  
  
 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 성능 개체와 카운터가 있습니다. 성능 개체는 각 개체가 나타내는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 따라 이름이 지정됩니다.  
  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 성능 개체의 이름 지정 방법을 보여 줍니다.  
  
|인스턴스 유형|개체 이름|  
|-------------------|-----------------|  
|Default|**SQLAgent:** *개체*:*카운터*|  
|명명된 형식|**SQLAgent$**<br /> ***instance_name* :** *개체*:*카운터*|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다음과 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 성능 개체가 포함됩니다.  
  
|개체 이름|Description|  
|-----------------|-----------------|  
|[SQLAgent:Jobs](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|시작된 작업, 성공률 및 현재 상태에 대한 성능 정보|  
|[SQLAgent:JobSteps](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|작업 단계에 대한 상태 정보|  
|[SQLAgent:Alerts](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|경고 및 알림 수에 대한 정보|  
|[SQLAgent:Statistics](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|일반 성능 정보|  
  
## <a name="see-also"></a>관련 항목  
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [시스템 모니터 시작&#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md)  
  
  
