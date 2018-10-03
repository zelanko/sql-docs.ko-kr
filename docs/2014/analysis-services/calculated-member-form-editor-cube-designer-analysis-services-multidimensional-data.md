---
title: 계산 멤버 폼 편집기 (계산 탭, 큐브 디자이너) (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.calculationexpression.calculatedmember.f1
ms.assetid: f7719b9e-b1e6-4792-90a6-30d9d8eb1196
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3a16319b01c6555aa3bf299da201d9662cd59f4b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049113"
---
# <a name="calculated-member-form-editor-calculations-tab-cube-designer-analysis-services---multidimensional-data"></a>계산 멤버 폼 편집기(계산 탭, 큐브 디자이너)(Analysis Services - 다차원 데이터)
  큐브 디자이너의 **계산** 탭에 있는 **계산 멤버 폼 편집기** 창을 사용하여 계산 멤버를 만들거나 수정할 수 있습니다.  
  
 **참고** 이 창은 폼 보기에만 표시됩니다.  
  
## <a name="options"></a>변수  
 **이름**  
 계산 멤버의 이름을 입력합니다.  
  
 **부모 속성**  
 **부모 계층**, **부모 멤버**및 **변경** 옵션을 보려면 확장합니다.  
  
 **부모 계층**  
 선택한 큐브에서 계산 멤버를 포함할 차원 및 계층을 선택합니다. 계산 측정값을 정의하려면 MEASURES를 선택합니다.  
  
 **부모 멤버**  
 계산 멤버 위에 나타낼 멤버를 선택합니다.  
  
 **참고** 이 옵션은 **부모 계층** 이 MEASURES 이외의 계층을 지정하는 경우에만 사용할 수 있습니다.  
  
 **변경**  
 **부모 멤버 선택** 대화 상자를 표시하여 **부모 멤버**에 대한 멤버를 선택하려면 이 옵션을 선택합니다. **부모 멤버 선택** 대화 상자에 대한 자세한 내용은 [부모 멤버 선택 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](select-parent-member-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.  
  
 **식**  
 계산 멤버에 대한 MDX(Multidimensional Expression) 식을 보거나 편집하려면 확장합니다.  
  
 **계산 도구** 창에서 선택한 요소를 이 옵션으로 끌어서 놓으면 선택한 요소의 MDX 구문을 포함시킬 수 있습니다.  
  
> [!NOTE]  
>  이 식은 문자열 또는 숫자 값으로 계산되는 것이 좋습니다.  
  
 **추가 속성**  
 **형식 문자열**, **표시**, **비어 있지 않은 동작**, **색 식**및 **글꼴 식** 옵션을 보려면 확장합니다.  
  
 **형식 문자열**  
 계산 멤버가 반환한 값의 형식을 지정하는 데 사용되는 MDX 형식 문자열을 입력하거나 미리 정의된 형식 문자열을 선택합니다.  
  
 MDX 형식 문자열에 대한 자세한 내용은 [FORMAT_STRING 내용&#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)을 참조하세요.  
  
 **Visible**  
 계산 멤버를 클라이언트 응용 프로그램에 표시하려면 **True** 를 선택합니다.  
  
 **비어 있지 않은 동작**  
 계산 멤버에 대해 MDX로 NON EMPTY 쿼리를 해결하는 데 사용하는 측정값의 이름을 선택합니다. **비어 있지 않은 동작** 속성이 비어 있는 경우 계산 멤버를 반복적으로 계산하여 멤버가 비어 있는지 확인해야 합니다. **비어 있지 않은 동작** 속성에 측정값의 이름이 있는 경우 지정한 측정값이 비어 있으면 계산 멤버도 비어 있는 것으로 처리됩니다.  
  
> [!WARNING]  
>  이 속성은 더 이상 사용되지 않습니다. 이 속성을 설정하지 마세요. 참조 [SQL Server 2014에서 Analysis Services 기능의 사용 되지 않는](deprecated-analysis-services-features-in-sql-server-2014.md) 세부 정보에 대 한 합니다.  
  
 **색 식**  
 **전경색** 및 **배경색** 옵션을 보려면 확장합니다.  
  
 **전경색**  
 계산 멤버의 전경색을 지정하는 MDX 식을 입력합니다.  
  
 **계산 도구** 창에서 선택한 요소를 이 옵션으로 끌어서 놓으면 선택한 요소의 MDX 구문을 포함시킬 수 있습니다.  
  
 색 선택 단추를 클릭하여 **색** 대화 상자를 표시하고 지정한 색의 RGB(Red-Green-Blue) 값을 MDX 식에 삽입할 수 있습니다. RGB 값에 대한 자세한 내용은 [FORE_COLOR 및 BACK_COLOR 내용&#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)을 참조하세요.  
  
 **배경색입니다.**  
 계산 멤버의 배경색을 지정하는 MDX 식을 입력합니다.  
  
 **계산 도구** 창에서 선택한 요소를 이 옵션으로 끌어서 놓으면 선택한 요소의 MDX 구문을 포함시킬 수 있습니다.  
  
 색 선택 단추를 클릭하여 **색** 대화 상자를 표시하고 지정한 색의 RGB(Red-Green-Blue) 값을 MDX 식에 삽입할 수 있습니다. RGB 값에 대한 자세한 내용은 [FORE_COLOR 및 BACK_COLOR 내용&#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)을 참조하세요.  
  
 **글꼴 식**  
 **글꼴 이름**, **글꼴 크기**및 **글꼴 플래그** 옵션을 보려면 확장합니다.  
  
 **글꼴 이름**  
 계산 멤버에 사용되는 글꼴의 이름을 지정하는 MDX 식을 입력합니다.  
  
 **계산 도구** 창에서 선택한 요소를 이 옵션으로 끌어서 놓으면 선택한 요소의 MDX 구문을 포함시킬 수 있습니다.  
  
 글꼴 선택 단추를 클릭하여 **글꼴** 대화 상자를 표시하고 지정한 글꼴의 속성 값을 MDX 식에 삽입할 수 있습니다. 속성 값에 대한 자세한 내용은 [속성 값 만들기 및 사용&#40;MDX&#41;](creating-and-using-property-values-mdx.md)을 참조하세요.  
  
 **글꼴 크기**  
 계산 멤버에 사용되는 글꼴의 크기를 지정하는 MDX 식을 입력합니다.  
  
 **계산 도구** 창에서 선택한 요소를 이 옵션으로 끌어서 놓으면 선택한 요소의 MDX 구문을 포함시킬 수 있습니다.  
  
 글꼴 선택 단추를 클릭하여 **글꼴** 대화 상자를 표시하고 지정한 글꼴의 속성 값을 MDX 식에 삽입할 수 있습니다. 속성 값에 대한 자세한 내용은 [속성 값 만들기 및 사용&#40;MDX&#41;](creating-and-using-property-values-mdx.md)을 참조하세요.  
  
 **글꼴 플래그**  
 밑줄이나 굵게와 같이 계산 멤버에 사용되는 글꼴의 글꼴 플래그를 포함하는 비트맵 값을 지정하는 MDX 식을 입력합니다.  
  
 **계산 도구** 창에서 선택한 요소를 이 옵션으로 끌어서 놓으면 선택한 요소의 MDX 구문을 포함시킬 수 있습니다.  
  
 글꼴 선택 단추를 클릭하여 **글꼴** 대화 상자를 표시하고 지정한 글꼴의 속성 값을 MDX 식에 삽입할 수 있습니다. 속성 값에 대한 자세한 내용은 [속성 값 만들기 및 사용&#40;MDX&#41;](creating-and-using-property-values-mdx.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [계산](multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [계산된 멤버 만들기](multidimensional-models/create-calculated-members.md)   
 [큐브 디자이너 &#40;Analysis Services-다차원 데이터&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [계산 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](calculations-cube-designer-analysis-services-multidimensional-data.md)   
 [도구 모음 &#40;계산 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](toolbar-calculations-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [스크립트 구성 도우미 &#40;계산 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](script-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [계산 도구 &#40;계산 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](calculation-tools-cube-designer-analysis-services-multidimensional-data.md)   
 [명명 된 집합 폼 편집기 &#40;계산 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](named-set-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [스크립트 편집기 &#40;계산 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](script-editor-calculations-cube-designer-analysis-services-multidimensional-data.md)  
  
  
