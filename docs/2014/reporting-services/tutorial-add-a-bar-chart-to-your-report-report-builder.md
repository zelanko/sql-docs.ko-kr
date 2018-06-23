---
title: '자습서: 보고서에 막대 차트 추가(보고서 작성기) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6956ebd6-0217-4087-a4fa-5cc1c3804691
caps.latest.revision: 10
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: f54e95b0b9bee1e989d9d9ccf85f513210302367
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36180789"
---
# <a name="tutorial-add-a-bar-chart-to-your-report-report-builder"></a>자습서: 보고서에 막대형 차트 추가(보고서 작성기)
  가로 막대형 차트는 범주 데이터를 가로로 표시합니다. 이렇게 하면 다음 작업에 도움이 됩니다.  
  
-   긴 범주 이름의 가독성 향상  
  
-   값으로 표시되는 시간을 이해하기 쉽게 표현  
  
-   여러 계열의 상대 값 비교  
  
 다음 그림에서는 2008년 및 2009년 상위 5명에 속하는 영업 사원의 판매 실적을 가지고 사전순으로 만든 가로 막대 차트를 보여 줍니다.  
  
 ![rs_BarChartTutorial](../../2014/tutorials/media/rs-barcharttutorial.gif "rs_BarChartTutorial")  
  
##  <a name="BackToTop"></a> 학습 내용  
 이 자습서에서는 다음 작업 방법을 배웁니다.  
  
