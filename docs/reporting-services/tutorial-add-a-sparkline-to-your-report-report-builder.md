---
title: "자습서: 보고서에 스파크라인 추가(보고서 작성기) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 18c90a36-48bf-4805-a960-2d1e8f00c2dc
caps.latest.revision: "17"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e1e9269a160a311fc076618d00deb7a0fb6432c2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="tutorial-add-a-sparkline-to-your-report-report-builder"></a>자습서: 보고서에 스파크라인 추가(보고서 작성기)

이 자습서에서는 [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)]에서 페이지가 매겨진 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 보고서에 스파크라인 차트와 함께 기본 테이블을 만듭니다.   
  
스파크라인과 데이터 막대는 작은 공간에 많은 정보가 포함되어 있는 작고 간단한 차트로, 대개 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 보고서에서 테이블과 행렬로 표시됩니다. 다음 그림에서는 만들려는 보고서와 비슷한 보고서를 보여 줍니다.  
  
![report-builder-sparkline-final](../reporting-services/media/report-builder-sparkline-final.png)  
     
이 자습서에 소요되는 예상 시간: 30분  
  
## <a name="requirements"></a>요구 사항  
요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)을 참조하세요.  
  
## <a name="CreateTable"></a>1. 테이블이 있는 보고서 만들기  
  
1.  컴퓨터,[웹 포털 또는 SharePoint 통합 모드에서](../reporting-services/report-builder/start-report-builder.md) 보고서 작성기를 시작 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 합니다.  
  
    **새 보고서 또는 데이터 집합** 대화 상자가 열립니다.  
  
    **새 보고서 또는 데이터 집합** 대화 상자가 표시되지 않는 경우 **파일** 메뉴 > **새로 만들기**를 클릭합니다.  
  
2.  왼쪽 창에 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **테이블 또는 행렬 마법사**를 클릭합니다.  
  
