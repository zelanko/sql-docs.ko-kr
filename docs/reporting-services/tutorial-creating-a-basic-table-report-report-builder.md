---
title: '자습서: 기본 테이블 보고서 만들기(보고서 작성기) | Microsoft Docs'
ms.date: 06/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: d9e30521-f8ae-4c45-89c3-d40727f622f7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5a97a0cfc446a32e02172d22391dec8e5ca13af6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63041207"
---
# <a name="tutorial-creating-a-basic-table-report-report-builder"></a>자습서: 기본 테이블 보고서 만들기(보고서 작성기)
이 자습서에서는 예제 판매 데이터를 기반으로 기본 테이블 보고서를 만드는 방법을 배웁니다. 다음 그림에서는 만들려는 보고서를 보여 줍니다.  
  
![SSRS_Tutorial_Basic_Table_Report](../reporting-services/media/ssrs-tutorial-basic-table-report.png)  
  

이 자습서에 소요되는 예상 시간: 20분  
  
## <a name="requirements"></a>요구 사항  
요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)을 참조하세요.  
  
## <a name="CreateTable"></a>1. 마법사를 사용하여 보고서 만들기  
테이블 또는 행렬 마법사를 사용하여 테이블 보고서를 만듭니다. 보고서 디자인 모드와 공유 데이터 세트 디자인 모드라는 두 가지 모드가 있습니다. 보고서 디자인 모드에서는 보고서 데이터 창에서 데이터를 지정하고 디자인 화면에서 보고서 레이아웃을 지정합니다. 공유 데이터 세트 디자인 모드에서는 다른 사용자와 공유할 데이터 세트 쿼리를 만듭니다. 이 자습서에서는 보고서 디자인 모드를 사용합니다.  
  
### <a name="to-create-a-report"></a>보고서를 만들려면  
  
1.  컴퓨터,[웹 포털 또는 SharePoint 통합 모드에서](../reporting-services/report-builder/start-report-builder.md) 보고서 작성기를 시작 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 합니다.  
  
    **새 보고서 또는 데이터 세트** 대화 상자가 열립니다.  
  
    **새 보고서 또는 데이터 세트** 대화 상자가 표시되지 않는 경우 **파일** 메뉴 &gt; **새로 만들기**를 클릭합니다.  
  
2.  왼쪽 창에 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **테이블 또는 행렬 마법사**를 선택합니다.  
  
## <a name="DataConnection"></a>1a. 테이블 마법사에서 데이터 연결 지정  
데이터 연결은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스와 같은 외부 데이터 원본에 연결하는 데 필요한 정보를 포함합니다. 일반적으로 데이터 원본 소유자로부터 사용할 자격 증명 유형과 연결 정보를 가져옵니다. 데이터 연결을 지정하기 위해 보고서 서버의 공유 데이터 원본을 사용하거나 이 보고서에만 사용되는 포함된 데이터 원본을 만들 수 있습니다.  
  
