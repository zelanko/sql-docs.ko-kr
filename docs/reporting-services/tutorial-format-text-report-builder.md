---
title: '자습서: 텍스트 서식 지정(보고서 작성기) | Microsoft Docs'
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 67d8513e-8a70-464b-b87f-e91d010cfd82
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 42d55cf53d282b2c092769cf4435fd240ba0cbce
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579343"
---
# <a name="tutorial-format-text-report-builder"></a>자습서: 텍스트 서식 지정(보고서 작성기)

이 자습서에서는 페이지가 매겨진 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 보고서의 텍스트에 서식을 지정하는 다양한 방법을 연습합니다. 다양한 서식을 실험할 수 있습니다. 

빈 보고서와 함께 데이터 원본 및 데이터 세트를 설정한 후 탐색할 서식을 선택할 수 있습니다. 다음 그림에서는 만들려는 보고서와 비슷한 보고서를 보여 줍니다.  
  
![report-build-format-report](../reporting-services/media/report-build-format-report.png) 
  
한 단계에서는 고의적으로 작업을 잘못 수행하므로 해당 작업이 잘못인 이유를 확인할 수 있습니다. 그런 다음 이를 올바르게 수정하여 원하는 결과를 얻을 수 있습니다.  
    
이 자습서에 소요되는 예상 시간: 20분  
  
## <a name="requirements"></a>요구 사항  
요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)을 참조하세요.  
  
## <a name="CreateReport"></a>빈 보고서와 함께 데이터 원본 및 데이터 세트 만들기  
  
### <a name="to-create-a-blank-report"></a>빈 보고서를 만들려면  
  
1.  컴퓨터,[웹 포털 또는 SharePoint 통합 모드에서](../reporting-services/report-builder/start-report-builder.md) 보고서 작성기를 시작 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 합니다.  
  
    **새 보고서 또는 데이터 세트** 대화 상자가 열립니다.  
  
    **새 보고서 또는 데이터 세트** 대화 상자가 표시되지 않는 경우 **파일** 메뉴 &gt; **새로 만들기**를 클릭합니다.  
 
2.  **시작** 대화 상자의 왼쪽 창에서 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **빈 보고서**를 클릭합니다.  
  
### <a name="to-create-a-data-source"></a>데이터 원본을 만들려면  
  
1.  보고서 데이터 창에서 **새로 만들기** > **데이터 원본**을 클릭합니다.  

    **보고서 데이터** 창이 표시되지 않는 경우 **보기** 탭에서 **보고서 데이터**를 선택합니다.
  
2.  **이름** 상자에 **TextDataSource**를 입력합니다.  
  
3.  **내 보고서에 포함된 연결 사용**을 클릭합니다.  
  
