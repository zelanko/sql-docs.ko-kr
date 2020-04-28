---
title: 계산 멤버 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 07f13e1c-0b20-4f9e-ad62-c438983f2785
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ede0a23a6e37c47a1af242748233ca49b0cdfab7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "69493881"
---
# <a name="defining-calculated-members"></a>계산 멤버 정의
  계산 멤버는 큐브 데이터, 산술 연산자, 숫자 및 함수 조합을 기반으로 정의되는 차원 또는 측정값 그룹의 멤버입니다. 예를 들어 큐브에 있는 두 개의 물리적 측정값 합계를 계산하는 계산 멤버를 만들 수 있습니다. 계산 멤버 정의는 큐브에 저장되지만 해당 값은 쿼리 시간에 계산됩니다.  
  
 계산 멤버를 만들려면 큐브 디자이너의 **계산 탭** 에 있는 **새 계산 멤버** 명령을 사용합니다. 측정값 차원을 비롯하여 모든 차원 내에서 계산 멤버를 만들 수 있습니다. 또한 **계산 속성** 대화 상자에서 표시 폴더 안에 계산 멤버를 둘 수 있습니다. 자세한 내용은 [계산](multidimensional-models-olap-logical-cube-objects/calculations.md), [다차원 모델의 계산](multidimensional-models/calculations-in-multidimensional-models.md)및 [계산 멤버 만들기](multidimensional-models/create-calculated-members.md)를 참조하세요.  
  
 이 항목의 태스크에서는 사용자들이 인터넷 판매, 대리점 판매 및 모든 판매에 대해 매출이익률과 매출 비율을 확인할 수 있는 계산 측정값을 정의합니다.  
  
## <a name="defining-calculations-to-aggregate-physical-measures"></a>물리적 측정값을 집계하는 계산 정의  
  
1.  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 대한 큐브 디자이너를 열고 **계산** 탭을 클릭합니다.  
  
     **계산 식** 창 및 **스크립트 구성 도우미** 창에는 기본 CALCULATE 명령이 제공됩니다. 이 명령은 큐브의 측정값을 AggregateFunction 속성으로 지정된 값에 따라 집계하도록 지정합니다. 측정값은 일반적으로 합산되지만 약간 다른 방식으로 계산되거나 집계될 수도 있습니다.  
  
     다음 그림에서는 큐브 디자이너의 **계산** 탭을 보여 줍니다.  
  
     ![큐브 디자이너의 계산 탭](../../2014/tutorials/media/l6-calculatedmembers-1.gif "큐브 디자이너의 계산 탭")  
  
2.  **계산** 탭의 도구 모음에서 **새 계산 멤버**를 클릭합니다.  
  
     이 새 계산 멤버의 속성을 정의할 수 있는 새 양식이 **계산 식** 창에 표시됩니다. 새 멤버는 **스크립트 구성 도우미** 창에도 표시됩니다.  
  
     다음 그림에서는 **새 계산 멤버** 를 클릭할 때 **계산 식**창에 나타나는 양식을 보여 줍니다.  
  
     ![계산 식 창 양식](../../2014/tutorials/media/l6-calculatedmembers-02.gif "계산 식 창 양식")  
  
3.  **이름** 상자에서 계산 측정값의 이름을로 `[Total Sales Amount]`변경 합니다.  
  
     계산 멤버의 이름에 공백이 들어 있으면 계산 멤버 이름을 대괄호로 묶어야 합니다.  
  
     기본적으로 **부모 계층** 목록의 **Measures** 차원에 새 계산 멤버가 생성됩니다. 측정값 차원의 계산 멤버를 계산 측정값이라고도 합니다.  
  
