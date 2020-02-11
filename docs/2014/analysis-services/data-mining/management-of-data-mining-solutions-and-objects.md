---
title: 데이터 마이닝 솔루션 및 개체 관리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], managing
- managing mining models
ms.assetid: 06fc61dd-925c-4347-8677-7046ee5d2f6f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 15574819cf0f0fec0d95fa2353c187cc55091e56
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084198"
---
# <a name="management-of-data-mining-solutions-and-objects"></a>데이터 마이닝 솔루션 및 개체 관리
  
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 는 기존 마이닝 구조와 마이닝 모델을 관리하는 데 활용할 수 있는 클라이언트 도구를 제공합니다. 이 섹션에서는 각 환경을 사용하여 수행할 수 있는 관리 작업에 대해 설명합니다.  
  
 이러한 도구 외에도 AMO를 사용하여 프로그래밍 방식으로 데이터 마이닝 개체를 관리하거나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 2007용 데이터 마이닝 추가 기능과 같이 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 데이터베이스에 연결되는 다른 클라이언트를 사용할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [데이터 마이닝 개체 이동](moving-data-mining-objects.md)  
  
 [데이터 마이닝&#41;&#40;처리 요구 사항 및 고려 사항](processing-requirements-and-considerations-data-mining.md)  
  
 [SQL Server Profiler를 사용 하 여 데이터 마이닝을 모니터링 &#40;Analysis Services 데이터 마이닝&#41;](using-sql-server-profiler-to-monitor-data-mining-analysis-services-data-mining.md)  
  
## <a name="location-of-data-mining-objects"></a>데이터 마이닝 개체 위치  
 처리된 마이닝 구조 및 모델은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 저장됩니다.  
  
 데이터 마이닝 개체를 개발할 때 모드 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 `Immediate` 데이터베이스에 대 한 연결을 만드는 경우 사용자가 만드는 모든 개체는 작업 하는 동안 서버에 즉시 추가 됩니다. 그러나 **** 에서 작업할 때의 기본 설정인 오프라인 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]모드에서 데이터 마이닝 개체를 디자인하는 경우에는 만드는 마이닝 개체가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스로 배포되기 전까지 메타데이터 컨테이너일 뿐입니다. 따라서 개체를 변경할 때마다 해당 개체를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버로 다시 배포해야 합니다. 데이터 마이닝 아키텍처에 대한 자세한 내용은 [물리적 아키텍처&#40;Analysis Services - 데이터 마이닝&#41;](physical-architecture-analysis-services-data-mining.md)를 참조하세요.  
  
> [!NOTE]  
>  
  [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007용 데이터 마이닝 추가 기능과 같은 일부 클라이언트를 사용하면 인스턴스에 대한 연결을 사용하지만 마이닝 구조 및 모델을 세션 기간 동안만 서버에 저장하는 세션 마이닝 모델 및 마이닝 구조를 만들 수도 있습니다. 이러한 모델도 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 저장된 구조 및 모델과 같이 여전히 클라이언트를 통해 관리할 수 있지만 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스와의 연결을 끊은 후에는 개체가 유지되지 않습니다.  
  
## <a name="managing-data-mining-objects-in-sql-server-data-tools"></a>SQL Server Data Tools에서 데이터 마이닝 개체 관리  
 
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 는 데이터 마이닝 개체를 쉽게 만들고, 찾아보고, 편집할 수 있는 여러 기능을 제공합니다.  
  
 다음 링크에서는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 사용하여 데이터 마이닝 개체를 수정하는 방법에 대한 정보를 제공합니다.  
  
-   [마이닝 구조에 사용되는 데이터 원본 뷰 편집](edit-the-data-source-view-used-for-a-mining-structure.md)  
  
-   [마이닝 구조 속성 변경](change-the-properties-of-a-mining-structure.md)  
  
-   [마이닝 모델의 속성 변경](change-the-properties-of-a-mining-model.md)  
  
-   [데이터 마이닝&#41;&#40;모델링 플래그 보기 또는 변경](modeling-flags-data-mining.md)  
  
-   [알고리즘 매개 변수 확인 또는 변경](view-or-change-algorithm-parameters.md)  
  
 일반적으로 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 도구로 활용하여 새 프로젝트를 개발한 후 기존 프로젝트에 추가한 다음 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]와 같은 도구를 사용하여 배포된 프로젝트와 개체를 관리합니다.  
  
 
  `Immediate` 옵션을 사용하고 온라인 모드로 서버에 연결하여 ssASnoversion 인스턴스에 이미 배포된 개체를 직접 수정할 수 있습니다. 자세한 내용은 [Connect in Online Mode to an Analysis Services Database](../multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)을 참조하세요.  
  
> [!WARNING]  
>  이름 또는 설명과 같은 메타데이터를 변경하는 작업을 비롯하여 마이닝 구조 또는 마이닝 모델을 변경하는 모든 작업을 수행한 후에는 구조나 모델을 다시 처리해야 합니다.  
  
 데이터 마이닝 프로젝트 또는 개체를 만드는 데 사용된 솔루션 파일이 없는 경우 Analysis Services 가져오기 마법사를 사용하여 서버에서 기존 프로젝트를 가져와서 개체를 수정한 다음 `Incremental` 옵션을 사용하여 다시 배포할 수 있습니다. 자세한 내용은 [Analysis Services 가져오기 마법사를 사용하여 데이터 마이닝 프로젝트 가져오기](import-a-data-mining-project-using-the-analysis-services-import-wizard.md)를 참조하세요.  
  
## <a name="managing-data-mining-objects-in-sql-server-management-studio"></a>SQL Server Management Studio에서 데이터 마이닝 개체 관리  
 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 마이닝 구조 및 마이닝 모델을 스크립팅, 처리 또는 삭제할 수 있습니다. 개체 탐색기를 사용하여 제한된 속성 집합만 볼 수 있지만 **DMX 쿼리** 창을 열고 마이닝 구조를 선택하면 마이닝 모델에 대한 추가 메타데이터를 볼 수 있습니다.  
  
-   [SQL Server Management Studio에서 DMX 쿼리 만들기](create-a-dmx-query-in-sql-server-management-studio.md)  
  
## <a name="managing-data-mining-objects-programmatically"></a>프로그래밍 방식으로 데이터 마이닝 개체 관리  
 다음과 같은 프로그래밍 언어를 사용하여 데이터 마이닝 개체를 생성, 변경, 처리 및 삭제할 수 있습니다. 각 언어는 서로 다른 태스크를 위해 설계되었으므로 수행할 수 있는 작업의 유형에는 제한이 있을 수 있습니다. 예를 들어 데이터 마이닝 개체의 일부 속성을 변경하는 데는 DMX(Data Mining Extensions)를 사용할 수 없고 XMLA나 AMO를 사용해야 합니다.  
  
### <a name="analysis-management-objects-amo"></a>AMO(Analysis Management Objects)  
 AMO(Analysis Management Objects)는 XMLA의 최상위에 작성되며 데이터 마이닝 개체를 완전히 제어할 수 있게 하는 개체 모델입니다. AMO를 사용하여 마이닝 구조와 마이닝 모델을 생성, 배포 및 모니터링할 수 있습니다.  
  
-   [AMO 개념 및 개체 모델](https://docs.microsoft.com/bi-reference/amo/amo-concepts-and-object-model)  
  
-   <xref:Microsoft.AnalysisServices>  
  
 **제한 사항:** 없음을.  
  
### <a name="data-mining-extensions-dmx"></a>DMX(Data Mining Extensions)  
 DMX(Data Mining Extensions)를 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 또는 ADOMD.Net 등의 다른 명령 인터페이스와 함께 사용하여 마이닝 구조와 마이닝 모델을 생성, 삭제 및 쿼리할 수 있습니다.  
  
-   [데이터 마이닝 확장 &#40;DMX&#41; 데이터 정의 문](/sql/dmx/dmx-statements-data-definition)  
  
 **제한 사항:** 일부 속성은 DMX를 사용 하 여 변경할 수 없습니다.  
  
### <a name="xml-for-analysis-xmla"></a>XMLA(XML for Analysis)  
 XMLA(XML for Analysis)는 모든 Analysis Services에 대한 데이터 정의 언어입니다. XMLA를 사용하면 대부분의 데이터 마이닝 개체와 서버 작업을 제어할 수 있습니다. 클라이언트와 서버 간의 모든 관리 작업은 XMLA를 사용하여 수행할 수 있습니다. 편의상 ASSL( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language)을 사용하여 XML을 래핑할 수 있습니다.  
  
 **제한 사항:** [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 내부 전용으로 지원 되며 XML DDL 스크립트에서 사용할 수 없는 일부 XMLA 문을 생성 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [개발자 가이드 &#40;Analysis Services&#41;](../analysis-services-developer-documentation.md)  
  
  
