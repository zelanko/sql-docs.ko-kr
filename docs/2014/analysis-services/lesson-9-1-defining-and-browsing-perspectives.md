---
title: 정의 및 큐브 뷰 찾아보기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 766004b9-6578-4914-a445-6f44843a5fb0
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 642d9a0f80f0efb0bc9d26b9a08ab7a6dbd521e1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208193"
---
# <a name="defining-and-browsing-perspectives"></a>큐브 뷰 정의 및 찾아보기
  큐브 뷰는 특정 목적을 위해 큐브의 보기를 단순화할 수 있습니다. 기본적으로 사용자들은 사용 권한이 있는 큐브의 모든 요소를 볼 수 있습니다. 사용자가 전체 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 큐브를 볼 때 표시되는 내용은 큐브의 기본 큐브 뷰입니다. 전체 큐브의 보기는 너무 복잡해서 사용자가 탐색하기 어려울 수 있으며, 비즈니스 인텔리전스 및 보고 요구 사항을 만족시키기 위해 큐브의 일부만 사용하면 되는 사용자에게는 더욱 그렇습니다.  
  
 큐브의 복잡성을 줄이기 위해 큐브에서 측정값 그룹, 측정값, 차원, 특성, 계층, KPI(핵심 성과 지표), 동작 및 계산 멤버의 부분만 표시하는 *큐브 뷰*라는 표시 가능한 큐브 하위 집합을 만들 수 있습니다. 이 방법은 특히 이전 릴리스의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]용으로 작성된 클라이언트 응용 프로그램으로 작업할 때 유용합니다. 예를 들어 이러한 클라이언트는 표시 폴더나 큐브 뷰에 대한 개념이 없지만 큐브 뷰는 이전 클라이언트에 큐브인 것처럼 표시됩니다. 자세한 내용은 [큐브 뷰](multidimensional-models-olap-logical-cube-objects/perspectives.md)및 [다차원 모델의 큐브 뷰](multidimensional-models/perspectives-in-multidimensional-models.md)를 참조하세요.  
  
> [!NOTE]  
>  큐브 뷰는 보안 메커니즘이 아닌 작업 효율을 높이기 위한 도구입니다. 큐브 뷰에 대한 모든 보안은 기본 큐브에서 상속됩니다.  
  
 이 항목의 태스크에서는 여러 다른 큐브 뷰를 정의한 후 이러한 각각의 새 큐브 뷰를 통해 큐브를 찾아봅니다.  
  
## <a name="defining-an-internet-sales-perspective"></a>인터넷 판매 큐브 뷰 정의  
  
1.  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 대한 큐브 디자이너를 열고 **큐브 뷰** 탭을 클릭합니다.  
  
     다음 그림에 표시된 것처럼 모든 개체 및 해당 개체 유형이 **큐브 뷰** 창에 나타납니다.  
  
     ![큐브 디자이너의 큐브 뷰 창](../../2014/tutorials/media/l9-perspectives-1.gif "큐브 디자이너의 큐브 뷰 창")  
  
2.  **큐브 뷰** 탭의 도구 모음에서 **새 큐브 뷰** 단추를 클릭합니다.  
  
     다음 그림에 표시된 것처럼 **큐브 뷰** 의 기본 이름과 함께 새 큐브 뷰가 **큐브 뷰 이름**열에 나타납니다. 개체에 대한 확인란의 선택을 취소할 때까지 모든 개체에 대한 확인란은 선택된 상태를 유지합니다. 이 큐브 뷰는 이 큐브의 기본 큐브 뷰와 동일합니다.  
  
     ![큐브 뷰 이름 열의 새 큐브 뷰](../../2014/tutorials/media/l9-perspectives-2.gif "큐브 뷰 이름 열의 새 큐브 뷰")  
  
3.  큐브 뷰 이름을 `Internet Sales`입니다.  
  
4.  다음 행에서 DefaultMeasure를 **Internet Sales-Sales Amount**로 설정합니다.  
  
     사용자가 이 큐브 뷰를 사용하여 큐브를 찾아볼 때 다른 측정값을 지정하지 않은 경우 이 측정값이 표시됩니다.  
  
    > [!NOTE]  
    >  또한 큐브의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 큐브 구조 **탭에 있는 속성 창에서 전체** Tutorial 큐브에 대한 기본 측정값을 설정할 수도 있습니다.  
  
5.  다음 개체에 대한 확인란의 선택을 취소합니다.  
  
    -   `Reseller Sales` 측정값 그룹  
  
    -   **Sales Quotas** 측정값 그룹  
  
    -   **Sales Quotas 1** 측정값 그룹  
  
    -   **Reseller** 큐브 차원  
  
    -   **Reseller Geography** 큐브 차원  
  
    -   **Sales Territory** 큐브 차원  
  
    -   **Employee** 큐브 차원  
  
    -   **Promotion** 큐브 차원  
  
    -   **Reseller Revenue** KPI  
  
    -   **Large Resellers** 명명된 집합  
  
    -   **Total Sales Amount** 계산 멤버  
  
    -   **Total Product Cost** 계산 멤버  
  
    -   **Reseller GPM** 계산 멤버  
  
    -   **Total GPM** 계산 멤버  
  
    -   **Reseller Sales Ratio to All Products** 계산 멤버  
  
    -   **Total Sales Ratio to All Products** 계산 멤버  
  
     이러한 개체는 인터넷 판매와 관련이 없습니다.  
  
    > [!NOTE]  
    >  각 차원 내에서 큐브 뷰에 표시하려는 사용자 정의 계층 및 특성을 따로 선택할 수도 있습니다.  
  
