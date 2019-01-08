---
title: 'Analysis Services 자습서 단원 4: 관계 만들기 | Microsoft Docs'
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a39978dc461bd660d932e13561ed4d00c4041e0e
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52394527"
---
# <a name="create-relationships"></a>관계 만들기

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는 데이터를 가져올 때 자동으로 생성 된 관계를 확인 하 고 다른 테이블 간에 새 관계를 추가 합니다. 관계는 두 테이블에 있는 데이터의 상관 관계를 설정하기 위한 테이블 간 연결입니다. 예를 들어 DimProduct 테이블과 DimProductSubcategory 테이블의 경우 테이블의 각 제품이 하위 범주에 속한다는 점에서 두 테이블 간에는 관계가 있습니다. 자세한 내용은 참조 하세요 [관계](../tabular-models/relationships-ssas-tabular.md)합니다.
  
이 단원에 소요되는 예상 시간: **10 분**  
  
## <a name="prerequisites"></a>사전 요구 사항  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행하려면 이전 단원을 완료해야 합니다. [3 단원: 날짜 테이블로 표시](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)합니다. 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>기존 관계를 검토하고 새 관계 추가  

데이터 가져오기를 사용 하 여 데이터를 가져올 때 AdventureWorksDW 데이터베이스에서 7 개의 테이블을 가져왔습니다. 일반적으로 관계형 원본에서 데이터를 가져올 때 기존 관계 없는 데이터와 함께 자동으로 가져옵니다. 데이터 모델에서 관계를 자동으로 만들려면 데이터를 가져오기 위해, 데이터 원본에 테이블 사이 관계 여야 합니다.

모델 작성 진행 하기 전에 테이블 간의 관계가 확인 해야 제대로 생성 되었습니다. 이 자습서에서는 세 개의 새 관계 추가 합니다.  

  
#### <a name="to-review-existing-relationships"></a>기존 관계를 검토하려면  
  
1.  클릭 합니다 **모델** 메뉴 > **모델 뷰** > **다이어그램 보기**합니다.  

    이제 다이어그램 뷰의 모델 디자이너에 나타나는 모든 테이블을 표시 하는 그래픽 형식을 가져온 서로 줄. 테이블 사이의 줄은 데이터를 가져올 때 자동으로 생성된 관계를 나타냅니다.
    
    ![as-lesson4-diagram](../tutorial-tabular-1400/media/as-lesson4-diagram.png)
  
    > [!NOTE]
    > 테이블 간의 관계가 표시 되지 않으면, 데이터 원본에서 해당 테이블 간의 관계가 없으면 가지 것을 의미 합니다.

    모델 디자이너의 오른쪽 아래 모서리에 있는 미니 맵 컨트롤을 사용 하 여 테이블을 최대한 많이 포함 됩니다. 또한 테이블을 클릭하여 다른 위치에 끌어다 놓거나, 테이블 간 간격을 좁히거나, 테이블을 특정 순서로 배치할 수 있습니다. 테이블을 이동 해도 테이블 간의 관계는 적용 되지 않습니다. 특정 테이블의 모든 열을 보려면 클릭 한 후 끌어서 테이블 가장자리를 확장 하거나 축소 합니다.  
  
2.  사이의 실선을 클릭 합니다 **DimCustomer** 테이블 및 **DimGeography** 테이블입니다. 이러한 두 테이블 사이의 실선은이 관계가 활성, 즉, DAX 수식을 계산할 때 기본적으로는 보여 줍니다.  
  
    알림 합니다 **GeographyKey** 열에는 **DimCustomer** 테이블 및 **GeographyKey** 열에는 **DimGeography** 모두 이제 테이블 각각 상자 내에 표시 합니다. 이러한 열은 관계에 사용 됩니다. 관계의 속성을 현재에 표시 합니다 **속성** 창입니다.  
  
    > [!TIP]  
    > 또한 테이블 형식으로 모든 테이블 간에 관계를 표시 하려면 관계 관리 대화 상자를 사용할 수 있습니다. 테이블 형식 모델 탐색기에서 마우스 오른쪽 단추로 클릭 **관계** > **관계 관리**합니다.
  
