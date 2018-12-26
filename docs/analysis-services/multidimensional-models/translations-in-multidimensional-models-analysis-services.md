---
title: 번역 (Analysis Services) 다차원 모델의 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b8511efe6b567fad82ab45f7f5a53188b0f13643
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147078"
---
# <a name="translations-in-multidimensional-models-analysis-services"></a>다차원 모델의 번역(Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  번역할 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 개체에 적절한 디자이너를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 번역을 정의할 수 있습니다. 번역을 정의하면 해당 **개체와 연결된** 개체의 속성에 대해 지정한 언어로 지정한 명시적 리터럴 값을 가진 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Translation [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체가 생성됩니다.  
  
## <a name="elements-of-a-multi-lingual-data-model"></a>다국어 데이터 모델의 요소  
 다국어 솔루션에 사용되는 데이터 모델에서는 번역된 레이블(필드 이름 및 설명) 이상의 것들이 필요합니다. 또한 다양한 언어 스크립트에 명시되는 데이터 값도 제공해야 합니다. 다국어 솔루션을 만들려면 개별 특성이 데이터를 반환하는 외부 데이터베이스의 열에 바인딩되어야 합니다.  
  
 Adventure Works 샘플 데이터베이스(관계형 데이터 웨어하우스는 물론 다차원 데이터베이스 포함)에서는 Analysis Services의 번역 기능을 보여 줍니다. 샘플 모델에는 번역된 캡션과 설명이 포함됩니다. 샘플 관계형 데이터 웨어하우스에는 모델에서 지역화된 특성 멤버를 제공하는 번역된 값의 열이 포함됩니다.  
  
 모델에 사용할 수 있는 번역된 데이터 값을 보기:  
  
1.  Adventure Works 다차원 모델을 디자이너에서 엽니다.  
  
2.  솔루션 탐색기에서 데이터 원본 뷰를 열고 Adventure Works DW를 두 번 클릭\<버전 >.dsv 합니다.  
  
3.  dimDate, dimProduct, dimProductCategory 또는 dimProductSubcateogry를 찾습니다. 이 차원들 모두에는 월, 요일, 제품 이름, 범주 이름 등에 대한 번역된 멤버용 특성이 포함되어 있습니다.  
  
