---
title: '자습서: 보고서에 막대 차트 추가(보고서 작성기) | Microsoft Docs'
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 6956ebd6-0217-4087-a4fa-5cc1c3804691
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8e6855a7a6a47021a635e12b2c53515ed20aa6f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63041187"
---
# <a name="tutorial-add-a-bar-chart-to-your-report-report-builder"></a>자습서: 보고서에 막대형 차트 추가(보고서 작성기)
이 자습서에서는 [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)] 의 마법사를 사용하여 페이지가 매겨진 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 보고서에 가로 막대형 차트를 만듭니다. 그런 다음 필터를 추가하고 차트를 향상시킵니다. 

가로 막대형 차트는 범주 데이터를 가로로 표시합니다. 이렇게 하면 다음 작업에 도움이 됩니다.  
  
-   긴 범주 이름의 가독성 향상  
-   값으로 표시되는 시간을 이해하기 쉽게 표현   
-   여러 계열의 상대 값 비교  
  
다음 그림에서는 2014년 및 2015년 상위 5명에 속하는 영업 사원의 판매 실적을 가지고 2015년 최고 매출에서 최저 매출순으로 만든 가로 막대형 차트를 보여 줍니다.  
  
![report-builder-bar-chart](../reporting-services/media/report-builder-bar-chart.png) 
  
 
> [!NOTE]  
> 이 자습서에서 마법사의 단계는 하나의 절차로 통합됩니다. 보고서 서버를 찾고, 데이터 세트를 만들고, 데이터 원본을 선택하는 방법에 대한 단계별 지침은 이 시리즈의 첫 번째 자습서인 [자습서: 기본 테이블 보고서 만들기&#40;보고서 작성기&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)을 참조하세요.  
  
이 자습서에 소요되는 예상 시간: 15분  
  
## <a name="requirements"></a>요구 사항  
요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)을 참조하세요.  
  
## <a name="Chart"></a>1. 차트 마법사에서 차트 보고서 만들기  
차트 마법사를 사용하여 포함된 데이터 세트를 만들고 공유 데이터 원본을 선택하고 가로 막대형 차트를 만듭니다.  
  
> [!NOTE]  
> 이 자습서의 쿼리에는 데이터 값이 포함되어 있으므로 외부 데이터 원본이 필요하지 않습니다. 따라서 쿼리가 상당히 길어집니다. 비즈니스 환경에서는 쿼리에 데이터가 포함되지 않을 것입니다. 이 자습서의 쿼리는 학습용으로만 제공됩니다.  
  
1.  [웹 포털, SharePoint 통합 모드의 보고서 서버 또는 컴퓨터에서](../reporting-services/report-builder/start-report-builder.md) 보고서 작성기를 시작 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 합니다.  
  
     **시작** 대화 상자가 나타납니다.  
  
     ![보고서 작성기 시작](../reporting-services/media/rb-getstarted.png "보고서 작성기 시작")  
  
     **시작** 대화 상자가 나타나지 않을 경우 **파일** >**새로 만들기**를 클릭합니다. **새 보고서 또는 데이터 세트** 대화 상자에 **시작** 대화 상자와 같은 내용이 가장 많이 들어 있습니다. 
      
2.  왼쪽 창에 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **차트 마법사**를 클릭합니다.  
  
4.  **데이터 세트 선택** 페이지에서 **데이터 세트 만들기**를 클릭한 후, **다음**을 클릭합니다.  
  