4.  **계산** 탭의 **계산 도구** 창에 있는 **메타데이터** 탭에서 **Measures** 를 확장한 후 **Internet Sales** 를 확장하여 **Internet Sales** 측정값 그룹에 대한 메타데이터를 확인합니다.  
  
     **계산 도구** 창의 메타데이터 요소를 **식** 상자로 끌어온 다음 연산자 및 기타 요소를 추가하여 MDX(Multidimensional Expressions) 식을 만들 수 있습니다. 또는 **식** 상자에 직접 MDX 식을 입력할 수 있습니다.  
  
    > [!NOTE]  
    >  **계산 도구** 창에 메타데이터가 표시되지 않으면 도구 모음에서 **다시 연결** 을 클릭합니다. 이 옵션을 사용할 수 없으면 큐브를 처리하거나 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 시작해야 할 수 있습니다.  
  
5.  **계산 도구** 창의 **메타데이터** 탭에서 **계산 식** 창의 **식** 상자로 **Internet Sales-Sales Amount** 를 끌어옵니다.  
  
6.  **식** 상자에서`+`[Measures].[Internet Sales-Sales Amount] **뒤에 더하기 기호(**)를 입력합니다.  
  
7.  **계산 도구** 창의 **메타데이터** 탭에서 **Reseller Sales**를 확장한 후 **계산 식** 창의 **식** 상자에서 더하기 기호(+) 뒤로 **Reseller Sales-Sales Amount** 를 끌어옵니다.  
  
8.  **형식 문자열** 목록에서 **"Currency"를 선택 합니다.**  
  
9. **비어 있지 않은 동작** 목록에서 **Internet Sales-Sales Amount** 및 **Reseller Sales-Sales Amount**에 대한 확인란을 선택한 다음 **확인**을 클릭합니다.  
  
     **비어 있지 않은 동작** 목록에서 지정한 측정값은 MDX의 NON EMPTY 쿼리를 해결하는 데 사용됩니다. **비어 있지 않은 동작** 목록에 하나 이상의 측정값을 지정하면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 지정된 모든 측정값이 비어 있는 경우 계산 멤버를 비어 있는 것으로 취급합니다. **비어 있지 않은 동작** 속성을 비워 두면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 계산 멤버 자체를 계산하여 멤버가 비어 있는지 여부를 확인해야 합니다.  
  
     다음 그림에서는 이전 단계에서 지정한 설정으로 채워진 **계산 식** 창을 보여 줍니다.  
  
     ![채워진 계산 식 창](../../2014/tutorials/media/l6-calculatedmembers-03.gif "채워진 계산 식 창")  
  
10. **계산** 탭의 도구 모음에서 **스크립트 보기**를 클릭한 후 **계산 식** 창에서 계산 스크립트를 검토합니다.  
  
     새 계산은 초기 CALCULATE 식에 추가되며 개별 계산은 세미콜론으로 구분됩니다. 또한 계산 스크립트 맨 앞에 설명이 표시됩니다. 계산 스크립트 내에 계산 그룹에 대한 설명을 추가하면 사용자 자신 및 다른 개발자가 복잡한 계산 스크립트를 이해하는 데 도움을 주므로 바람직합니다.  
  
11. 계산 스크립트에서 **Calculate;** 명령 뒤, 새로 추가한 계산 스크립트 앞에 새 줄을 추가한 후 다음 텍스트를 별도의 줄로 스크립트에 추가합니다.  
  
    ```  
    /* Calculations to aggregate Internet Sales and Reseller Sales measures */  
    ```  
  
     다음 그림에서는 자습서의 이 부분에서 **계산 식** 창에 표시되어야 하는 계산 스크립트를 보여 줍니다.  
  
     ![계산 식 창의 스크립트](../../2014/tutorials/media/l6-calculatedmembers-04.gif "계산 식 창의 스크립트")  
  
12. **계산** 탭의 도구 모음에서 **폼 보기**를 클릭 하 고 `[Total Sales Amount]` **스크립트 구성 도우미** 창에서가 선택 되어 있는지 확인 한 다음 **새 계산 멤버**를 클릭 합니다.  
  
13. 이 새 계산 멤버의 이름을로 `[Total Product Cost]`변경 하 고 **식** 상자에 다음 식을 만듭니다.  
  
    ```  
    [Measures].[Internet Sales-Total Product Cost] + [Measures].[Reseller Sales-Total Product Cost]  
    ```  
  