4.  **데이터 집합 선택** 페이지에서 **데이터 집합 만들기** > **다음**을 선택합니다. **데이터 원본에 대한 연결 선택** 페이지가 열립니다.  
  
    > [!NOTE]  
    > 이 자습서를 사용하기 위해 특정 데이터가 필요하지는 않습니다. SQL Server 데이터베이스에 연결하기만 하면 됩니다. **데이터 원본 연결**에 나열된 데이터 원본 연결이 이미 있는 경우 해당 데이터 원본 연결을 선택하고 10단계로 이동할 수 있습니다. 자세한 내용은 [데이터에 연결하는 다른 방법&#40;보고서 작성기&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)를 참조하세요.  
  
5.  **새로 만들기**를 클릭합니다. **데이터 원본 속성** 대화 상자가 열립니다.  
  
6.  **이름**에 데이터 원본 이름으로 **Product Sales**를 입력합니다.  
  
7.  **연결 유형 선택**에서 **Microsoft SQL Server** 가 선택되어 있는지 확인합니다.  
  
8.  **연결 문자열**에 다음 텍스트를 입력합니다.  
  
    `Data Source\=<servername>`  
  
    `<servername>`식(예: Report001)은 SQL Server 데이터베이스 엔진의 인스턴스가 설치된 컴퓨터를 지정합니다. 보고서 데이터는 SQL Server 데이터베이스에서 추출되지 않았으므로 데이터베이스 이름을 포함하지 않아야 합니다. 지정된 서버의 기본 데이터베이스는 쿼리를 구문 분석하는 데 사용됩니다.  
  
9. **자격 증명**을 클릭합니다. 외부 데이터 원본에 액세스하는 데 필요한 자격 증명을 입력합니다.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    **데이터 원본에 대한 연결 선택** 페이지로 돌아갑니다.  
  
11. 데이터 원본에 연결할 수 있는지 확인하려면 **연결 테스트**를 클릭합니다.  
  
    "연결되었습니다."라는 메시지가 나타납니다.  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. **다음**을 클릭합니다.  
  
## <a name="Query"></a>2. 테이블 마법사에서 쿼리 및 테이블 레이아웃 만들기  
보고서에서는 미리 정의된 쿼리가 포함된 공유 데이터 집합을 사용하거나 해당 보고서에만 사용할 포함된 데이터 집합을 만들 수 있습니다. 이 자습서에서는 포함된 데이터 집합을 만듭니다.  
  
> [!NOTE]  
> 이 자습서의 쿼리에는 데이터 값이 포함되어 있으므로 외부 데이터 원본이 필요하지 않습니다. 따라서 쿼리가 상당히 길어집니다. 비즈니스 환경에서는 쿼리에 데이터가 포함되지 않을 것입니다. 이 자습서의 쿼리는 학습용으로만 제공됩니다.  
  
### <a name="to-create-a-query-and-table-layout-in-the-table-wizard"></a>테이블 마법사에서 쿼리 및 테이블 레이아웃을 만들려면 
  
1.  **쿼리 디자인** 페이지에 관계형 쿼리 디자이너가 열립니다. 이 자습서에서는 텍스트 기반 쿼리 디자이너를 사용합니다.  
  
2.  **텍스트로 편집**을 클릭합니다. 텍스트 기반 쿼리 디자이너에 쿼리 창과 결과 창이 표시됩니다.  
  
3.  [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리 **상자에 다음** 쿼리를 붙여 넣습니다.  
  
    ```  
    SELECT CAST('2015-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Budget Movie-Maker' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Slim Digital' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,'Accessories' as Subcategory,    
       'Budget Movie-Maker' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Carrying Case' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-04' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
4.  쿼리 디자이너 도구 모음에서 실행(**!**)을 클릭합니다.  
  
    쿼리가 실행되고 **SalesDate**, **Subcategory**, **Product**, **Sales**및 **Quantity**필드에 대한 결과 집합이 표시됩니다.  
  
5.  **다음**을 클릭합니다.  
  
6.  **필드 정렬** 페이지에서 **값** 에 **Sales**를 끌어옵니다.  
  
    **Sales** 는 Sum 함수로 집계됩니다. 값은 [Sum(Sales)]입니다.  
  
7.  **행 그룹** 에 **Product**를 끌어옵니다.  
  
8.  **열 그룹** 에 **SalesDate**를 끌어옵니다.  

    ![report-builder-sparkline-arrange-fields](../reporting-services/media/report-builder-sparkline-arrange-fields.png)
  
9. **다음**을 클릭합니다.  
  
10. **레이아웃 선택** 페이지의 **옵션**에서 **부분합 및 총합계 표시** 가 선택되어 있는지 확인합니다.  
  
    마법사 미리 보기 창에 3개의 행이 있는 테이블이 표시됩니다. 보고서를 실행하면 각 행이 다음과 같은 방식으로 표시됩니다.  
  
    *  첫 번째 행은 열 제목을 보여 주기 위해 테이블에 대해 한 번씩 나타납니다.  
  
    *  두 번째 행은 각 제품에 대해 한 번씩 반복되고 제품 이름, 일일 합계 및 라인 합계를 표시합니다.  
  
    *  세 번째 행은 테이블에 대해 한 번씩 나타나 총합계를 표시합니다.  
    
    ![report-builder-sparkline-choose-layout](../reporting-services/media/report-builder-sparkline-choose-layout.png)
  
11. **다음**을 클릭합니다.  
  
12. **마침**을 클릭합니다.  
  
14. 디자인 화면에 테이블이 추가됩니다. 이 테이블에는 열 3개와 행 3개가 있습니다.  
  
    그룹화 창을 확인합니다. 그룹화 창이 표시되지 않는 경우 **보기** 메뉴에서 **그룹화**를 클릭합니다. 행 그룹 창에는 **Product**라는 한 개의 행 그룹이 표시됩니다. 열 그룹 창에는 **SalesDate**라는 한 개의 열 그룹이 표시됩니다. 세부 데이터는 모두 데이터 집합 쿼리로 검색된 데이터입니다.  
    
    ![report-builder-sparkline-grouping-pane](../reporting-services/media/report-builder-sparkline-grouping-pane.png)
  
15. **실행** 을 클릭하여 보고서를 미리 봅니다.  

### <a name="FormatCurrency"></a>2a. 데이터 형식을 통화로 지정  
기본적으로 **Sales** 필드의 요약 데이터에는 일반 숫자가 표시됩니다. 서식을 지정하여 숫자가 통화로 표시되도록 합니다. **자리 표시자 스타일** 을 설정/해제하여 서식 있는 입력란 및 자리 표시자 텍스트를 보기 값으로 표시합니다.  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 전환합니다.  
  
2.  **SalesDate** 열에서 두 번째 행(열 제목 행 아래)의 셀을 클릭합니다. Ctrl 키를 누른 상태로 `[Sum(Sales)]`이 들어 있는 셀을 모두 선택합니다. 

    ![report-builder-select-sum-sales](../reporting-services/media/report-builder-select-sum-sales.png) 
  
3.  **홈** 탭 > **숫자** 그룹에서 **통화**를 클릭합니다. 셀이 변경되어 형식 지정된 통화가 표시됩니다.  

    ![report-builder-placeholder-currency](../reporting-services/media/report-builder-placeholder-currency.png)
  
    국가별 설정이 영어(미국)인 경우 기본 예제 텍스트는 [**$12,345.00**]입니다. 예제 통화 값이 표시되지 않는 경우 **숫자** 그룹에서 **자리 표시자 스타일** > **샘플 값**을 클릭합니다.  
    
    ![report-builder-placeholder-value-button](../reporting-services/media/report-builder-placeholder-value-button.png)
   
### <a name="FormatDates"></a>2b. (선택 사항) 데이터 서식을 날짜로 지정  
기본적으로 **SalesDate** 필드에는 날짜 및 시간 정보가 표시됩니다. 날짜만 표시되도록 서식을 지정할 수 있습니다.  
  
1.  `[SalesDate]`가 들어 있는 셀을 클릭합니다.  
  
3.  **홈** 탭 > **숫자** 그룹 > **날짜**를 선택합니다.  
  
    셀에 예제 날짜 **[1/31/2000]**이 표시됩니다.
     
4.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
**SalesDate** 값은 기본 날짜 형식으로 표시되고 **Sales** 의 요약 값은 통화로 표시됩니다.   
  
## <a name="Sparkline"></a>3. 스파크라인 추가    
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  테이블의 Total 열을 선택합니다.  
  
3.  마우스 오른쪽 단추를 클릭하고 **열 삽입**을 가리킨 다음 **왼쪽**을 클릭합니다.  

    ![report-builder-add-column-left](../reporting-services/media/report-builder-add-column-left.png)
  
4.  새 열에서 `[Product]` 행의 셀을 마우스 오른쪽 단추로 클릭 > **삽입** > **스파크라인**을 선택합니다.  

    ![report-builder-insert-sparkline](../reporting-services/media/report-builder-insert-sparkline.png)
  
5.  **스파크라인 유형 선택** 대화 상자에서 **열** 행의 첫 번째 스파크라인이 선택되어 있는지 확인한 다음 **확인**을 클릭합니다.  
  
6.  스파크라인을 클릭하여 차트 데이터 창을 표시합니다.  
  
7.  값 상자의 더하기 기호(+)를 클릭한 다음 **Sales**를 클릭합니다. 

    ![report-builder-sparkline-values](../reporting-services/media/report-builder-sparkline-values.png) 
  
    그러면 **Sales** 필드의 값이 스파크라인의 값이 됩니다.  
  
8.  범주 그룹 상자의 더하기 기호(+)를 클릭한 다음 **SalesDate**를 클릭합니다.  
  
9. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
    스파크라인 차트의 각 막대가 서로 정렬되어 있지 않고, 데이터의 두 번째 행에는 네 개의 막대만 있으므로 여섯 개의 막대가 있는 첫 번째 행보다 막대의 너비가 넓습니다. 이로 인해 각 제품의 값을 일별로 비교할 수 없으므로 막대가 정렬되어야 합니다.  
  
    또한 각 행마다 가장 높은 막대는 행 높이와 같습니다. 각 행의 가장 큰 값은 같지 않으므로 이로 인해 혼동될 수 있습니다. 즉, Budget Movie-Maker의 가장 큰 값은 $10,400이지만 Slim Digital의 가장 큰 값은 이의 두 배 이상인 $26,576입니다. 그럼에도 불구하고 이 두 행의 가장 큰 막대는 서로 높이가 같습니다. 모든 스파크라인에서 동일한 배율을 사용해야 합니다.  
  
     ![report-builder-sparkline-misaligned](../reporting-services/media/report-builder-sparkline-misaligned.png)
  
## <a name="AlignSparklines"></a>4. 세로 및 가로로 스파크라인 맞추기  
스파크라인은 모두 동일한 측정값을 사용하지 않는 경우 읽기가 어렵습니다. 각 스파크라인의 가로 축과 세로 축이 나머지와 일치해야 합니다.  
   
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  스파크라인을 마우스 오른쪽 단추로 클릭하고 **세로 축 속성**을 클릭합니다.  
  
3.  **다음 위치의 축 정렬** 확인란을 선택합니다. Tablix1이 목록의 유일한 옵션입니다.  
  
     이 옵션은 각 스파크라인의 막대 높이를 서로 상대적인 높이로 설정합니다. 
  
4.  **확인**을 클릭합니다.  
  
5.  스파크라인을 마우스 오른쪽 단추로 클릭한 다음 **가로 축 속성**을 클릭합니다.  
  
6.  **다음 위치의 축 정렬** 확인란을 선택합니다. Tablix1이 목록의 유일한 옵션입니다. 
  
    이 옵션은 각 스파크라인의 막대 너비를 서로 상대적인 너비로 설정합니다. 다른 스파크라인보다 막대가 적은 스파크라인에서는 데이터가 없는 부분을 나타내는 빈 공간이 표시됩니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  **실행** 을 다시 클릭하여 보고서를 미리 봅니다.  
  
이제 각 스파크라인의 모든 막대가 다른 스파크라인의 막대와 정렬되며 높이는 상대적입니다.  
  
![report-builder-sparkline-aligned](../reporting-services/media/report-builder-sparkline-aligned.png)
  
## <a name="Width"></a>7. (선택 사항) 열 너비 변경  
기본적으로 테이블의 각 셀은 입력란을 포함합니다. 페이지를 렌더링하면 입력란은 텍스트를 수용하도록 세로로 확장됩니다. 렌더링된 보고서에서 각 행은 해당 행에서 가장 길게 렌더링된 입력란의 높이에 맞춰 확장됩니다. 디자인 화면에서 행의 높이는 렌더링된 보고서의 행 높이에 영향을 주지 않습니다.  
  
각 행의 세로 크기를 줄이려면 열 입력란에 들어갈 예상 내용이 한 줄에 수용되는 범위에서 열 너비를 확장합니다.  
  
### <a name="to-change-the-width-of-columns"></a>열의 너비를 변경하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  테이블을 클릭하여 테이블 위와 옆에 회색 막대가 표시되도록 합니다. 이러한 막대는 열 및 행 핸들입니다.
  
3.  열 핸들 사이의 선에 커서를 두면 커서가 양방향 화살표로 바뀝니다. **Product** 열을 끌어 제품 이름이 한 줄에 표시되도록 합니다.  
  
4.  **실행** 을 클릭하여 보고서를 미리 보고 너비가 충분한지 확인합니다.  
  
## <a name="Title"></a>8. (선택 사항) 보고서 제목 추가  
보고서 제목은 보고서 맨 위에 나타납니다. 보고서 제목을 보고서 머리글에 배치하거나, 보고서 머리글이 사용되지 않을 경우 보고서 본문의 맨 위에 있는 입력란에 배치할 수 있습니다. 이 자습서에서는 보고서 본문의 맨 위에 자동으로 표시되는 입력란을 사용합니다.  
  
글꼴 스타일, 크기 및 색을 텍스트의 각 문자나 구 단위로 다르게 적용하여 더 보기 좋게 꾸밀 수 있습니다. 자세한 내용은 [입력란의 텍스트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)을 참조하세요.  
  
### <a name="to-add-a-report-title"></a>보고서 제목을 추가하려면  
  
1.  디자인 화면에서 **제목을 추가하려면 클릭하십시오.**를 클릭합니다.  
  
2.  **Sales by Date**를 입력한 다음 입력란 바깥쪽을 클릭합니다.  
  
3.  **Product Sales**가 포함된 입력란을 선택합니다.  
  
4.  홈 탭 > **글꼴** 그룹 > **색**에서 **청록색**을 선택합니다.  
  
7.  **굵게**를 선택합니다.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Save"></a>9. 보고서 저장  
보고서 서버 또는 컴퓨터에 보고서를 저장합니다. 보고서를 보고서 서버에 저장하지 않을 경우 보고서 파트 및 하위 보고서와 같은 여러 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능을 사용할 수 없습니다.  
  
### <a name="to-save-the-report-on-a-report-server"></a>보고서를 보고서 서버에 저장하려면  
  
1.  **보고서 작성기** 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
2.  **최근에 사용한 사이트 및 서버**를 클릭합니다.  
  
3.  보고서를 저장할 수 있는 권한을 가진 보고서 서버의 이름을 선택하거나 입력합니다.  
  
    "보고서 서버에 연결하는 중"이라는 메시지가 나타납니다. 연결되면 보고서 서버 관리자가 보고서의 기본 위치로 지정한 보고서 폴더의 내용이 표시됩니다.  
  
4.  **이름**에서 기본 이름을 **Product Sales**로 바꿉니다.  
  
5.  **저장**을 클릭합니다.  
  
보고서가 보고서 서버에 저장됩니다. 연결된 보고서 서버의 이름이 창 아래쪽에 있는 상태 표시줄에 나타납니다.  
  
### <a name="to-save-the-report-on-your-computer"></a>컴퓨터에 보고서를 저장하려면  
  
1.  **보고서 작성기** 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
2.  **바탕 화면**, **내 문서**또는 **내 컴퓨터**를 클릭하여 보고서를 저장할 폴더를 찾습니다.  
  
3.  **이름**에서 기본 이름을 **Product Sales**로 바꿉니다.  
  
4.  **저장**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  

이것으로 스파크라인 차트가 있는 테이블 보고서를 만드는 자습서를 마칩니다. 스파크라인에 대한 자세한 내용은 [스파크라인 및 데이터 막대](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)를 참조하세요.  
  
[보고서 작성기 자습서](../reporting-services/report-builder-tutorials.md) 
[SQL Server 2016의 보고서 작성기](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
