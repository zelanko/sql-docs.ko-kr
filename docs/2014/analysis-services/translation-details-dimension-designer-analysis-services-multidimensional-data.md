---
title: 번역 세부 정보 (번역 탭, 차원 디자이너) (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.translations.translationpane.tranlationdetails.f1
ms.assetid: 0aa61df3-f2b0-4703-a63b-124da672dcc3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f8debb50a798ba46457942e0e79a9d45ab392c1
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66065850"
---
# <a name="translation-details-translations-tab-dimension-designer-analysis-services---multidimensional-data"></a>번역 세부 정보(번역 탭, 차원 디자이너)(Analysis Services - 다차원 데이터)
  차원 디자이너에서 **번역** 탭의 **번역 세부 정보** 창을 사용하여 현재 선택한 차원의 번역을 정의하고 관리할 수 있습니다.  
  
 **번역 세부 정보 창을 표시 하려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트를 연 다음 원하는 차원을 엽니다.  
  
2.  **번역** 탭을 클릭합니다.  
  
## <a name="options"></a>변수  
 **기본 언어**  
 차원 개체의 이름을 기본 언어로 설정합니다.  
  
 **개체 유형**  
 번역될 속성을 표시합니다. 값이 지정된 개체와 속성만 번역할 수 있습니다. 다음은 번역할 수 있는 속성입니다.  
  
-   차원  
  
     `Caption` 및 `AttributeAllMember` 속성  
  
-   attribute  
  
     `Caption`, `AttributeHierarchyDisplayFolder` 및 `NamingTemplate` 속성  
  
    > [!NOTE]  
    >  `NamingTemplate` 속성은 부모 특성에 대해서만 사용할 수 있습니다.  
  
-   계층  
  
     `Caption` 및 `AllMemberName` 속성  
  
-   Level  
  
     `Caption` 속성  
  
 **\<Language>**  
 차원 개체의 속성 값을 선택한 언어로 입력하거나 선택합니다. 줄임표 단추(**...**)를 클릭하면 편집 중인 속성에 따라 추가 대화 상자가 열립니다.  
  
-   `NamingTemplate` 속성  
  
     [수준 명명 템플릿 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](level-naming-template-dialog-box-analysis-services-multidimensional-data.md)를 표시합니다.  
  
-   `Caption` 속성(특성의 경우)  
  
     [특성 데이터 번역 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](attribute-data-translation-dialog-box-analysis-services-multidimensional-data.md)를 표시합니다.  
  
## <a name="shortcut-menu"></a>바로 가기 메뉴  
 다음 옵션은 **번역 세부 정보** 창에서 번역을 마우스 오른쪽 단추로 클릭하면 표시되는 바로 가기 메뉴에서 사용할 수 있습니다.  
  
 **새 번역**  
 **언어 선택** 대화 상자를 표시하여 새 번역을 만들려면 선택합니다. 해당 번역은 **번역 세부 정보** 표에 새 열로 나타납니다.  
  
 **번역 삭제**  
 선택한 번역을 삭제하려면 선택합니다.  
  
> [!NOTE]  
>  이 옵션은 셀을 마우스 오른쪽 단추로 클릭하여 번역을 삭제한 경우에만 사용할 수 있습니다.  
  
 **새 캡션 열**  
 **특성 데이터 번역** 대화 상자를 표시하고 **번역 세부 정보** 표에서 특성을 수정할 때 새 캡션 열을 정의하려면 선택합니다. 이 옵션을 사용하려면 **번역 세부 정보** 표에서 특성에 대한 번역 열의 셀을 선택해야 합니다.  
  
> [!NOTE]  
>  이 옵션은 셀을 마우스 오른쪽 단추로 클릭하여 특성의 번역 열을 삭제한 경우에만 사용할 수 있습니다.  
  
 **캡션 열 편집**  
 **특성 데이터 번역** 대화 상자를 표시하고 **번역 세부 정보** 표에서 특성을 수정할 때 기존 캡션 열을 수정하려면 선택합니다.  
  
> [!NOTE]  
>  이 옵션은 **번역 세부 정보** 표에서 특성에 대한 캡션 열이 포함된 번역 열의 셀을 선택하는 경우에만 사용할 수 있습니다.  
  
 **캡션 열 삭제**  
 **번역 세부 정보** 표에서 선택한 특성의 캡션 열을 삭제하려면 선택합니다.  
  
> [!NOTE]  
>  이 옵션은 특성의 캡션 열이 포함된 번역 열의 셀을 마우스 오른쪽 단추로 클릭한 경우에만 사용할 수 있습니다.  
  
 **모든 특성 표시**  
 특성 계층이 해제된 특성을 포함하여 선택한 차원에 대해 정의된 모든 특성을 표시하거나 숨기려면 선택합니다.  
  
## <a name="see-also"></a>관련 항목  
 [번역 &#40;차원 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
