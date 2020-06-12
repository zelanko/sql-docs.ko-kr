---
title: Analysis Services 개인 설정 확장 프로그램 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- personalization extensions [Multidimensional Databases]
ms.assetid: 0f144059-24e0-40c0-bde4-d48c75e46598
author: minewiskan
ms.author: owend
ms.openlocfilehash: cddb6b604e0fc397e6640637db7320898d2beb5c
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546765"
---
# <a name="analysis-services-personalization-extensions"></a>Analysis Services 개인 설정 확장 프로그램
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]개인 설정 확장 프로그램은 플러그 인 아키텍처를 구현 하는 개념을 기반으로 합니다. 플러그 인 아키텍처에서는 동적으로 새 큐브 개체 및 기능을 개발하여 다른 개발자와 손쉽게 공유할 수 있습니다. 따라서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개인 설정 확장 프로그램은 다음을 달성할 수 있도록 하는 기능을 제공 합니다.  
  
-   **동적 디자인 및 배포** 사용자는 개인 설정 확장 프로그램을 디자인 하 고 배포 하는 즉시 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 다음 사용자 세션이 시작 될 때 개체와 기능에 액세스할 수 있습니다.  
  
-   **인터페이스 독립성** 사용자는 개인 설정 확장 프로그램을 만드는 데 사용 하는 인터페이스에 관계 없이 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 모든 인터페이스를 사용 하 여 개체와 기능에 액세스할 수 있습니다.  
  
-   **세션 컨텍스트** [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개인 설정 확장 프로그램은 기존 인프라에서 영구적 개체가 아니므로 큐브를 다시 처리 하지 않아도 됩니다. 이러한 프로그램은 사용자가 데이터베이스에 연결하는 시점에 사용자에 대해 노출 및 생성되며 해당 사용자 세션 동안 사용 가능한 상태로 유지됩니다.  
  
-   **신속한 배포** [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]다른 소프트웨어 개발자와 개인 설정 확장 프로그램을 공유 하 여이 확장 기능을 찾을 수 있는 위치 또는 방법에 대 한 자세한 사양을 고려해 서는 안 됩니다.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개인 설정 확장 프로그램의 용도는 많습니다. 예를 들어 회사의 영업에 여러 통화가 관련된 경우가 있습니다. 큐브에 액세스하는 사람에 해당하는 지역 통화로 통합된 영업을 반환하는 계산 멤버를 만들 수 있습니다. 이 멤버를 개인 설정 확장 프로그램으로 만듭니다. 그런 다음 이 계산 멤버를 사용자 그룹과 공유합니다. 공유하면 이러한 사용자들은 서버에 연결한 즉시 계산 멤버에 액세스할 수 있게 됩니다. 사용자가 사용하는 인터페이스가 계산 멤버를 만들 때 사용된 인터페이스와 다른 경우에도 액세스할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]개인 설정 확장 프로그램은 기존 관리 되는 어셈블리 아키텍처를 간단 하 고 세련 되 게 수정 하 여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] <xref:Microsoft.AnalysisServices.AdomdServer> 개체 모델, MDX (Multidimensional Expressions) 구문 및 스키마 행 집합 전체에 노출 됩니다.  
  
## <a name="logical-architecture"></a>논리 아키텍처  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개인 설정 확장 프로그램의 아키텍처는 관리 어셈블리 아키텍처와 다음 네 가지의 기본 요소를 기반으로 합니다.  
  
 [PlugInAttribute] 사용자 지정 특성  
 서비스를 시작할 때에서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 필요한 어셈블리를 로드 하 고 사용자 지정 특성이 있는 클래스를 확인 합니다 <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> .  
  