4.  연결 형식이 Microsoft SQL Server인지 확인한 다음 **연결 문자열** 상자에 다음을 입력합니다. `Data Source = <servername>`  
  
    > [!NOTE]  
    > `<servername>`식(예: Report001)은 SQL Server 데이터베이스 엔진의 인스턴스가 설치된 컴퓨터를 지정합니다. 이 자습서를 사용하기 위해 특정 데이터가 필요하지는 않습니다. SQL Server 데이터베이스에 연결하기만 하면 됩니다. **데이터 원본 연결**에 나열된 데이터 원본 연결이 이미 있는 경우 해당 데이터 원본 연결을 선택하고 다음 절차인 "데이터 세트를 만들려면"으로 이동할 수 있습니다. 자세한 내용은 [데이터에 연결하는 다른 방법&#40;보고서 작성기&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)를 참조하세요.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-create-a-dataset"></a>데이터 세트를 만들려면  
  
1.  보고서 데이터 창에서 **새로 만들기** > **데이터 집합**을 클릭합니다.  
  
2.  데이터 원본이 **TextDataSource**인지 확인합니다.  
  
3.  **이름** 상자에 **TextDataset**를 입력합니다.  
  
4.  **텍스트** 쿼리 유형이 선택되어 있는지 확인한 다음 **쿼리 디자이너**를 클릭합니다.  
  
5.  **텍스트로 편집**을 클릭합니다.  
  
6.  쿼리 창에 다음 쿼리를 붙여 넣습니다.  

    > [!NOTE]  
    > 이 자습서의 쿼리에는 이미 데이터 값이 포함되어 있으므로 외부 데이터 원본이 필요하지 않습니다. 따라서 쿼리가 상당히 길어집니다. 비즈니스 환경에서는 쿼리에 데이터가 포함되지 않을 것입니다. 이 자습서의 쿼리는 학습용으로만 제공됩니다.  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity, 'Install Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity, 'Report Builder in SQL Server' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity, 'Install Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity, 'Report Builder in SQL Server' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity, 'Install Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity, 'Report Builder in SQL Server' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity, 'Install Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity, 'Report Builder in SQL Server' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity, 'Install Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity, 'Report Builder in SQL Server' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity, 'Install Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity, 'Report Builder in SQL Server' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity, 'Install Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity, 'Report Builder in SQL Server' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity, 'Install Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity, 'Report Builder in SQL Server' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity, 'Install Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity, 'Report Builder in SQL Server' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity, 'Install Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity, 'Report Builder in SQL Server' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    ```  
  
7.  실행(**!**)을 클릭하여 쿼리를 실행합니다.  
  
    쿼리 결과는 보고서에 표시할 수 있는 데이터입니다.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]

9.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="AddField"></a>보고서 디자인 화면에 필드 추가  
데이터 세트의 필드가 보고서에 나타나도록 하려는 경우 먼저 해당 필드를 디자인 화면으로 직접 끌 수 있습니다. 이 연습에서는 이러한 방법이 올바르지 않은 이유와 대신 사용할 수 있는 방법을 보여 줍니다.  
  
### <a name="to-add-a-field-to-the-report-and-get-the-wrong-result"></a>보고서에 필드를 추가하려면(잘못된 결과)  
  
1.  보고서 데이터 창의 **FullName** 필드를 디자인 화면으로 끌어옵니다.  
  
    보고서 작성기에서 `<Expr>`로 표시된 식이 있는 입력란이 만들어집니다.  
  
2.  **실행**을 클릭합니다.  
  
    쿼리에서 사전순으로 첫 번째 레코드인 **Fernando Ross**레코드 하나만 표시됩니다. 즉, 이 필드가 반복되어 해당 필드의 다른 레코드가 표시되지 않습니다.  
  
3.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
4.  입력란에서 `<Expr>` 식을 선택합니다.  
  
5.  **값** 속성에 대한 속성 창에서 다음을 확인합니다. 속성 창이 표시되지 않으면 **보기** 탭에서 **속성**을 선택합니다.  
  
    ```  
    =First(Fields!FullName.Value, "TextDataSet")  
    ```  
  
    `First` 함수는 필드의 첫 번째 값만 검색하도록 디자인되었으므로 첫 번째 값만 검색되었습니다.  
  
    필드를 디자인 화면으로 직접 끌어 올 때 입력란이 만들어졌습니다. 입력란 자체는 데이터 영역이 아니므로 보고서 데이터 세트의 데이터가 표시되지 않습니다. 테이블, 행렬 및 목록과 같은 데이터 영역의 입력란에는 데이터가 표시됩니다.  
  
6.  입력란을 선택하고 Delete 키를 누릅니다. 식이 선택된 경우 입력란을 선택하려면 Esc 키를 누릅니다.  
  
### <a name="to-add-a-field-to-the-report-and-get-the-right-result"></a>보고서에 필드를 추가하려면(올바른 결과)  
  
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
  
    입력란을 목록 데이터 영역으로 끌어 데이터 세트의 해당 필드에 있는 데이터를 표시합니다.  
  
7.  목록 상자를 선택하고 Delete 키를 누릅니다.  
  
## <a name="AddTable"></a>보고서 디자인 화면에 테이블 추가  
하이퍼링크와 회전된 텍스트를 배치할 수 있도록 테이블을 만듭니다.   
  
1.  **삽입** 탭 > **테이블** > **테이블 마법사**를 클릭합니다.  
  
2.  새 테이블 또는 행렬 마법사의 **데이터 세트 선택** 페이지에서 **이 보고서의 기존 데이터 세트 또는 공유 데이터 세트 선택** > **TextDataset(이 보고서)** > **다음**을 클릭합니다.  
  
3.  **필드 정렬** 페이지에서 **Territory**, **LinkText**및 **Product** 필드를 **행 그룹**으로 끌고 **Sales** 필드를 **값**으로 끈 후 **다음**을 클릭합니다.  

    ![report-builder-text-arrange-fields](../reporting-services/media/report-builder-text-arrange-fields.png)
  
4.  **레이아웃 선택** 페이지에서 테이블 전체를 볼 수 있도록 **그룹 확장/축소** 확인란의 선택을 취소하고 **다음**을 클릭합니다. 
  
5.  **마침**을 클릭합니다.  
  
6.  **실행**을 클릭합니다.  
  
    테이블에 이상이 없어 보이지만 두 개의 합계 행이 있습니다. **LinkText** 열에는 합계 행이 필요하지 않습니다.  
    
    ![report-builder-format-2-totals](../reporting-services/media/report-builder-format-2-totals.png)
  
8.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
9. **LinkText** 열의 **전체** 셀을 선택한 다음, Shift 키를 누른 상태로 오른쪽에 있는 두 셀, 즉 **제품** 열의 빈 셀과 **판매** 열의 `[Sum(Sales)]` 셀을 선택합니다.  
  
11. 이 세 개의 셀을 선택한 상태에서 이 셀 중 하나를 마우스 오른쪽 단추로 클릭한 다음 **행 삭제**를 클릭합니다.  

    ![report-builder-format-delete-rows](../reporting-services/media/report-builder-format-delete-rows.png)
  
12. **실행**을 클릭합니다.  

    이제 하나의 합계 행만 있습니다.
    
    ![report-builder-format-one-total](../reporting-services/media/report-builder-format-one-total.png)
  
## <a name="AddHyperlink"></a>보고서에 하이퍼링크 추가  
이 섹션에서는 이전 섹션의 테이블에 있는 텍스트에 하이퍼링크를 추가합니다.  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  `[LinkText]`가 들어 있는 셀을 마우스 오른쪽 단추로 클릭하고 **입력란 속성**을 클릭합니다.  
  
3.  **작업** 탭에서 **URL로 이동**을 클릭합니다.  
  
5.  **URL 선택** 상자에서 **[URL]** 을 클릭한 다음 **확인**을 클릭합니다.  
  
6.  텍스트가 다르게 표시되지 않습니다. 텍스트가 링크 텍스트처럼 표시되도록 해야 합니다.  
  
7.  `[LinkText]`을(를) 선택합니다.  
  
8.  **홈** 탭 > **글꼴**에서 **밑줄**을 선택하고 **색**을 **파란색**으로 변경합니다.  
  
9. **실행**을 클릭합니다.  
  
    이제 텍스트가 링크처럼 표시됩니다.  
    
    ![report-builder-format-hyperlink](../reporting-services/media/report-builder-format-hyperlink.png)
  
10. 링크를 클릭합니다. 컴퓨터가 인터넷에 연결되어 있으면 보고서 작성기 도움말 항목이 브라우저에서 열립니다.  
  
## <a name="RotateText"></a>보고서의 텍스트 회전  
이 섹션에서는 이전 섹션의 테이블에 있는 텍스트 일부를 회전합니다.  
 
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  가 들어 있는 셀을 클릭합니다.(!!) `[Territory].`  
  
3.  **홈** 탭의 **글꼴** 섹션에서 **굵게** 단추를 클릭합니다.  
  
4.  속성 창이 열려 있지 않으면 **보기** 탭에서 **속성** 확인란을 선택합니다.  
  
5.  속성 창에서 WritingMode 속성을 찾은 다음 **기본값** 에서 **Rotate270**으로 변경합니다.  
 
    > [!NOTE]  
    > 속성 창의 속성이 범주로 구성되어 있는 경우 WritingMode는 **지역화** 범주에 있습니다. 셀만 선택하고 텍스트는 선택하지 말아야 합니다. WritingMode는 텍스트가 아니라 입력란의 속성입니다.  

    ![report-builder-select-territory-cell](../reporting-services/media/report-builder-select-territory-cell.png)
   
6.  **홈** 탭 > **단락** 섹션에서 **중간** 및 **가운데**를 선택하여 셀에서 세로 및 가로로 가운데에 있는 텍스트를 찾습니다.  
  
8.  실행(**!**)을 클릭합니다.  
  
이제 `[Territory]` 셀에 있는 텍스트가 셀의 아래쪽에서 위쪽으로 세로로 움직입니다.  

![report-builder-format-rotate-270](../reporting-services/media/report-builder-format-rotate-270.png)

## <a name="FormatCurrency"></a>통화 서식 지정  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 전환합니다.  
  
2.  `[Sum(Sales)]`이 들어 있는 위쪽 테이블 셀을 클릭하고 Shift 키를 누른 상태로 `[Sum(Sales)]`이 들어 있는 아래쪽 테이블 셀을 클릭합니다.  
  
3.  **홈** 탭 > **숫자** 그룹 > **통화** 단추를 클릭합니다.  
  
4.  (옵션) 국가별 설정이 영어(미국)인 경우 기본 예제 텍스트는 [**$12,345.00**]입니다. 예제 통화 값이 표시되지 않는 경우 **숫자** 그룹에서 **자리 표시자 스타일** > **샘플 값**을 클릭합니다.  

    ![report-builder-placeholder-value-button](../reporting-services/media/report-builder-placeholder-value-button.png)
  
5.  (옵션) **홈** 탭에 있는 **숫자** 그룹에서 **소수 자릿수 줄이기** 단추를 두 번 클릭하여 센트가 표시되지 않는 달러 숫자를 표시합니다.  
  
6.  실행(**!**)을 클릭하여 보고서를 미리 봅니다.  
  
이제 보고서에 서식이 지정된 데이터가 표시되므로 보다 쉽게 읽을 수 있습니다.  

![report-build-format-report](../reporting-services/media/report-build-format-report.png)
    
## <a name="FormatHTML"></a>HTML 서식을 사용하여 텍스트 표시  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 전환합니다.  
  
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
  
4.  모든 텍스트가 들어가도록 입력란의 아래쪽 가장자리를 끕니다. 끌면 디자인 화면이 더 커집니다.

5. 입력란의 모든 텍스트를 선택합니다.  
  
5.  선택한 모든 텍스트를 마우스 오른쪽 단추로 클릭하고 **텍스트 속성**을 클릭합니다.  
  
    이 속성은 입력란이 아니라 텍스트의 속성이므로 하나의 입력란에서 일반 텍스트와 HTML 태그를 스타일로 사용하는 텍스트가 혼합된 형태를 사용할 수 있습니다.  
  
6.  **일반** 탭의 **태그 형식**에서 **HTML - HTML 태그를 스타일로 해석**을 클릭합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  실행(**!**)을 클릭하여 보고서를 미리 봅니다.  
  
입력란의 텍스트가 머리글, 단락 및 글머리 기호 목록으로 표시됩니다.  
  
![report-builder-format-html](../reporting-services/media/report-builder-format-html.png)

## <a name="Save"></a>보고서 저장  
보고서를 보고서 서버, SharePoint 라이브러리 또는 컴퓨터에 저장할 수 있습니다.  
  
이 자습서에서는 보고서를 보고서 서버에 저장합니다. 보고서 서버에 액세스할 수 없는 경우에는 보고서를 컴퓨터에 저장하십시오.  
  
### <a name="to-save-the-report-on-a-report-server"></a>보고서를 보고서 서버에 저장하려면  
  
1.  **보고서 작성기** 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
2.  **최근에 사용한 사이트 및 서버**를 클릭합니다.  
  
3.  보고서를 저장할 수 있는 권한을 가진 보고서 서버의 이름을 선택하거나 입력합니다.  
  
    "보고서 서버에 연결하는 중"이라는 메시지가 나타납니다. 연결되면 보고서 서버 관리자가 보고서의 기본 위치로 지정한 보고서 폴더의 내용이 표시됩니다.  
  
4.  **이름**에서 기본 이름을 선택한 이름으로 대체합니다.

5.  **저장**을 클릭합니다.  
  
보고서가 보고서 서버에 저장됩니다. 연결된 보고서 서버의 이름이 창 아래쪽에 있는 상태 표시줄에 나타납니다.  
  
### <a name="to-save-the-report-on-your-computer"></a>컴퓨터에 보고서를 저장하려면  
  
1.  **보고서 작성기** 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
2.  **바탕 화면**, **내 문서**또는 **내 컴퓨터**를 클릭한 다음 보고서를 저장할 폴더를 찾습니다.  
  
3.  **이름**에서 기본 이름을 선택한 이름으로 대체합니다. 
  
4.  **저장**을 클릭합니다.  

## <a name="next-steps"></a>Next Steps

보고서 작성기에서는 여러 가지 방법으로 텍스트 서식을 지정할 수 있습니다. [자습서: 자유 형식 보고서 만들기](../reporting-services/tutorial-creating-a-free-form-report-report-builder.md)에 더 많은 예제가 포함되어 있습니다.  

[보고서 작성기 자습서](../reporting-services/report-builder-tutorials.md) 
[보고서 항목 서식 지정](../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)  
[SQL Server의 보고서 작성기](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
