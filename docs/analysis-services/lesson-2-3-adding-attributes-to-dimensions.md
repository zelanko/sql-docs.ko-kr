---
title: 차원에 특성 추가 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8c1332055548135595e4ccc59e0028992a2466a6
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="lesson-2-3---adding-attributes-to-dimensions"></a>Lesson 2-3-차원에 특성 추가
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

이제 차원을 정의했으므로 차원의 각 데이터 요소를 나타내는 특성으로 차원을 채울 수 있습니다. 일반적으로 특성은 데이터 원본 뷰의 필드를 기반으로 합니다. 차원에 특성을 추가할 때 데이터 원본 뷰에 있는 테이블의 필드를 포함할 수 있습니다.  
  
이 태스크에서는 차원 디자이너를 사용하여 Customer 및 Product 차원에 특성을 추가합니다. Customer 차원에는 Customer 및 Geography 테이블의 필드를 기반으로 하는 특성이 포함됩니다.  
  
## <a name="adding-attributes-to-the-customer-dimension"></a>Customer 차원에 특성 추가  
  
#### <a name="to-add-attributes"></a>특성을 추가하려면  
  
1.  Customer 차원에 대한 차원 디자이너를 엽니다. 이렇게 하려면 솔루션 탐색기의 **차원** 노드에서 **Customer** 차원을 두 번 클릭합니다.  
  
2.  **특성** 창에서 큐브 마법사에 의해 만들어진 Customer Key 및 Geography Key 특성을 확인합니다.  
  
3.  **차원 구조** 탭의 도구 모음에서 확대/축소 아이콘을 사용하여 **데이터 원본 뷰** 창의 테이블을 100%로 볼 수 있습니다.  
  
4.  **데이터 원본 뷰** 창의 **Customer** 테이블에서 다음 열을 **특성** 창으로 끕니다.  
  
    -   **BirthDate**  
  
    -   **MaritalStatus**  
  
    -   **Gender**  
  
    -   **EmailAddress**  
  
    -   **YearlyIncome**  
  
    -   **TotalChildren**  
  
    -   **NumberChildrenAtHome**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **HouseOwnerFlag**  
  
    -   **NumberCarsOwned**  
  
    -   **전화**  
  
    -   **DateFirstPurchase**  
  
    -   **CommuteDistance**  
  
5.  **데이터 원본 뷰** 창의 **Geography** 테이블에서 다음 열을 **특성** 창으로 끕니다.  
  
    -   **City**  
  
    -   **StateProvinceName**  
  
    -   **EnglishCountryRegionName**  
  
    -   **PostalCode**  
  
6.  파일 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="adding-attributes-to-the-product-dimension"></a>Product 차원에 특성 추가  
  
#### <a name="to-add-attributes"></a>특성을 추가하려면  
  
1.  Product 차원에 대한 차원 디자이너를 엽니다. 솔루션 탐색기에서 **Product** 차원을 두 번 클릭합니다.  
  
2.  **특성** 창에서 큐브 마법사에 의해 만들어진 Product Key 특성을 확인합니다.  
  
3.  **차원 구조** 탭의 도구 모음에서 확대/축소 아이콘을 사용하여 **데이터 원본 뷰** 창의 테이블을 100%로 볼 수 있습니다.  
  
4.  **데이터 원본 뷰** 창의 **Product** 테이블에서 다음 열을 **특성** 창으로 끕니다.  
  
    -   **StandardCost**  
  
    -   **색**  
  
    -   **SafetyStockLevel**  
  
    -   **ReorderPoint**  
  
    -   **ListPrice**  
  
    -   **크기**  
  
    -   **SizeRange**  
  
    -   **Weight**  
  
    -   **DaysToManufacture**  
  
    -   **ProductLine**  
  
    -   **DealerPrice**  
  
    -   **클래스**  
  
    -   **스타일**  
  
    -   **ModelName**  
  
    -   **StartDate**  
  
    -   **EndDate**  
  
    -   **상태**  
  
5.  파일 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[큐브 및 차원 속성 검토](../analysis-services/lesson-2-4-reviewing-cube-and-dimension-properties.md)  
  
## <a name="see-also"></a>관련 항목:  
[차원 특성 속성 참조](../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
  
