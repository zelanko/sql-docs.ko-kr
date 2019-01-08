---
title: Customer 차원 수정 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 5b5aed99-1760-4bc7-b248-52ecb0b97ebc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 55bf692e1b24bb0184f9b126a0bde5c0ee7e0657
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52513273"
---
# <a name="modifying-the-customer-dimension"></a>Customer 차원 수정
  다양한 방법을 통해 큐브에서 차원의 유용성과 기능을 향상시킬 수 있습니다. 이 항목의 태스크에서는 Customer 차원을 수정합니다.  
  
## <a name="renaming-attributes"></a>특성 이름 바꾸기  
 차원 디자이너의 **차원 구조** 탭을 사용하여 특성 이름을 바꿀 수 있습니다.  
  
#### <a name="to-rename-an-attribute"></a>특성 이름을 바꾸려면  
  
1.  **에서 Customer 차원에 대한** 차원 디자이너 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]로 전환합니다. 이렇게 하려면 솔루션 탐색기의 **차원** 노드에서 **Customer** 차원을 두 번 클릭합니다.  
  
2.  **특성** 창에서 **English Country Region Name**을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 클릭합니다. 특성의 이름을 변경 `Country-Region`합니다.  
  
3.  같은 방법으로 다음 특성 이름을 변경합니다.  
  
    -   **English Education** 특성-변경 `Education`  
  
    -   **English Occupation** 특성-변경 `Occupation`  
  
    -   **State Province Name** 특성-변경 `State-Province`  
  
4.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="creating-a-hierarchy"></a>계층 만들기  
 **특성** 창에서 **계층** 창으로 특성을 끌어 새 계층을 만들 수 있습니다.  
  
#### <a name="to-create-a-hierarchy"></a>계층을 만들려면  
  
1.  끌어서 합니다 `Country-Region` 에서 특성을 **특성** 창의 **계층** 창.  
  
2.  끌어서를 `State-Province` 에서 특성을 **특성** 창을  **\<새 수준 >** 셀에 **계층** 합니다 아래창`Country-Region` 수준.  
  
3.  끌어서를 **도시** 에서 특성을 **특성** 창의  **\<새 수준 >** 셀에 **계층** 창 아래는 `State-Province` 수준입니다.  
  
4.  에 **계층** 창을 **차원 구조** 탭, 제목 표시줄을 마우스 오른쪽 단추로 클릭 합니다 **계층** 계층 **이름바꾸기**를 입력 하 고 `Customer Geography`입니다.  
  
     계층 이름이 이제 `Customer Geography`합니다.  
  
