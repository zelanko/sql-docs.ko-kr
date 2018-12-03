---
title: 리소스 사용 모니터링(시스템 모니터) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server], resource usage
- System Monitor [SQL Server], about Windows System Monitor
- resource usage monitoring [SQL Server]
- System Monitor [SQL Server]
- counters [SQL Server], resource usage subjects
- performance counters [SQL Server], resource usage subjects
- Windows System Monitor [SQL Server], about Windows System Monitor
- monitoring [SQL Server], server resource usage
- monitoring resource usage [SQL Server]
- Windows System Monitor [SQL Server]
- database monitoring [SQL Server], resource usage
- database performance [SQL Server], resource usage
- tuning databases [SQL Server], resource usage
- server performance [SQL Server], resource usage
ms.assetid: f2993a28-0b81-46f2-aec0-6877fe990387
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 22a27d64dcd7b6a1ae081d07c15092b32aa99ece
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158915"
---
# <a name="monitor-resource-usage-system-monitor"></a>리소스 사용 모니터링(시스템 모니터)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Microsoft Windows 서버 운영 체제를 실행 중인 경우 시스템 모니터 그래픽 도구를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 성능을 측정할 수 있습니다. 이 도구에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 및 성능 카운터를 보거나 프로세서, 메모리, 캐시, 스레드 및 프로세스 등 다른 개체의 동작을 볼 수 있습니다. 각 개체는 장치 사용, 큐 길이, 지연, 처리량 및 내부 정체의 기타 지표를 측정하는 관련 카운터 집합을 포함합니다.  
  
> [!NOTE]  
>  Windows NT 4.0 이후 버전에서는 성능 모니터가 시스템 모니터로 대체되었습니다.  
  
## <a name="benefits-of-system-monitor"></a>시스템 모니터의 이점  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능과 Windows 성능 간의 상관 관계를 확인하려면 Windows 운영 체제 카운터와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 카운터를 동시에 모니터링하는 것이 좋습니다. 예를 들어 Windows 디스크 입/출력(I/O) 카운터와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Buffer Manager 카운터를 동시에 모니터링하면 전체 시스템의 동작을 알 수 있습니다.  
  
 시스템 모니터를 사용하여 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업과 성능에 대한 통계를 얻을 수 있습니다. 시스템 모니터를 사용하여 다음을 수행할 수 있습니다.  
  
-   컴퓨터 수에 상관없이 동시에 데이터를 봅니다.  
  
-   현재 작업을 반영한 차트를 보거나 변경하고 사용자가 정의한 빈도에 따라 업데이트된 카운터 값을 표시합니다.  
  
-   추가 처리 및 인쇄를 위해 차트, 로그, 경고 로그, 보고서에서 스프레드시트나 데이터베이스 응용 프로그램으로 내보냅니다.  
  
-   경고 로그에 있는 이벤트를 나열하고 네트워크 경고를 발생시켜 사용자에게 알릴 수 있는 시스템 경고를 추가합니다.  
  
-   처음으로 카운터 값이 사용자가 정의한 값보다 크거나 작게 될 때 또는 그럴 때마다 매번 미리 정의한 응용 프로그램을 실행합니다.  
  
-   여러 컴퓨터의 다양한 개체에 대한 데이터를 포함한 로그 파일을 만듭니다.  
  
-   한 파일에 다른 기존 로그 파일에서 선택한 섹션을 추가하여 장기 보관 파일을 만듭니다.  
  
-   현재 작업 보고서를 보거나 기존 로그 파일로부터 보고서를 만듭니다.  
  
-   개별 차트, 경고, 로그, 보고서 설정 또는 전체 작업 영역 설정을 다시 사용할 수 있도록 저장합니다.  
  
    > [!NOTE]  
    >  Windows NT 4.0 이후로 시스템 모니터가 성능 모니터를 대체합니다. 시스템 모니터 또는 성능 모니터를 사용하여 이 태스크를 할 수 있습니다.  
  
## <a name="system-monitor-performance"></a>시스템 모니터 성능  
 성능 관련 문제를 검사하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Microsoft Windows 운영 체제를 모니터링할 때 초기에는 다음 3개 주요 영역을 집중적으로 모니터링합니다.  
  
-   디스크 작업  
  
-   프로세서 사용률  
  
-   메모리 사용  
  
 시스템 모니터가 실행 중인 컴퓨터를 모니터링하면 컴퓨터 성능에 약간의 영향을 줄 수 있으므로 시스템 모니터 데이터를 다른 디스크나 컴퓨터에 기록해 모니터링하는 컴퓨터에 미치는 영향을 줄이거나 시스템 모니터를 원격 컴퓨터에서 실행하십시오. 또한 관심 있는 카운터만 모니터링해야 합니다. 너무 많은 수의 카운터를 모니터링하면 모니터링 프로세스에 리소스 사용 오버헤드가 추가되고 모니터링하고 있는 컴퓨터의 성능에 영향을 미칩니다.  
  
## <a name="system-monitor-tasks"></a>시스템 모니터 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|시스템 모니터를 사용하는 경우에 대해 설명하고 시스템 모니터를 사용하는 경우의 성능 오버헤드에 대해 알아봅니다.|[시스템 모니터 실행](../../relational-databases/performance-monitor/run-system-monitor.md)|  
|디스크 카운터를 모니터링하여 SQL Server 구성 요소에서 생성된 I/O 양과 디스크 작업을 확인하는 방법에 대해 설명합니다.|[디스크 사용량 모니터링](../../relational-databases/performance-monitor/monitor-disk-usage.md)|  
|Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 모니터링하여 CPU 사용량이 정상 범위에 있는지를 확인하는 방법에 대해 설명합니다.|[CPU 사용량 모니터링](../../relational-databases/performance-monitor/monitor-cpu-usage.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 모니터링하여 메모리 사용이 일반적인 범위 이내에 있는지를 확인하는 방법에 대해 설명합니다.|[메모리 사용량 모니터링](../../relational-databases/performance-monitor/monitor-memory-usage.md)|  
|시스템 모니터 카운터의 임계값에 도달했을 때 발생하는 경고를 만드는 방법에 대해 설명합니다.|[SQL Server 데이터베이스 경고 만들기](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)|  
|차트, 경고, 로그 및 보고서를 만들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 모니터링하는 방법에 대해 설명합니다.|[차트, 경고, 로그 및 보고서 만들기](../../relational-databases/performance-monitor/create-charts-alerts-logs-and-reports.md)|  
|시스템 모니터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 실행 중인 컴퓨터에서 작업을 모니터링하는 데 사용하는 개체 및 카운터를 나열합니다.|[SQL Server 개체 사용](../../relational-databases/performance-monitor/use-sql-server-objects.md)|  
|시스템 모니터에서 메모리 내 OLTP 작업을 모니터링하는 데 사용하는 개체 및 카운터를 나열합니다.|[SQL Server XTP&#40;메모리 내 OLTP&#41; 성능 카운터](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)|  
  
  