14. **형식 문자열** 목록에서 **"Currency"** 를 선택합니다.  
  
15. **비어 있지 않은 동작** 목록에서 **Internet Sales-Total Product Cost** 및 **Reseller Sales-Total Product Cost**에 대한 확인란을 선택한 다음 **확인**을 클릭합니다.  
  
     이제 두 개의 계산 멤버가 정의되었으며 이 멤버는 **스크립트 구성 도우미** 창에 표시됩니다. 이러한 계산 멤버는 계산 스크립트에서 이후 정의하는 다른 계산에도 사용할 수 있습니다. **스크립트 구성 도우미** 창에서 계산 멤버를 선택하여 계산 멤버의 정의를 확인할 수 있습니다. 계산 멤버의 정의는 폼 보기의 **계산 식** 창에 나타납니다. 새로 정의한 계산 멤버는 해당 개체를 배포한 후에만 **계산 도구** 창에 나타납니다. 계산을 위한 추가 처리는 필요하지 않습니다.  
  
## <a name="defining-gross-profit-margin-calculations"></a>매출이익률 계산 정의  
  
1.  `[Total Product Cost]` **스크립트 구성 도우미** 창에서가 선택 되어 있는지 확인 한 다음 **계산** 탭의 도구 모음에서 **새 계산 멤버** 를 클릭 합니다.  
  
2.  **이름** 상자에서이 새 계산 측정값의 이름을로 `[Internet GPM]`변경 합니다.  
  
3.  **식** 상자에서 다음 MDX 식을 만듭니다.  
  
    ```  
    ([Measures].[Internet Sales-Sales Amount] -   
    [Measures].[Internet Sales-Total Product Cost]) /  
    [Measures].[Internet Sales-Sales Amount]  
    ```  
  
4.  **형식 문자열** 목록에서 **"Percent"** 를 선택합니다.  
  
5.  **비어 있지 않은 동작** 목록에서 **Internet Sales-Sales Amount**에 대한 확인란을 선택한 다음 **확인**을 클릭합니다.  
  
6.  **계산** 탭의 도구 모음에서 **새 계산 멤버**를 클릭합니다.  
  
7.  **이름** 상자에서이 새 계산 측정값의 이름을로 `[Reseller GPM]`변경 합니다.  
  
8.  **식** 상자에서 다음 MDX 식을 만듭니다.  
  
    ```  
    ([Measures].[Reseller Sales-Sales Amount] -   
    [Measures].[Reseller Sales-Total Product Cost]) /  
    [Measures].[Reseller Sales-Sales Amount]  
    ```  
  
9. **형식 문자열** 목록에서 **"Percent"** 를 선택합니다.  
  
10. **비어 있지 않은 동작** 목록에서 **Reseller Sales-Sales Amount**에 대한 확인란을 선택한 다음 **확인**을 클릭합니다.  
  
11. **계산** 탭의 도구 모음에서 **새 계산 멤버**를 클릭합니다.  
  
12. **이름** 상자에서이 계산 측정값의 이름을로 `[Total GPM]`변경 합니다.  
  
13. **식** 상자에서 다음 MDX 식을 만듭니다.  
  
    ```  
    ([Measures].[Total Sales Amount] -   
    [Measures].[Total Product Cost]) /  
    [Measures].[Total Sales Amount]  
    ```  
  
     이 계산 멤버는 다른 계산 멤버를 참조하고 있습니다. 이 계산 멤버는 자신이 참조하는 계산 멤버 다음에 계산되므로 유효한 계산 멤버입니다.  
  
14. **형식 문자열** 목록에서 **"Percent"** 를 선택합니다.  
  
15. **비어 있지 않은 동작** 목록에서 **Internet Sales-Sales Amount** 및 **Reseller Sales-Sales Amount**에 대한 확인란을 선택한 다음 **확인**을 클릭합니다.  
  
16. **계산** 탭의 도구 모음에서 **스크립트 보기** 를 클릭하고 계산 스크립트에 방금 추가한 3개의 계산을 검토합니다.  
  
