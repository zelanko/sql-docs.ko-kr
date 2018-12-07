---
title: '자습서: 보고서에 KPI 추가(보고서 작성기) | Microsoft Docs'
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 1bf77859-0b33-4f40-abaf-ebeeb6ebb1f8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ee2333bc6d369bbc9908198d8cfa2fa18ce23065
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52712644"
---
# <a name="tutorial-adding-a-kpi-to-your-report-report-builder"></a>자습서: 보고서에 KPI 추가(보고서 작성기)
이 [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)] 자습서에서는 페이지가 매겨진 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 보고서에 KPI(핵심 성과 지표)를 추가합니다.  

KPI는 비즈니스 측면에서 중요한 측정 가능한 값입니다. 이 시나리오에서 제품 하위 범주별 판매 요약이 KPI입니다. KPI의 현재 상태는 색, 계기 및 표시기를 사용하여 표시됩니다.
  
만들려는 보고서는 다음 그림과 유사합니다.  
  
![report-builder-kpi-report](../reporting-services/media/report-builder-kpi-report.png)
    
> [!NOTE]  
> 이 자습서에서 마법사의 단계는 두 개의 절차로 통합됩니다. 하나는 데이터 집합을 만드는 절차이고 다른 하나는 테이블을 만드는 절차입니다. 보고서 서버를 찾고, 데이터 원본을 선택하고, 데이터 집합을 만들고, 마법사를 실행하는 방법에 대한 단계별 지침은 이 시리즈의 첫 번째 자습서인 [자습서: 기본 테이블 보고서 만들기&#40;보고서 작성기&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)를 참조하세요.  
  
이 자습서에 소요되는 예상 시간: 15분  
  
## <a name="requirements"></a>요구 사항  
요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)을 참조하세요.  
  
## <a name="Table"></a>1. 테이블 또는 행렬 마법사에서 테이블 보고서 및 데이터 집합 만들기  
이 섹션에서는 공유 데이터 원본을 선택하고, 포함된 데이터 집합을 만들고, 테이블에 데이터를 표시합니다.  
 
### <a name="to-create-a-table-with-an-embedded-dataset"></a>포함된 데이터 집합으로 테이블을 만들려면  
  
1.  컴퓨터,[웹 포털 또는 SharePoint 통합 모드에서](../reporting-services/report-builder/start-report-builder.md) 보고서 작성기를 시작 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 합니다.  
  
    **새 보고서 또는 데이터 집합** 대화 상자가 열립니다.  
  
    **새 보고서 또는 데이터 집합** 대화 상자가 표시되지 않는 경우 **파일** 메뉴 > **새로 만들기**를 클릭합니다.  
  
2.  왼쪽 창에 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **테이블 또는 행렬 마법사**를 클릭합니다.  
  
4.  **데이터 집합 선택** 페이지에서 **데이터 집합 만들기**를 클릭합니다.  
  
5.  **다음**을 클릭합니다.  
  
