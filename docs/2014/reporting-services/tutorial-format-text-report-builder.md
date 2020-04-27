---
title: '자습서: 텍스트 서식 지정(보고서 작성기) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 67d8513e-8a70-464b-b87f-e91d010cfd82
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dc58232ed3025063fb329392b58895ed667465f4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098899"
---
# <a name="tutorial-format-text-report-builder"></a>자습서: 텍스트 서식 지정(보고서 작성기)
  이 자습서에서는 텍스트에 서식을 지정하는 다양한 방법을 연습해 볼 수 있습니다. 빈 보고서와 함께 데이터 원본 및 데이터 세트을 설정한 후 탐색할 단계를 선택할 수 있습니다.  
  
 다음 그림에서는 만들려는 보고서와 비슷한 보고서를 보여 줍니다.  
  
 ![rs_FormatTextFinal](../../2014/tutorials/media/rs-formattextfinal.gif "rs_FormatTextFinal")  
  
 한 단계에서는 고의적으로 작업을 잘못 수행하므로 해당 작업이 잘못인 이유를 확인할 수 있습니다. 그런 다음 이를 올바르게 수정하여 원하는 결과를 얻을 수 있습니다.  
  
 이 자습서에서 만드는 향상된 버전의 보고서는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 보고서 작성기의 예제 보고서로 제공됩니다. 이 예제 보고서 및 기타 보고서를 다운로드하는 방법은 [보고서 작성기 예제 보고서(Report Builder sample reports)](https://go.microsoft.com/fwlink/?LinkId=184851)를 참조하십시오.  
  
##  <a name="what-you-will-learn"></a><a name="BackToTop"></a>학습 내용  
  
### <a name="set-up-the-report"></a>보고서 설정  
 1. [빈 보고서와 함께 데이터 원본 및 데이터 세트 만들기](#CreateReport)  
  
 2. [보고서 디자인 화면에 필드 추가(잘못 추가한 후 올바르게 추가)](#AddField)  
  
 3. [보고서 디자인 화면에 테이블 추가](#AddTable)  
  
### <a name="pick-and-choose"></a>선택  
 [보고서에 하이퍼링크 추가](#AddHyperlink)  
  
 [보고서의 텍스트 회전](#RotateText)  
  
 [HTML 서식을 사용하여 텍스트 표시](#FormatHTML)  
  
 [통화 서식 지정](#FormatCurrency)  
  
 [보고서 저장](#Save)  
  
 이 자습서에 소요되는 예상 시간: 20분  
  
## <a name="requirements"></a>요구 사항  
 요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/report-builder-tutorials.md)을 참조하세요.  
  
##  <a name="create-a-blank-report-with-a-data-source-and-dataset"></a><a name="CreateReport"></a>데이터 원본 및 데이터 집합을 사용 하 여 빈 보고서 만들기  
  
#### <a name="to-create-a-blank-report"></a>빈 보고서를 만들려면  
  
1.  **시작**을 클릭 하 고 **프로그램**, [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] **보고서 작성기**을 차례로 가리킨 다음 **보고서 작성기**를 클릭 합니다.  
  
    > [!NOTE]  
    >  **시작** 대화 상자가 나타나야 합니다. 이 대화 상자가 나타나지 않으면 보고서 작성기 단추에서 **새로 만들기**를 클릭합니다.  
  
2.  **시작** 대화 상자의 왼쪽 창에서 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **빈 보고서**를 클릭합니다.  
  
#### <a name="to-create-a-data-source"></a>데이터 원본을 만들려면  
  
1.  보고서 데이터 창에서 **새로 만들기**를 클릭 한 다음 **데이터 원본**을 클릭 합니다.  
  
2.  **이름** 상자에 **TextDataSource**를 입력합니다.  
  
3.  **내 보고서에 포함된 연결 사용**을 클릭합니다.  
  
4.  연결 형식이 Microsoft SQL Server인지 확인한 다음 **연결 문자열** 상자에 **Data Source = \<servername>** 을 입력합니다.  
  
    > [!NOTE]  
    >  \<서버 이름> (예:: report001))는 SQL Server 데이터베이스 엔진 인스턴스가 설치 된 컴퓨터를 지정 합니다. 이 자습서를 사용하기 위해 특정 데이터가 필요하지는 않습니다. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 데이터베이스에 연결하기만 하면 됩니다. **데이터 원본 연결**에 나열된 데이터 원본 연결이 이미 있는 경우 해당 데이터 원본 연결을 선택하고 다음 절차인 "데이터 세트를 만들려면"으로 이동할 수 있습니다. 자세한 내용은 [데이터에 연결하는 다른 방법&#40;보고서 작성기&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)를 참조하세요.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-create-a-dataset"></a>데이터 세트를 만들려면  
  
1.  보고서 데이터 창에서 **새로 만들기**를 클릭 한 다음 **데이터 집합**을 클릭 합니다.  
  
2.  데이터 원본이 **TextDataSource**인지 확인합니다.  
  
3.  **이름** 상자에 **TextDataset**를 입력합니다.  
  
4.  **텍스트** 쿼리 유형이 선택되어 있는지 확인한 다음 **쿼리 디자이너**를 클릭합니다.  
  
5.  **텍스트로 편집**을 클릭합니다.  
  
6.  쿼리 창에 다음 쿼리를 붙여 넣습니다.  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    ```  
  
7.  실행(**!**)을 클릭하여 쿼리를 실행합니다.  
  
     쿼리 결과는 보고서에 표시할 수 있는 데이터입니다.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="add-a-field-to-the-report-design-surface"></a><a name="AddField"></a>보고서에 필드 추가 Design Surface  
 데이터 세트의 필드가 보고서에 나타나도록 하려는 경우 먼저 해당 필드를 디자인 화면으로 직접 끌 수 있습니다. 이 연습에서는 이러한 방법이 올바르지 않은 이유와 대신 사용할 수 있는 방법을 보여 줍니다.  
  
#### <a name="to-add-a-field-to-the-report-and-get-the-wrong-result"></a>보고서에 필드를 추가하려면(잘못된 결과)  
  
1.  보고서 데이터 창의 **FullName** 필드를 디자인 화면으로 끌어옵니다.  
  
     보고서 작성기 Expr>으로 \<표시 되는 식을 사용 하 여 입력란을 만듭니다.  
  
2.  **실행**을 클릭합니다.  
  
     쿼리의 첫 번째 레코드 **김철수 Ross**레코드는 하나 뿐입니다. 즉, 이 필드가 반복되어 해당 필드의 다른 레코드가 표시되지 않습니다.  
  
3.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
4.  텍스트 상자에서 \<식> 식을 선택 합니다.  
  
5.  **값** 속성에 대한 속성 창에서 다음을 확인합니다. 속성 창이 표시되지 않으면 **보기** 탭에서 **속성**을 선택합니다.  
  
    ```  
    =First(Fields!FullName.Value, "TextDataSet")  
    ```  
  
     `First` 함수는 필드의 첫 번째 값만 검색하도록 디자인되었으므로 첫 번째 값만 검색되었습니다.  
  
     필드를 디자인 화면으로 직접 끌어 올 때 입력란이 만들어졌습니다. 입력란 자체는 데이터 영역이 아니므로 보고서 데이터 세트의 데이터가 표시되지 않습니다. 테이블, 행렬 및 목록과 같은 데이터 영역의 입력란에는 데이터가 표시됩니다.  
  
6.  입력란을 선택하고 Delete 키를 누릅니다. 식이 선택된 경우 입력란을 선택하려면 Esc 키를 누릅니다.  
  
#### <a name="to-add-a-field-to-the-report-and-get-the-right-result"></a>보고서에 필드를 추가하려면(올바른 결과)  
  
1.  리본의 **삽입** 탭에 있는 **데이터 영역** 영역에서 **목록**을 클릭합니다. 디자인 화면을 클릭한 다음 끌어서 약 2인치 너비와 1인치 높이의 상자를 만듭니다.  
  
2.  보고서 데이터 창의 **FullName** 필드를 목록 상자로 끌어옵니다.  
  
     이번에는 보고서 작성기에서 `[FullName]` 식이 있는 입력란이 만들어집니다.  
  
3.  **실행**을 클릭합니다.  
  
     이번에는 입력란이 반복되어 쿼리의 모든 레코드가 표시됩니다.  
  
4.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
5.  입력란에서 식을 선택합니다.  
  
6.  **값** 속성에 대한 속성 창에서 다음을 확인합니다.  
  
    ```  
    =Fields!FullName.Value  
    ```  
  
     입력란을 목록 데이터 영역으로 끌어 데이터 세트에 있는 데이터를 표시합니다.  
  
7.  목록 상자를 선택하고 Delete 키를 누릅니다.  
  
##  <a name="add-a-table-to-the-report-design-surface"></a><a name="AddTable"></a>보고서에 테이블을 추가 Design Surface  
 하이퍼링크와 회전된 텍스트를 배치할 수 있도록 테이블을 만듭니다.  
  
#### <a name="to-add-a-table-to-the-report"></a>보고서에 테이블을 추가하려면  
  
1.  **삽입** 메뉴에서 **테이블**을 클릭 한 다음 **테이블 마법사**를 클릭 합니다.  
  
2.  새 테이블 또는 행렬 마법사의 **데이터 집합 선택** 페이지에서 **이 보고서 또는 공유 데이터 집합의 기존 데이터 집합 선택**을 클릭 하 고 **textdataset (이 보고서)** 를 클릭 한 후 **다음**을 클릭 합니다.  
  
3.  **필드 정렬** 페이지에서 **지역**, **t**및 **Product** 필드를 **행 그룹**으로 끌고 **Sales** 필드를 **값**으로 끈 후 **다음**을 클릭 합니다.  
  
4.  **레이아웃 선택** 페이지에서 전체 테이블을 볼 수 있도록 **그룹 확장/축소** 확인란의 선택을 취소 하 고 **다음**을 클릭 합니다.  
  
5.  **스타일 선택** 페이지에서 **슬레이트**를 클릭 한 다음 **마침**을 클릭 합니다.  
  
6.  테이블을 끌어 제목 블록 아래에 배치합니다.  
  
7.  **실행**을 클릭합니다.  
  
     테이블에 이상이 없어 보이지만 두 개의 합계 행이 있습니다. **T** 필드에는 합계 행이 필요 하지 않습니다.  
  
8.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
9. 이 들어 `[LinkText]`있는 입력란을 마우스 오른쪽 단추로 클릭 하 고 **셀 분할**을 클릭 합니다.  
  
10. `[LinkText]` 셀 아래의 빈 셀을 선택한 다음 shift 키를 누른 상태로 오른쪽에 있는 두 셀을 선택 합니다. **Product** 열의 **합계** 셀과 **Sales** 열의 `[Sum(Sales)]` 셀을 선택 합니다.  
  
11. 이 세 개의 셀을 선택한 상태에서 해당 셀 중 하나를 마우스 오른쪽 단추로 클릭 하 고 **행 삭제**를 클릭 합니다.  
  
12. **실행**을 클릭합니다.  
  
##  <a name="add-a-hyperlink-to-the-report"></a><a name="AddHyperlink"></a>보고서에 하이퍼링크 추가  
 이 섹션에서는 이전 섹션의 테이블에 있는 텍스트에 하이퍼링크를 추가합니다.  
  
#### <a name="to-add-a-hyperlink-to-the-report"></a>보고서에 하이퍼링크를 추가하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  `[LinkText]`가 들어 있는 셀을 마우스 오른쪽 단추로 클릭하고 **입력란 속성**을 클릭합니다.  
  
3.  **텍스트 상자 속성** 상자에서 **동작**을 클릭 합니다.  
  
4.  **URL로 이동을**클릭 합니다.  
  
5.  **Url 선택** 상자에서 **[url]** 을 클릭 한 다음 **확인**을 클릭 합니다.  
  
6.  텍스트가 다르게 표시되지 않습니다. 텍스트가 링크 텍스트처럼 표시되도록 해야 합니다.  
  
7.  `[LinkText]`를 선택합니다.  
  
8.  **홈** 탭의 **글꼴** 섹션에서 **밑줄** 단추를 클릭 하 고 **색** 단추 옆에 있는 드롭다운 화살표를 클릭 한 다음 **Blue**를 클릭 합니다.  
  
9. **실행**을 클릭합니다.  
  
     이제 텍스트가 링크처럼 표시됩니다.  
  
10. 링크를 클릭합니다. 컴퓨터가 인터넷에 연결되어 있으면 보고서 작성기 도움말 항목이 브라우저에서 열립니다.  
  
##  <a name="rotate-text-in-the-report"></a><a name="RotateText"></a>보고서의 텍스트 회전  
 이 섹션에서는 이전 섹션의 테이블에 있는 텍스트 일부를 회전합니다.  
  
#### <a name="to-rotate-text"></a>텍스트를 회전하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  가 들어 있는 셀을 클릭합니다.(!!) `[Territory].`  
  
3.  **홈** 탭의 **글꼴** 섹션에서 **굵게** 단추를 클릭합니다.  
  
4.  속성 창이 열려 있지 않으면 **보기** 탭에서 **속성** 확인란을 선택합니다.  
  
5.  속성 창에서 WritingMode 속성을 찾습니다.  
  
    > [!NOTE]  
    >  속성 창의 속성이 범주로 구성되어 있는 경우 WritingMode는 **지역화** 범주에 있습니다. 셀만 선택하고 텍스트는 선택하지 말아야 합니다. WritingMode는 텍스트가 아니라 입력란의 속성입니다.  
  
6.  목록 상자에서 **Rotate270**를 클릭 합니다.  
  
7.  **단락** 섹션의 **홈** 탭에서 **가운데** 및 **가운데** 단추를 클릭 하 여 셀 가운데에서 세로 및 가로로 가운데에 있는 텍스트를 찾습니다.  
  
8.  실행 (**!**)을 클릭합니다.  
  
 이제 `[Territory]` 셀에 있는 텍스트가 셀의 아래쪽에서 위쪽으로 세로로 움직입니다.  
  
##  <a name="displaying-text-with-html-formatting"></a><a name="FormatHTML"></a>HTML 서식을 사용 하 여 텍스트 표시  
  
#### <a name="to-display-text-formatted-as-html"></a>HTML로 서식이 지정된 텍스트를 표시하려면  
  
1.  디자인 **을 클릭 하 여 디자인** 뷰로 전환 합니다.  
  
2.  **삽입** 탭에서 **입력란**을 클릭하고 디자인 화면에서 마우스 단추를 클릭한 다음 끌어서 테이블 아래에 약 4인치 너비와 3인치 높이의 입력란을 만듭니다.  
  
3.  이 텍스트를 복사하여 입력란에 붙여 넣습니다.  
  
    ```  
    <h4>Limitations of cascading style sheet attributes</h4>  
          <p>Only a basic set of <b>cascading style sheet (CSS)</b> attributes are defined:</p>  
          <ul><li>  
              text-align, text-indent  
            </li><li>  
              font-family, font-size  
            </li><li>  
              color  
            </li><li>  
              padding, padding-bottom, padding-top, padding-right, padding-left  
            </li><li>  
              font-weight  
            </li></ul>  
    ```  
  
4.  입력란의 모든 텍스트를 선택합니다.  
  
     이 속성은 입력란이 아니라 텍스트의 속성이므로 하나의 입력란에서 일반 텍스트와 HTML 태그를 스타일로 사용하는 텍스트가 혼합된 형태를 사용할 수 있습니다.  
  
5.  선택한 모든 텍스트를 마우스 오른쪽 단추로 클릭하고 **텍스트 속성**을 클릭합니다.  
  
6.  **일반** 페이지의 **태그 형식**에서 **html-Html 태그를 스타일로 해석**을 클릭 합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  실행(**!**)을 클릭하여 보고서를 미리 봅니다.  
  
 입력란의 텍스트가 머리글, 단락 및 글머리 기호 목록으로 표시됩니다.  
  
##  <a name="format-currency"></a><a name="FormatCurrency"></a>통화 형식 지정  
  
#### <a name="to-format-numbers-as-currency"></a>숫자를 통화 서식으로 지정하려면  
  
1.  디자인 **을 클릭 하 여 디자인** 뷰로 전환 합니다.  
  
2.  `[Sum(Sales)]`이 들어 있는 위쪽 테이블 셀을 클릭하고 Shift 키를 누른 상태로 `[Sum(Sales)]`이 들어 있는 아래쪽 테이블 셀을 클릭합니다.  
  
3.  **홈** 탭의 **숫자** 그룹에서 **통화** 단추를 클릭합니다.  
  
4.  필드 **홈** 탭의 **숫자** 그룹에서 **자리 표시자 스타일** 단추를 클릭 하 고 **샘플 값** 을 클릭 하 여 숫자의 서식을 지정 하는 방법을 확인 합니다.  
  
5.  (옵션) **홈** 탭에 있는 **숫자** 그룹에서 **소수 자릿수 줄이기** 단추를 두 번 클릭하여 센트가 표시되지 않는 달러 숫자를 표시합니다.  
  
6.  실행(**!**)을 클릭하여 보고서를 미리 봅니다.  
  
 이제 보고서에 서식이 지정된 데이터가 표시되므로 보다 쉽게 읽을 수 있습니다.  
  
##  <a name="save-the-report"></a><a name="Save"></a>보고서 저장  
 보고서를 보고서 서버, SharePoint 라이브러리 또는 컴퓨터에 저장할 수 있습니다.  
  
 이 자습서에서는 보고서를 보고서 서버에 저장합니다. 보고서 서버에 액세스할 수 없는 경우에는 보고서를 컴퓨터에 저장하십시오.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>보고서를 보고서 서버에 저장하려면  
  
1.  **보고서 작성기** 단추에서 다른 **이름으로 저장**을 클릭 합니다.  
  
2.  **최근에 사용한 사이트 및 서버**를 클릭합니다.  
  
3.  보고서를 저장할 수 있는 권한을 가진 보고서 서버의 이름을 선택하거나 입력합니다.  
  
     "보고서 서버에 연결하는 중"이라는 메시지가 나타납니다. 연결되면 보고서 서버 관리자가 보고서의 기본 위치로 지정한 보고서 폴더의 내용이 표시됩니다.  
  
4.  **이름**에서 기본 이름을 선택한 이름으로 대체합니다.  
  
5.  **저장**을 클릭합니다.  
  
 보고서가 보고서 서버에 저장됩니다. 연결된 보고서 서버의 이름이 창 아래쪽에 있는 상태 표시줄에 나타납니다.  
  
#### <a name="to-save-the-report-on-your-computer"></a>컴퓨터에 보고서를 저장하려면  
  
1.  **보고서 작성기** 단추에서 다른 **이름으로 저장**을 클릭 합니다.  
  
2.  **바탕 화면**, **내 문서**또는 **내 컴퓨터**를 클릭한 다음 보고서를 저장할 폴더를 찾습니다.  
  
3.  **이름**에서 기본 이름을 선택한 이름으로 대체합니다.  
  
4.  **저장**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
 보고서 작성기 자습서에서 텍스트의 서식을 지정 하는 방법에는 여러 가지가 있습니다. &#40;보고서 작성기&#41;추가 예제를 포함 하는 [자유 형식 보고서를 만듭니다](../reporting-services/tutorial-creating-a-free-form-report-report-builder.md) .  
  
## <a name="see-also"></a>참고 항목  
 [자습서 &#40;보고서 작성기&#41;](report-builder-tutorials.md)   
 [보고서 항목 서식 지정 &#40;보고서 작성기 및 SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [SQL Server 2014의 보고서 작성기](report-builder/report-builder-in-sql-server-2016.md)  
  
  