3.  확인할 때 다음 관계가 생성 AdventureWorksDW 데이터베이스에서 가져온 각 테이블:  
  
    |활성|Table|관련 조회 테이블|  
    |----------|---------|------------------------|  
    |사용자 계정 컨트롤|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |사용자 계정 컨트롤|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |사용자 계정 컨트롤|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |사용자 계정 컨트롤|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |사용자 계정 컨트롤|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    관계의 값이 없는 경우 다음 테이블을 포함 하는 모델 확인 합니다. DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory 및 FactInternetSales 합니다. 동일한 데이터 원본 연결의 테이블을 별도 간의 관계가 시간에 가져오는 경우 해당 만들어지지 않으므로 테이블과 수동으로 만들어야 합니다. 관계 없음이 표시 하는 경우 데이터 원본에 관계가 없음을 의미 합니다. 데이터 모델에서 해당 작업을 수동으로 만들 수 있습니다.

### <a name="take-a-closer-look"></a>자세히 보기

다이어그램 뷰에 화살표, 별표 및 테이블 간의 관계를 보여 주는 선 수를 확인할 수 있습니다.

![as-lesson4-line](../tutorial-tabular-1400/media/as-lesson4-line.png)

화살표는 필터 방향을 나타냅니다. 이 테이블은 별표 표시는 *많은* 관계의 카디널리티에 한 쪽이이 테이블은 표시를 *하나* 관계의 측면입니다. 관계 편집 해야 할 경우 예를 들어 관계의 필터 방향 또는 카디널리티를 변경, 관계 편집 대화 상자를 열려면 관계 선을 두 번 클릭 합니다.

![as-lesson4-edit](../tutorial-tabular-1400/media/as-lesson4-edit.png)

이러한 고급 데이터 모델링을 위한는 기능과이 자습서에서 다루지 않습니다. 자세한 내용은 참조 하세요 [양방향 교차 필터 Analysis Services 테이블 형식 모델에](../tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)입니다.

경우에 따라 특정 비즈니스 논리를 지원하기 위해 모델의 테이블 간에 관계를 추가로 만들어야 할 수도 있습니다. 이 자습서에서는 FactInternetSales 테이블과 DimDate 테이블 간에 세 개의 관계를 만들려고 해야 합니다.  
  
#### <a name="to-add-new-relationships-between-tables"></a>테이블 간에 새 관계를 추가하려면  
  
1.  모델 디자이너에서에서 **FactInternetSales** 테이블를 클릭 한 채로 **OrderDate** 열에 커서를 놓습니다를 **날짜** 열에는  **DimDate** 테이블을 놓습니다.  

    간에 활성 관계를 만들었음을 보여 주는 실선이 나타납니다 합니다 **OrderDate** 열에는 **Internet Sales** 테이블 및 **날짜** 열에는  **날짜** 테이블입니다. 
  
      ![as-lesson4-new](../tutorial-tabular-1400/media/as-lesson4-new.png) 
  
    > [!NOTE]  
    > 관계를 만들 때 기본 테이블과 관련된 조회 테이블 간에 카디널리티 및 필터 방향이 자동으로 선택 됩니다.  
  
2.  에 **FactInternetSales** 테이블을 클릭 한 채로 합니다 **DueDate** 열 커서를 놓습니다를 **날짜** 열에는 **DimDate** 테이블을 놓습니다.  
  
    간에 비활성 관계를 만들었음을 보여 주는 점선이 나타납니다 합니다 **DueDate** 열에는 **FactInternetSales** 테이블 및 **날짜** 열에는  **DimDate** 테이블입니다. 테이블 간에 관계를 여러 개 설정할 수 있지만 한 번에 하나의 관계만 활성 상태일 수 있습니다. 사용자 지정 DAX 식에서 특별 한 집계를 수행 하기 위해 비활성 관계를 만들 수 있습니다.  
  
3.  마지막으로 하나 이상의 관계를 만듭니다. 에 **FactInternetSales** 테이블을 클릭 한 채로 합니다 **ShipDate** 열 커서를 놓습니다를 **날짜** 열에는 **DimDate** 테이블을 놓습니다.  
    
     ![as-lesson4-newinactive](../tutorial-tabular-1400/media/as-lesson4-newinactive.png)
  
## <a name="whats-next"></a>다음 단계

[5 단원: 계산된 열 만들기](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)합니다.
  
  
  