6.  **데이터 원본에 대한 연결 선택** 페이지에서 기존 데이터 원본을 선택하거나 보고서 서버를 찾아 데이터 원본을 선택합니다. 데이터 원본을 사용할 수 없거나 보고서 서버에 대한 액세스 권한이 없는 경우 포함된 데이터 원본을 대신 사용할 수 있습니다. 자세한 내용은 [자습서: 기본 테이블 보고서 만들기&#40;보고서 작성기&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)를 참조하세요.  
  
7.  **다음**을 클릭합니다.  
  
8.  **쿼리 디자인** 페이지에서 **텍스트로 편집**을 클릭합니다.  
  
9. 쿼리 창에 다음 쿼리를 복사하여 붙여 넣습니다.  

    > [!NOTE]  
    > 이 자습서의 쿼리에는 데이터 값이 포함되어 있으므로 외부 데이터 원본이 필요하지 않습니다. 따라서 쿼리가 상당히 길어집니다. 비즈니스 환경에서는 쿼리에 데이터가 포함되지 않을 것입니다. 이 자습서의 쿼리는 학습용으로만 제공됩니다.  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2015-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
10. 쿼리 디자이너 도구 모음에서 실행(**!**)을 클릭합니다.

11. **다음**을 클릭합니다.  
  
## <a name="CompleteWizard"></a>2. 마법사에서 데이터 구성 및 레이아웃 선택  
테이블 또는 행렬 마법사는 데이터를 표시할 시작 디자인을 제공합니다. 이 마법사의 미리 보기 창에서는 테이블 또는 행렬 디자인을 완료하기 전에 데이터 그룹화의 결과를 시각화할 수 있습니다.  
  
### <a name="to-organize-data-into-groups-and-choose-a-layout"></a>데이터를 그룹으로 구성하고 레이아웃을 선택하려면 
  
1.  필드 정렬 페이지에서 **값**에 Product를 끌어옵니다.  
  
2.  **값** 의 Product 아래에 Quantity를 끌어옵니다.  
  
    Quantity는 숫자 필드를 요약하기 위한 기본 함수인 Sum 함수를 사용하여 요약됩니다.  
  
3.  **값** 의 Quantity 아래에 Sales를 끌어옵니다.  
  
    1, 2, 3단계에서는 테이블에 표시할 데이터를 지정했습니다.  
  
4.  **행 그룹**에 SalesDate를 끌어옵니다.  
  
5.  **행 그룹** 의 SalesDate 아래에 Subcategory를 끌어옵니다.  
  
    4, 5단계에서는 필드 값을 먼저 날짜 기준으로 정렬한 다음 해당 날짜의 모든 판매를 기준으로 정렬했습니다.  
  
6.  **다음**을 클릭합니다.  
  
    보고서를 실행하면 테이블에 각 날짜, 각 날짜의 모든 주문, 각 주문의 모든 제품, 수량 및 판매 합계가 표시됩니다.  
  
7.  레이아웃 선택 페이지의 **옵션**에서 **부분합 및 총합계 표시** 가 선택되어 있는지 확인합니다.  
  
8.  **블록형, 부분합 하단 표시** 가 선택되어 있는지 확인합니다.  
  
9. **그룹 확장/축소**옵션을 선택 취소합니다.  
  
    이 자습서에서 만든 보고서에는 부모 그룹 계층을 확장하여 자식 그룹 행 및 정보 행을 표시하는 데 사용할 수 있는 드릴다운 기능이 사용되지 않습니다.  
  
10. **다음**을 클릭합니다.  
  
11. **마침**을 클릭합니다.  
  
      디자인 화면에 테이블이 추가됩니다. 이 테이블에는 열 5개와 행 5개가 있습니다. 행 그룹 창에는 SalesDate, Subcategory 및 Details라는 3개의 행 그룹이 표시됩니다. 세부 데이터는 모두 데이터 집합 쿼리로 검색된 데이터입니다. 열 그룹 창은 비어 있습니다.  
      
      ![report-builder-kpi-row-groups](../reporting-services/media/report-builder-kpi-row-groups.png)
  
12. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
특정 날짜에 판매되는 각 제품에 대한 제품 이름, 판매 수량 및 판매 합계가 테이블에 표시됩니다. 이 데이터는 먼저 판매 날짜를 기준으로 정렬된 다음 하위 범주를 기준으로 정렬됩니다. 

![report-builder-kpi-basic-table](../reporting-services/media/report-builder-kpi-basic-table.png)
    
### <a name="format-dates-and-currency"></a>날짜 및 통화 형식 지정
열의 너비를 늘리고 날짜 및 통화 형식을 설정해 보겠습니다.

1. **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.

2. Product 이름은 더 많은 공간을 사용할 수 있습니다. Product 열 너비를 늘리기 위해 전체 테이블을 선택하고 Product 열 맨 위에 있는 열 핸들의 오른쪽 가장자리를 끕니다.

3. Ctrl 키를 누른 상태로 [Sum(Sales)]이 들어 있는 4개의 셀을 선택합니다.

4. **홈** 탭 > **숫자** > **통화**를 선택합니다. 셀이 변경되어 형식 지정된 통화가 표시됩니다.

   국가별 설정이 영어(미국)인 경우 기본 예제 텍스트는 [$12,345.00]입니다. 예제 통화 값이 표시되지 않는 경우 **숫자** 그룹에서 **자리 표시자 스타일** > **샘플 값**을 클릭합니다.
    
    ![report-builder-placeholder-value-button](../reporting-services/media/report-builder-placeholder-value-button.png)

5. (옵션) **홈** 탭에 있는 **숫자** 그룹에서 **소수 자릿수 줄이기** 단추를 두 번 클릭하여 센트가 표시되지 않는 달러 숫자를 표시합니다.

6. [SalesDate]가 들어 있는 셀을 클릭합니다.

6. **숫자** 그룹 > **날짜**를 선택합니다.

   셀에 예제 날짜 [1/31/2000]이 표시됩니다. 

12. **실행** 을 클릭하여 보고서를 미리 봅니다.  
 
![report-builder-kpi-format-numbers](../reporting-services/media/report-builder-kpi-format-numbers.png)

## <a name="BackgroundColors"></a>3. 배경색을 사용하여 KPI 표시  
배경색을 보고서 실행 시 계산되는 식으로 설정할 수 있습니다.  
  
### <a name="to-display-the-present-state-of-a-kpi-by-using-background-colors"></a>배경색을 사용하여 KPI의 현재 상태를 표시하려면  
  
1.  테이블에서 두 번째 `[Sum(Sales)]` 셀(하위 범주에 대한 매출이 표시되는 부분합 행)을 마우스 오른쪽 단추로 클릭하고 **입력란 속성**을 클릭합니다. 

    **입력란 속성**을 보려면 셀에 있는 텍스트가 아니라 셀을 선택해야 합니다. 
    
    ![report-builder-text-box-properties](../reporting-services/media/report-builder-text-box-properties.png)
  
2.  **채우기** 탭에서 **채우기 색** 옆에 있는 **fx** 단추를 클릭한 다음 **다음에 대한 식 설정: BackgroundColor** 필드에 다음 식을 입력합니다.  
  
    `=IIF(Sum(Fields!Sales.Value) >= 5000 ,"Lime", IIF(Sum(Fields!Sales.Value) < 2500, "Red","Yellow"))`  
  
     이렇게 하면 `[Sum(Sales)]` 의 집계된 합계가 5000보다 크거나 같은 각 셀의 "라임" 녹색으로 변경됩니다. 2500에서 5000 사이의 `[Sum(Sales)]` 값은 "노란색"이고, 2500보다 작은 값은 "빨간색"입니다.  
  
1.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
2.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
하위 범주에 대한 판매가 표시되는 부분합 행에서 셀의 배경색은 판매 합계 값에 따라 빨강, 노랑 또는 녹색으로 표시됩니다.  

![report-builder-kpi-colors](../reporting-services/media/report-builder-kpi-colors.png)
  
## <a name="Gauge"></a>4. 계기를 사용하여 KPI 표시  
계기는 데이터 집합의 단일 값을 표시합니다. 이 자습서에서는 가로 선형 계기를 사용하는데, 이 계기가 작고 테이블 셀 내에서 사용되는 경우에도 모양이 읽기 쉽고 단순하기 때문입니다. 자세한 내용은 [계기&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/gauges-report-builder-and-ssrs.md)를 참조하세요.  
  
### <a name="to-display-the-present-state-of-a-kpi-using-a-gauge"></a>계기를 사용하여 KPI의 현재 상태를 표시하려면  
  
1.  디자인 뷰로 다시 전환합니다.  
  
2.  테이블에서 Sales 열의 열 핸들을 마우스 오른쪽 단추로 클릭 > **열 삽입** > **오른쪽**을 선택합니다. 테이블에 새 열이 추가됩니다.  

    ![report-builder-kpi-insert-column](../reporting-services/media/report-builder-kpi-insert-column.png)
  
3.  열 제목에 **Linear KPI** 를 입력합니다.  
  
4.  **삽입** 탭 > **데이터 시각화** > **계기**에서 테이블 외부 디자인 화면을 클릭합니다.   
  
5.  **계기 유형 선택** 대화 상자에서 첫 번째 선형 계기 유형인 **가로**를 선택합니다.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    디자인 화면에 계기가 추가됩니다.  
  
7.  보고서 데이터 창의 데이터 집합에서 `Sales` 필드를 계기로 끕니다. **계기 데이터** 창이 열립니다.  
  
    `Sales` 필드를 계기에 놓으면 **값** 목록으로 이동하고 기본 제공 Sum 함수를 사용하여 집계됩니다.  
   
    ![report-builder-kpi-drag-sales-field](../reporting-services/media/report-builder-kpi-drag-sales-field.png)
   
9. **계기 데이터** 창에서 **LinearPointer1** > **포인터 속성**옆에 있는 화살표를 클릭합니다.  
  
10. **선형 포인터 속성** 대화 상자 > **포인터 옵션** 탭 > **포인터 형식**에서 **막대**가 선택되어 있는지 확인합니다. 
 
11. **확인**을 클릭합니다.  
  
12. 계기 눈금을 마우스 오른쪽 단추로 클릭하고 **눈금 속성**을 클릭합니다.  
  
13. **선형 눈금 속성** 대화 상자 > **일반** 탭에서 **최대값**을 25000으로 설정합니다.  

    > [!NOTE]  
    > 25000과 같은 상수 대신 식을 사용하여 **최대값** 옵션의 값을 동적으로 계산할 수 있습니다. 이 식은 집계 기능의 집계를 사용하며 `=Max(Sum(Fields!Sales.value), "Tablix1")`식처럼 나타납니다.  

14. **레이블** 탭에서 **눈금 레이블 숨기기**를 선택합니다.

15. **확인**을 클릭합니다.
  
14. 배경색 수식을 추가한 필드 옆에 있는 `Subcategory` 필드에 대한 부분합 판매량을 표시하는 행에서 선형 KPI 열의 두 번째 빈 셀로 테이블 안의 계기를 끕니다.  
  
    > [!NOTE]  
    > 가로 선형 계기가 셀에 맞도록 열 크기를 조정해야 할 수도 있습니다. 열 크기를 조정하려면 테이블을 선택하고 열 핸들을 끕니다. 보고서 디자인 화면의 크기가 테이블에 맞게 조정됩니다.  
  
15. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
    계기에서 녹색 막대의 가로 길이는 KPI 값에 따라 변경됩니다.  
  
![report-builder-linear-kpi](../reporting-services/media/report-builder-linear-kpi.png) 
  
## <a name="Indicator"></a>5. 표시기를 사용하여 KPI 표시  
표시기는 데이터 값을 한 눈에 파악할 수 있는 작고 간단한 계기입니다. 크기와 단순함으로 인해 표시기는 흔히 테이블과 행렬에 사용됩니다. 자세한 내용은 [표시기&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/indicators-report-builder-and-ssrs.md)를 참조하세요.  
  
### <a name="to-display-the-present-state-of-a-kpi-using-an-indicator"></a>표시기를 사용하여 KPI의 현재 상태를 표시하려면  
  
1.  디자인 뷰로 전환합니다.  
  
2.  테이블에서 마지막 절차에서 추가한 선형 KPI 열에 대한 열 핸들을 마우스 오른쪽 단추로 클릭 > **열 삽입** > **오른쪽**을 선택합니다. 테이블에 새 열이 추가됩니다.  
  
3.  열 제목에 **Stoplight KPI** 를 입력합니다.  
  
4.  마지막 절차에서 추가한 선형 계기 옆에 있는 부분합 하위 범주의 셀을 클릭합니다.  
  
5.  **삽입** 탭 > **데이터 시각화**에서 > **표시기**를 두 번 클릭합니다.  
  
6.  **표시기 유형 선택** 대화 상자의 **셰이프**에서 첫 번째 셰이프 유형인 **3색 신호등(테두리 없음)** 을 선택합니다.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    새 Stoplight KPI 열에 있는 셀에 표시기가 추가됩니다.  
  
8.  표시기를 마우스 오른쪽 단추로 클릭하고 **표시기 속성**을 클릭합니다.  
  
9. **값 및 상태** 탭의 **값** 상자에서 **[Sum(Sales)]** 를 선택합니다. 다른 옵션은 변경하지 마세요.  
  
    기본적으로 데이터 영역에서 데이터 동기화가 발생하며 보고서에 있는 테이블 데이터 영역의 이름인 **Tablix1**값이 **동기화 범위** 상자에 나타납니다.  
  
    이 보고서에서는 하위 범주 부분합의 셀에 놓인 표시기의 범위를 변경하여 SalesDate 필드에서 동기화할 수도 있습니다.  
  
11. **확인**을 클릭합니다.

11. **실행** 을 클릭하여 보고서를 미리 봅니다.  

![report-builder-kpi-stoplight](../reporting-services/media/report-builder-kpi-stoplight.png)
  
## <a name="Title"></a>6. 보고서 제목 추가  
보고서 제목은 보고서 맨 위에 나타납니다. 보고서 제목을 보고서 머리글에 배치하거나, 보고서 머리글이 사용되지 않을 경우 보고서 본문의 맨 위에 있는 입력란에 배치할 수 있습니다. 이 섹션에서는 보고서 본문의 맨 위에 자동으로 배치되는 입력란을 사용합니다.  
  
글꼴 스타일, 크기 및 색을 텍스트의 각 문자나 구 단위로 다르게 적용하여 텍스트를 더 보기 좋게 꾸밀 수 있습니다. 자세한 내용은 [입력란의 텍스트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)을 참조하세요.  
  
### <a name="to-add-a-report-title"></a>보고서 제목을 추가하려면  
  
1.  디자인 화면에서 **제목을 추가하려면 클릭하십시오.** 를 클릭합니다.  
  
2.  **Product Sales KPIs**를 입력한 다음 입력란 바깥쪽을 클릭합니다.  
  
3.  필요에 따라 **Product Sales KPI**가 들어 있는 입력란을 마우스 오른쪽 단추로 클릭하고 **입력란 속성**을 클릭한 다음 글꼴 탭에서 다른 글꼴 스타일, 크기 및 색을 선택합니다.  
  
4.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
## <a name="Save"></a>7. 보고서 저장  
보고서 서버 또는 컴퓨터에 보고서를 저장합니다. 보고서를 보고서 서버에 저장하지 않을 경우 보고서 파트 및 하위 보고서와 같은 여러 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능을 사용할 수 없습니다.  
  
### <a name="to-save-the-report-on-a-report-server"></a>보고서를 보고서 서버에 저장하려면  
  
1.  **보고서 작성기** 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
2.  **최근에 사용한 사이트 및 서버**를 클릭합니다.  
  
3.  보고서를 저장할 수 있는 권한을 가진 보고서 서버의 이름을 선택하거나 입력합니다.  
  
    "보고서 서버에 연결하는 중"이라는 메시지가 나타납니다. 연결되면 보고서 서버 관리자가 보고서의 기본 위치로 지정한 보고서 폴더의 내용이 표시됩니다.  
  
4.  **이름**에서 기본 이름을 **Product Sales KPI**로 바꿉니다.  
  
5.  **저장**을 클릭합니다.  
  
보고서가 보고서 서버에 저장됩니다. 연결된 보고서 서버의 이름이 창 아래쪽에 있는 상태 표시줄에 나타납니다.  
  
### <a name="to-save-the-report-on-your-computer"></a>컴퓨터에 보고서를 저장하려면  
  
1.  **보고서 작성기** 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
2.  **바탕 화면**, **내 문서**또는 **내 컴퓨터**를 클릭하여 보고서를 저장할 폴더를 찾습니다.  
  
> [!NOTE]  
> 보고서 서버에 액세스할 수 없는 경우 **바탕 화면**, **내 문서**또는 **내 컴퓨터** 를 클릭하고 보고서를 컴퓨터에 저장합니다.  
  
1.  **이름**에서 기본 이름을 **Product Sales KPI**로 바꿉니다.  
  
2.  **저장**을 클릭합니다.  
  
## <a name="next-steps"></a>Next Steps  
보고서에 KPI 추가 자습서를 성공적으로 완료했습니다. 참조 항목:
*  [계기](../reporting-services/report-design/gauges-report-builder-and-ssrs.md)
* [표시기](../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>참고 항목  
* [보고서 작성기 자습서](../reporting-services/report-builder-tutorials.md)
* [SQL Server의 보고서 작성기](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

