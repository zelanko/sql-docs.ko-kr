---
title: '자습서: 행렬 보고서 만들기(보고서 작성기) | Microsoft Docs'
ms.custom: ''
ms.date: 06/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 9ee19c2e-2a8c-4bb0-9274-04a5812c2e96
caps.latest.revision: 15
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 274a385ad25081cdd4db13b9a46e1557db15ac70
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33036460"
---
# <a name="tutorial-creating-a-matrix-report-report-builder"></a>자습서: 행렬 보고서 만들기(보고서 작성기)
이 자습서에서는 중첩된 행 및 열 그룹의 샘플 판매 데이터 행렬을 사용하여 페이지가 매겨진 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 보고서를 만드는 방법을 설명합니다. 

또한 인접한 열 그룹을 만들고, 열의 서식을 지정하고, 텍스트를 회전합니다. 다음 그림에서는 만들려는 보고서와 비슷한 보고서를 보여 줍니다.  
  
![report-builder-matrix-tutorial](../reporting-services/media/report-builder-matrix-tutorial.png)
   
이 자습서에 소요되는 예상 시간: 20분  
  
## <a name="requirements"></a>요구 사항  
요구 사항에 대한 자세한 내용은 [자습서의 필수 조건](../reporting-services/prerequisites-for-tutorials-report-builder.md)을 참조하세요. 
  
## <a name="CreateMatrix"></a>1. 새 테이블 또는 행렬 마법사에서 행렬 보고서 및 데이터 집합 만들기  
이 섹션에서는 공유 데이터 원본을 선택하고, 포함된 데이터 집합을 만들고, 행렬에 데이터를 표시합니다.  
  
> [!NOTE]  
> 이 자습서의 쿼리에는 이미 데이터 값이 포함되어 있으므로 외부 데이터 원본이 필요하지 않습니다. 따라서 쿼리가 상당히 길어집니다. 비즈니스 환경에서는 쿼리에 데이터가 포함되지 않을 것입니다. 이 자습서의 쿼리는 학습용으로만 제공됩니다.  
  
### <a name="to-create-a-matrix"></a>행렬을 만들려면  
  
1.  컴퓨터,[웹 포털 또는 SharePoint 통합 모드에서](../reporting-services/report-builder/start-report-builder.md) 보고서 작성기를 시작 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 합니다.  
  
    **새 보고서 또는 데이터 집합** 대화 상자가 열립니다.  
  
    **새 보고서 또는 데이터 집합** 대화 상자가 표시되지 않는 경우 **파일** 메뉴 > **새로 만들기**를 클릭합니다.  
  
2.  왼쪽 창에 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **테이블 또는 행렬 마법사**를 클릭합니다.  
  
4.  **데이터 집합 선택** 페이지에서 **데이터 집합 만들기**를 클릭합니다.  
  
5.  **다음**을 클릭합니다.  
  
