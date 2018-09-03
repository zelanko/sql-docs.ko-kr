---
title: '자습서: 보고서에 원형 차트 추가(보고서 작성기) | Microsoft Docs'
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.suite: pro-bi
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: eaadf7bf-c312-428a-b214-0a1fbf959c3f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 390297f03dfc5e7bc8c6892142dce67704106504
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43276332"
---
# <a name="tutorial-add-a-pie-chart-to-your-report-report-builder"></a>자습서: 보고서에 원형 차트 추가(보고서 작성기)
이 자습서에서는 페이지가 매겨진 Reporting Services 보고서에 원형 차트를 만듭니다. 백분율을 추가하고 작은 조각을 한 조각으로 결합합니다.

원형 차트와 도넛형 차트는 데이터를 전체에 대한 비율로 표시합니다. 두 차트에는 축이 없습니다. 원형 차트에 숫자 필드를 추가하면 차트에서 전체에 대한 각 값의 백분율을 계산합니다.  

다음 그림에서는 만들어질 원형 차트를 보여 줍니다. 
 
![report-builder-pie-chart-final](../reporting-services/media/report-builder-pie-chart-final.png)
  
원형 차트에 데이터 요소가 너무 많으면 데이터 요소 레이블이 복잡해져서 가독성이 떨어질 수 있습니다. 이 경우 여러 개의 작은 조각을 하나의 큰 조각으로 결합하는 것이 좋습니다. 데이터를 몇 개의 데이터 요소로 집계하면 원형 차트를 더 쉽게 읽을 수 있습니다.  
 
> [!NOTE]  
> 이 자습서에서 마법사의 단계는 두 개의 절차로 통합됩니다. 보고서 서버를 찾고 데이터 원본을 추가하고 데이터 집합을 추가하는 방법에 대한 단계별 지침은 이 시리즈의 첫 번째 자습서인 [자습서: 기본 테이블 보고서 만들기&#40;보고서 작성기&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)를 참조하세요.  
  
이 자습서에 소요되는 예상 시간: 10분  
  
## <a name="requirements"></a>요구 사항  
요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)을 참조하세요.  
  
## <a name="Chart"></a>1. 차트 마법사에서 원형 차트 만들기  
이 섹션에서는 차트 마법사를 사용하여 포함된 데이터 집합을 만들고, 공유 데이터 원본을 선택하고, 원형 차트를 만듭니다.  

  
1.  컴퓨터,[웹 포털 또는 SharePoint 통합 모드에서](../reporting-services/report-builder/start-report-builder.md) 보고서 작성기를 시작 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 합니다.  
  
    **새 보고서 또는 데이터 집합** 대화 상자가 열립니다.  
  
    **새 보고서 또는 데이터 집합** 대화 상자가 표시되지 않는 경우 **파일** 메뉴 > **새로 만들기**를 클릭합니다.  
  
2.  왼쪽 창에 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **차트 마법사**를 클릭합니다.  
  
4.  **데이터 집합 선택** 페이지에서 **데이터 집합 만들기**를 클릭하고 **다음**을 클릭합니다.  
  
