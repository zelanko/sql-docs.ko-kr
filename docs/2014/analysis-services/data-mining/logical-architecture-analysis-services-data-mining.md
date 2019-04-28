---
title: 논리적 아키텍처 (Analysis Services-데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], about mining structures
- logical architecture [Data Mining]
- architecture [Analysis Services], mining models
- mining models [Analysis Services], about data mining models
- architecture [Analysis Services]
ms.assetid: 4e0cbf46-cc60-4e91-a292-9a69f29746f0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fbfbdc87e7657f8d1d20e75186be2f3c0d79a900
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722195"
---
# <a name="logical-architecture-analysis-services---data-mining"></a>논리적 아키텍처(Analysis Services - 데이터 마이닝)
  데이터 마이닝은 여러 구성 요소와의 상호 작용을 수반하는 프로세스입니다.  
  
-   우선 학습, 테스트 및 예측에 사용하기 위해 SQL Server 데이터베이스나 기타 데이터 원본에 있는 데이터의 원본에 액세스해야 합니다.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 Visual Studio를 사용하여 데이터 마이닝 구조와 모델을 정의합니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 데이터 마이닝 개체를 관리하고 예측 및 쿼리를 만듭니다.  
  
-   솔루션이 완료되면 이를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 인스턴스에 배포합니다.  
  
 이러한 솔루션 개체를 만드는 프로세스는 이미 여러 곳에 설명되어 있습니다. 자세한 내용은 [데이터 마이닝 솔루션](data-mining-solutions.md)을 참조하세요.  
  

  