이 자습서에서는 포함된 데이터 원본을 사용합니다. 공유 데이터 원본 사용 방법에 대한 자세한 내용은 [데이터에 연결하는 다른 방법&#40;보고서 작성기&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)을 참조하세요.  
  
### <a name="to-create-an-embedded-data-source"></a>포함된 데이터 원본을 만들려면  
  
1.  **데이터 세트 선택** 페이지에서 **데이터 세트 만들기**를 선택한 후, **다음**을 클릭합니다. **데이터 원본에 대한 연결 선택** 페이지가 열립니다.  
  
2.  **새로 만들기**를 클릭합니다. **데이터 원본 속성** 대화 상자가 열립니다.  
  
3.  **이름**에 데이터 원본의 이름인 **Product Sales** 를 입력합니다.  
  
4.  **연결 유형 선택**에서 **Microsoft SQL Server** 가 선택되어 있는지 확인합니다.  
  
5.  **연결 문자열**에 다음 텍스트를 입력합니다. 여기서 \<servername>은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.  
  
    ```  
    Data Source=<servername>  
    ```  
  
    데이터베이스에서 데이터를 검색하는 대신 데이터가 포함된 쿼리를 사용하기 때문에 연결 문자열에 데이터베이스 이름은 포함되어 있지 않습니다. 자세한 내용은 [자습서의 사전 요구 사항 &#40;보고서 작성기&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)를 참조하세요.  
  
6.  **자격 증명** 탭을 클릭합니다. 외부 데이터 원본에 액세스하는 데 필요한 자격 증명을 입력합니다.  
  
7. 일반 탭을 다시 클릭합니다. 데이터 원본에 연결할 수 있는지 확인하려면 **연결 테스트**를 클릭합니다.  
  
    "연결되었습니다."라는 메시지가 나타납니다.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    새 데이터베이스가 선택되어 있는 **데이터 원본에 대한 연결 선택** 페이지로 돌아갑니다.  
  
9. **다음**을 클릭합니다.  
  
## <a name="Query"></a>1b. 테이블 마법사에서 쿼리 만들기  
보고서에서는 미리 정의된 쿼리가 포함된 공유 데이터 세트를 사용하거나 이 보고서 하나에만 사용할 포함된 데이터 세트를 만들 수 있습니다. 이 자습서에서는 포함된 데이터 세트를 만듭니다.  
  
> [!NOTE]  
> 이 자습서의 쿼리에는 데이터 값이 포함되어 있으므로 외부 데이터 원본이 필요하지 않습니다. 따라서 쿼리가 상당히 길어집니다. 비즈니스 환경에서는 쿼리에 데이터가 포함되지 않을 것입니다. 이 자습서의 쿼리는 학습용으로만 제공됩니다.  
  
### <a name="to-create-a-query"></a>쿼리를 만들려면  
  
1.  **쿼리 디자인** 페이지에 관계형 쿼리 디자이너가 열립니다. 이 자습서에서는 텍스트 기반 쿼리 디자이너를 사용합니다.  
  
    **텍스트로 편집**을 클릭합니다. 텍스트 기반 쿼리 디자이너에 쿼리 창과 결과 창이 표시됩니다.  
  
2.  빈 위쪽 상자에 다음 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리를 붙여넣습니다.  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(9924.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
  
    ```  
  
3.  쿼리 디자이너 도구 모음에서 **실행** ( **!** )을 클릭합니다.  
  
    쿼리가 실행되고 SalesDate, Subcategory, Product, Sales 및 Quantity 필드에 대한 결과 집합이 표시됩니다.  
  
    결과 집합의 열 제목은 쿼리에 있는 이름을 기반으로 합니다. 데이터 세트의 열 제목은 필드 이름이 되며 보고서에 저장됩니다. 마법사를 완료한 후 보고서 데이터 창에서 데이터 세트 필드 모음을 볼 수 있습니다.  
  
4.  **다음**을 클릭합니다.  
  
## <a name="Groups"></a>1c. 테이블 마법사에서 데이터를 그룹으로 구성  
그룹화할 필드를 선택할 때 세부 데이터와 집계 데이터가 표시되는 행과 열이 포함된 테이블을 디자인합니다.  
  
### <a name="to-organize-data-into-groups"></a>데이터를 그룹으로 구성하려면  
  
1.  **필드 정렬** 페이지에서 **값**에 Product를 끌어옵니다.  
  
2.  **값** 의 Product 아래에 Quantity를 끌어옵니다.  
  
    Quantity는 숫자 필드에 대한 기본 집계 함수인 Sum 함수를 통해 자동으로 집계됩니다. 값은 [Sum(Quantity)]입니다.  
  
    [Sum(Quantity)] 옆의 화살표를 선택하여 사용 가능한 다른 집계 함수를 봅니다. 집계 함수를 변경하지 마십시오.  
  
3.  **값** 의 [Sum(Quantity)] 아래에 Sales를 끌어옵니다.  
  
    Sales는 Sum 함수로 집계됩니다. 값은 [Sum(Sales)]입니다.  
  
    1, 2, 3단계에서는 테이블에 표시할 데이터를 지정했습니다.  
  
4.  **행 그룹**에 SalesDate를 끌어옵니다.  
  
5.  **행 그룹** 의 SalesDate 아래에 Subcategory를 끌어옵니다.  
  
    4, 5단계에서는 필드 값을 먼저 날짜 기준으로 정렬한 다음 해당 날짜의 제품 하위 범주를 기준으로 정렬했습니다.  
  
6.  **다음**을 클릭합니다.  
  
## <a name="Subtotals"></a>1d. 테이블 마법사에서 부분합 및 합계 행 추가  
그룹을 만든 후 필드에 대한 집계 값을 표시할 행을 추가하고 행 서식을 지정할 수 있습니다. 모든 데이터를 표시할지 또는 사용자가 그룹화된 데이터를 대화형으로 확장하거나 축소할 수 있도록 할지 여부를 선택할 수 있습니다.  
  
### <a name="to-add-subtotals-and-totals"></a>부분합 및 합계를 추가하려면  
  
1.  **레이아웃 선택** 페이지의 **옵션**에서 **부분합 및 총합계 표시** 가 선택되어 있는지 확인합니다.  
  
2.  **블록형, 부분합 하단 표시** 가 선택되어 있는지 확인합니다.  
  
    마법사 미리 보기 창에 5개의 행이 있는 테이블이 표시됩니다. 보고서를 실행하면 각 행이 다음과 같은 방식으로 표시됩니다.  
  
    1.  첫 번째 행은 열 제목을 보여 주기 위해 테이블에 대해 한 번씩 반복됩니다.  
  
    2.  두 번째 행은 판매 주문의 각 품목에 대해 한 번씩 반복되고 제품 이름, 주문 수량 및 라인 합계를 표시합니다.  
  
    3.  세 번째 행은 주문당 부분합을 표시하기 위해 각 판매 주문에 대해 한 번씩 반복됩니다.  
  
    4.  네 번째 행은 일별 부분합을 표시하기 위해 각 주문 날짜에 대해 한 번씩 반복됩니다.  
  
    5.  다섯 번째 행은 총합계를 표시하기 위해 테이블에 대해 한 번씩 반복됩니다.  
  
3.  **그룹 확장/축소**옵션을 선택 취소합니다. 이 자습서에서 만든 보고서에는 부모 그룹 계층을 확장하여 자식 그룹 행 및 정보 행을 표시하는 데 사용할 수 있는 드릴다운 기능이 사용되지 않습니다.  
  
4.  **다음** 을 클릭하여 테이블을 미리 본 다음 **마침**을 클릭합니다.  
  
디자인 화면에 테이블이 추가됩니다. 이 테이블에는 열 5개와 행 5개가 있습니다. 행 그룹 창에는 SalesDate, Subcategory 및 Details라는 3개의 행 그룹이 표시됩니다. 세부 데이터는 모두 데이터 세트 쿼리로 검색된 데이터입니다.  
  
## <a name="FormatCurrency"></a>2. 데이터 형식을 통화로 지정  
기본적으로 Sales 필드의 요약 데이터에는 일반 숫자가 표시됩니다. 서식을 지정하여 숫자가 통화로 표시되도록 합니다.   
  
### <a name="to-format-a-currency-field"></a>통화 필드의 서식을 지정하려면  
  
1.  디자인 뷰에서 서식 있는 입력란과 자리 표시자 텍스트를 샘플 값으로 확인하려면 **홈** 탭의 **숫자** 그룹에서 **자리 표시자 스타일** 아이콘 옆의 화살표 > **샘플 값**을 클릭합니다.  
  
2.   Sales 열에서 두 번째 행(열 제목 행 아래)의 셀을 클릭하고 아래쪽으로 끌어서 `[Sum(Sales)]`이 포함된 모든 셀을 선택합니다.  
  
3.  **홈** 탭의 **숫자** 그룹에서 **통화** 단추를 클릭합니다. 셀이 변경되어 형식 지정된 통화가 표시됩니다.  
  
    국가별 설정이 영어(미국)인 경우 기본 예제 텍스트는 [ **$12,345.00**]입니다. 예제 통화 값이 표시되지 않는 경우 **홈** 탭의 **숫자** 그룹에서 **자리 표시자 스타일** 아이콘 옆의 화살표 > **샘플 값**을 클릭합니다.  
  
4.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
Sales의 요약 값이 통화로 표시됩니다.  
  
## <a name="FormatDate"></a>3. 데이터 형식을 날짜로 지정  
기본적으로 SalesDate 필드에는 날짜 및 시간이 표시됩니다. 날짜만 표시되도록 서식을 지정할 수 있습니다.  
  
### <a name="to-format-a-date-field-as-the-default-format"></a>날짜 필드를 기본 형식으로 지정하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  `[SalesDate]`가 들어 있는 셀을 클릭합니다.  
  
3.  리본의 **홈** 탭에 있는 **숫자** 그룹에서 화살표를 클릭하고 **날짜**를 선택합니다.  
  
    셀에 예제 날짜 **[1/31/2000]** 이 표시됩니다. 예제 날짜가 표시되지 않는 경우 **홈** 탭의 **숫자** 그룹에서 **자리 표시자 스타일** 아이콘 옆의 화살표 > **샘플 값**을 클릭합니다.  
  
4.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
SalesDate 값이 기본 날짜 형식으로 표시됩니다.  
  
### <a name="to-change-the-date-format-to-a-custom-format"></a>날짜 형식을 사용자 지정 형식으로 변경하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  `[SalesDate]`가 들어 있는 셀을 선택합니다.  
  
3.  **홈** 탭의 **숫자** 그룹에서 오른쪽 아래에 있는 화살표를 클릭하여 대화 상자를 엽니다.  
  
    **입력란 속성** 대화 상자가 열립니다.  
  
4.  범주 창에서 **날짜** 가 선택되어 있는지 확인합니다.  
  
5.  **유형** 창에서 **January 31, 2000**을 선택합니다.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    셀에 예제 날짜 **[January 31, 2000]** 이 표시됩니다.  
  
7.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
SalesDate 값이 월에 해당하는 숫자 대신 월 이름을 표시합니다.  
  
## <a name="Width"></a>4. 열 너비 변경  
기본적으로 테이블의 각 셀은 입력란을 포함합니다. 페이지를 렌더링하면 입력란은 텍스트를 수용하도록 세로로 확장됩니다. 렌더링된 보고서에서 각 행은 해당 행에서 가장 길게 렌더링된 입력란의 높이에 맞춰 확장됩니다. 디자인 화면에서 행의 높이는 렌더링된 보고서의 행 높이에 영향을 주지 않습니다.  
  
각 행의 세로 크기를 줄이려면 열 입력란에 들어갈 예상 내용이 한 줄에 수용되는 범위에서 열 너비를 확장합니다.  
  
### <a name="to-change-the-width-of-table-columns"></a>테이블 열의 너비를 변경하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  테이블을 클릭하여 열 핸들과 행 핸들이 테이블 위와 옆에 표시되도록 합니다.  
  
    테이블 위쪽 및 옆쪽을 따라 표시되는 회색 막대는 행 및 열 핸들입니다.  
  
3.  열 핸들 사이의 선에 커서를 두면 커서가 양방향 화살표로 바뀝니다. 열을 끌어 너비를 원하는 대로 조정합니다. 예를 들어 제품 이름이 한 줄에 표시되도록 제품에 대한 열을 확장합니다.  
  
4.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
## <a name="Title"></a>5. 보고서 제목 추가  
보고서 제목은 보고서 맨 위에 나타납니다. 보고서 제목을 보고서 머리글에 배치하거나, 보고서 머리글이 사용되지 않을 경우 보고서 본문의 맨 위에 있는 입력란에 배치할 수 있습니다. 이 자습서에서는 보고서 본문의 맨 위에 자동으로 표시되는 입력란을 사용합니다.  
  
글꼴 스타일, 크기 및 색을 텍스트의 각 문자나 구 단위로 다르게 적용하여 더 보기 좋게 꾸밀 수 있습니다. 자세한 내용은 [입력란의 텍스트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)을 참조하세요.  
  
### <a name="to-add-a-report-title"></a>보고서 제목을 추가하려면  
  
1.  디자인 화면에서 **제목을 추가하려면 클릭하십시오.** 를 클릭합니다.  
  
2.  **Product Sales**를 입력한 다음 입력란 바깥쪽을 클릭합니다.  
  
3.  **Product Sales** 가 들어 있는 입력란을 마우스 오른쪽 단추로 클릭하고 **입력란 속성**을 클릭합니다.  
  
4.  **입력란 속성** 대화 상자에서 **글꼴**을 클릭합니다.  
  
5.  **크기** 목록에서 **18pt**를 선택합니다.  
  
6.  **색** 목록에서 **수레국화 청색**을 선택합니다.  
  
7.  **굵게**를 선택합니다.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Save"></a>6. 보고서 저장  
보고서 서버 또는 컴퓨터에 보고서를 저장합니다. 보고서를 보고서 서버에 저장하지 않을 경우 보고서 파트 및 하위 보고서와 같은 여러 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능을 사용할 수 없습니다.  
  
### <a name="to-save-the-report-on-a-report-server"></a>보고서를 보고서 서버에 저장하려면  
  
1.  **파일** > **다른 이름으로 저장**을 클릭합니다.  
  
2.  **최근에 사용한 사이트 및 서버**를 클릭합니다.  
  
3.  보고서를 저장할 수 있는 권한을 가진 보고서 서버의 이름을 선택하거나 입력합니다.  
  
    "보고서 서버에 연결하는 중"이라는 메시지가 나타납니다. 연결되면 보고서 서버 관리자가 보고서의 기본 위치로 지정한 보고서 폴더의 내용이 표시됩니다.  
  
4.  **이름**에서 **제목 없음** 을 **Product_Sales**로 바꿉니다.  
  
5.  **저장**을 클릭합니다.  
  
보고서가 보고서 서버에 저장됩니다. 연결된 보고서 서버의 이름이 창 아래쪽에 있는 상태 표시줄에 나타납니다.  
  
### <a name="to-save-the-report-on-your-computer"></a>컴퓨터에 보고서를 저장하려면  
  
1.  **파일** > **다른 이름으로 저장**을 클릭합니다.  
  
2.  **바탕 화면**, **내 문서**또는 **내 컴퓨터**를 클릭하여 보고서를 저장할 폴더를 찾습니다.  
  
3.  **이름**에서 **제목 없음** 을 **Product Sales**로 바꿉니다.  
  
4.  **저장**을 클릭합니다.  
  
## <a name="Export"></a>7. 보고서 내보내기  
보고서는 Microsoft Excel 및 CSV(쉼표로 구분된 값) 파일과 같은 여러 형식으로 내보낼 수 있습니다. 자세한 내용은 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)에서 페이지 매김을 제어하는 데 사용되는 규칙을 이해해야 합니다.  
  
이 자습서에서는 보고서를 Excel로 내보내고 보고서에 속성을 설정하여 통합 문서 탭 이름을 사용자 지정합니다.  
  
### <a name="to-specify-the-workbook-tab-name"></a>통합 문서 탭 이름을 지정하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  디자인 화면에서 보고서 바깥쪽의 아무 곳이나 클릭합니다.  
  
3.  속성 창에서 InitialPageName 속성을 찾아 **Product Sales Excel**을 입력합니다.  
  
    > [!NOTE]  
    > 속성 창이 표시되지 않으면 **보기** 탭에서 **속성**을 선택합니다.  
    > 속성 창에 속성이 표시되지 않는 경우 창의 맨 위에 있는 **사전순** 단추를 선택하여 모든 속성을 사전순으로 정렬해 보세요.   
  
### <a name="to-export-a-report-to-excel"></a>보고서를 Excel로 내보내려면  
  
1.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
2.  리본에서 **내보내기** > **Excel**을 클릭합니다.  
  
    이 열립니다.  
  
3.  **다른 이름으로 저장** 대화 상자에서 파일을 저장할 위치를 찾습니다.  
  
4.  **파일 이름** 상자에 **Product_Sales_Excel**을 입력합니다.  
  
5.  파일 형식이 **Excel(\*.xls)** 인지 확인합니다.  
  
6.  **저장**을 클릭합니다.  
  
### <a name="to-view-the-report-in-excel"></a>Excel에서 보고서를 보려면  
  
1.  통합 문서를 저장한 폴더를 열고 **Product_Sales_Excel.xlsx**를 두 번 클릭합니다.  
  
2.  통합 문서 탭의 이름이 **Product Sales Excel**인지 확인합니다.  
  
## <a name="next-steps"></a>Next Steps  
이것으로 기본 테이블 보고서를 만드는 방법에 대한 연습을 마칩니다. 테이블에 대한 자세한 내용은 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[보고서 작성기 자습서](../reporting-services/report-builder-tutorials.md)  
[SQL Server의 보고서 작성기](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

