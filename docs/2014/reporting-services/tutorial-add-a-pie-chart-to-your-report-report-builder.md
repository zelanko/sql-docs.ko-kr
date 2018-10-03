---
title: '자습서: 보고서에 원형 차트 추가(보고서 작성기) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: eaadf7bf-c312-428a-b214-0a1fbf959c3f
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 12c567f91d526d3ac44485704f7c76fdfa345c11
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48202533"
---
# <a name="tutorial-add-a-pie-chart-to-your-report-report-builder"></a>자습서: 보고서에 원형 차트 추가(보고서 작성기)
  원형 차트와 도넛형 차트는 데이터를 전체에 대한 비율로 표시합니다. 원형 차트는 그룹 간의 비교에 가장 일반적으로 사용됩니다. 원형 및 도넛형 차트는 피라미드형 및 깔때기형 차트와 마찬가지로 셰이프 차트라고 하는 차트 그룹으로 이루어집니다. 셰이프 차트에는 축이 없습니다. 셰이프 차트에 숫자 필드를 배치하면 차트에서 각각의 값이 전체 합계에 대해 차지하는 비율이 계산됩니다.  
  
 원형 차트에 데이터 요소가 너무 많으면 데이터 요소 레이블이 복잡해져서 가독성이 떨어질 수 있습니다. 이런 경우에는 꺾은선형 차트를 사용하는 것이 좋습니다. 원형 차트는 데이터를 몇 개의 데이터 요소로 집계한 후에만 사용하는 것이 좋습니다.  
  
 다음 그림에서는 만들려는 원형 차트를 보여 줍니다.  
  
 ![rs_TutorialPieChartConcave](../../2014/tutorials/media/rs-tutorialpiechartconcave.gif "rs_TutorialPieChartConcave")  
  
##  <a name="BackToTop"></a> 학습할 내용  
 이 자습서에서는 다음 작업 방법을 배웁니다.  
  