4.  임의 필드를 마우스 오른쪽 단추로 클릭하고 **데이터 탐색**을 선택합니다. 각 멤버의 영어, 스페인어, 프랑스어 번역이 표시됩니다.  
  
 날짜, 시간 및 통화에 대한 형식은 번역을 통해 구현되지 않습니다. 클라이언트의 로캘을 기반으로 문화 관련 형식을 동적으로 제공하려면 통화 변환 마법사와 **FormatString** 속성을 사용합니다. 자세한 내용은 [통화 변환&#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md) 및 [FormatString 요소&#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/formatstring-element-assl)를 참조하세요.  
  
 Analysis Services 자습서의[Lesson 9: Defining Perspectives and Translations](../../analysis-services/lesson-9-defining-perspectives-and-translations.md) 에서는 번역 만들기 및 테스트를 위한 절차를 순서대로 안내합니다.  
  
## <a name="defining-translations"></a>번역 정의  
  
### <a name="add-translations-to-a-cube"></a>큐브에 번역 추가  
 큐브, 측정값 그룹, 측정값, 큐브 차원, 큐브 뷰, KPI, 작업, 명명된 집합 및 계산된 멤버에 번역을 추가할 수 있습니다.  
  
1.  솔루션 탐색기에서 큐브 이름을 두 번 클릭하여 큐브 디자이너를 엽니다.  
  
2.  **번역** 탭을 클릭합니다. 번역을 지원하는 모든 개체는 이 페이지에 나열됩니다.  
  
3.  각 개체에 대해 대상 언어(내부적으로 LCID로 확인됨), 번역된 캡션 및 번역된 설명을 지정합니다. 언어 목록은 Management Studio에서 서버 언어를 설정하든, 아니면 단일 특성에 대한 번역 재정의를 추가하든 상관없이 전체 Analysis Services에서 일관됩니다.  
  
     데이터 정렬은 변경할 수 없다는 것을 기억해야 합니다. 번역 캡션을 통해 여러 언어를 지원하더라도 큐브에서는 기본적으로 하나의 데이터 정렬을 사용합니다(아래에 설명된 차원 특성의 경우 예외가 있음). 언어가 공유 데이터 정렬에서 제대로 정렬되지 않는 경우 데이터 정렬 요구 사항에 맞게 큐브를 복사해야 합니다.  
  
4.  프로젝트를 빌드하고 배포합니다.  
  
5.  로캘 식별자를 사용하도록 연결 문자열을 수정하여 Excel과 같은 클라이언트 애플리케이션을 사용하는 데이터베이스에 연결합니다. 자세한 내용은 [세계화 팁과 모범 사례&#40;Analysis Services&#41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md) 를 참조하세요.  
  
### <a name="add-translations-to-a-dimension-and-attributes"></a>차원 및 특성에 번역 추가  
 데이터베이스 차원, 특성, 계층 구조 및 계층 구조 내 수준에 번역을 추가할 수 있습니다.  
  
 번역된 캡션은 키보드나 복사-붙여넣기를 사용하여 수동으로 모델에 추가되지만 차원 특성 멤버의 경우 외부 데이터베이스에서 번역된 값을 얻을 수 있습니다. 특히 어떤 특성의 **CaptionColumn** 속성은 데이터 원본 뷰에 있는 열에 바인딩할 수 있습니다.  
  
 특성 수준에서 데이터 정렬 설정을 재정의할 수 있습니다. 예를 들어 전자/반자 구분을 조정하거나 특정 특성에 이진 정렬을 사용할 수도 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 데이터 정렬은 데이터 바인딩이 정의되어 있는 곳에 노출됩니다. 차원 특성 번역을 DSV에 있는 다른 원본 열에 바인딩하게 되므로 원본 열에 의해 사용되는 데이터 정렬을 지정할 수 있도록 데이터 정렬 설정을 사용할 수 있습니다. 관계형 데이터베이스의 열 데이터 정렬에 대한 자세한 내용은 [Set or Change the Column Collation](../../relational-databases/collations/set-or-change-the-column-collation.md) 을 참조하세요.  
  
1.  솔루션 탐색기에서 차원 이름을 두 번 클릭하여 차원 디자이너를 엽니다.  
  
2.  **번역** 탭을 클릭합니다. 번역을 지원하는 모든 차원 개체가 이 페이지에 나열됩니다.  
  
     각 개체에 대해 대상 언어(LCID로 확인), 번역된 캡션 및 번역된 설명을 지정합니다. 언어 목록은 Management Studio에서 서버 언어를 설정하든, 아니면 단일 특성에 대한 번역 재정의를 추가하든 상관없이 전체 Analysis Services에서 일관됩니다.  
  
3.  번역된 값을 제공하는 열에 특성 바인딩:  
  
    1.  역시 차원 디자이너에서 | **번역**에서 새 번역을 추가합니다. 언어를 선택합니다. 번역된 값을 허용하도록 페이지에 새 열이 나타납니다.  
  
    2.  특성 중 하나에 인접한 빈 셀에 커서를 놓습니다. 이 특성은 키가 될 수 없지만 다른 모든 특성은 가능한 선택 항목입니다. 안에 점이 있는 작은 단추가 표시됩니다. 단추를 클릭하여 **특성 데이터 번역 대화 상자**를 엽니다.  
  
    3.  캡션에 대한 번역을 입력합니다. 이 번역은 대상 언어로 된 데이터 레이블로 사용됩니다. 예를 들어 피벗 테이블 필드 목록의 필드 이름으로 사용됩니다.  
  
    4.  특성 멤버의 번역된 값을 제공하는 원본 열을 선택합니다. 차원에 바인딩된 테이블 또는 쿼리의 유일한 기존 열을 사용할 수 있습니다. 이 열이 없으면 데이터 원본 뷰, 차원 및 큐브를 수정하여 열을 선택해야 합니다.  
  
    5.  해당하는 경우 데이터 정렬 및 정렬 순서를 선택합니다.  
  
4.  프로젝트를 빌드하고 배포합니다.  
  
5.  로캘 식별자를 사용하도록 연결 문자열을 수정하여 Excel과 같은 클라이언트 애플리케이션을 사용하는 데이터베이스에 연결합니다. 자세한 내용은 [세계화 팁과 모범 사례&#40;Analysis Services&#41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md)를 참조하세요.  
  
### <a name="add-a-translation-of-the-database-name"></a>데이터베이스 이름의 번역 추가  
 데이터베이스 수준에서 데이터베이스 이름 및 설명에 대한 번역을 추가할 수 있습니다. 번역된 데이터베이스 이름은 언어의 LCID를 지정하는 클라이언트 연결에 표시될 수도 있지만 이것은 도구에 따라 다릅니다. 예를 들어, 연결에서 로캘 식별자를 지정하더라도 Management Studio에서는 데이터베이스를 볼 때 번역된 이름이 표시되지 않습니다. Analysis Services에 연결하기 위해 Management Studio에서 사용하는 API는 **Language** 속성을 읽지 않습니다.  
  
1.  솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하고 | **데이터베이스 편집** 을 선택하여 데이터베이스 디자이너를 엽니다.  
  
2.  번역에서 대상 언어(LCID로 확인), 번역된 캡션 및 번역된 설명을 지정합니다. 언어 목록은 Management Studio에서 서버 언어를 설정하든, 아니면 단일 특성에 대한 번역 재정의를 추가하든 상관없이 전체 Analysis Services에서 일관됩니다.  
  
3.  데이터베이스의 속성 페이지에서 **Language** 를 번역에 대해 지정한 것과 동일한 LCID로 설정합니다. 원할 경우 기본값이 더 이상 적절하지 않다면 **Collation** 도 설정합니다.  
  
4.  데이터베이스를 빌드하고 배포합니다.  
  
## <a name="deleting-translation-objects"></a>번역 개체 삭제  
 차원 디자이너 또는 큐브 디자이너에서 번역 개체를 마우스 오른쪽 단추로 클릭하여 영구적으로 제거할 수 있습니다. 삭제된 개체를 복원하거나 재활용할 수는 없으므로 계속하기 전에 영향을 받는 개체의 목록을 검토해야 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services의 세계화 시나리오](../../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [언어 및 데이터 정렬&#40;Analysis Services&#41;](../../analysis-services/languages-and-collations-analysis-services.md)  
  
  
