---
title: 뷰를 원본 데이터를 정의 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: af00938a-5a06-4fae-b2fc-f3fb0ca3cea5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca6e9661c65098bed1175c7108b18a482b14a542
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62730329"
---
# <a name="defining-a-data-source-view"></a>데이터 원본 뷰 정의
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트에 사용할 데이터 원본을 정의한 후 수행해야 할 다음 단계는 일반적으로 프로젝트에 대한 데이터 원본 뷰를 정의하는 것입니다. 데이터 원본 뷰는 프로젝트에서 데이터 원본에 의해 정의되는 뷰와 지정된 테이블의 메타데이터에 대한 단일 통합 뷰입니다. 메타데이터를 데이터 원본 뷰로 저장하면 기본 데이터 원본에 대한 연결이 열려 있지 않아도 개발 중에 메타데이터를 사용할 수 있습니다. 자세한 내용은 [다차원 모델의 데이터 원본 뷰](multidimensional-models/data-source-views-in-multidimensional-models.md)를 참조하세요.  
  
 다음 태스크에서는 **AdventureWorksDW2012** 데이터 원본의 테이블이 5개 포함된 데이터 원본 뷰를 정의합니다.  
  
### <a name="to-define-a-new-data-source-view"></a>새 데이터 원본 뷰를 정의하려면  
  
1.  Microsoft Visual Studio 창의 오른쪽에 있는 솔루션 탐색기에서 **데이터 원본 뷰**를 마우스 오른쪽 단추로 클릭하고 **새 데이터 원본 뷰**를 클릭합니다.  
  
2.  **데이터 원본 뷰 마법사 시작** 페이지에서 **다음**을 클릭합니다. **데이터 원본 선택** 페이지가 표시됩니다.  
  
3.  **관계형 데이터 원본**에서 **Adventure Works DW 2012** 데이터 원본이 선택되어 있습니다. **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  여러 데이터 원본을 기반으로 하는 데이터 원본 뷰를 만들려면 단일 데이터 원본을 기반으로 하는 데이터 원본 뷰를 먼저 정의합니다. 이 데이터 원본을 주 데이터 원본이라고 합니다. 그런 다음 보조 데이터 원본에 있는 테이블과 뷰를 추가할 수 있습니다. 여러 데이터 원본의 관련 테이블에 기초하는 특성이 포함된 차원을 디자인할 경우 해당 분산 쿼리 엔진 기능을 사용하려면 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터 원본을 주 데이터 원본으로 정의해야 할 수도 있습니다.  
  
4.  **테이블 및 뷰 선택** 페이지에서 선택한 데이터 원본에서 사용할 수 있는 개체 목록을 통해 테이블과 뷰를 선택합니다. 테이블과 뷰를 선택하는 데 도움이 되도록 이 목록을 필터링할 수 있습니다.  
  
    > [!NOTE]  
    >  오른쪽 위 모퉁이의 최대화 단추를 클릭하여 창이 전체 화면에 꽉 차도록 합니다. 이렇게 하면 사용할 수 있는 개체의 전체 목록을 보다 쉽게 볼 수 있습니다.  
  
     **사용 가능한 개체** 목록에서 다음 개체를 선택합니다. Ctrl 키를 누른 채 각 테이블을 클릭하면 여러 테이블을 선택할 수 있습니다.  
  
    -   **DimCustomer (dbo)**  
  
    -   **DimDate (dbo)**  
  
    -   **DimGeography (dbo)**  
  
    -   **DimProduct (dbo)**  
  
    -   **FactInternetSales (dbo)**  
  
5.  **>** 를 클릭하여 선택한 테이블을 **포함된 개체** 목록에 추가합니다.  
  
6.   **다음.**  
  
7.  이름 필드에서 **Adventure Works DW 2012** 가 표시되는지 확인하고 **마침**을 클릭합니다.  
  
     **Adventure Works DW 2012** 데이터 원본 뷰가 솔루션 탐색기의 **데이터 원본 뷰** 폴더에 표시됩니다. 데이터 원본 뷰의 내용도 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 데이터 원본 뷰 디자이너에 표시됩니다. 이 디자이너에는 다음과 같은 요소가 있습니다.  
  
    -   테이블과 테이블 관계가 그래픽으로 표시되는 **다이어그램** 창  
  
    -   테이블과 테이블 스키마 요소가 트리 뷰로 표시되는 **테이블** 창  
  
    -   데이터 원본 뷰의 하위 집합을 볼 수 있도록 하위 다이어그램을 만들 수 있는 **다이어그램 구성 도우미** 창  
  
    -   데이터 원본 뷰 디자이너용 도구 모음  
  
8.   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 개발 환경을 최대화하려면 **최대화** 단추를 클릭합니다.  
  
9. **다이어그램** 창의 테이블을 50% 비율로 보려면 데이터 원본 뷰 디자이너 도구 모음의 **확대/축소** 아이콘을 클릭합니다. 이렇게 하면 각 테이블의 열 정보가 숨겨집니다.  
  
10. 솔루션 탐색기를 숨기려면 제목 표시줄에 압정 아이콘으로 표시되는 **자동 숨기기** 단추를 클릭합니다. 솔루션 탐색기를 다시 표시하려면 개발 환경의 오른쪽에 있는 솔루션 탐색기 탭 위에 포인터를 놓습니다. 솔루션 탐색기 숨기기를 취소하려면 **자동 숨기기** 단추를 다시 클릭합니다.  
  
11. 기본적으로 창이 숨겨진 상태가 아니면 속성 창과 솔루션 탐색기 창의 제목 표시줄에 있는 **자동 숨기기** 를 클릭합니다.  
  
     이제 **다이어그램** 창에서 모든 테이블과 테이블 관계를 확인할 수 있습니다. FactInternetSales 테이블과 DimDate 테이블 간에는 3가지 관계가 있습니다. 각 판매에 있는 주문 날짜, 기한 및 운송 날짜라는 3가지 날짜가 판매와 관련이 있습니다 관계에 대한 세부 정보를 보려면 **다이어그램** 창에서 관계 화살표를 두 번 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [기본 테이블 이름 수정](lesson-1-4-modifying-default-table-names.md)  
  
## <a name="see-also"></a>관련 항목  
 [다차원 모델의 데이터 원본 뷰](multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