> [!NOTE]  
>  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]는 사용자 지정 특성을 정의하여 코드를 설명하고 런타임 동작에 영향을 미칩니다. 자세한 내용은 MSDN의 개발자 가이드에서 "[특성 개요](https://go.microsoft.com/fwlink/?LinkId=82929)" 항목을 참조 하십시오 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] .  
  
 사용자 지정 특성이 있는 모든 클래스에 대해 <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 은 해당 기본 생성자를 호출 합니다. 시작 시에 모든 생성자를 호출하면 새 개체를 만들 수 있는, 모든 사용자 동작으로부터 독립적인 공통된 장소가 제공됩니다.  
  
 클래스 생성자는 개인 설정 확장 프로그램의 제작 및 관리 정보를 위한 작은 캐시를 만드는 것 외에 일반적으로 <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened> 및 <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing> 이벤트를 구독합니다. 이러한 이벤트를 구독하지 못할 경우 CLR(공용 언어 런타임) 가비지 수집기에 의해 클래스가 부적절하게 정리 대상으로 표시될 수 있습니다.  
  
 세션 컨텍스트  
 개인 설정 확장 프로그램을 기반으로 하는 개체에 대해 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 클라이언트 세션 동안 실행 환경을 만들고, 이 환경에서 이러한 개체의 대부분을 동적으로 만듭니다. 다른 CLR 어셈블리와 마찬가지로 이 실행 환경도 다른 함수 및 저장 프로시저에 액세스할 수 있습니다. 사용자 세션이 종료 되 면는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 동적으로 생성 된 개체를 제거 하 고 실행 환경을 닫습니다.  
  
 이벤트  
 개체 만들기는 `On-Cube-OpenedCubeOpened` 및 `On-Cube-ClosingCubeClosing` 세션 이벤트에 의해 트리거됩니다.  
  
 클라이언트와 서버 간의 통신은 특정 이벤트를 통해 이루어집니다. 이러한 이벤트를 통해 클라이언트는 클라이언트의 개체 생성으로 이어지는 상황을 인식합니다. 클라이언트의 환경은 세션 이벤트와 큐브 이벤트, 두 개의 이벤트 집합을 사용하여 동적으로 만들어집니다.  
  
 세션 이벤트는 서버 개체와 연관됩니다. 클라이언트는 서버에 로그온 할 때 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 세션을 만들고 이벤트를 트리거합니다 <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened> . 클라이언트는 서버에서 세션을 종료 하면 이벤트를 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 트리거합니다 <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing> .  
  
 큐브 이벤트는 연결 개체와 연관됩니다. 큐브에 연결하면 <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeOpened> 이벤트가 트리거됩니다. 큐브를 닫거나 다른 큐브로 변경하여 큐브에 대한 연결을 닫으면 <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeClosing> 이벤트가 트리거됩니다.  
  
 추적 기능 및 오류 처리  
 모든 작업은 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]를 사용하여 추적 가능합니다. 처리되지 않은 오류는 Windows 이벤트 로그에 보고됩니다.  
  
 모든 개체 제작 및 관리는 이 아키텍처와는 관계없으며 전적으로 개체 개발자의 책임입니다.  
  
## <a name="infrastructure-foundations"></a>인프라 기반  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개인 설정 확장 프로그램은 기존 구성 요소를 기반으로 합니다. 다음은 개인 설정 확장 프로그램 기능을 제공하는 향상 및 개선 사항의 요약입니다.  
  
### <a name="assemblies"></a>어셈블리  
 사용자 지정 특성 <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute>를 사용자 지정 어셈블리에 추가하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개인 설정 확장 프로그램 클래스를 식별할 수 있습니다.  
  
### <a name="changes-to-the-adomdserver-object-model"></a>AdomdServer 개체 모델의 변경 내용  
 향상되었거나 모델에 추가된 <xref:Microsoft.AnalysisServices.AdomdServer> 개체 모델의 개체는 다음과 같습니다.  
  
#### <a name="new-adomdconnection-class"></a>새 AdomdConnection 클래스  
 <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection> 클래스는 새로운 클래스이며 속성과 이벤트를 통해 여러 개인 설정 확장 프로그램을 노출합니다.  
  
 **속성**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.SessionID%2A> - 현재 연결의 세션 ID를 나타내는 읽기 전용 문자열 값입니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.ClientCulture%2A> - 현재 세션에 연결된 클라이언트 culture에 대한 읽기 전용 참조입니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.User%2A> - 현재 사용자를 나타내는 ID 인터페이스의 읽기 전용 참조입니다.  
  
 **이벤트**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeOpened>  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeClosing>  
  
