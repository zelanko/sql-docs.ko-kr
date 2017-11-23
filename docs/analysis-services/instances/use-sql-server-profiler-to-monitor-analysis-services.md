---
title: "SQL Server Profiler를 사용 하 여 Analysis Services 모니터링 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- performance [Analysis Services], SQL Server Profiler
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 8b77dafc-4584-4e93-8ad7-299304391bfd
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 5c25432e05a7cc2de57456fb056d7501c05bdb50
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="use-sql-server-profiler-to-monitor-analysis-services"></a>SQL Server Profiler를 사용하여 Analysis Services 모니터링
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 일괄 처리나 트랜잭션 시작 같은 엔진 프로세스 이벤트를 추적하여 이러한 이벤트에 대한 데이터를 캡처하므로 서버와 데이터베이스 작업(예: 사용자 쿼리 또는 로그인 작업)을 모니터할 수 있습니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블이나 파일에 캡처해 나중에 분석할 때 사용할 수 있으며 같거나 다른 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 캡처한 이벤트를 재생해 그 영향을 정확하게 확인할 수도 있습니다. 실시간이나 단계별로 이벤트를 재생할 수 있습니다. 같은 시스템에서 성능 카운터와 함께 추적 이벤트를 실행하는 것도 매우 유용합니다. 프로파일러는 시간을 기반으로 이 둘의 상관 관계를 지정하고 단일 시간대로 표시할 수 있습니다. 추적 이벤트는 세부 정보를 제공하고 성능 카운터는 집계 뷰를 제공합니다. 추적을 만들고 실행하는 방법에 대한 자세한 내용은 [재생에 대한 프로파일러 추적 만들기&#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)를 참조하세요.  
  
 다음 표에서는 이 섹션에서 다루는 항목에 대해 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[SQL Server 프로파일러를 사용한 Analysis Services 모니터링 소개](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 모니터링하는 방법에 대해 설명합니다.|  
|[재생에 대한 프로파일러 추적 만들기&#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 재생용 추적을 만들기 위한 요구 사항에 대해 설명합니다.|  
|[Analysis Services 추적 이벤트](../../analysis-services/trace-events/analysis-services-trace-events.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 이벤트 클래스에 대해 설명합니다. 이러한 이벤트 클래스는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 생성한 동작에 매핑되고 추적 재생에 사용됩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 인스턴스 모니터](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
  