5.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="adding-a-named-calculation"></a>명명된 계산 추가  
 계산 열로 표시되는 SQL 식인 명명된 계산을 데이터 원본 뷰의 테이블에 추가할 수 있습니다. 이 식은 테이블의 열로 나타나고 동작합니다. 명명된 계산을 사용하면 기본 데이터 원본의 테이블을 수정하지 않고 데이터 원본 뷰에서 기존 테이블의 관계형 스키마를 확장할 수 있습니다. 자세한 내용은 [데이터 원본 뷰에서 명명된 계산 정의&#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)를 참조하세요.  
  
#### <a name="to-add-a-named-calculation"></a>명명된 계산을 추가하려면  
  
1.  솔루션 탐색기의 **[!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 데이터 원본 뷰** 폴더에서 **DW 2012** 데이터 원본 뷰를 두 번 클릭하여 엽니다.  
  
2.  왼쪽의 **테이블** 창에서 **Customer**를 마우스 오른쪽 단추로 클릭한 다음 **새 명명된 계산**을 클릭합니다.  
  
3.  에 **명명 된 계산 만들기** 대화 상자에서 `FullName` 에 **열 이름** 상자의 및 다음 입력 하거나 복사 하는 다음을 붙여 넣습니다 `CASE` 문에서 **식**  상자:  
  
    ```  
    CASE  
       WHEN MiddleName IS NULL THEN  
       FirstName + ' ' + LastName  
       ELSE  
       FirstName + ' ' + MiddleName + ' ' + LastName  
    END  
    ```  
  
     합니다 `CASE` 문을 연결 합니다 **FirstName**를 **MiddleName**, 및 **LastName** 고객에서 사용할 단일 열으로 열을 차원 표시 이름 합니다 **고객** 특성입니다.  
  
4.  **확인**을 클릭한 다음 **테이블** 창에서 **Customer** 를 확장합니다.  
  
     `FullName` 임을 나타내는 아이콘과 함께 명명 된 계산이 Customer 테이블의 열 목록에 나타납니다 명명된 된 계산 합니다.  
  
5.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
6.  **테이블** 창에서 **Customer**를 마우스 오른쪽 단추로 클릭하고 **데이터 탐색**을 클릭합니다.  
  
7.  **Customer 테이블 탐색** 뷰의 마지막 열을 검토합니다.  
  
     다음에 유의 합니다 `FullName` 원래 데이터 원본을 수정 하지 않고 기본 데이터 원본에서 여러 열의 데이터를에서 올바르게 연결한 열 데이터 원본 뷰에 나타납니다.  
  
8.  **Customer 테이블 탐색** 탭을 닫습니다.  
  
## <a name="using-the-named-calculation-for-member-names"></a>멤버 이름에 명명된 계산 사용  
 데이터 원본 뷰에서 명명된 계산을 만든 후에는 이 명명된 계산을 특성의 속성으로 사용할 수 있습니다.  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>멤버 이름에 명명된 계산을 사용하려면  
  
1.  Customer 차원에 대한 차원 디자이너로 전환합니다.  
  
2.  **차원 구조** 탭의 **특성** 창에서 **Customer Key** 특성을 클릭합니다.  
  
3.  속성 창을 열고 제목 표시줄의 **자동 숨기기** 단추를 클릭하여 열린 상태를 유지하도록 합니다.  
  
4.  에 **이름을** 속성 필드에 입력 `Full Name`합니다.  
  
5.  클릭 합니다 **NameColumn** 속성 아래에 필드 및 클릭 한 다음 (**...** ) 버튼을 클릭 하 여 **이름 열** 대화 상자.  
  
6.  선택 `FullName` 맨 아래에 **원본 열** 목록을 연 다음 클릭 **확인**합니다.  
  
7.  차원 구조 탭에서 끌어를 `Full Name` 에서 특성을 **특성** 창의  **\<새 수준 >** 셀에 **계층** 창, 아래 합니다 **도시** 수준입니다.  
  
8.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="defining-display-folders"></a>표시 폴더 정의  
 사용자가 좀 더 쉽게 사용할 수 있도록 표시 폴더를 사용하여 사용자와 특성 계층을 폴더 구조로 그룹화할 수 있습니다.  
  
#### <a name="to-define-display-folders"></a>표시 폴더를 정의하려면  
  
1.  Customer 차원에 대한 **차원 구조** 탭을 엽니다.  
  
2.  **특성** 창에서 Ctrl 키를 누른 채 각 항목을 클릭하여 다음 특성을 선택합니다.  
  
    -   **City**  
  
    -   `Country-Region`  
  
    -   **우편 번호**  
  
    -   `State-Province`  
  
3.  속성 창에서 클릭 합니다 **AttributeHierarchyDisplayFolder** (전체 이름을 표시 하려면 가리켜야 할 수도 있습니다) 맨 위에 있는 속성 필드 입력 `Location`합니다.  
  
4.  에 **계층** 창 클릭 `Customer Geography`를 선택한 후 오른쪽 속성 창에서 `Location` 값으로는 **DisplayFolder** 속성입니다.  
  
5.  **특성** 창에서 Ctrl 키를 누른 채 각 항목을 클릭하여 다음 특성을 선택합니다.  
  
    -   **Commute Distance**  
  
    -   `Education`  
  
    -   **Gender**  
  
    -   **House Owner Flag**  
  
    -   **Marital Status**  
  
    -   **Number Cars Owned**  
  
    -   **Number Children At Home**  
  
    -   `Occupation`  
  
    -   **Total Children**  
  
    -   **Yearly Income**  
  
6.  속성 창에서 클릭 합니다 **AttributeHierarchyDisplayFolder** 속성 맨 위에 있는 필드를 입력 한 다음 `Demographic`합니다.  
  
7.  **특성** 창에서 Ctrl 키를 누른 채 각 항목을 클릭하여 다음 특성을 선택합니다.  
  
    -   **Email Address**  
  
    -   **전화**  
  
8.  속성 창에서 클릭 합니다 **AttributeHierarchyDisplayFolder** 속성 필드 형식과 `Contacts`합니다.  
  
9. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="defining-composite-keycolumns"></a>복합 KeyColumns 정의  
 **KeyColumns** 속성에는 특성의 키를 나타내는 열이 포함됩니다. 이 단원에 대 한 복합 키를 만듭니다는 **도시** 고 `State-Province` 특성입니다. 복합 키는 특성을 고유하게 식별해야 하는 경우 도움이 됩니다. 예를 들어 관계를 정의할 때 특성이이 자습서의 뒷부분에 **도시** 특성이 고유 하 게 식별 해야 합니다는 `State-Province` 특성입니다. 그런데 서로 다른 시/도에 같은 이름의 도시가 여러 개 있을 수 있습니다. 이러한 이유로 **City** 특성에 대해 **StateProvinceName** 및 **City** 열로 구성된 복합 키를 만드는 것입니다. 자세한 내용은 [특성의 KeyColumn 속성 수정](multidimensional-models/attribute-properties-modify-the-keycolumn-property.md)을 참조하세요.  
  
#### <a name="to-define-composite-keycolumns-for-the-city-attribute"></a>City 특성에 대한 복합 KeyColumns를 정의하려면  
  
1.  Customer 차원에 대한 **차원 구조** 탭을 엽니다.  
  
2.  **특성** 창에서 **City** 특성을 클릭합니다.  
  
3.  **속성** 창의 아래쪽에서 **KeyColumns** 필드를 클릭한 다음 찾아보기 단추(**...**)를 클릭합니다.  
  
4.  **키 열** 대화 상자의 **사용 가능한 열** 목록에서 **StateProvinceName**열을 선택한 후 **>** 단추를 클릭합니다.  
  
     이제 **City** 및 **StateProvinceName** 열이 **키 열** 목록에 표시됩니다.  
  
5.  **확인**을 클릭합니다.  
  
6.  **City** 특성의 **NameColumn** 속성을 설정하려면 속성 창에서 **NameColumn** 필드를 클릭한 다음 찾아보기 단추(**...**)를 클릭합니다.  
  
7.  **이름 열** 대화 상자의 **원본 열** 목록에서 **City**를 선택한 후 **확인**을 클릭합니다.  
  
8.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
#### <a name="to-define-composite-keycolumns-for-the-state-province-attribute"></a>State-Province 특성에 대한 복합 KeyColumns를 정의하려면  
  
1.  Customer 차원에 대한 **차원 구조** 탭을 엽니다.  
  
2.  에 **특성** 창 클릭는 `State-Province` 특성입니다.  
  
3.  **속성** 창에서 **KeyColumns** 필드를 클릭한 후 찾아보기 단추(**...**)를 클릭합니다.  
  
4.  **키 열** 대화 상자의 **사용 가능한 열** 목록에서 **EnglishCountryRegionName**열을 선택한 후 **>** 단추를 클릭합니다.  
  
     이제 **EnglishCountryRegionName** 및 **StateProvinceName** 열이 **키 열** 목록에 표시됩니다.  
  
5.  **확인**을 클릭합니다.  
  
6.  설정 하는 **NameColumn** 의 속성을 `State-Province` 특성을 클릭 합니다 **NameColumn** 속성 창에서 필드를 클릭 한 다음 (**...** ) 단추입니다.  
  
7.  **이름 열** 대화 상자의 **원본 열** 목록에서 **StateProvinceName**을 선택한 후 **확인**을 클릭합니다.  
  
8.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="defining-attribute-relationships"></a>특성 관계 정의  
 기본 데이터가 특성 관계를 지원하는 경우 특성 간의 특성 관계를 정의해야 합니다. 특성 관계를 정의하면 차원, 파티션 및 쿼리 처리가 빨라집니다. 자세한 내용은 [특성 관계 정의](multidimensional-models/attribute-relationships-define.md) 및 [특성 관계](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)를 참조하세요.  
  
#### <a name="to-define-attribute-relationships"></a>특성 관계를 정의하려면  
  
1.  Customer 차원의 **차원 디자이너** 에서 **특성 관계** 탭을 클릭합니다. 기다려야 할 수도 있습니다.  
  
2.  다이어그램에서 **City** 특성을 마우스 오른쪽 단추로 클릭한 다음 **새 특성 관계**를 클릭합니다.  
  
3.  **특성 관계 만들기** 대화 상자에서 **원본 특성** 은 **City**입니다. 설정 된 **관련 특성** 에 `State-Province`입니다.  
  
4.  **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
     멤버 간의 관계는 시간이 지나도 변경되지 않으므로 관계 유형은 **고정**입니다. 예를 들어 도시가 다른 시/도 소속으로 변경될 가능성은 거의 없습니다.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  다이어그램에서 마우스 오른쪽 단추로 클릭 합니다 `State-Province` 특성 및 선택한 **새 특성 관계**합니다.  
  
7.  에 **특성 관계 만들기** 대화 상자를 **원본 특성** 는 `State-Province`합니다. 설정 된 **관련 특성** 에 `Country-Region`입니다.  
  
8.  **관계 유형** 목록에서 관계 유형을 **고정**으로 설정합니다.  
  
9. **확인**을 클릭합니다.  
  
10. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="deploying-changes-processing-the-objects-and-viewing-the-changes"></a>변경 내용 배포, 개체 처리 및 변경 내용 표시  
 특성과 계층을 변경한 후에 변경 내용을 표시하려면 먼저 변경 내용을 배포하고 관련 개체를 다시 처리해야 합니다.  
  
#### <a name="to-deploy-the-changes-process-the-objects-and-view-the-changes"></a>변경 내용을 배포하고 개체를 처리한 다음 변경 내용을 표시하려면  
  
1.  **의** 빌드 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
2.  **배포가 완료되었습니다.** 메시지를 받은 후 Customer 차원에 대한 차원 디자이너의 **브라우저** 탭을 클릭한 다음 디자이너 도구 모음의 왼쪽에 있는 다시 연결 단추를 클릭합니다.  
  
3.  확인 `Customer Geography` 가 선택 합니다 **계층** 목록을 연 다음 브라우저 창에서 확장 **모든**, 확장 **오스트레일리아**, 확장 **새 남부 Wales**을 펼친 다음 **Coffs Harbour**합니다.  
  
     브라우저에 해당 도시의 고객이 표시됩니다.  
  
4.  **Tutorial 큐브에 대한** 큐브 디자이너 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 로 전환합니다. 이렇게 하려면 **솔루션 탐색기** 의 **큐브** 노드에서 **Analysis Services Tutorial**큐브를 두 번 클릭합니다.  
  
5.  **브라우저** 탭을 클릭한 다음 디자이너 도구 모음에서 다시 연결 단추를 클릭합니다.  
  
6.  **측정값 그룹** 창에서 **Customer**를 확장합니다.  
  
     긴 특성 목록이 아니라 표시 폴더와 표시 폴더 값이 포함되지 않은 특성만 Customer 아래에 나타납니다.  
  
7.  **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [Product 차원 수정](lesson-3-3-modifying-the-product-dimension.md)  
  
## <a name="see-also"></a>관련 항목  
 [차원 특성 속성 참조](multidimensional-models/dimension-attribute-properties-reference.md)   
 [차원에서 특성 제거](multidimensional-models/attribute-properties-remove-an-attribute-from-a-dimension.md)   
 [특성 이름을 바꾸려면](multidimensional-models/attribute-properties-rename-an-attribute.md)   
 [데이터 원본 뷰에서 명명된 계산 정의&#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