5.  **데이터 원본에 대한 연결 선택** 페이지에서 기존 데이터 원본을 선택하거나 보고서 서버를 찾아 데이터 원본을 선택하고 **다음**을 클릭합니다. 사용자 이름과 암호를 입력해야 할 수 있습니다.  
  
    > [!NOTE]  
    > 적절한 권한만 가지고 있으면 선택하는 데이터 원본은 중요하지 않습니다. 데이터를 데이터 원본에서 가져오는 것은 아니기 때문입니다. 자세한 내용은 [데이터에 연결하는 다른 방법&#40;보고서 작성기&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)를 참조하세요.  
  
6.  **쿼리 디자인** 페이지에서 **텍스트로 편집**을 클릭합니다.  
  
7.  쿼리 창에 다음 쿼리를 붙여 넣습니다.  

    > [!NOTE]  
    > 이 자습서의 쿼리에는 데이터 값이 포함되어 있으므로 외부 데이터 원본이 필요하지 않습니다. 따라서 쿼리가 길어집니다. 비즈니스 환경에서는 쿼리에 데이터가 포함되지 않을 것입니다. 이 자습서의 쿼리는 학습용으로만 제공됩니다.  
  
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
  
## <a name="ChartType"></a>2. 차트 종류 선택  
미리 정의된 다양한 차트 종류 중에서 선택할 수 있습니다.  

  
1.  **차트 종류 선택** 페이지에서 **원형**을 클릭하고 **다음**을 클릭합니다. **차트 필드 정렬** 페이지가 열립니다.  
  
    **차트 필드 정렬** 페이지에서 Product 필드를 **범주** 창으로 끌어옵니다. 범주는 원형 차트의 조각 수를 정의합니다. 이 예제에서는 각 제품에 대해 하나씩 총 8개의 조각이 사용됩니다.  
  
2.  Sales 필드를 **값** 창으로 끌어옵니다. Sales는 하위 범주의 판매액을 나타냅니다. 차트에 각 제품의 집계가 표시되기 때문에 **값** 창에는 `[Sum(Sales)]` 이 표시됩니다.  
  
3.  **다음** 을 클릭하여 미리 보기를 확인합니다.  
  
5.  **마침**을 클릭합니다.  
  
    디자인 화면에 차트가 추가됩니다. 원형 차트의 실제 값은 표시되지 않고 차트 모양을 파악할 수 있도록 제품 1, 제품 2 등이 표시됩니다.  
    
    ![report-builder-pie-chart-first-design](../reporting-services/media/report-builder-pie-chart-first-design.png)
  
6.  차트를 클릭하여 차트 핸들을 표시합니다. 차트의 오른쪽 아래를 끌어 차트를 확장합니다. 보고서 디자인 화면도 차트 크기에 맞게 확장됩니다.  
  
7.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
각 제품에 대해 하나씩 총 8개 조각으로 구성된 원형 차트가 보고서에 표시됩니다. 이제 실제 제품이 표시되고, 각 조각의 크기는 해당 제품의 판매량을 나타냅니다. 전체 조각 중 3개는 폭이 좁습니다.  

![report-builder-pie-chart-first-preview](../reporting-services/media/report-builder-pie-chart-first-preview.png)
  
## <a name="Percentages"></a>3. 각 조각에 백분율 표시  
원형 차트의 각 조각에 원형 전체에 대한 해당 조각의 백분율을 표시할 수 있습니다.  

  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  원형 차트를 마우스 오른쪽 단추로 클릭하고 **데이터 레이블 표시**를 클릭합니다. 차트에 데이터 레이블이 나타납니다.  
  
3.  레이블을 마우스 오른쪽 단추로 클릭하고 **계열 레이블 속성**을 클릭합니다.  
  
4.  **레이블 데이터** 상자에서 **#PERCENT**를 선택합니다.  
    
5.  (옵션) 레이블을 표시할 때 사용할 소수 자릿수를 지정하려면 **#PERCENT****레이블 데이터** 상자에 **{Pn}** 을 입력합니다. 여기서 *n*은 표시할 소수 자릿수입니다. 예를 들어 소수 자릿수를 표시하지 않으려면 **#PERCENT{P0}** 을 입력합니다.  

6.  값을 백분율로 표시하려면 UseValueAsLabel 속성이 false여야 합니다. **동작 확인** 대화 상자에서 이 값을 설정할지 묻는 메시지가 표시되면 **예**를 클릭합니다.  
  
    > [!NOTE]  
    > **계열 레이블 속성** 대화 상자의 **숫자 형식** 은 백분율 서식을 지정하는 데 영향을 주지 않고 레이블의 서식을 백분율로 지정하기만 하며 각 조각이 원형 차트에서 나타내는 백분율을 계산하지는 않습니다.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
각 원형 조각이 전체에서 나타내는 백분율이 보고서에 표시됩니다.  

![report-builder-pie-chart-preview-percents](../reporting-services/media/report-builder-pie-chart-preview-percents.png)
  
## <a name="CombineSlices"></a>4. 작은 조각들을 하나의 조각으로 결합  
원형 차트의 조각 중 3개는 폭이 좁습니다. 여러 개의 작은 조각을 세 조각 모두를 나타내는 하나의 큰 "기타" 조각으로 결합할 수 있습니다.  

1.  보고서 디자인 뷰로 전환합니다.  
  
2.  속성 창이 표시되지 않는 경우 **보기** 탭 > **표시/숨기기** 그룹 > **속성**을 선택합니다.  
  
3.  디자인 화면에서 원형 차트의 조각을 아무 것이나 클릭합니다. 계열의 속성이 속성 창에 표시됩니다.  
  
4.  **일반** 섹션에서 **CustomAttributes** 노드를 확장합니다.  
  
5.  **CollectedStyle** 속성을 **SingleSlice**로 설정합니다.  

    ![report-builder-pie-chart-single-slice-property](../reporting-services/media/report-builder-pie-chart-single-slice-property.png)
 
6.  **CollectedThreshold** 속성이 5로 설정되었는지 확인합니다.  
  
7.  **CollectedThresholdUsePercent** 속성이 **True**로 설정되었는지 확인합니다.  
  
8.  **홈** 탭에서 **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
이제 범례에 "기타" 범주가 표시됩니다. 새 원형 조각은 5% 미만인 모든 조각을 전체 원형의 6%를 차지하는 조각 하나로 결합합니다.  

![report-builder-pie-chart-start-at-90](../reporting-services/media/report-builder-pie-chart-start-at-90.png)
 
## <a name="DrawingEffect"></a>5. 원형 차트 값을 위쪽에서 시작하기 

기본적으로 원형 차트에서는 데이터 집합의 첫 번째 값이 원형의 위쪽으로부터 90도가 되는 지점에서 시작됩니다. 이전 섹션의 원형 차트에서 이를 확인할 수 있습니다.

이 섹션에서는 첫 번째 값이 위쪽에서 시작하도록 설정합니다.

1.  보고서 디자인 뷰로 전환합니다.  

2. 원형 자체를 선택합니다.

3. 속성 창의 **사용자 지정 특성**에서 PieStartAngle을 **0** 에서 **270**으로 변경합니다.

4. **실행** 을 클릭하여 보고서를 미리 봅니다.

이제 원형 차트 조각이 사전순으로 표시되고, 위쪽에서 시작하여 "기타" 조각으로 끝납니다.

![report-builder-pie-chart-start-at-top](../reporting-services/media/report-builder-pie-chart-start-at-top.png)
  
## <a name="Title"></a>6. 보고서 제목 추가  
  
원형 차트가 보고서의 유일한 시각화 요소이므로 차트에는 제목이 필요하지 않습니다. 보고서 제목만 있으면 됩니다.
  
1.  차트에서 차트 제목 상자를 선택하고 Delete 키를 누릅니다.

2. 디자인 화면에서 **제목을 추가하려면 클릭하십시오.** 를 클릭합니다.  
  
2.  **Camera and Camcorder Sales**를 입력하고 Enter 키를 누른 다음 **As a Percentage of Total Sales**를 입력합니다. 그러면 다음과 같이 표시됩니다.  
  
    **Camera and Camcorder Sales**  
  
    **As a Percentage of Total Sales**  
  
3.  **Camera and Camcorder Sales**를 선택하고 **홈** 탭 > **글꼴** 섹션에서 > **굵게**를 클릭합니다.  
  
4.  **As a Percentage of Total Sales**를 선택하고 **홈** 탭 > **글꼴** 섹션에서 > 글꼴 크기를 **10**으로 설정합니다.  
  
5.  (선택 사항) 제목 입력란을 두 줄 텍스트를 포함하도록 크게 만들어야 할 수 있습니다.  
  
    이 제목은 보고서 맨 위에 나타납니다. 페이지 머리글이 정의되지 않았을 경우 보고서 본문의 맨 위에 있는 항목은 보고서 머리글에 해당합니다.  
  
6.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
## <a name="Save"></a>7. 보고서 저장  
  
### <a name="to-save-the-report"></a>보고서를 저장하려면  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  **파일** 메뉴에서 **저장**을 클릭합니다.  
  
3.  **이름**에 **Sales Pie Chart**를 입력합니다.  
  
4.  **저장**을 클릭합니다.  
  
보고서가 보고서 서버에 저장됩니다.  
  
## <a name="next-steps"></a>Next Steps  
보고서에 원형 차트 추가 자습서를 성공적으로 완료했습니다. 차트에 대한 자세한 내용은 [차트&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/charts-report-builder-and-ssrs.md) 및 [스파크라인 및 데이터 막대&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[보고서 작성기 자습서](../reporting-services/report-builder-tutorials.md)  
[SQL Server 2016의 보고서 작성기](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

