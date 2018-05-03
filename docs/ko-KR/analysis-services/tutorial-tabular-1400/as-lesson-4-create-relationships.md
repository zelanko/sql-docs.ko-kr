---
title: 'Analysis Services 자습서 4 단원: 관계 만들기 | Microsoft Docs'
description: Analysis Services tutorial 프로젝트에서 관계를 만드는 방법을 설명 합니다.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 14bba10123ab1161b336934286e38a32fb351bf5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-relationships"></a>관계 만들기

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는 데이터를 가져올 때 자동으로 생성 된 관계를 확인 및 서로 다른 테이블 간에 새 관계를 추가 합니다. 관계는 두 테이블에 있는 데이터의 상관 관계를 설정하기 위한 테이블 간 연결입니다. 예를 들어 DimProduct 테이블과 DimProductSubcategory 테이블의 경우 테이블의 각 제품이 하위 범주에 속한다는 점에서 두 테이블 간에는 관계가 있습니다. 자세한 내용은 참고 [관계](../tabular-models/relationships-ssas-tabular.md)합니다.
  
이 단원에 소요되는 예상 시간: **10분**  
  
## <a name="prerequisites"></a>필수 구성 요소  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [3 단원: 날짜 테이블로 표시](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)합니다. 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>기존 관계를 검토하고 새 관계 추가  

데이터 가져오기를 사용 하 여 데이터를 가져올 때 AdventureWorksDW 데이터베이스에서 7 개의 테이블을 가져왔습니다. 일반적으로 관계형 원본에서 데이터를 가져올 때 기존 관계 없는 데이터와 함께 자동으로 가져옵니다. 데이터 모델에 자동으로 관계를 만들려면 데이터 가져오기에 대 한 순서로 데이터 원본에 테이블 간의 관계 이어야 합니다.

이러한 테이블 간의 관계를 확인 해야 모델 제작을 계속 진행 하기 전에 제대로 생성 되었는지 합니다. 이 자습서에서는 세 개의 새로운 관계도 추가 합니다.  

  
#### <a name="to-review-existing-relationships"></a>기존 관계를 검토하려면  
  
1.  클릭는 **모델** 메뉴 > **모델 뷰** > **다이어그램 보기**합니다.  

    모델 디자이너가 이제 다이어그램 보기에 나타납니다. 모든 테이블을 표시 하는 그래픽 형식을 가져온 서로 줄만 작성 합니다. 테이블 사이의 줄은 데이터를 가져올 때 자동으로 생성된 관계를 나타냅니다.
    
    ![as-lesson4-diagram](../tutorial-tabular-1400/media/as-lesson4-diagram.png)
  
    > [!NOTE]
    > 테이블 간의 관계가 표시 되지 않으면, 데이터 원본에서 해당 테이블 간의 관계가 없음을 의미 없는 의미 가능성이 높습니다.

    모델 디자이너의 오른쪽 아래 모서리에 미니 맵 컨트롤을 사용 하 여 테이블을 가능한 한 많은 포함 됩니다. 또한 테이블을 클릭하여 다른 위치에 끌어다 놓거나, 테이블 간 간격을 좁히거나, 테이블을 특정 순서로 배치할 수 있습니다. 테이블 이동 테이블 간의 관계에는 영향을 주지 않습니다. 특정 테이블의 모든 열을 보려면 클릭 끌어서 테이블 가장자리를 확장 하거나 축소 합니다.  
  
2.  클릭 사이의 실선은 **DimCustomer** 테이블 및 **DimGeography** 테이블입니다. 이러한 두 테이블 사이의 실선을 보여 줍니다이 관계는 활성 상태 이면 즉, DAX 수식을 계산할 때 기본적으로 사용 됩니다.  
  
    공지는 **GeographyKey** 열에는 **DimCustomer** 테이블 및 **GeographyKey** 열에는 **DimGeography** 테이블 이제 모두 각각 상자 내에 표시 합니다. 이러한 열은 관계에 사용 됩니다. 또한 관계의 속성이 **속성** 창에 표시됩니다.  
  
    > [!TIP]  
    > 또한 테이블 형식으로 모든 테이블 간의 관계를 표시 하려면 관계 관리 대화 상자를 사용할 수 있습니다. 테이블 형식 모델 탐색기에서 마우스 오른쪽 단추로 클릭 **관계** > **관계 관리**합니다.
  
