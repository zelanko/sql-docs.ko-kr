---
title: 다차원 모델의 번역 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.deletelanguagefirm.f1
ms.assetid: 5521f8ef-b10a-4861-9df7-1e43e0a1fb3f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f3238267021c0fd4054fb9757ea8d00cae6114dc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218945"
---
# <a name="translations-in-multidimensional-models"></a>다차원 모델의 번역
  다국어 지원은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 번역을 사용 하 여 수행 됩니다. 번역에는 다국어로 제공할 수 있는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체 속성의 언어 식별자와 바인딩이 포함됩니다. 예를 들어 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 대해 번역을 정의하여 지정한 언어로 해당 데이터베이스의 캡션과 설명을 제공할 수 있습니다. 번역에 대 한 자세한 내용은 참조 하세요. [큐브 번역](../multidimensional-models-olap-logical-cube-objects/cube-translations.md)합니다.  
  
## <a name="defining-translations"></a>번역 정의  
 번역할 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 개체에 적절한 디자이너를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 번역을 정의할 수 있습니다. 번역을 정의 생성을 `Translation` 적절 한 연관 된 개체 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결 된 속성에 대해 지정한 언어로 지정한 명시적 리터럴 값을 가진 개체를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체입니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 번역이 연결될 수 있는 개체와 속성은 다음과 같습니다.  
  
|Object|속성|디자이너|  
|------------|----------------|--------------|  
|데이터베이스|`Caption`, `Description`|[일반 &#40;데이터베이스 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](../general-database-designer-analysis-services-multidimensional-data.md)|  
|Cube|`Caption`, `Description`|[번역 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|측정값 그룹|`Caption`|[번역 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|이름|`Caption`, `DisplayFolder`|[번역 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|큐브 차원|`Caption`|[번역 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Cube|`Caption`|[번역 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|KPI(핵심 성과 지표)|`Caption`, `Description`, `DisplayFolder`|[번역 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|작업|`Caption`|[번역 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|명명된 집합|`Caption`|[번역 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|계산 멤버|`Caption`|[번역 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|데이터베이스 차원|`Caption`, `AttributeAllMember`|[번역 &#40;차원 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|attribute|`Caption`를 `CaptionColumn` <sup>1</sup>하십시오 `AttributeHierarchyDisplayFolder`, `NamingTemplate`, `MembersWithDataCaption`|[번역 &#40;차원 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|계층|`Caption`, `AllMemberName`|[번역 &#40;차원 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|Level|`Caption`|[번역 &#40;차원 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
  
 <sup>1</sup> 는 `CaptionColumn` 특성의 속성을 데이터 원본 뷰의 열에 바인딩될 수 및 이외의 다른 번역과 달리 인스턴스에 지정 된 Windows 데이터 정렬을 사용할 수 있습니다.  
  
### <a name="defining-attribute-translations"></a>특성 번역 정의  
 데이터베이스 차원의 특성과 연결된 번역은 다른 번역과 달리 다음과 같이 처리됩니다.  
  
-   명시적 리터럴 값 대신 열 바인딩을 `CaptionColumn` 속성과 연결하여 해당 특성의 멤버 이름을 번역할 수 있습니다.  
  
-   인스턴스에 지정된 데이터 정렬이 아닌 Windows 데이터 정렬을 사용할 수 있으므로 번역에 지정한 언어에 대해 특성 멤버를 올바로 정렬할 수 있습니다.  
  
 사용할 수 있습니다는 **특성 데이터 번역** 대화 상자 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 데이터베이스 차원의 특성에 대 한 번역을 정의할 수 있습니다. 에 대 한 자세한 내용은 합니다 **특성 데이터 번역** 대화 상자, 참조 [특성 데이터 번역 대화 상자 &#40;Analysis Services-Multidimensional Data&#41;](../attribute-data-translation-dialog-box-analysis-services-multidimensional-data.md).  
  
## <a name="resolving-translations"></a>번역 확인  
 클라이언트 애플리케이션이 지정한 언어 식별자로 정보를 요청하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체의 데이터 및 메타데이터를 가장 근사한 언어 식별자로 확인합니다. 클라이언트 애플리케이션이 기본 언어를 지정하지 않거나 중립 로캘 ID(0) 또는 기본 언어 처리 식별자(1024)를 지정하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 인스턴스에 대해 기본 언어를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체의 데이터 및 메타데이터를 반환합니다.  
  
 클라이언트 애플리케이션이 기본 언어 식별자가 아닌 언어 식별자를 지정하면 인스턴스는 모든 사용 가능한 개체에 대해 모든 사용 가능한 번역을 반복합니다. 지정한 언어 식별자가 특정 번역의 언어 식별자와 일치하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 해당 번역을 반환합니다. 일치하는 항목이 없으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 다음 방법 중 하나를 사용하여 지정한 언어 식별자와 가장 근사한 언어 식별자를 가진 번역을 반환합니다.  
  
-   다음 언어 식별자의 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 지정한 언어 식별자의 번역이 정의되지 않은 경우에 대해 대체 언어 식별자를 사용합니다.  
  
    |지정한 언어 식별자|대체 언어 식별자|  
    |-----------------------------------|-----------------------------------|  
    |3076 - 중국어(홍콩 특별 행정구, 중국)|1028 - 중국어(대만)|  
    |5124 - 중국어(마카오 특별 행정구)|1028 - 중국어(대만)|  
    |1028 - 중국어(대만)|기본 언어|  
    |4100 - 중국어(싱가포르)|2052 - 중국어(중국)|  
    |2074 - 크로아티아어|기본 언어|  
    |3098 - 크로아티아어(키릴 자모)|기본 언어|  
  
-   다른 모든 지정한 언어 식별자의 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 지정한 언어 식별자의 주 언어를 추출하고 이 언어에 가장 일치하는 Windows 언어 식별자를 검색합니다. 가장 일치하는 언어 식별자의 번역이 없거나 지정한 언어 식별자가 주 언어에 가장 일치하면 기본 언어가 사용됩니다.  
  
## <a name="deleting-translation-objects"></a>번역 개체 삭제  
 차원 디자이너 또는 큐브 디자이너에서 번역 개체를 마우스 오른쪽 단추로 클릭하여 영구적으로 제거할 수 있습니다. 삭제된 개체를 복원하거나 재활용할 수는 없으므로 계속하기 전에 영향을 받는 개체의 목록을 검토해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 다차원에 대 한 세계화 시나리오](../globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [언어 및 데이터 정렬 &#40;Analysis Services&#41;](../languages-and-collations-analysis-services.md)  
  
  