5.  **데이터 원본에 대한 연결 선택** 페이지에서 기존 데이터 원본을 선택하거나 보고서 서버를 찾아 데이터 원본을 선택하고 **다음**을 클릭합니다. 사용자 이름과 암호를 입력해야 할 수 있습니다.  
  
    > [!NOTE]  
    > 적절한 권한만 가지고 있으면 선택하는 데이터 원본은 중요하지 않습니다. 데이터를 데이터 원본에서 가져오는 것은 아니기 때문입니다. 자세한 내용은 [데이터에 연결하는 다른 방법&#40;보고서 작성기&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)를 참조하세요.  
  
6.  **쿼리 디자인** 페이지에서 **텍스트로 편집**을 클릭합니다.  
  
7.  쿼리 창에 다음 쿼리를 붙여 넣습니다.  
  
    ```  
    SELECT 'Luis' as FirstName, 'Alverca' as LastName, CAST(170000.00 AS money) AS SalesYear2015, CAST(150000. AS money) AS SalesYear2014  
    UNION SELECT 'Jeffrey' as FirstName, 'Zeng' as LastName, CAST(210000. AS money) AS SalesYear2015, CAST(190000. AS money) AS SalesYear2014  
    UNION SELECT 'Houman' as FirstName, 'Pournasseh' as LastName, CAST(150000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Robin' as FirstName, 'Wood' as LastName, CAST(75000. AS money) AS SalesYear2015, CAST(175000. AS money) AS SalesYear2014  
    UNION SELECT 'Daniela' as FirstName, 'Guaita' as LastName,  CAST(170000. AS money) AS SalesYear2015, CAST(175000. AS money) AS SalesYear2014  
    UNION SELECT 'John' as FirstName, 'Yokim' as LastName, CAST(160000. AS money) AS SalesYear2015, CAST(195000. AS money) AS SalesYear2014  
    UNION SELECT 'Delphine' as FirstName, 'Ribaute' as LastName, CAST(180000. AS money) AS SalesYear2015, CAST(205000. AS money) AS SalesYear2014  
    UNION SELECT 'Robert' as FirstName, 'Hernady' as LastName, CAST(140000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Tanja' as FirstName, 'Plate' as LastName, CAST(150000. AS money) AS SalesYear2015, CAST(160000. AS money) AS SalesYear2014  
    UNION SELECT 'David' as FirstName, 'Bradley' as LastName, CAST(210000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Michal' as FirstName, 'Jaworski' as LastName, CAST(175000. AS money) AS SalesYear2015, CAST(220000. AS money) AS SalesYear2014  
    UNION SELECT 'Chris' as FirstName, 'Ashton' as LastName, CAST(195000. AS money) AS SalesYear2015, CAST(205000. AS money) AS SalesYear2014  
    UNION SELECT 'Pongsiri' as FirstName, 'Hirunyanitiwatna' as LastName, CAST(175000. AS money) AS SalesYear2015, CAST(215000. AS money) AS SalesYear2014  
    UNION SELECT 'Brian' as FirstName, 'Burke' as LastName, CAST(187000. AS money) AS SalesYear2015, CAST(207000. AS money) AS SalesYear2014  
    ```  
  
8.  (옵션) 실행 단추( **!** )를 클릭하여 차트의 기반으로 사용될 데이터를 확인합니다.  
  
9. **다음**을 클릭합니다.  
  
## <a name="ChartType"></a>2. 가로 막대형 차트 만들기  
 
1.  **차트 종류 선택** 페이지에서 기본 차트 종류는 세로 막대형 차트입니다.  
  
2.  **가로 막대형**을 클릭하고 **다음**을 클릭합니다.  
  
    **차트 필드 정렬** 페이지의 **사용 가능한 필드** 창에는 FirstName, LastName, SalesYear2015 및 SalesYear2014의 4개 필드가 있습니다.  
  
3.  LastName을 범주 창으로 끌어 옵니다.  
  
4.  SalesYear2015를 값 창으로 끌어옵니다. SalesYear2015는 각 영업 사원의 2015년도 판매액을 나타냅니다. 차트에 각 제품의 집계가 표시되기 때문에 값 창에는 `[Sum(SalesYear2015)]` 가 표시됩니다.  
  
5.  SalesYear2014를 SalesYear2015 아래의 값 창으로 끌어옵니다. SalesYear2014는 각 영업 사원의 2014년도 판매액을 나타냅니다.  
  
6.  **다음**을 클릭합니다.  
  
7.  **마침**을 클릭합니다.  
  
    디자인 화면에 차트가 추가됩니다. 새 가로 막대형 차트에는 대표 데이터만 표시됩니다. 범례는 사용자 이름이 아니라 Last Name A, Last Name B 등으로, 보고서의 대략적인 모양을 보여 줍니다. 
  
9. 차트를 클릭하여 차트 핸들을 표시합니다. 차트의 오른쪽 아래 모퉁이를 끌어 차트의 크기를 늘립니다. 끌면 디자인 화면이 더 커집니다. 
  
10. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
가로 막대형 차트에는 각 영업 사원의 2014년과 2015년 판매량이 표시됩니다. 막대 길이는 총 판매량에 해당합니다.  
  
## <a name="AllValues"></a>3. 세로 축의 모든 이름 표시  
기본적으로 세로 축의 값 중 일부만 표시됩니다. 모든 범주를 표시하도록 차트를 변경할 수 있습니다.  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  세로 축을 마우스 오른쪽 단추로 클릭한 다음 **세로 축 속성**을 클릭합니다.  
  
3.  **축 범위 및 간격**의 **간격** 상자에 **1**을 입력합니다.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
> [!NOTE]  
> 세로 축에서 영업 사원의 이름을 읽을 수 없는 경우에는 차트를 늘리거나 축 레이블의 서식 옵션을 변경합니다.  
  
### <a name="CategoryExpression"></a>세로 축에 성 및 이름 표시  
각 영업 사원의 성 다음에 이름이 오도록 범주 식을 변경할 수 있습니다.  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  차트를 두 번 클릭하여 **차트 데이터** 창을 표시합니다.  
  
3.  **범주 그룹** 영역에서 [LastName]을 마우스 오른쪽 단추로 클릭한 다음 **범주 그룹 속성**을 클릭합니다.  
  
4.  레이블에서 식 단추(fx)를 클릭합니다.  
  
5.  다음 식을 입력합니다. `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
    이 식은 성, 쉼표 및 이름을 연결합니다.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
보고서를 실행할 때 이름이 표시되지 않으면 데이터를 수동으로 새로 고칩니다. 미리 보기 모드에 있는 동안 **탐색** 그룹의 **실행** 탭에서 **새로 고침**을 클릭합니다.  
  
> [!NOTE]  
> 세로 축에서 영업 사원의 이름을 읽을 수 없는 경우에는 차트를 늘리거나 축 레이블의 서식 옵션을 변경합니다.  
  
## <a name="Sort"></a>4. 세로 축의 정렬 순서 변경  
차트에서 데이터를 정렬하면 범주 축에서 값 순서를 변경하게 됩니다.  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  차트를 두 번 클릭하여 **차트 데이터** 창을 표시합니다.  
  
3.  **범주 그룹** 영역에서 [LastName]을 마우스 오른쪽 단추로 클릭한 다음 **범주 그룹 속성**을 클릭합니다.  
  
4.  **정렬**을 클릭합니다. **정렬 옵션을 변경하십시오.** 페이지에 정렬 식 목록이 표시됩니다. 기본적으로 이 목록에는 원래 범주 그룹 식과 동일한 정렬 식이 있습니다.  
  
5.  **정렬 기준**에서 **[SalesYear2015]** 를 클릭합니다.  
  
6.  **순서** 목록에서 **내림차순** 을 선택하여 2015년 판매량이 가장 큰 값부터 가장 작은 값 순서로 이름이 표시되도록 합니다.
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
가로 축의 이름은 2015년 판매량이 가장 큰 값부터 가장 작은 값 순서로 정렬되며 **Zeng** 이 맨 위에 있습니다.  
  
## <a name="Legend"></a>5. 범례 이동  
차트 값을 더 쉽게 읽을 수 있도록 차트 범례를 이동할 수 있습니다. 예를 들어 막대가 가로로 표시되는 가로 막대형 차트에서는 범례가 차트 영역의 위나 아래에 표시되도록 범례 위치를 변경할 수 있습니다. 이렇게 하면 막대의 가로 공간을 늘릴 수 있습니다.  
  
#### <a name="to-display-the-legend-below-the-chart-area-of-a-bar-chart"></a>가로 막대형 차트의 차트 영역 아래쪽에 범례를 표시하려면  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  차트의 범례를 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **범례 속성**을 선택합니다.  
  
4.  **범례 위치**에서 다른 위치를 선택합니다. 예를 들어 아래쪽 가운데 옵션으로 위치를 설정합니다.  
  
    범례가 차트의 위쪽이나 아래쪽에 배치될 경우 범례 레이아웃은 세로에서 가로로 변경됩니다. **레이아웃** 드롭다운 목록에서 다른 레이아웃을 선택할 수 있습니다.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
## <a name="ChartTitle"></a>6. 차트 제목 지정  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  차트 맨 위의 **차트 제목** 단어를 선택하고 **Sales for 2014 and 2015**를 입력합니다.  
  
3.  속성 창에서 제목이 선택된 상태로 **색** 을 **검정** 으로, **FontSize** 를 **12pt**로 설정합니다. 
  
4.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
## <a name="Horizontal"></a>7. 가로 축의 서식 및 레이블 지정  
기본적으로 가로 축에는 차트 크기에 맞게 자동으로 늘어나는 일반 형식으로 값이 표시됩니다. 통화 형식으로 변경할 수 있습니다.  
   
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  차트 아래쪽의 가로 축을 클릭하여 선택합니다.  
  
3.  **홈** 탭 > **숫자** 그룹 > **통화**를 클릭합니다. 가로 축 레이블이 통화로 변경됩니다.  
  
3.  (선택 사항) 십진수를 제거합니다. **통화** 단추 주위에 있는 **소수 자릿수 줄이기** 단추를 두 번 클릭합니다.  
  
4.  가로 축을 마우스 오른쪽 단추로 클릭한 다음 **가로 축 속성**을 클릭합니다.  
  
5.  **숫자** 탭에서 **천 단위로 값 표시**를 선택합니다.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  

8.  가로 축을 마우스 오른쪽 단추로 클릭하고 **축 제목 표시**를 선택합니다.
  
7.  **축 제목** 상자에 **Sales in thousands** 를 입력하고 Enter 키를 누릅니다.  

    >**참고:** 입력하는 동안에는 축 제목 상자가 세로 축에 있는 것처럼 표시됩니다. 하지만 Enter 키를 누르면 가로 축으로 이동합니다.
  
9. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
판매액은 보고서 가로 축에 천 단위로 표시되며 소수 자릿수가 없습니다.  
  
## <a name="Filter"></a>8. 상위 5개 값을 표시하는 필터 추가  
차트에 필터를 추가하여 차트에 포함하거나 제외할 데이터 세트의 데이터를 지정할 수 있습니다.   
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  차트를 두 번 클릭하여 **차트 데이터** 창을 표시합니다.  
  
3.  **범주 그룹** 영역에서 [LastName] 필드를 마우스 오른쪽 단추로 클릭한 다음 **범주 그룹 속성**을 클릭합니다.  
  
4.  **필터**를 클릭합니다. **필터 변경** 페이지에 필터 식 목록이 표시될 수 있습니다. 기본적으로 이 목록은 비어 있습니다.  
  
5.  **추가**를 클릭합니다. 새로운 빈 필터가 나타납니다.  
  
6.  **식**에서 **[Sum(SalesYear2015)]** 를 입력합니다. 기본 식 `=Sum(Fields!SalesYear2015.Value)`이 만들어집니다. 이 식은 **fx** 단추를 클릭하면 볼 수 있습니다.  
  
7.  데이터 형식이 **Text**인지 확인합니다.  
  
8.  **연산자**의 드롭다운 목록에서 **Top N** 을 선택합니다.  
  
9. **값**에 **=5**식을 입력합니다.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
보고서를 실행할 때 결과가 필터링되지 않으면 데이터를 수동으로 새로 고칩니다. **탐색** 그룹의 **실행** 탭에서 **새로 고침**을 클릭합니다.  
  
2015년도 매출 데이터에서 상위 5명에 속하는 영업 사원의 이름이 차트에 표시됩니다.  
  
## <a name="Title"></a>9. 보고서 제목 추가  
  
1.  디자인 화면에서 **제목을 추가하려면 클릭하십시오.** 를 클릭합니다.  
  
2.  **Sales Bar Chart**를 입력하고 Enter 키를 누른 다음 **Top Five Sellers for 2015**를 입력하면 다음과 같이 표시됩니다.  
  
    **Sales Bar Chart**  
  
    **Top Five Sellers for 2015**  
  
3.  **Sales Bar Chart**를 선택하고 **굵게** 단추를 클릭합니다.  
  
4.  **Top Five Sellers for 2015**를 선택하고 **홈** 탭의 **글꼴** 섹션에서 글꼴 크기를 **10**으로 설정합니다.  
  
5.  (옵션) 두 줄 텍스트를 포함하기 위해 제목 입력란의 높이를 늘리고 가로 막대형 차트의 위쪽을 아래로 잡아당겨야 할 수도 있습니다.  
  
    이 제목은 보고서 맨 위에 나타납니다. 페이지 머리글이 정의되지 않았을 경우 보고서 본문의 맨 위에 있는 항목은 보고서 머리글에 해당합니다.  
  
6.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
## <a name="Save"></a>10. 보고서 저장  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  **파일** > **다른 이름으로 저장**을 클릭합니다.  
  
3.  **이름**에 **Sales Bar Chart**를 입력합니다.  

    컴퓨터 또는 보고서 서버에 저장할 수 있습니다.
  
4.  **저장**을 클릭합니다.   
  
## <a name="next-steps"></a>Next Steps  
보고서에 가로 막대형 차트 추가 자습서를 성공적으로 완료했습니다. 차트에 대한 자세한 내용은 [차트](../reporting-services/report-design/charts-report-builder-and-ssrs.md) 및 [가로 막대형 차트](../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[보고서 작성기 자습서](../reporting-services/report-builder-tutorials.md)  
[SQL Server의 보고서 작성기](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