3.  때 다음 관계가 생성 되었는지 확인 AdventureWorksDW 데이터베이스에서 가져온 각 테이블:  
  
    |활성|테이블|관련 조회 테이블|  
    |----------|---------|------------------------|  
    |예|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |예|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |예|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |예|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |예|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    다음 테이블을 포함 하는 모델에 관계 중 하나라도 없으면 확인: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory, 및 FactInternetSales 합니다. 별도 간의 관계가 시간에 같은 데이터 원본 연결의 테이블을 가져오는 경우 해당 테이블은 생성 되지 않으며 수동으로 만들어야 합니다. 관계가 없음을 표시 하는 경우 데이터 원본에 없는 관계 없는 의미 합니다. 데이터 모델에서 수동으로 만들 수 있습니다.

### <a name="take-a-closer-look"></a>자세히 조사

다이어그램 보기에서 화살표는 별표 및 테이블 간의 관계를 표시 하는 줄 번호를 확인 합니다.

![as-lesson4-line](../tutorial-tabular-1400/media/as-lesson4-line.png)

화살표는 필터 방향을 나타냅니다. 별표는이 테이블은 표시는 *많은* 관계의 카디널리티 및 한 쪽이이 테이블은 표시는 *하나의* 관계의 측면입니다. 관계; 편집 하려는 경우 예를 들어 관계의 필터 방향을 나 카디널리티 변경, 관계 편집 대화 상자를 열려면 관계 선을 두 번 클릭 합니다.

![as-lesson4-edit](../tutorial-tabular-1400/media/as-lesson4-edit.png)

이 기능은 고급 데이터 모델링을 위한 있으며이 자습서에서 다루지 않습니다. 자세한 내용은 참고 [양방향 교차 필터에서 Analysis Services 테이블 형식 모델에 대 한](../tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)합니다.

경우에 따라 특정 비즈니스 논리를 지원하기 위해 모델의 테이블 간에 관계를 추가로 만들어야 할 수도 있습니다. 이 자습서에서는 세 개의 FactInternetSales 테이블과 DimDate 테이블 간에 관계를 추가로 만들 해야 합니다.  
  
#### <a name="to-add-new-relationships-between-tables"></a>테이블 간에 새 관계를 추가하려면  
  
1.  모델 디자이너에서의 **FactInternetSales** 테이블을 클릭 한 채로 **OrderDate** 열에서 다음 커서를 끌어는 **날짜** 열에는 **DimDate** 테이블을 마우스를 놓습니다.  

    간에 활성 관계를 만들었음을 보여 주는 실선이 나타납니다는 **OrderDate** 열에는 **인터넷 판매** 테이블 및 **날짜** 열에는 **날짜** 테이블입니다. 
  
      ![as-lesson4-new](../tutorial-tabular-1400/media/as-lesson4-new.png) 
  
    > [!NOTE]  
    > 관계를 만들 때 기본 테이블과 관련된 조회 테이블 간에 카디널리티 및 필터 방향은 자동으로 선택 됩니다.  
  
2.  에 **FactInternetSales** 테이블을 클릭 한 채로 **DueDate** 열에서 다음 커서를 끌어는 **날짜** 열에는 **DimDate** 테이블을 마우스를 놓습니다.  
  
    간에 비활성 관계를 만들었음을 보여 주는 점선이 나타납니다는 **DueDate** 열에는 **FactInternetSales** 테이블 및 **날짜** 열에는 **DimDate** 테이블입니다. 테이블 간에 관계를 여러 개 설정할 수 있지만 한 번에 하나의 관계만 활성 상태일 수 있습니다. 사용자 지정 하는 DAX 식에서 특별 한 집계를 수행 하는 현재 비활성 관계를 만들 수 있습니다.  
  
3.  마지막으로 관계를 하나 더 만듭니다. 에 **FactInternetSales** 테이블을 클릭 한 채로 **ShipDate** 열에서 다음 커서를 끌어는 **날짜** 열에는 **DimDate** 테이블을 마우스를 놓습니다.  
    
     ![as-lesson4-newinactive](../tutorial-tabular-1400/media/as-lesson4-newinactive.png)
  
## <a name="whats-next"></a>다음 단계

[5 단원: 계산된 열 만들기](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)합니다.
  
  
  
