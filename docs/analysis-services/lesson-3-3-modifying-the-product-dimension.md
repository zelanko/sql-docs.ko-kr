---
title: "Product 차원 수정 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 8e3ffecd-7f40-41a8-8735-bc9858a310cb
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8bbed44f2b02b0d94678513185dbf682a537e9e5
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2018
---
# <a name="lesson-3-3---modifying-the-product-dimension"></a>단원 3-3-Product 차원 수정
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

이 항목의 태스크에서는 명명된 계산을 사용하여 제품 라인에 대해 보다 설명적인 이름을 제공하고 Product 차원에 계층을 정의하고 계층에 대해 (All) 멤버 이름을 지정합니다. 또한 특성을 표시 폴더로 그룹화합니다.  
  
## <a name="adding-a-named-calculation"></a>명명된 계산 추가  
데이터 원본 뷰에서 테이블에 명명된 계산을 추가할 수 있습니다. 다음 태스크에서는 전체 제품 라인 이름을 표시하는 명명된 계산을 만듭니다.  
  
#### <a name="to-add-a-named-calculation"></a>명명된 계산을 추가하려면  
  
1.  **Adventure Works DW 2012** 데이터 원본 뷰를 열려면 솔루션 탐색기의 **데이터 원본 뷰** 폴더에서 **Adventure Works DW 2012** 를 두 번 클릭합니다.  
  
2.  다이어그램 창의 맨 아래에서 **Product** 테이블 머리글을 마우스 오른쪽 단추로 클릭한 다음 **새 명명된 계산**을 클릭합니다.  
  
3.  **명명된 계산 만들기** 대화 상자의 **열 이름** 상자에 **ProductLineName** 을 입력합니다.  
  
4.  **식** 상자에 다음 **CASE** 문을 입력하거나 복사하여 붙여넣습니다.  
  
    ```  
    CASE ProductLine  
       WHEN 'M' THEN 'Mountain'  
       WHEN 'R' THEN 'Road'  
       WHEN 'S' THEN 'Accessory'  
       WHEN 'T' THEN 'Touring'  
       ELSE 'Components'  
    END  
    ```  
  
    이 **CASE** 문은 큐브의 각 제품 라인에 대해 알기 쉬운 이름을 만듭니다.  
  
5.  **확인** 을 클릭하여 **ProductLineName** 명명된 계산을 만듭니다. 기다려야 할 수도 있습니다.  
  
6.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="modifying-the-namecolumn-property-of-an-attribute"></a>특성의 NameColumn 속성 수정  
  
#### <a name="to-modify-the-namecolumn-property-value-of-an-attribute"></a>특성의 NameColumn 속성 값을 수정하려면  
  
1.  Product 차원에 대한 차원 디자이너로 전환합니다. 이렇게 하려면 솔루션 탐색기의 **차원** 노드에서 **Product** 차원을 두 번 클릭합니다.  
  
2.  **차원 구조** 탭의 **특성** 창에서 **Product Line**을 선택합니다.  
  
3.  화면 오른쪽에 있는 속성 창의 맨 아래에서 **NameColumn** 속성 필드를 클릭한 다음 찾아보기(**…**) 단추를 클릭하여 **이름 열** 대화 상자를 엽니다. 화면 오른쪽의 **속성** 탭을 클릭하여 속성 창을 열어야 할 수도 있습니다.  
  
4.  **원본 열** 목록의 맨 아래에서 **ProductLineName** 을 선택하고 **확인**을 클릭합니다.  
  
    이제 NameColumn 필드에 **Product.ProductLineName (WChar)**텍스트가 포함됩니다. **Product Line** 특성 계층의 멤버가 약식 제품 라인 이름이 아니라 전체 제품 라인 이름을 표시합니다.  
  
5.  **차원 구조** 탭의 **특성** 창에서 **Product Key**를 선택합니다.  
  
6.  속성 창에서 **NameColumn** 속성 필드를 클릭한 다음 줄임표(**…**) 단추를 클릭하여 **이름 열** 대화 상자를 엽니다.  
  
7.  **원본 열** 목록에서 **EnglishProductName** 을 선택하고 **확인**을 클릭합니다.  
  
    이제 NameColumn 필드에 **Product.EnglishProductName (WChar)**텍스트가 포함됩니다.  
  
8.  속성 창에서 위로 스크롤하여 **Name** 속성 필드를 클릭하고 **Product Name**을 입력합니다.  
  
## <a name="creating-a-hierarchy"></a>계층 만들기  
  
#### <a name="to-create-a-hierarchy"></a>계층을 만들려면  
  
1.  **특성** 창의 **Product Line** 특성을 **계층** 창으로 끌어옵니다.  
  
2.  **특성** 창의 **Model Name** 특성을 **<new level>** 계층 **창의** Product Line **수준 아래** 셀에 끌어옵니다.  
  
3.  **특성** 창의 **Product Name** 특성을 **<new level>** 계층 **창의** Model Name **수준 아래** 셀에 끌어옵니다. 이전 단원에서 Product Key를 Product Name으로 바꿨습니다.  
  
