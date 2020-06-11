---
title: 수준 및 멤버 (브라우저 탭, 차원 디자이너) (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.browsertab.levelsandmembers.f1
ms.assetid: 3f61e384-5b4e-4480-a7ed-b408de2fdea7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 3f858f2ba6fe542d84e3bd6e7617b2d1565c0ca2
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84542015"
---
# <a name="level-and-members-browser-tab-dimension-designer-analysis-services---multidimensional-data"></a>수준 및 멤버(브라우저 탭, 차원 디자이너)(Analysis Services - 다차원 데이터)
  이 창을 사용하여 현재 선택한 계층 및 언어의 멤버를 찾아볼 수 있습니다. 찾아볼 계층 또는 언어를 선택하려면 **도구 모음** 창의 **계층** 및 **언어** 옵션을 사용합니다. 도구 모음 창에 대 한 자세한 내용은 [도구 모음 &#40;브라우저 탭, 차원 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](toolbar-browser-tab-dimension-designer-analysis-services-multidimensional-data.md)를 참조 하세요.  
  
## <a name="writeback-mode"></a>쓰기 저장 모드  
 쓰기 저장 모드를 설정하면 이 창의 기능이 바뀝니다. 쓰기 저장 모드를 설정하려면 선택한 차원을 쓰기 가능하도록 설정, 즉 차원의 `WriteEnabled` 속성을 true로 설정하고 해당 차원을 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 배포해야 합니다.  
  
 쓰기 저장 모드를 설정하려면 **도구 모음** 창에서 **쓰기 저장** 을 선택하거나 **수준 및 멤버** 창을 마우스 오른쪽 단추로 클릭한 다음 상황에 맞는 메뉴에서 **쓰기 저장** 을 선택합니다.  
  
 쓰기 저장 모드를 설정하면 **수준 및 멤버** 창에서 다음과 같은 추가 동작을 수행할 수 있습니다.  
  
|작업|수행하는 작업|  
|-----------|-------------|  
|선택한 계층 내에서 형제 및 자식 멤버 생성|선택한 멤버를 마우스 오른쪽 단추로 클릭한 다음 상황에 맞는 메뉴에서 **형제 만들기**를 선택하여 형제 멤버를 만들거나 **자식 만들기**를 선택하여 자식 멤버를 만듭니다.|  
|선택한 멤버를 계층에서 위 또는 아래로 이동|멤버를 해당 부모 또는 자식 멤버로 끌거나 **도구 모음** 창에서 **들여쓰기** 또는 **내어쓰기** 를 클릭하여 선택한 멤버를 계층 수준에서 위 또는 아래로 이동합니다.|  
|선택한 멤버 이름 바꾸기|선택한 멤버를 마우스 오른쪽 단추로 클릭한 다음 **이름 바꾸기**를 선택하거나 이미 선택한 멤버를 클릭합니다.|  
|멤버 속성 값 편집|선택한 멤버에 대해 선택한 멤버 속성에서 값을 두 번 클릭하여 편집합니다.|  
  
## <a name="options"></a>옵션  
 **현재 수준**  
 **트리** 에서 현재 선택한 멤버가 속한 수준을 표시합니다.  
  
 **Tree**  
 현재 선택한 계층 및 언어의 멤버를 표시합니다.  
  
 도구 모음 창의 **멤버 속성** 옵션에서 멤버 속성을 선택하면 각 멤버 속성이 열로 표시됩니다.  
  
 쓰기 저장 모드를 설정하면 차원의 키 특성과 연결된 각 키 열에 대해 하나의 열이 표시됩니다.  
  
## <a name="context-menu"></a>상황에 맞는 메뉴  
 선택한 멤버에 대한 **수준 및 멤버** 창을 마우스 오른쪽 단추로 클릭하면 표시되는 상황에 맞는 메뉴에서 다음과 같은 옵션을 사용할 수 있습니다.  
  
 **형제 만들기**  
 선택한 멤버와 같은 수준에서 새 멤버를 만듭니다.  
  
> [!NOTE]  
>  이 옵션은 (All) 수준이 아닌 수준에서 멤버를 선택한 경우에만 사용할 수 있습니다.  
  
> [!NOTE]  
>  이 옵션은 쓰기 저장 모드가 설정된 경우에만 표시됩니다.  
  
 **자식 만들기**  
 선택한 멤버의 다음 하위 수준에서 새 멤버를 선택한 멤버의 자식으로 만듭니다.  
  
> [!NOTE]  
>  이 옵션은 최하위 수준이 아닌 수준의 멤버를 선택한 경우에만 사용할 수 있습니다.  
  
> [!NOTE]  
>  이 옵션은 쓰기 저장 모드가 설정된 경우에만 표시됩니다.  
  
 **잘라내기**  
 선택한 멤버를 클립보드로 복사하고 계층에서 제거합니다.  
  
> [!NOTE]  
>  이 옵션은 All 멤버가 아닌 멤버를 선택한 경우에만 사용할 수 있습니다.  
  
> [!NOTE]  
>  이 옵션은 쓰기 저장 모드가 설정된 경우에만 표시됩니다.  
  
 **붙여넣기**  
 **잘라내기** 를 사용하여 이전에 제거한 멤버를 선택한 멤버 바로 뒤에 붙여넣습니다.  
  
> [!NOTE]  
>  이 옵션은 쓰기 저장 모드가 설정된 경우에만 표시됩니다.  
  
 **삭제**  
 선택한 멤버를 계층에서 제거합니다.  
  
> [!NOTE]  
>  이 옵션은 All 멤버가 아닌 멤버를 선택한 경우에만 사용할 수 있습니다.  
  
> [!NOTE]  
>  이 옵션은 쓰기 저장 모드가 설정된 경우에만 표시됩니다.  
  
 **이름 바꾸기**  
 선택한 멤버의 이름을 편집하려면 선택합니다.  
  
> [!NOTE]  
>  이 옵션은 All 멤버가 아닌 멤버를 선택한 경우에만 사용할 수 있습니다.  
  
> [!NOTE]  
>  이 옵션은 쓰기 저장 모드가 설정된 경우에만 표시됩니다.  
  
 **멤버 필터**  
 **멤버 필터** 대화 상자를 표시하고 선택한 계층에 대한 **수준 및 멤버**에 표시된 멤버를 필터링할 수 있습니다. **멤버 필터** 대화 상자에 대한 자세한 내용은 [멤버 필터 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.  
  
 **모두 확장**  
 **트리**에서 모든 멤버를 확장합니다.  
  
> [!NOTE]  
>  이 옵션은 최하위 수준이 아닌 수준의 멤버를 선택한 경우에만 사용할 수 있습니다.  
  
 **모두 축소**  
 **트리**에서 모든 멤버를 축소합니다.  
  
 **멤버 확장**  
 **트리**에서 선택한 멤버를 확장합니다.  
  
 **멤버 축소**  
 **트리**에서 선택한 멤버를 축소합니다.  
  
 **쓰기 저장(writeback)**  
 쓰기 저장 모드를 설정하려면 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [도구 모음 &#40;브라우저 탭, 차원 디자이너&#41; &#40;Analysis Services 다차원 데이터&#41;](toolbar-browser-tab-dimension-designer-analysis-services-multidimensional-data.md)   
 [브라우저 &#40;차원 디자이너&#41; &#40;Analysis Services 다차원 데이터&#41;](browser-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