6.  **데이터 원본에 대한 연결 선택** 페이지에서 기존 데이터 원본을 선택하거나 보고서 서버를 찾아 데이터 원본을 선택합니다. 데이터 원본을 사용할 수 없거나 보고서 서버에 대한 액세스 권한이 없는 경우 포함된 데이터 원본을 대신 사용할 수 있습니다. 포함된 데이터 원본을 만드는 방법에 대한 자세한 내용은 [자습서: 기본 테이블 보고서 만들기&#40;보고서 작성기&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)를 참조하세요.  
  
7.  **다음**을 클릭합니다.  
  
8.  **쿼리 디자인** 페이지에서 **텍스트로 편집**을 클릭합니다.  
  
9. 쿼리 창에 다음 쿼리를 복사하여 붙여 넣습니다.  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
10. (옵션) 실행 아이콘(!)을 클릭하여 쿼리를 실행하고 데이터를 확인합니다.

11. **다음**을 클릭합니다.  
  
## <a name="Groups"></a>2. 새 테이블 또는 행렬 마법사에서 데이터 구성 및 레이아웃 선택  
이 마법사를 사용하여 데이터를 표시할 시작 디자인을 제공할 수 있습니다. 이 마법사의 미리 보기 창에서는 행렬 디자인을 완료하기 전에 데이터 그룹화의 결과를 시각화할 수 있습니다.  
  
1.  **필드 정렬** 페이지에서 **사용 가능한 필드** 의 Territory를 **행 그룹**으로 끌어옵니다.  
  
2.  SalesDate를 **행 그룹** 으로 끌어 Territory 아래에 배치합니다.  
  
    **행 그룹** 에 필드가 나열되는 순서에 따라 그룹 계층 구조가 정의됩니다. 1-2단계에서는 필드 값을 먼저 지역별로 구성한 다음 판매 날짜별로 구성했습니다.  
  
3.  Subcategory를 **열 그룹**으로 끌어옵니다.  
  
4.  Product를 **열 그룹** 으로 끌어 Subcategory 아래에 배치합니다.  
  
    **열 그룹** 에 필드가 나열되는 순서에 따라 그룹 계층 구조가 정의됩니다. 3-4단계에서는 필드 값을 먼저 하위 범주별로 구성한 다음 제품별로 구성했습니다.  
  
5.  Sales를 **값**으로 끌어옵니다.  
  
    Sales는 숫자 필드를 요약하기 위한 기본 함수인 Sum 함수를 사용하여 요약됩니다.  
  
6.  Quantity를 **값**으로 끌어옵니다.  
  
    Quantity는 Sum 함수를 사용하여 요약됩니다.  
  
    5-6단계에서는 행렬 데이터 셀에 표시할 데이터를 지정했습니다.
    
    ![report-builder-arrange-fields-report-wizard](../reporting-services/media/report-builder-arrange-fields-report-wizard.png)  
  
7.  **다음**을 클릭합니다.  
  
8.  레이아웃 선택 페이지의 **옵션**에서 **부분합 및 총합계 표시** 가 선택되어 있는지 확인합니다.  
  
9. **블록형, 부분합 하단 표시** 가 선택되어 있는지 확인합니다.  
  
10. **그룹 확장/축소** 옵션이 선택되어 있는지 확인합니다.  
  
11. **다음**을 클릭합니다.  
  
13. **마침**을 클릭합니다.  
  
    디자인 화면에 행렬이 추가됩니다. 행 그룹 창에는 Territory 및 SalesDate라는 두 개의 행 그룹이 표시됩니다. 열 그룹 창에는 하위 범주 및 제품이라는 두 개의 열 그룹이 표시됩니다. 세부 데이터는 모두 데이터 집합 쿼리로 검색된 데이터입니다.  
    
    ![report-builder-row-and-column-groups](../reporting-services/media/report-builder-row-and-column-groups.png)
  
14. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
    특정 날짜에 판매된 각 제품에 대해 해당 제품이 속한 하위 범주 및 판매 지역이 행렬에 표시됩니다.  

14. 하위 범주 확장 보고서의 너비가 빠르게 확장되는 것을 확인할 수 있습니다.

![report-builder-expand-matrix](../reporting-services/media/report-builder-expand-matrix.png)
  
## <a name="FormatData"></a>3. 데이터 서식 지정  
기본적으로 Sales 필드의 요약 데이터에는 일반 숫자가 표시되고, SalesDate 필드의 요약 데이터에는 날짜와 시간 정보가 모두 표시됩니다. 이 섹션에서는 숫자를 통화로 표시하도록 Sales 필드의 서식을 지정하고 날짜만 표시하도록 SalesDate 필드의 서식을 지정합니다. **자리 표시자 스타일** 을 설정/해제하여 서식 있는 입력란 및 자리 표시자 텍스트를 보기 값으로 표시합니다.  
  
### <a name="to-format-fields"></a>필드의 서식을 지정하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 전환합니다.  
  
2.  Ctrl 키를 누른 상태로 `[Sum(Sales)]`이 들어 있는 9개의 셀을 선택합니다.  
  
3.  **홈** 탭 > **숫자** > **통화**를 선택합니다. 셀이 변경되어 형식 지정된 통화가 표시됩니다.  
  
    국가별 설정이 영어(미국)인 경우 기본 예제 텍스트는 [**$12,345.00**]입니다. 예제 통화 값이 표시되지 않는 경우 **숫자** 그룹에서 **자리 표시자 스타일** > **샘플 값**을 클릭합니다.  
    
    ![report-builder-placeholder-value](../reporting-services/media/report-builder-placeholder-value.png)
  
4.  `[SalesDate]`가 들어 있는 셀을 클릭합니다.  
  
5.  **숫자** 그룹 > **날짜**를 선택합니다.  
  
    셀에 예제 날짜 **[1/31/2000]** 이 표시됩니다. 예제 날짜가 표시되지 않으면 **숫자** 그룹에서 **자리 표시자 스타일** 을 클릭한 다음 **보기 값**을 클릭합니다.  
  
6.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
날짜 값은 날짜만 표시되고 판매 값은 통화로 표시됩니다.  
  
## <a name="AdjacentGroup"></a>4. 인접 열 그룹 추가  
행 및 열 그룹을 부모-자식 관계로 중첩하거나 형제 관계로 인접하게 중첩할 수 있습니다.  
  
이 섹션에서는 Subcategory 열 그룹에 인접한 열 그룹을 추가하고, 셀을 복사하여 새 열 그룹을 채운 다음, 식을 사용하여 열 그룹 머리글의 값을 만듭니다.  
  
### <a name="to-add-an-adjacent-column-group"></a>인접 열 그룹을 추가하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  `[Subcategory]`가 들어 있는 셀을 마우스 오른쪽 단추로 클릭하고 **그룹 추가**를 가리킨 다음 **오른쪽에 인접**을 클릭합니다.  
  
    **테이블릭스 그룹** 대화 상자가 열립니다.  
  
3.  **그룹화 방법** 목록에서 SalesDate를 선택한 다음 **확인**을 클릭합니다.  
  
    새 열 그룹이 Subcategory 열 그룹의 오른쪽에 추가됩니다.  
  
4.  `[SalesDate],` 가 들어 있는 새 열 그룹의 셀을 마우스 오른쪽 단추로 클릭한 다음 **식**을 클릭합니다.  
  
5.  식 상자에 다음 식을 복사합니다.  
  
    ```  
    =WeekdayName(DatePart("w",Fields!SalesDate.Value))  
    ```  
  
    이 식은 판매 날짜에서 요일 이름을 추출합니다. 자세한 내용은 [식&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
6.  Total이 들어 있는 Subcategory 열 그룹의 셀을 마우스 오른쪽 단추로 클릭한 다음 **복사**를 클릭합니다.  
  
7.  5단계에서 만든 식이 들어 있는 셀 바로 아래의 셀을 마우스 오른쪽 단추로 클릭한 다음 **붙여넣기**를 클릭합니다.  
  
8.  Ctrl 키를 누릅니다.  
  
9. Subcategory 그룹에서 Sales 열 머리글과 해당 열 아래에 있는 세 개의 셀을 클릭한 다음 **복사**를 클릭합니다.  
  
10. 네 개의 셀을 새 열 그룹에 있는 빈 셀에 붙여 넣습니다.  
  
11. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
보고서에 Monday 및 Tuesday라는 열이 포함됩니다. 데이터 집합에는 이러한 두 요일에 대한 데이터만 포함됩니다.  

![report-builder-matrix-weekdays](../reporting-services/media/report-builder-matrix-weekdays.png)
  
> [!NOTE]  
> 데이터에 다른 요일이 포함된 경우 보고서에도 해당 요일에 대한 열이 포함됩니다. 각 열에는 **Sales**열 머리글과 지역별 판매 합계가 표시됩니다.  
  
## <a name="Width"></a>5. 열 너비 변경  
행렬이 포함된 보고서를 실행하면 일반적으로 가로와 세로로 확장됩니다. 가로 확장을 제어하는 기능은 특히 보고서를 인쇄용 보고서에 사용되는 Microsoft Word 또는 Adobe PDF 등의 형식으로 내보내려고 할 때 중요합니다. 보고서가 여러 페이지에 걸쳐 가로로 확장될 경우에는 인쇄된 페이지를 이해하기 어렵습니다. 가로 확장을 최소화하려면 데이터를 자르지 않고 표시하는 데 필요한 너비로만 열 크기를 조정합니다. 제목이 데이터를 표시하는 데 필요한 너비에 맞도록 열의 이름을 변경해도 됩니다.  
  
### <a name="to-rename-and-resize-the-columns"></a>열의 이름을 바꾸고 크기를 조정하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  가장 왼쪽에 있는 Quantity 열의 텍스트를 선택하고 **QTY**를 입력합니다.  
  
    이제 열 제목은 QTY가 됩니다.  
  
3.  Quantity라는 다른 두 열에 대해 2단계를 반복합니다.
  
4.  행렬을 클릭하여 열 핸들과 행 핸들이 행렬 위와 옆에 표시되도록 합니다.  
  
    테이블 위쪽 및 옆쪽을 따라 표시되는 회색 막대는 행 및 열 핸들입니다.  
    
    ![report-builder-column-handles](../reporting-services/media/report-builder-column-handles.png)
  
5.  가장 왼쪽에 있는 QTY 열의 크기를 조정하려면 커서가 양방향 화살표로 바뀌도록 열 핸들 사이의 선에 커서를 놓습니다. 열의 너비가 1/2인치가 될 때까지 열을 왼쪽으로 끌어옵니다.  
  
    너비가 1/2인치인 열은 수량을 표시하는 데 충분합니다.  
  
6.  QTY라는 다른 열에 대해 5단계를 반복합니다.  
  
7.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
이제 수량을 포함하는 열이 더 좁고 이름이 QTY로 표시됩니다.  
  
## <a name="MergeCells"></a>6. 행렬 셀 병합  
모퉁이 영역은 행렬의 왼쪽 위 모퉁이에 있습니다. 행렬의 행 및 열 그룹 수에 따라 모퉁이 영역에 있는 셀 수가 달라집니다. 이 자습서에서 작성하는 행렬의 모퉁이 영역에는 네 개의 셀이 있습니다. 이러한 셀은 행 및 열 그룹 계층의 깊이를 반영하여 두 개의 행과 두 개의 열로 정렬됩니다. 이 네 개의 셀은 이 보고서에서 사용되지 않으므로 한 개의 셀로 병합합니다.  
  
### <a name="to-merge-matrix-cells"></a>행렬 셀을 병합하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  행렬을 클릭하여 열 핸들과 행 핸들이 행렬 위와 옆에 표시되도록 합니다.  
  
3.  Ctrl 키를 누른 상태로 네 개의 모퉁이 셀을 선택합니다.  
  
4.  셀을 마우스 오른쪽 단추로 클릭한 다음 **셀 병합**을 클릭합니다.  
  
5.  새로 병합된 셀을 마우스 오른쪽 단추로 클릭한 다음 **입력란 속성**을 클릭합니다.  
  
6.  **테두리** 탭 > **사전 설정** > **없음**을 선택합니다.
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
행렬의 위쪽 모퉁이에 있는 셀이 더 이상 표시되지 않습니다. 
  
## <a name="HeaderTitle"></a>7. 보고서 머리글 및 보고서 제목 추가  
보고서 제목은 보고서 맨 위에 나타납니다. 보고서 제목을 보고서 머리글에 배치하거나, 보고서 머리글이 사용되지 않을 경우 보고서 본문의 맨 위에 있는 입력란에 배치할 수 있습니다. 이 자습서에서는 보고서의 위쪽에 있는 입력란을 제거하고 머리글에 제목을 추가합니다.  
  
### <a name="to-add-a-report-header-and-report-title"></a>보고서 머리글 및 보고서 제목을 추가하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  보고서 본문의 맨 위에서 **제목을 추가하려면 클릭하십시오.** 가 들어 있는 입력란을 선택한 다음 Delete 키를 누릅니다.  
  
3.  **삽입** 탭 > **헤더** > **헤더 추가**를 선택합니다.  
  
    머리글이 보고서 본문의 위쪽에 추가됩니다.  
  
4.  **삽입** 탭에서 **입력란**을 클릭한 다음 입력란을 보고서 머리글 안으로 끌어옵니다. 입력란의 길이와 높이를 각각 6인치와 3/4인치로 만들고 보고서 머리글의 왼쪽에 배치합니다.  
  
5.  입력란에 **Sales by Territory, Subcategory, and Day**를 입력합니다.  
  
6.  입력한 텍스트를 선택한 다음 **홈** 탭 > **글꼴**을 선택합니다.
    * **크기 24pt**
    * **색 적갈색**
 
10. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
보고서의 보고서 머리글에 보고서 제목이 포함됩니다.  
  
## <a name="Save"></a>8. 보고서 저장  
보고서를 보고서 서버, SharePoint 라이브러리 또는 컴퓨터에 저장할 수 있습니다.  
  
이 자습서에서는 보고서를 보고서 서버에 저장합니다. 보고서 서버에 액세스할 수 없는 경우에는 보고서를 컴퓨터에 저장하십시오.  
  
### <a name="to-save-the-report-on-a-report-server"></a>보고서를 보고서 서버에 저장하려면  
  
1.  **보고서 작성기** 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
2.  **최근에 사용한 사이트 및 서버**를 클릭합니다.  
  
3.  보고서를 저장할 수 있는 권한을 가진 보고서 서버의 이름을 선택하거나 입력합니다.  
  
    "보고서 서버에 연결하는 중"이라는 메시지가 나타납니다. 연결되면 보고서 서버 관리자가 기본 보고서 위치로 지정한 보고서 폴더의 내용이 표시됩니다.  
  
4.  **이름**에서 기본 이름을 **SalesByTerritorySubcategory**로 바꿉니다.  
  
5.  **저장**을 클릭합니다.  
  
보고서가 보고서 서버에 저장됩니다. 연결된 보고서 서버의 이름이 창 아래쪽에 있는 상태 표시줄에 나타납니다.  
  
#### <a name="to-save-the-report-on-your-computer"></a>컴퓨터에 보고서를 저장하려면  
  
1.  **보고서 작성기** 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
2.  **바탕 화면**, **내 문서**또는 **내 컴퓨터**를 클릭한 다음 보고서를 저장할 폴더를 찾습니다.  
  
3.  **이름**에서 기본 이름을 **SalesByTerritorySubcategory**로 바꿉니다.  
  
4.  **저장**을 클릭합니다.  
  
## <a name="RotateTextBox"></a>9. (선택 사항) 입력란 270도 회전  
행렬이 있는 보고서는 실행 시 가로 및 세로로 확장될 수 있습니다. 입력란을 세로로 회전하거나 270도 회전하면 가로 공간을 절약할 수 있습니다. 그러면 렌더링된 보고서의 너비가 좁아지며, 보고서가 Microsoft Word 등의 형식으로 내보낼 경우 인쇄되는 페이지에 더 잘 맞게 됩니다.  
  
입력란에서는 텍스트를 가로 및 세로(위에서 아래로)로 표시할 수도 있습니다. 자세한 내용은 [입력란&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)를 참조하세요.  
  
### <a name="to-rotate-text-box-270-degrees"></a>입력란을 270도 회전하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  가 들어 있는 셀을 선택합니다.(!!) `[Territory].` 

    >**참고**: 텍스트가 아니라 셀을 선택합니다. WritingMode 속성은 셀에만 사용할 수 있습니다.
    
     ![report-builder-select-territory-cell](../reporting-services/media/report-builder-select-territory-cell.png)
  
3.  속성 창에서 WritingMode 속성을 찾은 다음 **기본값** 에서 **Rotate270**으로 변경합니다.  
  
    속성 창이 열려 있지 않으면 리본의 **보기** 탭을 클릭하고 **속성**을 선택합니다.  
  
4.  CanGrow 속성이 **True**로 설정되었는지 확인합니다.  
  
5.  **홈** 탭 > **단락** 섹션에서 **중간** 및 **가운데**를 선택하여 셀에서 세로 및 가로로 가운데에 있는 텍스트를 찾습니다.  
 
6. Territory 열의 너비를 1/2인치로 조정하고 열 제목을 삭제합니다.  
6.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
지역 이름이 아래에서 위쪽으로 세로로 표시됩니다. Territory 행 그룹의 높이는 지역 이름의 길이에 따라 달라집니다.  
  
## <a name="next-steps"></a>Next Steps  
이것으로 행렬 보고서를 만드는 자습서를 마칩니다. 행렬에 대한 자세한 내용은 다음을 참조하세요. 
-    [테이블, 행렬 및 목록](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)
-    [행렬 만들기](../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)
-    [테이블릭스 데이터 영역](../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md) 
-    [테이블릭스 데이터 영역 셀, 행 및 열](../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>참고 항목  
[보고서 작성기 자습서](../reporting-services/report-builder-tutorials.md)  
[SQL Server 2016의 보고서 작성기](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