17. 계산 스크립트에서 `[Internet GPM]` 계산 바로 앞에 새 줄을 추가한 후 다음 텍스트를 별도의 줄로 스크립트에 추가 합니다.  
  
    ```  
    /* Calculations to calculate gross profit margin */  
    ```  
  
     다음 그림에서는 3개의 새 계산을 포함하는 **식** 창을 보여 줍니다.  
  
     ![계산 식 창의 새 계산](../../2014/tutorials/media/l6-calculatedmembers-05.gif "계산 식 창의 새 계산")  
  
## <a name="defining-the-percent-of-total-calculations"></a>총 계산의 백분율 정의  
  
1.  **계산** 탭의 도구 모음에서 **폼 보기**를 클릭합니다.  
  
2.  **스크립트 구성 도우미** 창에서를 선택한 `[Total GPM]`다음 **계산** 탭의 도구 모음에서 **새 계산 멤버** 를 클릭 합니다.  
  
     **새 계산 멤버** 를 클릭하기 전에 **스크립트 구성 도우미** 창에서 최종 계산 멤버를 클릭하면 새 계산 멤버가 스크립트 끝에 삽입됩니다. 스크립트는 **스크립트 구성 도우미** 창에 나타난 순서대로 실행됩니다.  
  
3.  이 새 계산 멤버의 이름을로 `[Internet Sales Ratio to All Products]`변경 합니다.  
  
4.  **식** 입력란에 다음 식을 입력합니다.  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Internet Sales-Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Internet Sales-Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Internet Sales-Sales Amount] )  
        End  
    ```  
  
     이 MDX 식은 각 제품의 총 인터넷 판매에 영향을 미치는 요인을 계산합니다. Case 문을 IS EMPTY 함수와 함께 사용하면 제품 판매가 없을 때 0으로 나누기 오류가 발생하지 않습니다.  
  
5.  **형식 문자열** 목록에서 **"Percent"** 를 선택합니다.  
  
6.  **비어 있지 않은 동작** 목록에서 **Internet Sales-Sales Amount**에 대한 확인란을 선택한 다음 **확인**을 클릭합니다.  
  
7.  **계산** 탭의 도구 모음에서 **새 계산 멤버**를 클릭합니다.  
  
8.  이 계산 멤버의 이름을로 `[Reseller Sales Ratio to All Products]`변경 합니다.  
  
9. **식** 입력란에 다음 식을 입력합니다.  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Reseller Sales-Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Reseller Sales-Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Reseller Sales-Sales Amount] )  
        End  
    ```  
  
10. **형식 문자열** 목록에서 **"Percent"** 를 선택합니다.  
  
11. **비어 있지 않은 동작** 목록에서 **Reseller Sales-Sales Amount**에 대한 확인란을 선택한 다음 **확인**을 클릭합니다.  
  
12. **계산** 탭의 도구 모음에서 **새 계산 멤버**를 클릭합니다.  
  
13. 이 계산 멤버의 이름을로 `[Total Sales Ratio to All Products]`변경 합니다.  
  
