---
title: "SQL Server 2016의 Analysis Services 기능과 관련된 새로운 변경 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "주요 변경 내용 [Analysis Services]"
  - "Analysis Services 업그레이드"
ms.assetid: aeb02542-5a6c-458c-a110-13413dd3e9d9
caps.latest.revision: 55
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 53
---
# SQL Server 2016의 Analysis Services 기능과 관련된 새로운 변경
  *새로운 변경* 이 적용되면 모델이나 서버를 업그레이드한 후에 데이터 모델, 응용 프로그램 코드 또는 스크립트가 더 이상 작동하지 않습니다.  
  
> [!NOTE]  
>  반면 *동작 변경* 은 모델이나 응용 프로그램 사용을 중단하지는 않지만 이전 릴리스와는 다른 방식으로 동작하도록 하는 코드 변경이라 할 수 있습니다.  동작 변경의 예로는 기본값 변경, 이전에는 허용되었던 속성이나 옵션의 구성 금지 등이 있을 수 있습니다. 이번 릴리스의 동작 변경에 대해 자세히 알아보려면 [Behavior Changes to Analysis Services Features in SQL Server 2016](../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md)을 참조하세요.  
  
## .NET 4.0 버전 업그레이드  
 이제 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]의 AMO(Analysis Services 관리 개체), ADOMD.NET 및 TOM(테이블 형식 개체 모델) 클라이언트 라이브러리가 .NET 4.0 런타임을 대상으로 합니다. .NET 3.5를 대상으로 하는 응용 프로그램의 경우 새로운 변경 사항이 될 수 있습니다. 이러한 어셈블리의 최신 버전을 사용하는 응용 프로그램은 이제 .NET 4.0 이상을 대상으로 해야 합니다.  
  
## AMO 버전 업그레이드  
 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] [AMO&#40;Analysis Services 관리 개체&#41;](../Topic/Analysis%20Services%20Management%20Objects%20\(AMO\).md)의 버전 업그레이드이며 상황에 따라 새로운 변경 사항입니다.  AMO로 호출되는 기존 코드와 스크립트는 이전 버전에서 업그레이드하기 전과 동일하게 실행됩니다. 그러나 응용 프로그램을 *다시 컴파일* 해야 하며 대상 인스턴스가 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 인 경우에는 코드나 스크립트가 작동하도록 다음 네임스페이스를 추가해야 합니다.  
  
```  
  
using Microsoft.AnalysisServices;  
using Microsoft.AnalysisServices.Core;  
  
```  
  
 코드에서 Microsoft.AnalysisServices 어셈블리를 참조할 때마다 [Microsoft.AnalysisServices.Core](../Topic/Microsoft.AnalysisServices.Core.md) 네임스페이스가 필요합니다. 이전에는 **Microsoft.AnalysisServices** 네임스페이스에만 포함되었던 개체가 테이블 형식 시나리오와 다차원 시나리오에서 같은 방식으로 사용되는 경우 이번 릴리스에서는 Core 네임스페이스로 이동됩니다.  예를 들어 서버 관련 API는 Core 네임스페이스로 이동됩니다.  
  
 이처럼 이제는 네임스페이스가 여러 개 사용되지만 모든 네임스페이스는 같은 어셈블리(Microsoft.AnalysisServices.dll)에 포함됩니다.  
  
## XEvent DISCOVER 변경 사항  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]의 SSMS에서 XEvent DISCOVER 스트리밍을 보다 효과적으로 지원하기 위해 `DISCOVER_XEVENT_TRACE_DEFINITION`이 다음과 같은 XEvent 추적으로 대체됩니다.  
  
-   DISCOVER_XEVENT_PACKAGES  
  
-   DISCOVER_XEVENT_OBJECT  
  
-   DISCOVER_XEVENT_OBJECT_COLUMNS  
  
-   DISCOVER_XEVENT_SESSION_TARGETS  
  
## 관련 항목:  
 [Analysis Services 이전 버전과의 호환성](../analysis-services/analysis-services-backward-compatibility.md)  
  
  