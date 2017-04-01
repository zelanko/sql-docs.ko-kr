---
title: "SQL Server 2016에서 사용되지 않는 Analysis Services 기능 | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Analysis Services, 이전 버전과의 호환성"
  - "SSAS, 이전 버전과의 호환성"
  - "SQL Server Analysis Services, 이전 버전과의 호환성"
  - "사용되지 않는 기능 [Analysis Services]"
ms.assetid: 2c96ecfe-a170-41d0-bee3-74503f880197
caps.latest.revision: 52
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 52
---
# SQL Server 2016에서 사용되지 않는 Analysis Services 기능
  *사용되지 않는 기능* 은 이후 릴리스에서는 제품에서 제거될 예정이지만 이전 버전과의 호환성을 유지하기 위해 현재 릴리스에서는 계속 지원되며 포함되어 있는 기능입니다. 일반적으로 사용되지 않는 기능은 주 릴리스(최초 공지 이후 2개 릴리스 이내)에서 제거됩니다. 예를 들어 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 에서 사용되지 않는 것으로 공지된 기능은 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에서 지원되지 않을 수 있습니다.  
  
 **SQL Server의 다음 주 릴리스에서 지원되지 않을 예정인 기능**  
  
|||  
|-|-|  
|**범주**|**기능**|  
|다차원|원격 파티션|  
|다차원|원격으로 연결된 측정값 그룹|  
|다차원|차원 쓰기(writeback)|  
|다차원|연결된 차원|  
  
 **SQL Server의 향후 릴리스에서 지원되지 않을 예정인 기능**  
  
|||  
|-|-|  
|**범주**|**기능**|  
|다차원|자동 관리 캐싱을 위한 SQL Server 테이블 알림.  <br />자동 관리 캐싱을 위한 폴링을 대신 사용할 수 있습니다. <br />[자동 관리 캐싱&#40;차원&#41;](../analysis-services/multidimensional-models-olap-logical-dimension-objects/proactive-caching-dimensions.md) 및 [자동 관리 캐싱&#40;파티션&#41;](../Topic/Proactive%20Caching%20\(Partitions\).md)을 참조하세요.|  
|다차원|세션 큐브. 대체 기능은 없습니다.|  
|다차원|로컬 큐브. 대체 기능은 없습니다.|  
|테이블 형식|테이블 형식 모델 1100 및 1103 호환성 수준은 향후 릴리스에서 지원되지 않을 예정입니다. 대신 모델을 호환성 수준 1200으로 설정하여 모델 정의를 테이블 형식 메타데이터로 변환할 수 있습니다. [Compatibility Level for Tabular models in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)을 참조하세요.|  
|Tools|추적 캡처용 SQL Server Profiler<br /><br /> SQL Server Management Studio에 포함된 확장 이벤트 프로파일러를 대신 사용할 수 있습니다.  <br /> [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)을 참조하세요.|  
|Tools|추적 재생용 Server Profiler <br />대체 기능 대체 기능은 없습니다.|  
|추적 관리 개체 및 추적 API|Analysis Services 추적 및 재생 개체용 API를 포함하는 Microsoft.AnalysisServices.Trace 개체. 다음과 같은 여러 부분을 대신 사용할 수 있습니다.<br /><br /> -   추적 구성:  Microsoft.SqlServer.Management.XEvent<br />-   추적 읽기:  Microsoft.SqlServer.XEvent.Linq<br />-   추적 재생: 없음|  
  
> [!NOTE]  
>  이전에 사용이 중단된 기능에 대한 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 의 공지 사항은 계속 적용됩니다. 이러한 기능을 지원하는 코드는 아직 제품에서 삭제되지 않았으므로 이러한 기능 중 대부분은 이 릴리스에도 계속 포함되어 있습니다. 이전에 사용이 중단된 기능에 액세스할 수는 있지만, 이러한 기능은 사용되지 않는 것으로 간주되며 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 릴리스 사용 기간 중 언제든지 제품에서 실제로 제거될 수 있습니다. 그러므로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 의 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]를 기준으로 하는 새 모델이나 응용 프로그램에서는 사용되지 않는 기능을 사용하지 않는 것이 좋습니다.  
  
## 관련 항목:  
 [Analysis Services 이전 버전과의 호환성](../analysis-services/analysis-services-backward-compatibility.md)   
 [SQL Server 2016에서 제공이 중단된 Analysis Services 기능](../analysis-services/discontinued-analysis-services-functionality-in-sql-server-2016.md)  
  
  