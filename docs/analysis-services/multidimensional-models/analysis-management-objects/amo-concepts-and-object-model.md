---
title: "AMO 개념 및 개체 모델 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- AMO, classes
- Analysis Management Objects, classes
- objects [Analysis Management Objects]
- AMO, objects
- classes [AMO]
- AMO
- Analysis Management Objects
- Analysis Management Objects, objects
ms.assetid: 3b0cdf8e-46d5-4dfe-8b2c-233c27e1473e
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b53eed2fa7d7061958db31576e387e3a4af5b14c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="amo-concepts-and-object-model"></a>AMO 개념 및 개체 모델
  이 항목에서는 정의의 AMO Analysis Management Objects (), 다른 도구와의 아키텍처에 제공 된 라이브러리와 AMO의 관계 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], 및 AMO의 모든 주요 개체의 개념을 설명 합니다.  
  
 AMO는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]용 관리 클래스를 모두 포함하는 컬렉션으로, 관리되는 환경의 <xref:Microsoft.AnalysisServices> 네임스페이스에서 프로그래밍 방식으로 사용할 수 있습니다. 일반적으로 위치에서 액세스할 수 있는 AnalysisServices.dll 파일에 포함 된 클래스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 폴더 \100\SDK\Assemblies에서 파일이 설치\\합니다. AMO 클래스를 사용하려면 이 어셈블리에 대한 참조를 프로젝트에 포함합니다.  
  
 만들 수 있는 AMO를 사용 하 여 수정 하 고 큐브, 차원, 마이닝 구조와 같은 개체를 삭제 하 고 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스; 끝남, 이러한 모든 개체 동작은.NET Framework의 응용 프로그램에서 수행할 수 있습니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스에 저장된 정보를 처리하고 업데이트할 수도 있습니다.  
  
 AMO를 사용하여 데이터를 쿼리할 수는 없습니다. 사용 데이터를 쿼리하려면 [ADOMD.NET을 사용 하 여 개발](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [Analysis Services 아키텍처의 AMO](#AMOintheAnalysisServicesArchitecture)  
  
 [AMO 아키텍처](#AMOArchitecture)  
  
 [AMO를 사용 하 여](#bkmk_UsingAMO)  
  
 [AMO로 관리 태스크 자동화](#AutomatingAdministrativeTaskswithAMO)  
  
##  <a name="AMOintheAnalysisServicesArchitecture"></a>Analysis Services 아키텍처의 AMO  
 AMO는 개체 관리용으로만 설계되었으며 데이터를 쿼리하는 데는 사용할 수 없습니다. 사용자가 해야 할 경우 쿼리 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 클라이언트 응용 프로그램에서 사용 해야 클라이언트 응용 프로그램에서 데이터를 [ADOMD.NET을 사용 하 여 개발](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)합니다.  
  
##  <a name="AMOArchitecture"></a>AMO 아키텍처  
 AMO는 클래스의 인스턴스를 관리 하기 위한의 전체 라이브러리 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 클라이언트 응용 프로그램에서.NET Framework 버전 2.0의 관리 코드로 합니다.  
  
 AMO 클래스 라이브러리는 클래스 계층 구조로 설계되었으며 일부 클래스는 다른 클래스보다 먼저 인스턴스화되어야 코드에서 사용할 수 있습니다. 코드에서 언제든지 인스턴스화할 수 있는 보조 클래스도 있지만 대개는 이러한 보조 클래스 중 하나를 사용하기 전에 하나 이상의 계층 구조 클래스를 이미 인스턴스화한 경우가 많습니다.  
  
 다음 그림에서는 주요 클래스가 포함된 AMO 계층 구조를 개괄적으로 보여 줍니다. 이 그림에서는 클래스의 위치를 클래스의 컨테이너 및 피어 위치와 구분하여 보여 줍니다. <xref:Microsoft.AnalysisServices.Dimension>은 <xref:Microsoft.AnalysisServices.Database>와 <xref:Microsoft.AnalysisServices.Server>에 속하며 <xref:Microsoft.AnalysisServices.DataSource> 및 <xref:Microsoft.AnalysisServices.MiningStructure>와 동시에 만들어질 수 있습니다. 일부 피어 클래스는 다른 클래스를 사용하기 전에 인스턴스화되어야 합니다. 예를 들어 새 <xref:Microsoft.AnalysisServices.DataSource> 또는 <xref:Microsoft.AnalysisServices.Dimension>를 추가하려면 먼저 <xref:Microsoft.AnalysisServices.MiningStructure>의 인스턴스를 만들어야 합니다.  
  
 ![AMO 클래스 높은 수준의 뷰입니다](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-highlevelview-majorobjectshighlighted.gif "AMO 클래스 개요")  
  
 A *주요 개체* 다른 개체의 일부가 아니라 전체 엔터티인와 완전 한 개체를 나타내는 클래스입니다. <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Dimension> 및 <xref:Microsoft.AnalysisServices.MiningStructure>는 그 자체가 엔터티이므로 주요 개체에 해당합니다. 그러나 <xref:Microsoft.AnalysisServices.Level>은 <xref:Microsoft.AnalysisServices.Dimension>을 구성하는 요소이므로 주요 개체가 아닙니다. 주요 개체는 다른 개체와는 독립적으로 만들고 삭제, 수정 및 처리할 수 있습니다. 보조 개체는 부모 주요 개체를 만드는 작업의 일부로서만 만들 수 있는 개체입니다. 보조 개체는 일반적으로 주요 개체가 만들어질 때 만들어집니다. 보조 개체의 경우에는 기본 생성 개체가 없으므로 해당 개체를 만들 때 개체 값을 정의해야 합니다.  
  
 다음 그림에서는 <xref:Microsoft.AnalysisServices.Server> 개체에 포함된 주요 개체를 보여 줍니다.  
  
 ![강조 표시 된 AMO 주요 개체](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-majorobjects.gif "강조 표시 된 AMO 주요 개체")  
  
 ![(2)을 강조 표시 된 AMO 주요 개체](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-majorobjects-02.gif "강조 표시 된 AMO 주요 개체 (2)")  
  
 AMO를 사용하여 프로그래밍할 때 클래스와 포함된 클래스 간의 연결에는 <xref:Microsoft.AnalysisServices.Server> 및 <xref:Microsoft.AnalysisServices.Dimension>과 같은 컬렉션 형식 특성이 사용됩니다. 포함된 클래스의 한 인스턴스를 사용하려면 먼저 해당 클래스를 포함하거나 포함할 수 있는 컬렉션 개체에 대한 참조를 가져와야 합니다. 그런 다음 컬렉션에서 찾으려는 특정 개체를 찾고 해당 개체에 대한 참조를 가져와서 작업을 시작할 수 있습니다.  
  
### <a name="amo-classes"></a>AMO 클래스  
 AMO는 클라이언트 응용 프로그램에서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 인스턴스를 관리하기 위해 설계된 클래스 라이브러리입니다. AMO 라이브러리는 특정 태스크를 수행하기 위해 논리적으로 관련된 개체 그룹이라고 생각할 수 있습니다. AMO 클래스는 다음과 같이 분류될 수 있습니다.  
  
|클래스 집합|용도|  
|---------------|-------------|  
|[AMO 기본 클래스](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)|다른 클래스 집합을 사용하는 데 필요한 클래스입니다.|  
|[AMO OLAP 클래스](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-olap-classes.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 OLAP 개체를 관리하는 데 사용되는 클래스입니다.|  
|[AMO 데이터 마이닝 클래스](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-data-mining-classes.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 데이터 마이닝 개체를 관리하는 데 사용되는 클래스입니다.|  
|[AMO 보안 클래스](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-security-classes.md)|다른 개체에 대한 액세스를 제어하고 보안을 유지하는 데 사용되는 클래스입니다.|  
|[AMO 다른 클래스와 메서드](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md)|OLAP 또는 데이터 마이닝 관리자의 일상 업무에 도움이 되는 클래스와 메서드입니다.|  
  
##  <a name="bkmk_UsingAMO"></a>AMO를 사용 하 여  
 AMO는 예를 들어 팩트 테이블의 새 데이터를 기반으로 측정값 그룹에 새 파티션을 만들거나 새 데이터를 기반으로 마이닝 모델을 다시 학습하는 등의 반복적인 태스크를 자동화하는 데 특히 유용합니다. 새 개체를 만드는 이러한 태스크는 일반적으로 월별, 주별 또는 분기별로 수행되며 응용 프로그램에서는 새 데이터를 기반으로 새 개체의 이름을 쉽게 지정할 수 있습니다.  
  
##### <a name="analysis-services-administrators"></a>Analysis Services 관리자  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 관리자는 AMO를 사용하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스의 처리를 자동화할 수 있습니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스를 디자인하고 배포하려면 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]를 사용해야 합니다.  
  
##### <a name="developers"></a>개발자  
 개발자는 AMO를 사용하여 지정된 사용자 집합을 위한 관리 인터페이스를 개발할 수 있습니다. 이러한 인터페이스는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체에 대한 액세스를 제한하고 사용자가 특정 태스크만 수행하도록 제한할 수 있습니다. 예를 들어 AMO를 사용하면 사용자가 모든 데이터베이스 개체를 보고 데이터베이스 중 하나를 선택하여 지정된 장치 집합의 한 장치에 백업하는 데 사용할 수 있는 백업 응용 프로그램을 만들 수 있습니다.  
  
 개발자는 응용 프로그램에 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 논리를 포함할 수도 있습니다. 이를 위해 개발자는 사용자 입력 또는 기타 요소를 기반으로 큐브, 차원, 마이닝 구조 및 마이닝 모델을 만들 수 있습니다.  
  
##### <a name="olap-advanced-users"></a>OLAP 고급 사용자  
 OLAP 고급 사용자는 일반적으로 프로그래밍 배경 지식이 풍부하며 데이터 개체를 보다 정밀하게 사용하여 데이터 분석 기능을 향상시키려는 데이터 분석가나 그 밖의 경험 있는 데이터 사용자입니다. 오프라인으로 작업해야 하는 사용자의 경우에는 오프라인으로 전환하기 전에 로컬 큐브를 만드는 과정을 자동화하는 데 AMO를 유용하게 사용할 수 있습니다.  
  
##### <a name="data-mining-advanced-users"></a>데이터 마이닝 고급 사용자  
 데이터 마이닝 고급 사용자의 경우 AMO는 정기적으로 다시 학습해야 하는 모델 집합이 매우 많을 때 가장 유용합니다.  
  
##  <a name="AutomatingAdministrativeTaskswithAMO"></a>AMO로 관리 태스크 자동화  
 대부분의 반복적인 태스크는 개발자가 선택한 언어를 사용하여 응용 프로그램으로 개발된 경우보다 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]를 사용하여 개발된 경우에 가장 적절하게 디자인, 배포 및 유지 관리됩니다. 하지만 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]를 사용하여 자동화할 수 없는 반복적 태스크의 경우에는 AMO를 사용할 수 있습니다.. AMO는 또한 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]를 사용하여 비즈니스 인텔리전스를 위한 특수화된 응용 프로그램을 개발하려는 경우에도 유용합니다.  
  
##### <a name="automatic-object-management"></a>자동 개체 관리  
 AMO를 사용하면 사용자 입력 또는 새로 받은 데이터를 기반으로 <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.MiningStructure>, <xref:Microsoft.AnalysisServices.MiningModel> 또는 <xref:Microsoft.AnalysisServices.Role>과 같은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체를 만들거나 업데이트하거나 삭제하기가 매우 쉽습니다. AMO는 개발된 솔루션을 ISV(Independent Software Vendor)부터 최종 고객에게까지 배포해야 하는 설치 응용 프로그램에 이상적입니다. 설치 응용 프로그램에서는 이전 버전이 있는지 확인하고, 구조를 업데이트하고, 더 이상 유용하지 않은 개체를 제거하고, 새 개체를 만들 수 있습니다. 이전 버전이 없으면 모든 항목을 처음부터 새로 만들 수 있습니다.  
  
 AMO를 사용하면 매우 간단하게 새 데이터를 기반으로 새 파티션을 만들 수 있으며 프로젝트 범위를 벗어난 이전 파티션은 제거할 수 있습니다. 예를 들어 최근 36개월 동안의 데이터를 사용하는 재무 분석 솔루션의 경우 한 달 동안의 데이터를 새로 받는 즉시 37개월 전의 데이터는 제거될 수 있습니다. 또한 성능을 최적화하기 위해 사용량에 따라 새 집계를 디자인하여 최근 12개월에 적용할 수 있습니다.  
  
##### <a name="automatic-object-processing"></a>자동 개체 처리  
 AMO를 사용하여 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]를 사용하는 예약된 태스크와 일반적인 데이터 흐름의 범위를 벗어나는 특정 이벤트에 응답함으로써 개체를 처리하고 가용성을 업데이트할 수 있습니다.  
  
##### <a name="automatic-security-management"></a>자동 보안 관리  
 보안 관리를 자동화하여 역할 및 사용 권한에 새 사용자를 포함하거나 다른 사용자의 기간이 만료되는 즉시 해당 사용자를 제거할 수 있습니다. 새 인터페이스를 만들어 보안 관리자의 보안 관리 작업을 간단하게 할 수도 있습니다. 이는 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]를 사용하는 것보다 간단할 수 있습니다.  
  
##### <a name="automatic-backup-management"></a>자동 백업 관리  
 자동 백업 관리는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 태스크를 사용하여 수행하거나 자동으로 실행되는 특수화된 AMO 응용 프로그램을 만들어 수행할 수 있습니다. AMO를 사용하면 운영자의 일상 업무에 도움이 되는 운영자용 백업 인터페이스를 개발할 수 있습니다.  
  
##### <a name="tasks-amo-is-not-intended-for"></a>AMO를 사용할 수 없는 태스크  
 AMO는 데이터를 쿼리하는 데는 사용할 수 없습니다. 큐브 및 마이닝 모델을 포함한 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터를 쿼리하려면 사용자 응용 프로그램에서 ADOMD.NET을 사용해야 합니다. 자세한 내용은 참조 [ADOMD.NET을 사용 하 여 개발](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)합니다.  
  
  