1.  [차트 마법사에서 차트 만들기](#Chart)  
  
2.  [차트 종류 선택](#ChartType)  
  
3.  [세로 축에 모든 범주 값 표시](#AllValues)  
  
4.  [세로 축의 이름 표시 수정](#Sort)  
  
5.  [범례 이동](#Legend)  
  
6.  [차트 제목 이동](#ChartTitle)  
  
7.  [가로 축의 서식 및 레이블](#Horizontal)  
  
8.  [상위 5 개 값을 표시 하는 필터를 추가 합니다.](#Filter)  
  
9. [보고서 제목 추가](#Title)  
  
10. [보고서 저장](#Save)  
  
> [!NOTE]  
>  이 자습서에서 마법사의 단계는 하나의 절차로 통합됩니다. 보고서 서버를 찾고, 데이터 집합을 만들고, 데이터 원본을 선택하는 방법에 대한 단계별 지침은 이 시리즈의 첫 번째 자습서인 [자습서: 기본 테이블 보고서 만들기&#40;보고서 작성기&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)를 참조하세요.  
  
 이 자습서에 소요되는 예상 시간: 15분  
  
## <a name="requirements"></a>요구 사항  
 요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/report-builder-tutorials.md)을 참조하세요.  
  
##  <a name="Chart"></a> 1. 차트 마법사에서 차트 보고서 만들기  
 **시작** 대화 상자, 포함된 된 데이터 집합을 만들려면 공유 데이터 원본을 선택 하 고 차트 마법사를 사용 하 여 가로 막대형 차트를 만듭니다.  
  
> [!NOTE]  
>  이 자습서의 쿼리에는 데이터 값이 포함되어 있으므로 외부 데이터 원본이 필요하지 않습니다. 따라서 쿼리가 상당히 길어집니다. 비즈니스 환경에서는 쿼리에 데이터가 포함되지 않을 것입니다. 이 자습서의 쿼리는 학습용으로만 제공됩니다.  
  
#### <a name="to-create-a-new-chart-report"></a>새 차트 보고서를 만들려면  
  
1.  **시작**을 클릭하고 **프로그램**, **Microsoft SQL Server 2012 보고서 작성기**를 차례로 가리킨 다음 **보고서 작성기**를 클릭합니다.  
  
     **시작** 대화 상자가 나타납니다.  
  
    > [!NOTE]  
    >  경우는 **시작** 대화 상자는 되지, 보고서 작성기 단추를 클릭 나타나며 클릭 **새로**합니다.  
  
2.  왼쪽 창에 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **차트 마법사**를 클릭합니다.  
  
4.  **데이터 집합 선택** 페이지에서 **데이터 집합 만들기**를 클릭하고 **다음**을 클릭합니다.  
  
5.  **데이터 원본에 대한 연결 선택** 페이지에서 기존 데이터 원본을 선택하거나 보고서 서버를 찾아 데이터 원본을 선택하고 **다음**을 클릭합니다. 사용자 이름과 암호를 입력해야 할 수 있습니다.  
  
    > [!NOTE]  
    >  적절한 권한만 가지고 있으면 선택하는 데이터 원본은 중요하지 않습니다. 데이터를 데이터 원본에서 가져오는 것은 아니기 때문입니다. 자세한 내용은 [데이터에 연결하는 다른 방법&#40;보고서 작성기&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)를 참조하세요.  
  
6.  **쿼리 디자인** 페이지에서 **텍스트로 편집**을 클릭합니다.  
  
7.  쿼리 창에 다음 쿼리를 붙여 넣습니다.  
  
    ```  
    SELECT 'Luis' as FirstName, 'Alverca' as LastName, CAST(170000.00 AS money) AS SalesYear2009, CAST(150000. AS money) AS SalesYear2008  
    UNION SELECT 'Jeffrey' as FirstName, 'Zeng' as LastName, CAST(210000. AS money) AS SalesYear2009, CAST(190000. AS money) AS SalesYear2008  
    UNION SELECT 'Houman' as FirstName, 'Pournasseh' as LastName, CAST(150000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Robin' as FirstName, 'Wood' as LastName, CAST(75000. AS money) AS SalesYear2009, CAST(175000. AS money) AS SalesYear2008  
    UNION SELECT 'Daniela' as FirstName, 'Guaita' as LastName,  CAST(170000. AS money) AS SalesYear2009, CAST(175000. AS money) AS SalesYear2008  
    UNION SELECT 'John' as FirstName, 'Yokim' as LastName, CAST(160000. AS money) AS SalesYear2009, CAST(195000. AS money) AS SalesYear2008  
    UNION SELECT 'Delphine' as FirstName, 'Ribaute' as LastName, CAST(180000. AS money) AS SalesYear2009, CAST(205000. AS money) AS SalesYear2008  
    UNION SELECT 'Robert' as FirstName, 'Hernady' as LastName, CAST(140000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Tanja' as FirstName, 'Plate' as LastName, CAST(150000. AS money) AS SalesYear2009, CAST(160000. AS money) AS SalesYear2008  
    UNION SELECT 'David' as FirstName, 'Bradley' as LastName, CAST(210000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Michal' as FirstName, 'Jaworski' as LastName, CAST(175000. AS money) AS SalesYear2009, CAST(220000. AS money) AS SalesYear2008  
    UNION SELECT 'Chris' as FirstName, 'Ashton' as LastName, CAST(195000. AS money) AS SalesYear2009, CAST(205000. AS money) AS SalesYear2008  
    UNION SELECT 'Pongsiri' as FirstName, 'Hirunyanitiwatna' as LastName, CAST(175000. AS money) AS SalesYear2009, CAST(215000. AS money) AS SalesYear2008  
    UNION SELECT 'Brian' as FirstName, 'Burke' as LastName, CAST(187000. AS money) AS SalesYear2009, CAST(207000. AS money) AS SalesYear2008  
    ```  
  
8.  (옵션) 실행 단추(**!**)를 클릭하여 차트의 기반으로 사용될 데이터를 확인합니다.  
  
9. **다음**을 클릭합니다.  
  
##  <a name="ChartType"></a> 2. 차트 종류 선택  
 미리 정의된 다양한 차트 종류 중에서 선택할 수 있습니다.  
  
#### <a name="to-add-a-column-chart"></a>세로 막대형 차트를 추가하려면  
  
1.  **차트 종류 선택** 페이지에서 기본 차트 종류는 세로 막대형 차트입니다.  
  
2.  **가로 막대형**을 클릭하고 **다음**을 클릭합니다.  
  
     에 **차트 필드 정렬** 페이지에서 4 개의 필드는 **사용 가능한 필드** 창: FirstName, LastName, SalesYear2009 및 salesyear2008 필드가 있습니다.  
  
3.  LastName을 범주 창으로 끌어 옵니다.  
  
4.  SalesYear2009를 값 창으로 끌어 옵니다. SalesYear2009는 각 영업 사원의 2009년도 판매액을 나타냅니다. 차트에 각 제품의 집계가 표시되기 때문에 값 창에는 `[Sum(SalesYear2009)]`가 표시됩니다.  
  
5.  SalesYear2008을 SalesYear2009 아래의 값 창으로 끌어 옵니다. SalesYear2008은 각 영업 사원의 2008년도 판매액을 나타냅니다.  
  
6.  **다음**을 클릭합니다.  
  
7.  에 **스타일 선택** 페이지의 스타일 창에서 스타일을 선택 합니다.  
  
     스타일은 글꼴 스타일, 색 집합 및 테두리 스타일을 지정합니다. 스타일을 선택하면 미리 보기 창에 해당 스타일이 적용된 예제 차트가 표시됩니다.  
  
8.  **마침**을 클릭합니다.  
  
     디자인 화면에 차트가 추가됩니다.  
  
9. 차트를 클릭하여 차트 핸들을 표시합니다. 차트의 오른쪽 아래 모퉁이를 끌어 차트의 크기를 늘립니다.  
  
10. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 보고서에는 각 영업 사원의 2008년과 2009년 판매량에 대한 가로 막대형 차트가 표시됩니다. 막대 길이는 총 판매량에 해당합니다.  
  
##  <a name="AllValues"></a> 3. 세로 축의 이름 표시 수정  
 기본적으로 세로 축의 값 중 일부만 표시됩니다. 모든 범주를 표시하도록 차트를 변경할 수 있습니다.  
  
#### <a name="to-display-all-sales-persons-along-the-category-axis-of-a-bar-chart"></a>가로 막대형 차트의 범주 축에 모든 영업 사원을 표시하려면  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  세로 축을 마우스 오른쪽 단추로 누른 **세로 축 속성**합니다.  
  
3.  **축 범위 및 간격**의 **간격** 상자에 **1**을 입력합니다.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  세로 마우스 오른쪽 단추로 클릭 **축 제목** 선택을 취소 하 고는 **축 제목 표시** 확인란 합니다.  
  
6.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
> [!NOTE]  
>  세로 축에서 영업 사원의 이름을 읽을 수 없는 경우에는 차트를 늘리거나 축 레이블의 서식 옵션을 변경합니다.  
  
###  <a name="CategoryExpression"></a> 세로 축에 성 및 이름 표시  
 각 영업 사원의 성 다음에 이름이 오도록 범주 식을 변경할 수 있습니다.  
  
##### <a name="to-change-the-category-expression"></a>범주 식을 변경하려면  
  
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
>  세로 축에서 영업 사원의 이름을 읽을 수 없는 경우에는 차트를 늘리거나 축 레이블의 서식 옵션을 변경합니다.  
  
##  <a name="Sort"></a> 4. 세로 축에서 이름 정렬 순서를 변경할 수 있습니다.  
 차트에서 데이터를 정렬하면 범주 축에서 값 순서를 변경하게 됩니다.  
  
#### <a name="to-sort-the-names-in-alphabetical-order-on-the-bar-chart"></a>가로 막대형 차트에서 이름을 사전순으로 정렬하려면  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  차트를 두 번 클릭하여 **차트 데이터** 창을 표시합니다.  
  
3.  **범주 그룹** 영역에서 [LastName]을 마우스 오른쪽 단추로 클릭한 다음 **범주 그룹 속성**을 클릭합니다.  
  
4.  **정렬**을 클릭합니다. **정렬 옵션을 변경하십시오.** 페이지에 정렬 식 목록이 표시됩니다. 기본적으로 이 목록에는 원래 범주 그룹 식과 동일한 정렬 식이 있습니다.  
  
5.  정렬 기준 식을 클릭 (**Fx**) 단추입니다.  
  
6.  다음 식을 입력합니다. `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
7.  **확인**을 클릭합니다.  
  
8.  에 **범주 그룹 속성** 페이지는 **순서** 드롭 다운 목록 **Z에서 A**합니다. 그러면 이름이 내림차순으로 나타나도록 역방향 사전순이 선택됩니다.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 가로 축의 이름은으로 반대 순서로 정렬 되어 **Alerca** 위쪽 및 **Zeng** 맨 아래에 있습니다.  
  
##  <a name="Legend"></a> 5. 범례 이동  
 차트 값을 더 쉽게 읽을 수 있도록 차트 범례를 이동할 수 있습니다. 예를 들어 막대가 가로로 표시되는 가로 막대형 차트에서는 범례가 차트 영역의 위나 아래에 표시되도록 범례 위치를 변경할 수 있습니다. 이렇게 하면 막대의 가로 공간을 늘릴 수 있습니다.  
  
#### <a name="to-display-the-legend-below-the-chart-area-of-a-bar-chart"></a>가로 막대형 차트의 차트 영역 아래쪽에 범례를 표시하려면  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  차트의 범례를 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **범례 속성**을 선택합니다.  
  
4.  **범례 위치**에서 다른 위치를 선택합니다. 예를 들어 아래쪽 가운데 옵션으로 위치를 설정합니다.  
  
     범례가 차트의 위쪽이나 아래쪽에 배치될 경우 범례 레이아웃은 세로에서 가로로 변경됩니다. **레이아웃** 드롭다운 목록에서 다른 레이아웃을 선택할 수 있습니다.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
##  <a name="ChartTitle"></a> 6. 차트 제목 지정  
  
#### <a name="to-change-the-chart-title-above-the-chart-area-of-a-bar-chart"></a>가로 막대형 차트의 차트 영역 위쪽에 있는 차트 제목을 변경하려면  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  단어 **차트 제목을** 입력 한 후 다음 텍스트와 차트의 위쪽: **Sales for 2008 and 2009**합니다.  
  
3.  텍스트 외부의 아무 곳이나 클릭합니다.  
  
4.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
##  <a name="Horizontal"></a> 7. 가로 축의 서식 및 레이블 지정  
 기본적으로 가로 축에는 차트 크기에 맞게 자동으로 늘어나는 일반 형식으로 값이 표시됩니다.  
  
#### <a name="to-format-the-numbers-on-the-horizontal-axis"></a>가로 축의 숫자에 형식을 지정하려면  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  차트 아래쪽의 가로 축을 클릭하여 선택합니다.  
  
     리본 메뉴에 **홈** 탭에 **번호** 그룹을 클릭 합니다는 **통화** 단추입니다. 가로 축 레이블이 통화로 변경됩니다.  
  
3.  (선택 사항) 십진수를 제거합니다. **통화** 단추 주위에 있는 **소수 자릿수 줄이기** 단추를 두 번 클릭합니다.  
  
4.  가로 축을 마우스 오른쪽 단추로 클릭한 다음 **가로 축 속성**을 클릭합니다.  
  
5.  에 **번호** 탭에서 **천 단위로 값 표시 합니다.**  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  마우스 오른쪽 단추로 클릭 **축 제목** 클릭 **축 제목 속성**합니다.  
  
8.  에 **제목 텍스트** 상자에 입력 합니다 **천 단위에서 판매** 클릭 **확인**합니다.  
  
9. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 판매액은 보고서 가로 축에 천 단위로 표시되며 십진수가 없습니다.  
  
##  <a name="Filter"></a> 8입니다. 상위 5개 값을 표시하는 필터 추가  
 차트에 필터를 추가하여 차트에 포함하거나 제외할 데이터 집합의 데이터를 지정할 수 있습니다.  
  
#### <a name="to-add-a-filter-and-display-the-top-five-values"></a>상위 5개 값을 표시하는 필터를 추가하려면  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  차트를 두 번 클릭하여 **차트 데이터** 창을 표시합니다.  
  
3.  **범주 그룹** 영역에서 [LastName] 필드를 마우스 오른쪽 단추로 클릭한 다음 **범주 그룹 속성**을 클릭합니다.  
  
4.  **필터**를 클릭합니다. **필터 변경** 페이지에 필터 식 목록이 표시될 수 있습니다. 기본적으로 이 목록은 비어 있습니다.  
  
5.  **추가**를 클릭합니다. 새로운 빈 필터가 나타납니다.  
  
6.  **식**, 형식 **[sum (salesyear2009)]** 합니다. 이렇게 하면 기본 식을 만들어집니다 `=Sum(Fields!SalesYear2009.Value)`, 클릭 하면 볼 수 있는 **fx** 단추입니다.  
  
7.  데이터 형식이 **Text**인지 확인합니다.  
  
8.  **연산자**의 드롭다운 목록에서 **Top N** 을 선택합니다.  
  
9. **값**에 **=5**식을 입력합니다.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 보고서를 실행할 때 결과가 필터링되지 않으면 데이터를 수동으로 새로 고칩니다. **탐색** 그룹의 **실행** 탭에서 **새로 고침**을 클릭합니다.  
  
 2009년도 매출 데이터에서 상위 5명에 속하는 영업 사원의 이름이 차트에 표시됩니다.  
  
##  <a name="Title"></a> 9입니다. 보고서 제목 추가  
  
#### <a name="to-add-a-report-title"></a>보고서 제목을 추가하려면  
  
1.  디자인 화면에서 **제목을 추가하려면 클릭하십시오.** 를 클릭합니다.  
  
2.  형식 **Sales Bar Chart**를 enter 키를 입력 하 고 다음 **Top Five Sellers for 2009**이므로 다음과 같습니다.  
  
     **Sales Bar Chart**  
  
     **Top Five Sellers for 2009**  
  
3.  **Sales Bar Chart**를 선택하고 **굵게** 단추를 클릭합니다.  
  
4.  선택 **Top Five Sellers for 2009**, 및는 **글꼴** 섹션에서 **홈** 탭, 글꼴 크기를 설정 **10**합니다.  
  
5.  (선택 사항) 제목 입력란을 두 줄 텍스트를 포함하도록 크게 만들어야 할 수 있습니다.  
  
     이 제목은 보고서 맨 위에 나타납니다. 페이지 머리글이 정의되지 않았을 경우 보고서 본문의 맨 위에 있는 항목은 보고서 머리글에 해당합니다.  
  
6.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
##  <a name="Save"></a> 10입니다. 보고서 저장  
  
#### <a name="to-save-the-report"></a>보고서를 저장하려면  
  
1.  보고서 디자인 뷰로 전환합니다.  
  
2.  **보고서 작성기** 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
3.  **이름**에 **Sales Bar Chart**를 입력합니다.  
  
4.  **저장**을 클릭합니다.  
  
 보고서가 보고서 서버에 저장됩니다.  
  
## <a name="next-steps"></a>다음 단계  
 보고서에 가로 막대형 차트 추가 자습서를 성공적으로 완료했습니다. 차트에 대한 자세한 내용은 [차트&#40;보고서 작성기 및 SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) 및 [스파크라인 및 데이터 막대&#40;보고서 작성기 및 SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [자습서 &#40;보고서 작성기&#41;](report-builder-tutorials.md)   
 [SQL Server 2014의 보고서 작성기](report-builder/report-builder-in-sql-server-2016.md)  
  
  