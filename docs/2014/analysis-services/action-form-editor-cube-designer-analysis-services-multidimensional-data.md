---
title: 동작 폼 편집기 (동작 탭, 큐브 디자이너) (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.action.f1
ms.assetid: c363a29b-6099-473c-9625-460cc15b3d95
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7ce8acc1630b9944b2ac858ba27a1f515bb19adc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181206"
---
# <a name="action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>동작 폼 편집기(동작 탭, 큐브 디자이너)(Analysis Services - 다차원 데이터)
  큐브 디자이너의 **작업** 탭에서 동작 폼 편집기 창을 사용하여 표준 작업을 생성 및 수정할 수 있습니다.  
  
## <a name="options"></a>변수  
 **이름**  
 동작의 이름을 입력합니다.  
  
 **동작 대상**  
 **대상 유형** 및 **대상 개체** 옵션을 보려면 확장합니다.  
  
 **대상 유형**  
 동작을 연결할 개체의 유형을 선택합니다. 서버는 지정한 유형의 개체에 해당되는 동작만 클라이언트에 반환합니다. **조건** 을 만족하고 다음 표에 지정된 개체를 선택한 경우에만 클라이언트에서 이러한 동작을 사용할 수 있습니다.  
  
|값|선택한 개체|  
|-----------|---------------------|  
|특성 멤버|**대상 개체**의 특성에 기반한 수준에서 멤버가 선택됩니다.|  
|셀|**대상 개체** 의 명명된 집합이 선택됩니다. 큐브의 모든 셀을 선택하려면 **셀 추가** 를 선택합니다.|  
|Cube|**대상 개체** 의 큐브가 선택됩니다. 현재 큐브를 사용하려면 CURRENTCUBE를 선택합니다.<br /><br /> 참고: CURRENTCUBE를 사용하면 큐브의 이름을 바꾸거나 동작을 다른 큐브로 복사하는 경우 이식성이 향상됩니다. CURRENTCUBE를 사용하여 현재 큐브를 나타내는 것이 좋습니다.|  
|차원 멤버|**대상 개체** 의 차원 멤버가 선택됩니다.|  
|계층|**대상 개체** 의 계층이 선택됩니다.|  
|계층 멤버|**대상 개체** 의 계층 내에 있는 멤버가 선택됩니다.|  
|Level|**대상 개체** 의 수준이 선택됩니다.|  
|수준 멤버|**대상 개체** 의 수준 내에 있는 멤버가 선택됩니다.|  
  
 **대상 개체**  
 동작을 연결할 개체를 선택합니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스는 선택한 개체에 적용되는 동작만 클라이언트에 반환합니다. 사용 가능한 개체 목록은 **대상 유형**에서 선택한 항목에 따라 달라집니다.  
  
 **조건(옵션)**  
 선택적 조건을 기술하는 MDX(Multidimensional Expression) 식을 입력합니다. 이 옵션은 **대상 개체**와 함께 사용되어 동작의 가용성을 추가로 제한합니다. 식은 부울 값을 반환해야 합니다. True인 경우 동작을 사용할 수 있습니다.  
  
 **계산 도구** 창에서 선택한 요소를 이 옵션으로 끌어서 놓으면 선택한 요소의 MDX 구문을 포함시킬 수 있습니다.  
  
 **동작 내용**  
 **유형** 및 **동작 식** 옵션을 보려면 확장합니다.  
  
 **형식**  
 작업을 실행할 때의 동작 유형을 선택합니다. 사용할 수 있는 동작 유형은 다음과 같습니다.  
  
|값|Description|  
|-----------|-----------------|  
|Dataset|클라이언트 응용 프로그램에서 실행 및 표시하며 다차원 데이터 집합을 나타내는 MDX(Multidimensional Expressions) 문을 반환합니다.|  
|소유|이 동작에 대한 **응용 프로그램** 설정과 연결된 클라이언트 응용 프로그램에서 해석할 수 있는 소유 문자열을 반환합니다.|  
|행 집합|클라이언트 응용 프로그램에서 실행 및 표시하며 테이블 형식 행 집합을 나타내는 MDX(Multidimensional Expressions) 문을 반환합니다.|  
|인수를 제거합니다.|클라이언트 응용 프로그램에서 실행할 명령 문자열을 반환합니다.|  
|URL|클라이언트 응용 프로그램에서 일반적으로 인터넷 브라우저로 여는 URL(Uniform Resource Location) 문자열을 반환합니다.|  
  
 동작 유형에 대한 자세한 내용은 [동작&#40;Analysis Services - 다차원 데이터&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md)을 참조하세요.  
  
 **동작 식**  
 해당 동작에서 실행할 클라이언트 응용 프로그램으로 반환한 문자열을 반환하는 MDX(Multidimensional Expression) 식을 입력합니다.  
  
 **추가 속성**  
 확장하면 **호출**, **응용 프로그램**, **설명**, **캡션**및 **MDX 캡션** 옵션이 표시됩니다.  
  
 **호출**  
 동작 실행 시기를 나타내는 설정을 선택합니다.  
  
> [!NOTE]  
>  이 옵션은 클라이언트 응용 프로그램에 동작 실행 시기에 대한 권장 사항만 제공할 뿐 직접 작업 호출을 제어하지는 않습니다.  
  
 다음 표에서는 사용 가능한 설정에 대해 설명합니다.  
  
|값|Description|  
|-----------|-----------------|  
|일괄 처리|동작이 일괄 처리 작업이나 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 태스크의 일부로 실행됩니다.|  
|대화형|사용자가 작업을 호출할 때 동작이 실행됩니다.|  
|열 때|큐브를 처음으로 열 때 동작이 실행됩니다.|  
  
 **응용 프로그램**  
 **동작 식**에서 반환한 문자열을 해석할 수 있는 응용 프로그램의 이름을 입력합니다.  
  
 이 옵션을 사용하여 이 동작을 가장 많이 사용하는 클라이언트 응용 프로그램을 식별하고 팝업 메뉴에서 해당 작업 옆에 적절한 아이콘을 표시할 수도 있습니다.  
  
> [!NOTE]  
>  이 옵션은 클라이언트 응용 프로그램에 동작을 실행해야 하는 클라이언트 응용 프로그램에 대한 권장 사항만 제공할 뿐 직접 작업에 대한 액세스를 제어하지는 않습니다. 클라이언트 응용 프로그램은 다른 클라이언트 응용 프로그램에 연결된 모든 동작을 숨겨야 합니다.  
  
 **설명**  
 동작에 대한 선택적 설명을 입력합니다.  
  
 **캡션**  
 **MDX 캡션** 이 **False**로 설정된 경우 클라이언트 응용 프로그램에서 동작에 대해 표시할 캡션을 입력합니다.  
  
 **MDX 캡션** 이 **True**로 설정된 경우 캡션 문자열을 반환하는 MDX(Multidimensional Expression) 식을 입력합니다.  
  
 **True**  
 클라이언트 응용 프로그램에서 동작에 대해 표시할 캡션을 나타내는 리터럴 문자열이 **캡션** 에 포함되어 있음을 나타내려면 **False** 를 선택합니다.  
  
 클라이언트 응용 프로그램에서 동작에 대해 표시할 캡션을 나타내는 문자열을 반환하는 MDX 식이 **캡션** 에 포함되어 있음을 나타내려면 **True** 를 선택합니다. 클라이언트 응용 프로그램으로 동작을 반환하기 전에 MDX 식을 확인해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [작업 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [도구 모음 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [동작 구성 도우미 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [계산 도구 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [드릴스루 동작 폼 편집기 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [보고 동작 폼 편집기 &#40;동작 탭, 큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  