## <a name="defining-a-reseller-sales-perspective"></a>Reseller Sales 큐브 뷰 정의  
  
1.  **큐브 뷰** 탭의 도구 모음에서 **새 큐브 뷰** 단추를 클릭합니다.  
  
2.  에 새 큐브 뷰의 이름을 변경할 `Reseller Sales`합니다.  
  
3.  **Reseller Sales-Sales Amount** 를 기본 측정값으로 설정합니다.  
  
     사용자가 이 큐브 뷰를 사용하여 큐브를 찾아볼 때 다른 측정값을 지정하지 않은 경우 이 측정값이 표시됩니다.  
  
4.  다음 개체에 대한 확인란의 선택을 취소합니다.  
  
    -   `Internet Sales` 측정값 그룹  
  
    -   **Internet Sales Reason** 측정값 그룹  
  
    -   **Customer** 큐브 차원  
  
    -   **Internet Sales Order Details** 큐브 차원  
  
    -   **Sales Reason** 큐브 차원  
  
    -   **Internet Sales Details Drillthrough Action** 드릴스루 동작  
  
    -   **Total Sales Amount** 계산 멤버  
  
    -   **Total Product Cost** 계산 멤버  
  
    -   **Internet GPM** 계산 멤버  
  
    -   **Total GPM** 계산 멤버  
  
    -   **Internet Sales Ratio to All Products** 계산 멤버  
  
    -   **Total Sales Ratio to All Products** 계산 멤버  
  
     이러한 개체는 대리점 판매와 관련이 없습니다.  
  
## <a name="defining-a-sales-summary-perspective"></a>판매 요약 큐브 뷰 정의  
  
1.  **큐브 뷰** 탭의 도구 모음에서 **새 큐브 뷰** 단추를 클릭합니다.  
  
2.  에 새 큐브 뷰의 이름을 변경할 `Sales Summary`합니다.  
  
    > [!NOTE]  
    >  계산 측정값은 기본 측정값으로 지정할 수 없습니다.  
  
3.  다음 개체에 대한 확인란의 선택을 취소합니다.  
  
    -   `Internet Sales` 측정값 그룹  
  
    -   `Reseller Sales` 측정값 그룹  
  
    -   **Internet Sales Reason** 측정값 그룹  
  
    -   **Sales Quotas** 측정값 그룹  
  
    -   **Sales Quotas1** 측정값 그룹  
  
    -   **Internet Sales Order Details** 큐브 차원  
  
    -   **Sales Reason** 큐브 차원  
  
    -   **Internet Sales Details Drillthrough Action** 드릴스루 동작  
  
4.  다음 개체에 대한 확인란을 선택합니다.  
  
    -   **Internet Sales Count** 측정값  
  
    -   **Reseller Sales Count** 측정값  
  
## <a name="browsing-the-cube-through-each-perspective"></a>각 큐브 뷰를 통해 큐브 찾아보기  
  
1.  **빌드** 메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
2.  배포가 성공적으로 완료되면 **브라우저** 탭으로 전환한 다음 **다시 연결** 단추를 클릭합니다.  
  
3.  Excel을 시작합니다.  
  
4.  다음 그림에 표시된 것처럼 Excel에서 분석에서 Excel에서 모델을 검색할 때 사용할 큐브 뷰를 선택하라는 메시지를 표시합니다.  
  
     ![Internet Sales 큐브 뷰에 대 한 개체](../../2014/tutorials/media/l9-perspectives-3.gif "Internet Sales 큐브 뷰 개체")  
  
5.  또는 다음 그림에 표시된 것처럼 Windows 시작 메뉴에서 Excel을 시작하고 localhost의 Analysis Services 자습서 데이터베이스에 대한 연결을 정의하고 데이터 연결 마법사에서 큐브 뷰를 선택합니다.  
  
     ![Excel에서 데이터 연결 마법사](../../2014/tutorials/media/l9-perspectives-3b.gif "Excel에서 데이터 연결 마법사")  
  
6.  선택 `Internet Sales` 에 **관점** 목록 및 측정값과 차원을 메타 데이터 창에서 검토 합니다.  
  
     Internet Sales 큐브 뷰에 대해 지정된 개체만 나타납니다.  
  
7.  메타데이터 창에서 **Measures**를 확장합니다.  
  
     멤버만 합니다 `Internet Sales` 측정값 그룹만 표시 됩니다, 함께 사용 하 여는 **Internet GPM** 하 고 **Internet Sales Ratio to All Products** 계산 멤버입니다.  
  
8.  모델에서 Excel을 다시 선택합니다. `Sales Summary`을(를) 선택합니다.  
  
     다음 그림에 표시된 것처럼 이러한 각 측정값 그룹에서 단일 측정값만 나타납니다.  
  
     ![Internet Sales 및 Reseller Sales 측정값](../../2014/tutorials/media/l9-perspectives-4.gif "Internet Sales 및 Reseller Sales 측정값")  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [번역 정의 및 찾아보기](../analysis-services/lesson-9-2-defining-and-browsing-translations.md)  
  
## <a name="see-also"></a>관련 항목  
 [큐브 뷰](multidimensional-models-olap-logical-cube-objects/perspectives.md)   
 [다차원 모델의 큐브 뷰](multidimensional-models/perspectives-in-multidimensional-models.md)  
  
  