4.  **차원 구조** 탭의 **계층** 창에서 **Hierarchy** 계층의 제목 표시줄을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 클릭한 다음 **Product Model Lines**를 입력합니다.  
  
    이제 계층 이름이 **Product Model Lines**가 됩니다.  
  
5.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="specifying-folder-names-and-all-member-names"></a>폴더 이름 및 모든 멤버 이름 지정  
  
#### <a name="to-specify-the-folder-and-member-names"></a>폴더 이름 및 멤버 이름을 지정하려면  
  
1.  **특성** 창에서 Ctrl 키를 누른 채 각 항목을 클릭하여 다음 특성을 선택합니다.  
  
    -   **클래스**  
  
    -   **색**  
  
    -   **Days To Manufacture**  
  
    -   **Reorder Point**  
  
    -   **Safety Stock Level**  
  
    -   **크기**  
  
    -   **Size Range**  
  
    -   **스타일**  
  
    -   **Weight**  
  
2.  속성 창의 **AttributeHierarchyDisplayFolder** 속성 필드에서 **Stocking**을 입력합니다.  
  
    이제 이러한 특성을 단일 표시 폴더로 그룹화했습니다.  
  
3.  **특성** 창에서 다음 특성을 선택합니다.  
  
    -   **Dealer Price**  
  
    -   **List Price**  
  
    -   **Standard Cost**  
  
4.  속성 창의 **AttributeHierarchyDisplayFolder** 속성 셀에 **Financial**을 입력합니다.  
  
    이제 이러한 특성을 두 번째 표시 폴더로 그룹화했습니다.  
  
5.  **특성** 창에서 다음 특성을 선택합니다.  
  
    -   **End Date**  
  
    -   **Start Date**  
  
    -   **상태**  
  
6.  속성 창의 **AttributeHierarchyDisplayFolder** 속성 셀에 **History**를 입력합니다.  
  
    이제 이러한 특성을 세 번째 표시 폴더로 그룹화했습니다.  
  
7.  **계층** 창에서 **Product Model Lines** 계층을 선택한 다음 속성 창의 **AllMemberName** 속성을 **All Products**로 변경합니다.  
  
8.  **계층** 창의 열린 영역을 클릭한 다음 속성 창의 맨 위에 있는 **AttributeAllMemberName** 속성을 **All Products**로 변경합니다.  
  
    열린 영역을 클릭하면 Product 차원 자체의 속성을 수정할 수 있습니다. **특성** 창의 특성 목록 맨 위에 있는 **Product** 를 클릭해도 됩니다.  
  
9. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="defining-attribute-relationships"></a>특성 관계 정의  
기본 데이터가 특성 관계를 지원하는 경우 특성 간의 특성 관계를 정의해야 합니다. 특성 관계를 정의하면 차원, 파티션 및 쿼리 처리가 빨라집니다. 자세한 내용은 [특성 관계 정의](../analysis-services/multidimensional-models/attribute-relationships-define.md) 및 [특성 관계](../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)를 참조하세요.  
  
#### <a name="to-define-attribute-relationships"></a>특성 관계를 정의하려면  
  
1.  Product 차원의 **차원 디자이너** 에서 **특성 관계** 탭을 클릭합니다.  
  
2.  다이어그램에서 **Model Name** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 클릭합니다.  
  
3.  **특성 관계 만들기** 대화 상자에서 **원본 특성**은 **Model Name**입니다. **관련 특성** 을 **Product Line**으로 설정합니다.  
  
    멤버 간의 관계는 시간이 지나면 변경될 수 있으므로 **관계 유형** 목록에서 관계 유형을 **유동** 으로 설정된 상태로 둡니다. 예를 들어 제품 모델은 나중에 다른 제품 라인으로 이전될 수 있습니다.  
  
4.  **확인**을 클릭합니다.  
  
5.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="reviewing-product-dimension-changes"></a>Product 차원 변경 내용 검토  
  
#### <a name="to-review-the-product-dimension-changes"></a>Product 차원 변경 내용을 검토하려면  
  
1.  **의** 빌드 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
2.  **배포가 완료되었습니다.** 메시지를 받은 후 **Product** 차원에 대한 **차원 디자이너** 의 **브라우저** 탭을 클릭한 다음 디자이너의 도구 모음에 있는 다시 연결 단추를 클릭합니다.  
  
3.  **계층** 목록에서 **Product Model Lines** 가 선택되어 있는지 확인한 다음 **All Products**를 확장합니다.  
  
    **All** 멤버의 이름이 **All Products**로 나타납니다. 이 단원의 앞부분에서 계층에 대한 **AllMemberName** 속성을 **All Products** 로 변경했기 때문입니다. 또한 **Product Line** 수준의 멤버는 이제 한 자로 된 약어가 아니라 알아보기 쉬운 이름을 갖게 되었습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[Date 차원 수정](../analysis-services/lesson-3-4-modifying-the-date-dimension.md)  
  
## <a name="see-also"></a>관련 항목:  
[데이터 원본 뷰 &#40; 명명 된 계산을 정의 합니다. Analysis Services &#41;](../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
[사용자 정의 계층 만들기](../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)  
[특성 계층에 대해 &#40;All&#41; 수준 구성](../analysis-services/multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