1.  [차트 마법사에서 원형 차트 만들기](#Chart)  
  
2.  [차트 종류 선택](#ChartType)  
  
3.  [각 조각에 백분율 표시](#Percentages)  
  
4.  [작은 조각을 한 조각으로 결합](#CombineSlices)  
  
5.  [그리기 효과 사용자 지정](#DrawingEffect)  
  
6.  [보고서 제목 추가](#Title)  
  
7.  [보고서 저장](#Save)  
  
> [!NOTE]  
>  이 자습서에서 마법사의 단계는 두 개의 절차로 통합됩니다. 보고서 서버를 찾고 데이터 원본을 추가하고 데이터 집합을 추가하는 방법에 대한 단계별 지침은 이 시리즈의 첫 번째 자습서인 [자습서: 기본 테이블 보고서 만들기&#40;보고서 작성기&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)를 참조하세요.  
  
 이 자습서에 소요되는 예상 시간: 10분  
  
## <a name="requirements"></a>요구 사항  
 요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/report-builder-tutorials.md)을 참조하세요.  
  
##  <a name="Chart"></a> 1. 차트 마법사에서 원형 차트 만들기  
 시작 대화 상자에서 차트 마법사를 사용하여 포함된 데이터 집합을 만들고, 공유 데이터 원본을 선택하고, 원형 차트를 만듭니다.  
  
> [!NOTE]  
>  이 자습서의 쿼리에는 데이터 값이 포함되어 있으므로 외부 데이터 원본이 필요하지 않습니다. 따라서 쿼리가 상당히 길어집니다. 비즈니스 환경에서는 쿼리에 데이터가 포함되지 않을 것입니다. 이 자습서의 쿼리는 학습용으로만 제공됩니다.  
  
#### <a name="to-create-a-new-chart-report"></a>새 차트 보고서를 만들려면  
  
1.  **시작**을 클릭하고 **프로그램**, **Microsoft SQL Server 2012 보고서 작성기**를 차례로 가리킨 다음 **보고서 작성기**를 클릭합니다.  
  
     시작 대화 상자가 나타납니다.  
  
    > [!NOTE]  
    >  시작 대화 상자가 나타나지 않으면 보고서 작성기 단추에서 클릭 **새로 만들기**합니다.  
  
2.  왼쪽 창에 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **차트 마법사**를 클릭합니다.  
  
4.  **데이터 집합 선택** 페이지에서 **데이터 집합 만들기**를 클릭하고 **다음**을 클릭합니다.  
  
5.  **데이터 원본에 대한 연결 선택** 페이지에서 기존 데이터 원본을 선택하거나 보고서 서버를 찾아 데이터 원본을 선택하고 **다음**을 클릭합니다. 사용자 이름과 암호를 입력해야 할 수 있습니다.  
  
    > [!NOTE]  
    >  적절한 권한만 가지고 있으면 선택하는 데이터 원본은 중요하지 않습니다. 데이터를 데이터 원본에서 가져오는 것은 아니기 때문입니다. 자세한 내용은 [데이터에 연결하는 다른 방법&#40;보고서 작성기&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)를 참조하세요.  
  
6.  **쿼리 디자인** 페이지에서 **텍스트로 편집**을 클릭합니다.  
  
7.  쿼리 창에 다음 쿼리를 붙여 넣습니다.  
  
    ```  
    SELECT 'Advanced Digital Camera' AS Product, CAST(254995.21 AS money) AS Sales  
    UNION SELECT 'Slim Digital Camera' AS Product, CAST(164499.04 AS money) AS Sales  
    UNION SELECT 'SLR Digital Camera' AS Product, CAST(782176.79 AS money) AS Sales  
    UNION SELECT 'Lens Adapter' AS Product, CAST(36333.08 AS money) AS Sales  
    UNION SELECT 'Macro Zoom Lens' AS Product, CAST(40199.3 AS money) AS Sales  
    UNION SELECT 'USB Cable' AS Product, CAST(53245.5 AS money) AS Sales  
    UNION SELECT 'Independent Filmmaker Camcorder' AS Product, CAST(452288.0 AS money) AS Sales  
    UNION SELECT 'Full Frame Digital Camera' AS Product, CAST(247250.85 AS money) AS Sales  
    ```  
  
8.  (옵션) 실행 단추(**!**)를 클릭하여 차트의 기반으로 사용될 데이터를 확인합니다.  
  
9. **다음**을 클릭합니다.  
  
##  <a name="ChartType"></a> 2. 차트 종류 선택  
 미리 정의된 다양한 차트 종류 중에서 선택할 수 있습니다.  
  
#### <a name="to-add-a-pie-chart"></a>원형 차트를 추가하려면  
  
1.  에 **차트 종류 선택** 페이지에서 **원형**를 클릭 하 고 **다음**합니다. **차트 필드 정렬** 페이지가 열립니다.  
  
     **차트 필드 정렬** 페이지에서 Product 필드를 **범주** 창으로 끌어옵니다. 범주는 원형 차트의 조각 수를 정의합니다. 이 예제에서는 각 제품에 대해 하나씩 총 8개의 조각이 사용됩니다.  
  
2.  Sales 필드를 **값** 창으로 끌어옵니다. Sales는 하위 범주의 판매액을 나타냅니다. 차트에 각 제품의 집계가 표시되기 때문에 **값** 창에는 `[Sum(Sales)]` 이 표시됩니다.  
  
3.  **다음**을 클릭합니다.  
  
4.  에 **스타일 선택** 페이지의 스타일 창에서 스타일을 선택 합니다.  
  
     스타일은 글꼴 스타일, 색 집합 및 테두리 스타일을 지정합니다. 스타일을 선택하면 미리 보기 창에 해당 스타일이 적용된 예제 차트가 표시됩니다.  
  
5.  **마침**을 클릭합니다.  
  
     디자인 화면에 차트가 추가됩니다.  
  
6.  차트를 클릭하여 차트 핸들을 표시합니다. 차트의 오른쪽 아래 모퉁이를 끌어 차트의 크기를 늘립니다. 보고서 디자인 화면이 차트 크기에 맞게 늘어납니다.  
  
7.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 각 제품에 대해 하나씩 총 8개 조각으로 구성된 원형 차트가 보고서에 표시됩니다. 각 조각의 크기는 해당 제품의 판매량을 나타냅니다. 전체 조각 중 3개는 폭이 좁습니다.  
  
##  <a name="Percentages"></a> 3. 각 조각에 백분율 표시  
 원형 차트의 각 조각에 원형 전체에 대한 해당 조각의 백분율을 표시할 수 있습니다.  
  
#### <a name="to-display-percentages-in-each-slice-of-the-pie-chart"></a>원형 차트의 각 조각에 백분율을 표시하려면  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  원형 차트를 마우스 오른쪽 단추로 클릭하고 **데이터 레이블 표시**를 클릭합니다. 차트에 데이터 레이블이 나타납니다.  
  
3.  레이블을 마우스 오른쪽 단추로 누른 **계열 레이블 속성**합니다.  
  
4.  데이터 레이블, 드롭다운 목록 상자에서 선택 **#percent{p0}"** 합니다.  
  
     값을 백분율로 표시하려면 UseValueAsLabel 속성이 false여야 합니다. **동작 확인** 대화 상자에서 이 값을 설정할지 묻는 메시지가 표시되면 **예**를 클릭합니다.  
  
5.  (선택 사항) 소수 자릿수 레이블을 지정 하려면 입력 `#PERCENT{Pn}` 여기서 *n* 표시할 소수 자릿수입니다. 예를 들어 소수 자리를 표시 하려면 입력 `#PERCENT{P0}`합니다.  
  
    > [!NOTE]  
    >  **계열 레이블 속성** 대화 상자의 **숫자 형식** 은 백분율 서식을 지정하는 데 영향을 주지 않고 레이블의 서식을 백분율로 지정하기만 하며 각 조각이 원형 차트에서 나타내는 백분율을 계산하지는 않습니다.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 각 원형 조각이 전체에서 나타내는 백분율이 보고서에 표시됩니다.  
  
##  <a name="CombineSlices"></a> 4. 작은 조각들을 하나의 조각으로 결합  
 원형 차트의 조각 중 3개는 폭이 좁습니다. 여러 개의 작은 조각을 해당 조각 모두를 나타내는 하나의 큰 조각으로 결합할 수 있습니다.  
  
#### <a name="to-combine-any-slices-on-the-pie-chart-smaller-than-5-percent-into-one-slice"></a>원형 차트에서 5% 미만의 조각을 하나의 조각으로 결합하려면  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  에 **보기** 탭의 **표시/숨기기** 그룹을 선택 **속성**합니다.  
  
3.  디자인 화면에서 원형 차트의 조각을 아무 것이나 클릭합니다. 계열의 속성이 속성 창에 표시됩니다.  
  
4.  **일반** 섹션에서 **CustomAttributes** 노드를 확장합니다.  
  
5.  **CollectedStyle** 속성을 **SingleSlice**로 설정합니다.  
  
6.  **CollectedThreshold** 속성이 5로 설정되었는지 확인합니다.  
  
7.  **CollectedThresholdUsePercent** 속성이 **True**로 설정되었는지 확인합니다.  
  
8.  리본 메뉴에 **홈** 탭을 클릭 **실행** 보고서를 미리 보려면.  
  
 이제 범례에 "기타"라는 범주가 나타납니다. 새 원형 조각은 5% 미만인 모든 조각을 전체 원형의 6%를 차지하는 조각 하나로 결합합니다.  
  
##  <a name="DrawingEffect"></a> 5. 그리기 효과 사용자 지정  
 차트 마법사에서 원형 차트의 기본 스타일은 오목 그리기 효과가 적용된 바다입니다. 마법사를 실행한 후 이러한 스타일을 변경할 수 있습니다.  
  
#### <a name="to-add-a-drawing-effect-to-the-pie-chart"></a>원형 차트에 그리기 효과를 추가하려면  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  속성 창이 열려 있지 않으면를 하는 경우는 **뷰** 탭을 선택 **속성**합니다.  
  
3.  원형 차트를 두 번 클릭합니다. 원형 차트의 계열 속성이 속성 창에 표시됩니다.  
  
4.  속성 창에서 **CustomAttributes** 노드를 확장합니다.  
  
5.  설정 된 **PieDrawingStyle** 하 **SoftEdge**합니다.  
  
    > [!NOTE]  
    >  그리기 효과와 3D 효과 옵션은 함께 사용할 수 없습니다. 차트에 3 차원 효과 적용 **PieDrawingStyle** 를 속성 창에서 사용할 수 없습니다.  
  
6.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 다음 그림에서는 부드러운 가장자리 효과가 적용된 원형 차트를 보여 줍니다.  
  
 ![rs_TutorialPieChartSoftEdge](../../2014/tutorials/media/rs-tutorialpiechartsoftedge.gif "rs_TutorialPieChartSoftEdge")  
  
##  <a name="Title"></a> 6. 보고서 제목 추가  
  
#### <a name="to-add-a-report-title"></a>보고서 제목을 추가하려면  
  
1.  디자인 화면에서 **제목을 추가하려면 클릭하십시오.** 를 클릭합니다.  
  
2.  **Camera and Camcorder Sales**를 입력하고 Enter 키를 누른 다음 **As a Percentage of Total Sales**를 입력합니다. 그러면 다음과 같이 표시됩니다.  
  
     **Camera and Camcorder Sales**  
  
     **As a Percentage of Total Sales**  
  
3.  선택 **Camera and Camcorder Sales**, 클릭는 **굵게** 에서 단추를 **글꼴** 섹션을 **홈** 리본 메뉴의 탭.  
  
4.  선택 **으로 a Percentage of Total Sales**, 및는 **글꼴** 섹션에서 합니다 **홈** 탭, 글꼴 크기를 설정 합니다 **10**합니다.  
  
5.  (선택 사항) 제목 입력란을 두 줄 텍스트를 포함하도록 크게 만들어야 할 수 있습니다.  
  
     이 제목은 보고서 맨 위에 나타납니다. 페이지 머리글이 정의되지 않았을 경우 보고서 본문의 맨 위에 있는 항목은 보고서 머리글에 해당합니다.  
  
6.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
##  <a name="Save"></a> 7. 보고서 저장  
  
#### <a name="to-save-the-report"></a>보고서를 저장하려면  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  보고서 작성기 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
3.  **이름**에 **Sales Pie Chart**를 입력합니다.  
  
4.  **저장**을 클릭합니다.  
  
 보고서가 보고서 서버에 저장됩니다.  
  
## <a name="next-steps"></a>다음 단계  
 보고서에 원형 차트 추가 자습서를 성공적으로 완료했습니다. 차트에 대한 자세한 내용은 [차트&#40;보고서 작성기 및 SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) 및 [스파크라인 및 데이터 막대&#40;보고서 작성기 및 SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [자습서 &#40;보고서 작성기&#41;](report-builder-tutorials.md)   
 [SQL Server 2014의 보고서 작성기](report-builder/report-builder-in-sql-server-2016.md)  
  
  
