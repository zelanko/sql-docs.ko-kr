---
title: "5 단원: 관계 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: abac1a00-f827-4c3e-a473-6db5c8a3a66f
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 318b583cc92dcd70c75f0eb04be262a82ecf7d1d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="lesson-4-create-relationships"></a>4단원: 관계 만들기
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

이 단원에서는 데이터를 가져올 때 자동으로 생성 된 관계를 확인 및 서로 다른 테이블 간에 새 관계를 추가 합니다. 관계는 두 테이블에 있는 데이터의 상관 관계를 설정하기 위한 테이블 간 연결입니다. 예를 들어 DimProduct 테이블과 DimProductSubcategory 테이블의 경우 테이블의 각 제품이 하위 범주에 속한다는 점에서 두 테이블 간에는 관계가 있습니다. 자세한 내용은 참고 [관계](../analysis-services/tabular-models/relationships-ssas-tabular.md)합니다.
  
이 단원에 소요되는 예상 시간: **10분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [3 단원: 날짜 테이블로 표시](../analysis-services/lesson-3-mark-as-date-table.md)합니다. 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>기존 관계를 검토하고 새 관계 추가  
테이블 가져오기 마법사를 사용 하 여 데이터를 가져올 때 AdventureWorksDW 데이터베이스에서 7 개의 테이블을 가져왔습니다. 일반적으로 관계형 원본에서 데이터를 가져올 때 기존 관계 없는 데이터와 함께 자동으로 가져옵니다. 그러나 모델 제작을 계속하기 전에 테이블 간 관계가 제대로 생성되었는지 확인해야 합니다. 이 자습서에서는 세 개의 새로운 관계도 추가합니다.  
  
#### <a name="to-review-existing-relationships"></a>기존 관계를 검토하려면  
  
1.  클릭는 **모델** 메뉴 > **모델 뷰** > **다이어그램 보기**합니다.  

    그러면 모델 디자이너가 다이어그램 뷰에 표시됩니다. 다이어그램 뷰는 사용자가 가져온 모든 테이블을 테이블 사이에 줄을 넣어 표시하는 그래픽 형식입니다. 테이블 사이의 줄은 데이터를 가져올 때 자동으로 생성된 관계를 나타냅니다.
    
    ![로-테이블 형식-lesson4-다이어그램](../analysis-services/media/as-tabular-lesson4-diagram.png)
  
    모델 디자이너의 오른쪽 아래에 있는 미니맵 컨트롤을 사용하여 뷰를 조정하면 테이블을 가능한 한 많이 포함할 수 있습니다. 또한 테이블을 클릭하여 다른 위치에 끌어다 놓거나, 테이블 간 간격을 좁히거나, 테이블을 특정 순서로 배치할 수 있습니다. 테이블을 이동해도 테이블 간 관계에는 영향이 없습니다. 특정 테이블의 모든 열을 보려면 테이블 가장자리를 클릭한 후 끌어서 테이블을 확장하거나 축소합니다.  
  
2.  클릭 사이의 실선은 **DimCustomer** 테이블 및 **DimGeography** 테이블입니다. 이 두 테이블 사이의 실선은 이 관계가 활성 상태이며 DAX 수식을 계산할 때 기본적으로 사용된다는 것을 나타냅니다.  
  
    공지는 **GeographyKey** 열에는 **DimCustomer** 테이블 및 **GeographyKey** 열에는 **DimGeography** 테이블 이제 모두 각각 상자 내에 표시 합니다. 이는 이 두 열이 관계에 사용되는 열임을 나타냅니다. 또한 관계의 속성이 **속성** 창에 표시됩니다.  
  
    > [!TIP]  
    > 다이어그램 뷰에서 모델 디자이너를 사용 하는 것 외에도 테이블 형식으로 모든 테이블 간의 관계를 나타낼 수도 관계 관리 대화 상자를 사용할 수 있습니다. 마우스 오른쪽 단추로 클릭 **관계** 테이블 형식 모델 탐색기에서를 클릭 한 다음 **관계 관리**합니다. 관계 관리 대화 상자는 데이터를 가져올 때 자동으로 생성 된 관계를 나타냅니다.  
  
