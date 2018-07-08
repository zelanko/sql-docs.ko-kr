---
title: 데이터 마이닝 쿼리 인터페이스 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- predictions [Analysis Services], DMX prediction queries
- predictions [DMX]
- DMX [Analysis Services], prediction queries
- prediction queries [DMX]
- predictions [Analysis Services]
- queries [DMX], prediction queries
- mining models [Analysis Services], DMX
ms.assetid: a8952427-fd8c-4300-8f62-25f57ac1be0c
caps.latest.revision: 49
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 07641be25c1e7828238ea4a6dd897240651735ce
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159654"
---
# <a name="data-mining-query-interfaces"></a>데이터 마이닝 쿼리 인터페이스
  데이터 마이닝 쿼리는 DMX(Data Mining Extensions) 언어를 기반으로 합니다. 분류, 위험 분석, 권장 사항 생성 및 선형 회귀를 포함한 모든 예측 및 모델링 태스크에 DMX를 사용합니다. 또한 모델을 처리할 때 생성된 패턴과 통계를 검색할 수 있습니다.  
  
 DMX를 사용하는 예측 쿼리의 구문은 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 쿼리 구문과 유사합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 와 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 모두 DMX 예측 쿼리 작성에 도움이 되는 도구를 제공합니다.  
  
 이 항목에서는 DMX를 사용하여 데이터 마이닝 쿼리를 만들고 실행하는 데 사용할 수 있는 인터페이스를 설명합니다.  
  
 [쿼리 도구](#bkmk_Tools)  
  
-   [예측 쿼리 작성기](#bkmk_Builder)  
  
-   [쿼리 편집기](#bkmk_QueryEditor)  
  
-   [DMX 템플릿](#bkmk_Templates)  
  
-   [Integration Services](#bkmk_SSIS)  
  
 [응용 프로그래밍 인터페이스(Application Programming Interfaces)](#bkmk_API)  
  
##  <a name="bkmk_Tools"></a> 데이터 마이닝 쿼리 도구  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 데이터 마이닝 개체에 대해 예측 쿼리, 내용 쿼리 및 데이터 정의 쿼리를 작성하는 데 사용할 수 있는 다음 도구가 있습니다.  
  
-   예측 쿼리 작성기  
  
-   쿼리 편집기  
  
-   DMX 템플릿  
  
-   Integration Services 데이터 마이닝 구성 요소  
  
###  <a name="bkmk_Builder"></a> 예측 쿼리 작성기  
 예측 쿼리 작성기는 데이터 마이닝 디자이너의 **마이닝 모델 예측** 탭에 포함되어 있습니다. 이 탭은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]및 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 사용할 수 있습니다.  
  
 쿼리 작성기를 사용할 때는 그래픽 도구를 사용하여 마이닝 모델을 선택하고, 새 사례 데이터를 추가하고, 예측 함수를 추가할 수 있습니다. 예측 쿼리 작성기는 쿼리를 수동으로 수정 하는 데 사용할 수 있는 텍스트 편집기 및 간단한 포함 **결과** 창 쿼리 결과 볼 수 있습니다.  
  
###  <a name="bkmk_QueryEditor"></a> 쿼리 편집기  
 쿼리 편집기에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 빌드 및 DMX 쿼리를 실행 하는 데 사용할 수 있는 도구를 제공 합니다. SQL Server Analysis Services의 인스턴스에 연결한 다음 데이터베이스, 마이닝 구조 열 및 마이닝 모델을 선택할 수 있습니다. **메타데이터 탐색기** 에는 찾아볼 수 있는 예측 함수의 목록이 포함되어 있습니다.  
  
###  <a name="bkmk_Templates"></a> DMX 템플릿  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 DMX 쿼리를 작성하는 데 사용할 수 있는 대화형 DMX 쿼리 템플릿을 제공합니다. 템플릿 목록이 표시되지 않는 경우 도구 모음에서 **보기** 를 클릭하고 **템플릿 탐색기**를 선택합니다. DMX, MDX 및 XMLA에 대한 템플릿이 포함된 모든 Analysis Services 템플릿을 보려면 큐브 아이콘을 클릭합니다.  
  
 템플릿을 사용하여 쿼리를 작성하려면 열려 있는 쿼리 창으로 템플릿을 끌어다 놓거나 템플릿을 두 번 클릭하여 새 연결 및 새 쿼리 창을 열면 됩니다.  
  
 템플릿에서 예측 쿼리를 만드는 방법에 대한 예제는 [템플릿에서 단일 예측 쿼리 작성](create-a-singleton-prediction-query-from-a-template.md)을 참조하세요.  
  
> [!WARNING]  
>  Microsoft Office Excel용 데이터 마이닝 추가 기능에도 복잡한 DMX 문을 작성하는 데 도움이 되는 대화형 쿼리 작성기와 함께 많은 템플릿이 포함되어 있습니다. 템플릿을 사용하려면 데이터 마이닝 클라이언트에서 **쿼리**를 클릭하고 **고급** 을 클릭합니다.  
  
###  <a name="bkmk_SSIS"></a> Integration Services 데이터 마이닝 구성 요소  
 예측 쿼리를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 일부로 포함할 수도 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 다음과 같은 태스크 및 변환을 통해 DMX 예측 쿼리와 DMX 문을 만들고 실행할 수 있습니다.  
  
|구성 요소|Description|  
|---------------|-----------------|  
|데이터 마이닝 쿼리 태스크|DMX 쿼리와 다른 DMX 문을 제어 흐름의 일부로 실행합니다.<br /><br /> 태스크 편집기는 예측 쿼리 작성기와 DMX 쿼리를 수동으로 수정하기 위한 입력란을 제공합니다. 그러나 태스크 편집기는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 솔루션의 개체에 대해 쿼리의 유효성을 검사할 수 없습니다. 따라서 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 또는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 내에서 쿼리를 만든 다음 문이나 쿼리의 텍스트를 태스크 편집기에 붙여넣는 것이 가장 좋습니다.|  
|데이터 마이닝 쿼리 변환|데이터 흐름 원본에서 제공된 데이터를 사용하여 데이터 흐름 내에서 예측 쿼리를 실행합니다.<br /><br /> 태스크 편집기는 예측 쿼리 작성기와 DMX 쿼리를 수동으로 수정하기 위한 입력란을 제공합니다.<br /><br /> 변환은 데이터 흐름의 데이터를 사용하는 쿼리(즉, PREDICTION JOIN 구문을 사용하는 쿼리)를 만드는 데만 사용할 수 있습니다. 이 구성 요소는 내용 쿼리나 다른 종류의 DMX 문을 실행하는 데 사용할 수 없습니다.|  
  
##  <a name="bkmk_API"></a> 응용 프로그래밍 인터페이스(Application Programming Interfaces)  
 OLE DB 또는 Analysis Services ADOMD 클라이언트와 같은 서버 프로토콜과 함께 다양한 프로그래밍 언어를 사용하여 데이터 마이닝 모델에 대해 쿼리를 실행하는 사용자 지정 응용 프로그램을 만들 수 있습니다. 자세한 내용은 [데이터 마이닝 프로그래밍](../dev-guide/data-mining-programming.md)을 참조하세요.  
  
 하지만 XMLA는 Analysis Service 서버와의 모든 상호 작용에 대한 기본 메시지 형식을 구성합니다. XMLA 메시지 내에서 쿼리는 DMX를 기반으로 하는 예측 쿼리를 전송하는지, 내용 쿼리를 전송하는지 또는 데이터 마이닝 스키마 행 집합을 사용하여 모델 메타데이터를 검색하는 쿼리를 전송하는지에 따라 다르게 표현됩니다.  
  
-   **예측 쿼리** 및 다른 모든 DMX 문의 텍스트는 XMLA [Command 요소&#40;XMLA&#41;](../xmla/xml-elements-properties/command-element-xmla.md) 요소의 [Statement 요소&#40;XMLA&#41;](../xmla/xml-elements-commands/statement-element-xmla.md) 요소 내에 텍스트로 배치된 DMX 쿼리와 함께 [Execute 메서드&#40;XMLA&#41;](../xmla/xml-elements-methods-execute.md) 메서드를 사용하여 XMLA로 전송됩니다.  
  
-   클러스터 수, 의사 결정 트리에 사용된 특성, 모델이 마지막으로 처리된 날짜, 모델을 만들 때 사용된 알고리즘 매개 변수와 같은 **모델 콘텐츠** 및 **모델 메타데이터**를 검색하려면 [Discover 메서드&#40;XMLA&#41;](../xmla/xml-elements-methods-discover.md) 메서드를 사용하고 [RequestType 요소&#40;XMLA&#41;](../xmla/xml-elements-properties/type-element-xmla.md) 머리글에서 데이터 마이닝 스키마 행 집합 중 하나를 지정할 수 있습니다. 쿼리의 범위를 좁히려면 [RestrictionList 요소&#40;XMLA&#41;](../xmla/xml-elements-properties/restrictionlist-element-xmla.md) 요소 내에 제한 사항으로 조건을 입력합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 참조](/sql/dmx/data-mining-extensions-dmx-reference)   
 [데이터 마이닝 솔루션](data-mining-solutions.md)   
 [DMX Select 문 이해](/sql/dmx/understanding-the-dmx-select-statement)   
 [구조 및 사용법 DMX 예측 쿼리](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)   
 [예측 쿼리 작성기를 사용 하 여 예측 쿼리 만들기](create-a-prediction-query-using-the-prediction-query-builder.md)   
 [SQL Server Management Studio에서 DMX 쿼리 만들기](create-a-dmx-query-in-sql-server-management-studio.md)  
  
  