14. **식** 입력란에 다음 식을 입력합니다.  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Total Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Total Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Total Sales Amount] )  
        End  
    ```  
  
15. **형식 문자열** 목록에서 **"Percent"** 를 선택합니다.  
  
16. **비어 있지 않은 동작** 목록에서 **Internet Sales-Sales Amount** 및 **Reseller Sales-Sales Amount**에 대한 확인란을 선택한 다음 **확인**을 클릭합니다.  
  
17. **계산** 탭의 도구 모음에서 **스크립트 보기**를 클릭하고 계산 스크립트에 방금 추가한 3개의 계산을 검토합니다.  
  
18. 계산 스크립트에서 `[Internet Sales Ratio to All Products]` 계산 바로 앞에 새 줄을 추가한 후 다음 텍스트를 별도의 줄로 스크립트에 추가 합니다.  
  
    ```  
    /* Calculations to calculate percentage of product to total product sales */  
    ```  
  
     이제 총 8개의 계산 멤버가 정의되었으며 이 멤버는 폼 보기에서 **스크립트 구성 도우미** 창에 표시됩니다.  
  
## <a name="browsing-the-new-calculated-members"></a>새 계산 멤버 검색  
  
1.  **의** 빌드 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
2.  배포가 성공적으로 완료되면 **브라우저** 탭으로 전환한 다음 **다시 연결**을 클릭합니다.  
  
3.  Excel 아이콘을 클릭한 다음 **사용**을 클릭합니다.  
  
4.  **피벗 테이블 필드 목록** 창에서 **값** 폴더를 확장하여 측정값 차원의 새 계산 멤버를 확인합니다.  
  
5.  **Total Sales Amount** 를 값 영역으로 끌어간 다음 결과를 검토합니다.  
  
     **Internet Sales** 및 **Reseller Sales** 측정값 그룹의 **Internet Sales-Sales Amount** 및 **Reseller Sales-Sales Amount** 측정값을 값 영역으로 끌어옵니다.  
  
     **Total Sales Amount** 측정값은 **Internet Sales-Sales Amount** 측정값과 **Reseller Sales-Sales Amount** 측정값을 합한 것입니다.  
  
6.  **보고서 필터** 영역의 필터 영역에 **Product Categories** 사용자 정의 계층을 추가한 후 **Mountain Bikes**를 기준으로 데이터를 필터링합니다.  
  
     **Mountain Bikes** 의 **Internet Sales-Sales Amount** 및 **Reseller Sales-Sales Amount** 측정값을 기반으로 제품 판매의 **Mountain Bikes** 범주에 대한 **Total Sales Amount**측정값이 계산됩니다.  
  
7.  행 레이블 영역에 **Date.Calendar Date** 사용자 정의 계층을 추가한 후 결과를 검토합니다.  
  
     **Mountain Bikes** 의 **Internet Sales-Sales Amount** 및 **Reseller Sales-Sales Amount** 측정값을 기반으로 제품 판매의 **Mountain Bikes** 범주에 대한 **Total Sales Amount**측정값이 연도별로 계산됩니다.  
  
8.  값 영역에 **Total GPM**, **Internet GPM**및 **Reseller GPM** 측정값을 추가한 후 결과를 검토합니다.  
  
     다음 그림에 표시된 것처럼 대리점 판매의 매출이익률은 인터넷 판매의 매출이익률보다 훨씬 낮습니다.  
  
     ![대리점 판매를 보여 주는 데이터 창](../../2014/tutorials/media/l6-calculatedmembers-7b.gif "대리점 판매를 보여 주는 데이터 창")  
  
9. 값 영역에 **Total Sales Ratio to All Products**, **Internet Sales Ratio to All Products**및 **Reseller Sales Ratio to All Products** 측정값을 추가합니다.  
  
     모든 제품 대비 산악 자전거 매출 비율은 인터넷 판매에서는 시간에 따라 증가하지만 대리점 판매의 경우는 감소합니다. 또한 모든 제품 대비 산악 자전거 매출 비율은 인터넷 판매의 경우보다 대리점 판매량이 더 낮습니다.  
  
10. 필터를 **Mountain Bikes** 에서 **Bikes**로 변경한 후 결과를 검토합니다.  
  
     여행용 자전거와 도로용 자전거는 밑지고 판매되는 경우가 많으므로 대리점을 통해 판매된 모든 자전거의 매출이익률은 적자입니다.  
  
11. 필터를 **Accessories**로 변경한 후 결과를 검토합니다.  
  
     부속품 판매는 시간에 따라 증가하지만 이러한 판매는 총 판매의 일부에 지나지 않습니다. 또한 부속품 판매의 매출이익률은 자전거 판매 매출이익률보다 높습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [명명된 집합 정의](lesson-6-2-defining-named-sets.md)  
  
## <a name="see-also"></a>참고 항목  
 [계산](multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [다차원 모델의 계산](multidimensional-models/calculations-in-multidimensional-models.md)   
 [계산 멤버 만들기](multidimensional-models/create-calculated-members.md)  
  
  