##  <a name="bkmk_SourceData"></a> 데이터 마이닝 원본 데이터  
 데이터 마이닝에 사용하는 데이터는 데이터 마이닝 솔루션에 저장되지 않고 바인딩만 저장됩니다. 데이터는 이전 버전의 SQL Server 또는 CRM 시스템에서 만들거나 플랫 파일로 만든 데이터베이스에 있을 수도 있습니다. 구조나 모델을 처리하여 학습하는 경우 데이터의 통계 요약이 생성됩니다. 이 통계 요약은 이후 작업에 사용하도록 유지될 수 있는 캐시에 저장되거나 처리 후 삭제됩니다. 자세한 내용은 [마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](mining-structures-analysis-services-data-mining.md)를 참조하세요.  
  
 데이터 원본 위에 추상화 계층을 제공하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DSV(데이터 원본 뷰) 개체 내에서 서로 다른 데이터를 조합할 수 있습니다. 테이블 간의 조인을 지정하거나 다 대 일 관계를 갖는 테이블을 추가하여 중첩 테이블 열을 만들 수 있습니다. 이러한 개체의 정의, 데이터 원본 및 데이터 원본 뷰는 *.ds 및 \*.dsv 파일 이름 확장명으로 솔루션 내에 저장됩니다. 만들기 및 사용 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본 및 데이터 원본 뷰를 참조 하세요 [지 원하는 데이터 원본 &#40;SSAS 다차원&#41;](../multidimensional-models/supported-data-sources-ssas-multidimensional.md)합니다.  
  
 AMO 또는 XMLA를 사용하여 데이터 원본 및 데이터 원본 뷰를 정의하고 변경할 수도 있습니다. 이러한 개체를 프로그래밍 방식으로 작업하는 방법에 대한 자세한 내용은 [논리 아키텍처 개요&#40;Analysis Services - 다차원 데이터&#41;](../multidimensional-models/olap-logical/logical-architecture-overview-analysis-services-multidimensional-data.md)를 참조하세요.  
  

  
##  <a name="bkmk_Structures"></a> Mining Structures  
 데이터 마이닝 구조는 마이닝 모델이 생성된 데이터 도메인을 정의하는 논리적 데이터 컨테이너입니다. 단일 마이닝 구조가 여러 마이닝 모델을 지원할 수 있습니다.  
  
 데이터 마이닝 솔루션에서 데이터를 사용해야 할 경우 Analysis Services에서는 원본의 데이터를 읽고 집계와 그 밖의 정보에 대한 캐시를 생성합니다. 기본적으로 이 캐시는 추가 모델을 지원하는 데 학습 데이터를 다시 사용할 수 있도록 유지됩니다. 캐시를 삭제하려면 마이닝 구조 개체의 `CacheMode` 속성을 `ClearAfterProcessing` 값으로 변경합니다. 자세한 내용은 [AMO 데이터 마이닝 클래스](https://docs.microsoft.com/bi-reference/amo/amo-data-mining-classes)를 참조하세요.  
  
 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 에서는 데이터를 학습 데이터 집합과 테스트 데이터 집합으로 분리하는 기능도 제공하므로 임의로 선택된 대표 데이터 집합에 대해 마이닝 모델을 테스트할 수 있습니다. 구조 캐시의 데이터는 실제 별도로 저장되는 것이 아니라 해당 특정 사례가 학습에 사용되는지, 테스트에 사용되는지를 나타내는 속성으로 표시됩니다. 캐시를 삭제한 경우에는 해당 정보를 검색할 수 없습니다.  
  
 자세한 내용은 [마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](mining-structures-analysis-services-data-mining.md)를 참조하세요.  
  
 데이터 마이닝 구조에는 중첩 테이블이 포함될 수도 있습니다. 중첩 테이블은 기본 데이터 테이블에서 모델링된 사례에 대한 추가 정보를 제공합니다. 자세한 내용은 [중첩 테이블&#40;Analysis Services - 데이터 마이닝&#41;](nested-tables-analysis-services-data-mining.md)을 참조하세요.  
  
 
  
##  <a name="bkmk_Models"></a> Mining Models  
 처리하기 전의 데이터 마이닝 모델은 메타데이터 속성의 조합에 불과합니다. 이러한 속성은 마이닝 구조와 데이터 마이닝 알고리즘을 지정하며 데이터가 처리되는 방식에 영향을 주는 매개 변수 및 필터 설정의 컬렉션을 정의합니다. 자세한 내용은 [마이닝 모델&#40;Analysis Services - 데이터 마이닝&#41;](mining-models-analysis-services-data-mining.md)을 참조하세요.  
  
 모델을 처리할 때 마이닝 구조 캐시에 저장된 학습 데이터는 데이터의 통계 속성과 알고리즘 및 해당 매개 변수에 의해 정의된 추론을 기반으로 패턴을 생성하는 데 사용됩니다. 이를 모델 *학습* 이라고 합니다.  
  
 학습 결과는 *모델 콘텐츠*내에 포함된 요약 데이터의 집합으로서, 발견된 패턴을 설명하고 예측을 생성하는 데 사용되는 규칙을 제공합니다. 자세한 내용은 [마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](mining-model-content-analysis-services-data-mining.md)를 참조하세요.  
  
 일부 사례에서는 모델의 논리 구조를 PMML(Predictive Modeling Markup Language)이라는 표준 형식에 따라 모델 수식 및 데이터 바인딩을 나타내는 파일로 내보낼 수도 있습니다. 이 논리 구조를 PMML을 활용하는 다른 시스템으로 가져올 수 있으며, 그런 다음 설명된 모델을 예측에 사용할 수 있습니다. 자세한 내용은 [DMX Select 문 이해](/sql/dmx/understanding-the-dmx-select-statement)를 참조하세요.  
  

  
##  <a name="bkmk_CustomObjects"></a> 사용자 지정 데이터 마이닝 개체  
 데이터 마이닝 프로젝트의 컨텍스트에서 사용하는 다른 개체(예: 정확도 차트 또는 예측 쿼리)는 솔루션 내에서 유지되지 않지만 ASSL을 사용하여 스크립팅하거나 AMO를 사용하여 생성할 수 있습니다.  
  
 또한 다음과 같은 사용자 지정 개체를 추가하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 인스턴스에서 사용 가능한 서비스 및 기능을 확장할 수 있습니다.  
  
 **사용자 지정 어셈블리**  
 CLR 또는 COM 규격 언어를 사용하여 .NET 어셈블리를 정의한 다음 SQL Server 인스턴스에 등록할 수 있습니다. 어셈블리 파일은 애플리케이션에 의해 정의된 위치에서 로드되며 복사본이 데이터와 함께 서버에 저장됩니다. 어셈블리 파일의 복사본은 서버가 시작될 때마다 어셈블리를 로드하는 데 사용됩니다.  
  
 자세한 내용은 [다차원 모델 어셈블리 관리](../multidimensional-models/multidimensional-model-assemblies-management.md)를 참조하세요.  
  
 **사용자 지정 저장 프로시저**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 마이닝은 저장 프로시저를 사용한 데이터 마이닝 개체 작업을 지원합니다. 사용자 고유의 저장 프로시저를 만들어 기능을 확장하거나 예측 쿼리 및 내용 쿼리에서 반환된 데이터를 쉽게 사용할 수 있습니다.  
  
 [저장 프로시저 정의](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
 교차 유효성 검사를 수행하는 데 사용할 수 있는 저장 프로시저는 다음과 같습니다.  
  
 [데이터 마이닝 저장 프로시저&#40;Analysis Services - 데이터 마이닝&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
 또한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에는 데이터 마이닝에 내부적으로 사용되는 많은 시스템 저장 프로시저가 포함되어 있습니다. 시스템 저장 프로시저는 내부적으로 사용되지만 유용한 바로 가기를 지정할 수 있습니다. Microsoft는 이러한 저장 프로시저를 필요에 따라 변경할 권리가 있습니다. 따라서 프로덕션 환경에서 사용하려는 경우 DMX, AMO 또는 XMLA를 사용하여 쿼리를 만드는 것이 좋습니다.  
  
 **사용자 지정 플러그 인 알고리즘**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 사용자 고유의 알고리즘을 만들어 서버 인스턴스에 새 데이터 마이닝 서비스로 추가할 수 있는 메커니즘을 제공합니다.  
  
 Analysis Services에서는 COM 인터페이스를 사용하여 플러그 인 알고리즘과 통신합니다. 새 알고리즘을 구현하는 방법에 대한 자세한 내용은 [Plugin Algorithms](plugin-algorithms.md)을 참조하십시오.  
  
 새 알고리즘을 사용하려면 먼저 각각의 새 알고리즘을 등록해야 합니다. 알고리즘을 등록하려면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스의 .ini 파일에 알고리즘의 필수 메타데이터를 추가하면 됩니다. 새 알고리즘을 사용할 각 인스턴스에 정보를 추가해야 합니다. 알고리즘을 추가한 후에는 인스턴스를 다시 시작하고 MINING_SERVICES 스키마 행 집합을 사용하여 알고리즘에서 지원하는 옵션 및 공급자를 비롯한 새 알고리즘을 볼 수 있습니다.  
  

  
## <a name="see-also"></a>관련 항목  
 [다차원 모델 개체 처리](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [DMX&#40;Data Mining Extensions&#41; 참조](/sql/dmx/data-mining-extensions-dmx-reference)  
  
  