3.  모델 디자이너에서 다이어그램 보기 또는 관계 관리 대화 상자를 사용 하 여 때 다음 관계가 생성 되었는지 확인 하려면 각 테이블에서에서 가져온 AdventureWorksDW 데이터베이스:  
  
    |활성|Table|관련 조회 테이블|  
    |----------|---------|------------------------|  
    |예|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |예|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |예|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |예|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |예|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    위의 표에 있는 관계 중 누락 된 경우 다음 표에서 모델에 포함 되어 있는지 확인: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory, 및 FactInternetSales 합니다. 동일한 데이터 원본 연결에서 각기 다른 시간에 테이블을 가져오는 경우에는 해당 테이블 간에 관계가 생성되지 않으므로 관계를 수동으로 만들어야 합니다.  

### <a name="take-a-closer-look"></a>자세히 조사
다이어그램 뷰에서 화살표는 별표 및 테이블 간의 관계를 표시 하는 줄 번호를 확인할 수 있습니다.

![으로 테이블 형식-lesson4-줄](../analysis-services/media/as-tabular-lesson4-line.png)

화살표는 테이블 관계의 카디널리티의 "다" 쪽 이며 1에서이 테이블은 관계의 한 쪽을 보여 줍니다.이 별표 표시 필터 방향을 보여 줍니다. 관계; 편집 하려는 경우 예를 들어 관계의 필터 방향을 나 카디널리티 변경, 관계 편집 대화 상자를 열려면 다이어그램 뷰에서 관계 선을 두 번 클릭 합니다.

![으로 테이블 형식-lesson4-편집](../analysis-services/media/as-tabular-lesson4-edit.png)

대부분의 경우는 관계를 편집할 필요가 없습니다. 이 기능은 고급 데이터 모델링을 위한 있으며이 자습서에서 다루지 않습니다. 자세한 내용은 참고 [양방향 교차 필터에서 SQL Server 2016 Analysis Services 테이블 형식 모델에 대 한](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)합니다.

경우에 따라 특정 비즈니스 논리를 지원하기 위해 모델의 테이블 간에 관계를 추가로 만들어야 할 수도 있습니다. 이 자습서에서는 세 개의 FactInternetSales 테이블과 DimDate 테이블 간에 관계를 추가로 만들 해야 합니다.  
  
#### <a name="to-add-new-relationships-between-tables"></a>테이블 간에 새 관계를 추가하려면  
  
1.  모델 디자이너에서의 **FactInternetSales** 테이블을 클릭 한 채로 **OrderDate** 열에서 다음 커서를 끌어는 **날짜** 열에는  **DimDate** 테이블을 마우스를 놓습니다.  

    간에 활성 관계를 만들었음을 보여 주는 실선이 나타납니다는 **OrderDate** 열에는 **인터넷 판매** 테이블 및 **날짜** 열에는 **날짜** 테이블입니다. 
  
      ![as-테이블 형식-lesson4-n e w](../analysis-services/media/as-tabular-lesson4-new.png) 
  
    > [!NOTE]  
    > 관계를 만들 때 기본 테이블과 관련된 조회 테이블 간에 카디널리티 및 필터 방향은 자동으로 선택 됩니다.  
  
2.  에 **FactInternetSales** 테이블을 클릭 한 채로 **DueDate** 열에서 다음 커서를 끌어는 **날짜** 열에는 **DimDate** 테이블을 마우스를 놓습니다.  
  
    간에 비활성 관계를 만들었음을 보여 주는 점선이 나타납니다는 **DueDate** 열에는 **FactInternetSales** 테이블 및 **날짜** 는 의열 **DimDate** 테이블입니다. 테이블 간에 관계를 여러 개 설정할 수 있지만 한 번에 하나의 관계만 활성 상태일 수 있습니다.  
  
3.  마지막으로, 관계를 하나 더; 만듭니다 에 **FactInternetSales** 테이블을 클릭 한 채로 **ShipDate** 열에서 다음 커서를 끌어는 **날짜** 열에는 **DimDate** 테이블 및 놓습니다.  
    
     ![로-테이블 형식-lesson4-newinactive](../analysis-services/media/as-tabular-lesson4-newinactive.png)
  
## <a name="whats-next"></a>다음 단계
다음 단원으로 이동: [5 단원: 계산 열 만들기](../analysis-services/lesson-5-create-calculated-columns.md)합니다.
  
  
  
