---
title: 쿼리 및 필터 (브라우저 탭, 큐브 디자이너) (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.filterpane.f1
ms.assetid: f5cf0bb1-3afb-4856-a2ef-614deb4e7e49
author: minewiskan
ms.author: owend
ms.openlocfilehash: aa501e2a5b23f32fbd10d244788b1e6e938e938b
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84539735"
---
# <a name="query-and-filter-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>쿼리 및 필터(브라우저 탭, 큐브 디자이너)(Analysis Services - 다차원 데이터)
  큐브 디자이너 **브라우저** 탭의 이 영역에는 찾아보기 또는 쿼리에서 사용할 데이터를 큐브에서 선택할 수 있는 쿼리 및 필터 영역이 포함되어 있습니다. 원하는 수의 큐브 개체를 추가한 다음 데이터 영역에서 결과를 보거나 Excel에서 분석을 사용하여 결과를 보고서로 내보내 최종 사용자에게 데이터가 어떻게 표시되는지 확인할 수 있습니다.  
  
> [!WARNING]  
>  이 영역의 데이터를 사용하는 경우 **브라우저** 는 기본적으로 그래픽 디자인 모드를 사용합니다. 하지만 **디자인 모드** 토글 단추를 클릭하면 MDX를 사용하여 쿼리를 직접 편집할 수 있습니다. 이 경우 차원에서 필터를 디자인하는 창이 표시되지 않습니다. 필터를 추가하려면 그래픽 디자인 모드로 다시 전환하면 됩니다.  
  
 기본적으로 쿼리를 실행할 때 **가장 정보** 페이지에 지정된 자격 증명이 아니라 현재 사용자의 자격 증명을 사용하여 데이터 원본에 연결합니다. 하지만 **도구 모음** 에서 **사용자 변경**을 클릭하여 쿼리 또는 보고서의 사용자 컨텍스트를 변경할 수도 있습니다.  
  
## <a name="options"></a>옵션  
 **치수나**  
 하위 큐브를 조각화할 차원을 선택합니다.  
  
 **계층**  
 하위 큐브를 조각화할 계층을 선택합니다.  
  
 **연산자**  
 **필터 식** 의 식이 선택한 계층에 적용되는 방법을 정의하는 연산자를 선택합니다. 다음 표에서는 사용 가능한 연산자에 대해 설명합니다.  
  
|값|설명|  
|-----------|-----------------|  
|**같음**|**필터 식**에서 정의한 집합으로 결과가 제한됩니다.|  
|**같지 않음**|**필터 식**에서 정의한 집합에서 제외된 멤버로 결과가 제한됩니다.|  
|**진행**|**필터 식**에서 선택한 명명된 집합으로 결과가 제한됩니다.|  
|**속하지 않음**|**필터 식**에서 선택한 명명된 집합에서 제외된 멤버로 결과가 제한됩니다.|  
|**포함**|이름에 **필터 식**의 문자열이 포함된 멤버로 결과가 제한됩니다.|  
|**시작 문자**|이름이 **필터 식**의 문자열로 시작하는 멤버로 결과가 제한됩니다.|  
|**범위(포함)**|**필터 식**에서 선택한 범위로 결과가 제한됩니다.|  
|**범위(제외)**|**필터 식**에서 선택한 범위에서 제외된 멤버로 결과가 제한됩니다.|  
|**MDX**|**필터 식**에서 설정한 MDX(Multidimensional Expression) 식으로 결과가 제한됩니다.|  
  
 **필터 식**  
 검색 결과가 제한되도록 **연산자**로 계산할 식을 입력합니다.  
  
> [!NOTE]  
>  이 필드는 선택한 연산자에 필요한 데이터 형식에 따라 모양이 변경되는 동적 데이터 입력 요소입니다.  
  
## <a name="see-also"></a>참고 항목  
 [큐브 디자이너 &#40;Analysis Services 다차원 데이터&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [브라우저 &#40;큐브 디자이너&#41; &#40;Analysis Services 다차원 데이터&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)   
 [도구 모음 &#40;브라우저 탭, 큐브 디자이너&#41; &#40;Analysis Services 다차원 데이터&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Excel에서 분석 &#40;브라우저 탭, 큐브 디자이너&#41; &#40;Analysis Services 다차원 데이터&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [메타 데이터 &#40;브라우저 탭, 큐브 디자이너&#41; &#40;Analysis Services 다차원 데이터&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)  
  
  