#### <a name="new-properties-in-the-context-class"></a>컨텍스트 클래스의 새 속성  
 <xref:Microsoft.AnalysisServices.AdomdServer.Context> 클래스에는 두 개의 새로운 속성이 있습니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Context.Server%2A> - 새 서버 개체에 대한 읽기 전용 참조입니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentConnection%2A> - 새 <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection> 개체에 대한 읽기 전용 참조입니다.  
  
#### <a name="new-server-class"></a>새 서버 클래스  
 <xref:Microsoft.AnalysisServices.AdomdServer.Server> 클래스는 새로운 클래스이며 클래스 속성과 이벤트를 통해 여러 개인 설정 확장 프로그램을 노출합니다.  
  
 **속성**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.Name%2A> - 서버 이름을 나타내는 읽기 전용 문자열 값입니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.Culture%2A> - 서버에 연결된 전역 culture에 대한 읽기 전용 참조입니다.  
  
 **이벤트**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened>  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing>  
  
#### <a name="adomdcommand-class"></a>AdomdCommand 클래스  
 <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand> 클래스는 이제 다음 MDX 명령을 지원합니다.  
  
-   [CREATE MEMBER 문&#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)  
  
-   [MDX &#40;업데이트 멤버 문&#41;](/sql/mdx/mdx-data-definition-update-member)  
  
-   [DROP MEMBER 문 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-member)  
  
-   [CREATE SET 문&#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-set)  
  
-   [DROP SET 문이 MDX를 &#40;&#41;](/sql/mdx/mdx-data-definition-drop-set)  
  
-   [MDX &#40;CREATE KPI 문&#41;](/sql/mdx/mdx-data-definition-create-kpi)  
  
-   [DROP KPI 문이 MDX를 &#40;&#41;](/sql/mdx/mdx-data-definition-drop-kpi)  
  
### <a name="mdx-extensions-and-enhancements"></a>MDX 확장 및 향상된 기능  
 CREATE MEMBER 명령은 `caption` 속성, `display_folder` 속성 및 `associated_measure_group` 속성을 통해 향상되었습니다.  
  
 계산 중 업데이트가 필요하고 이로 인해 우선 순위의 손실이 발생할 때 멤버 다시 만들기를 방지하기 위해 UPDATE MEMBER 명령이 추가되었습니다. 업데이트에서는 계산 멤버의 범위를 변경하거나 계산 멤버를 다른 부모로 이동하거나 다른 `solveorder`를 정의할 수 없습니다.  
  
 CREATE SET 명령은 `caption` 속성, `display_folder` 속성 및 새로운 `STATIC | DYNAMIC` 키워드를 통해 향상되었습니다. *Static* 은 집합이 생성 시에만 계산 됨을 의미 합니다. *Dynamic* 은 쿼리에서 집합이 사용 될 때마다 집합이 평가 됨을 의미 합니다. 키워드가 생략된 경우 기본값은 `STATIC`입니다.  
  
 CREATE KPI 및 DROP KPI 명령이 MDX 구문에 추가되었습니다. KPI는 모든 MDX 스크립트에서 동적으로 만들어질 수 있습니다.  
  
### <a name="schema-rowsets-extensions"></a>스키마 행 집합 확장  
 MDSCHEMA_MEMBERS *범위* 열이 추가 됩니다. 범위 값은 MDMEMBER_SCOPE_GLOBAL = 1, MDMEMBER_SCOPE_SESSION = 2와 같습니다.  
  
 MDSCHEMA_SETS *set_evaluation_context* 열이 추가 됩니다. 설정 평가 컨텍스트 값은 MDSET_RESOLUTION_STATIC = 1, MDSET_RESOLUTION_DYNAMIC = 2와 같습니다.  
  
 MDSCHEMA_KPIS에 scope 열이 추가되었습니다. 범위 값은 MDKPI_SCOPE_GLOBAL = 1, MDKPI_SCOPE_SESSION = 2와 같습니다.  
  
  
