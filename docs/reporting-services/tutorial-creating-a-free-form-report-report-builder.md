---
title: '자습서: 자유 형식 보고서 만들기(보고서 작성기) | Microsoft Docs'
ms.date: 09/02/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.suite: pro-bi
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: 87288b59-faf2-4b1d-a8e4-a7582baedf2f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bfd009008af99f853079c26e566a3b7194b4e304
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43265925"
---
# <a name="tutorial-creating-a-free-form-report-report-builder"></a>자습서: 자유 형식 보고서 만들기(보고서 작성기)
이 자습서에서는 뉴스레터 역할을 하는 페이지가 매겨진 보고서를 만듭니다. 각 페이지에는 정적 텍스트, 요약 시각적 개체 및 자세한 샘플 판매 데이터가 표시됩니다.

![report-builder-free-form-report-complete](../reporting-services/media/report-builder-free-form-report-complete.png)

이 보고서에서는 정보가 지역별로 그룹화되고 지역의 판매 관리자 이름과 세부 및 요약 판매 정보가 표시됩니다. 자유 형식 보고서의 기초로 목록 데이터 영역에서 시작한 다음 이미지가 있는 장식 패널, 데이터가 삽입된 정적 텍스트, 세부 정보를 표시할 테이블, 요약 정보를 표시할 원형 및 세로 막대형 차트(옵션) 등을 추가합니다.  
  
이 자습서에 소요되는 예상 시간: 20분  
  
## <a name="requirements"></a>요구 사항  
요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)을 참조하세요.  
  
## <a name="BlankReport"></a>1. 빈 보고서, 데이터 원본 및 데이터 집합 만들기  
  
> [!NOTE]  
> 이 자습서의 쿼리에는 데이터 값이 포함되어 있으므로 외부 데이터 원본이 필요하지 않습니다. 따라서 쿼리가 상당히 길어집니다. 비즈니스 환경에서는 쿼리에 데이터가 포함되지 않을 것입니다. 이 자습서의 쿼리는 학습용으로만 제공됩니다.  
  
### <a name="to-create-a-blank-report"></a>빈 보고서를 만들려면  
  
1.  컴퓨터,[웹 포털 또는 SharePoint 통합 모드에서](../reporting-services/report-builder/start-report-builder.md) 보고서 작성기를 시작 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 합니다.  
  
    **새 보고서 또는 데이터 집합** 대화 상자가 열립니다.  
  
    **새 보고서 또는 데이터 집합** 대화 상자가 표시되지 않는 경우 **파일** 메뉴 > **새로 만들기**를 클릭합니다.  
  
2.  왼쪽 창에서 **새 보고서** 가 선택되어 있는지 확인합니다. 
 
3.  오른쪽 창에서 **빈 보고서**를 클릭합니다.  
  
### <a name="to-create-a-new-data-source"></a>새 데이터 원본을 만들려면  
  
1.  보고서 데이터 창에서 **새로 만들기** > **데이터 원본**을 클릭합니다.  
  
2.  **이름** 상자에 **ListDataSource**를 입력합니다.  
  
3.  **내 보고서에 포함된 연결 사용**을 클릭합니다.  
  
4.  연결 형식이 Microsoft SQL Server인지 확인한 다음 **연결 문자열** 상자에 **Data Source = \<servername>** 을 입력합니다.  
  
    **\<servername>**(예: Report001)은 SQL Server 데이터베이스 엔진의 인스턴스가 설치된 컴퓨터를 지정합니다. 이 보고서의 데이터는 SQL Server 데이터베이스에서 추출된 것이 아니므로 데이터베이스 이름을 포함하면 안 됩니다. 지정된 서버의 기본 데이터베이스는 쿼리를 구문 분석하는 데만 사용됩니다.  
  
5.  **자격 증명**을 클릭하고 SQL Server 데이터베이스 엔진의 인스턴스에 연결해야 하는 자격 증명을 입력합니다.  
  
6.  **확인**을 클릭합니다.  
  
### <a name="to-create-a-new-dataset"></a>새 데이터 집합을 만들려면  
  
1.  보고서 데이터 창에서 **새로 만들기** > **데이터 집합**을 클릭합니다.  
  
2.  **이름** 상자에 **ListDataset**을 입력합니다.  
  
3.  **내 보고서에 포함된 데이터 집합 사용**을 클릭하고 데이터 원본이 **ListDataSource**인지 확인합니다.  
  
4.  **텍스트** 쿼리 유형이 선택되어 있는지 확인한 다음 **쿼리 디자이너**를 클릭합니다.  
  
5.  **텍스트로 편집**을 클릭합니다.  
  
6.  쿼리 창에 다음 쿼리를 복사하여 붙여 넣습니다.  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
7.  **실행** 아이콘(!)을 클릭하여 쿼리를 실행합니다.  
  
    쿼리 결과는 보고서에 표시할 수 있는 데이터입니다.  
  
    ![report-builder-free-form-tutorial-data](../reporting-services/media/report-builder-free-form-tutorial-data.png) 
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="List"></a>2. 목록 추가 및 구성  
[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에서 목록 데이터 영역은 자유 형식 보고서를 만드는 데 적합합니다. 테이블 및 행렬과 마찬가지로 *테이블릭스* 데이터 영역을 기반으로 합니다. 자세한 내용은 [목록을 사용하여 송장 및 양식 만들기](../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)를 참조하세요.  
  
목록을 사용하여 뉴스레터와 유사한 형식의 보고서에 판매 지역에 대한 판매 정보를 표시합니다. 이 정보는 지역별로 그룹화됩니다. 데이터를 지역별로 그룹화하는 새 행 그룹을 추가한 다음 기본 제공된 세부 정보 행 그룹을 삭제합니다.  
  
### <a name="to-add-a-list"></a>목록을 추가하려면  
  
1.  **삽입** 탭 > **데이터 영역** > **목록**으로 이동합니다. 

2. 보고서 본문(제목 및 바닥글 영역 사이)을 클릭한 다음 마우스를 끌어 목록 상자를 만듭니다. 목록 상자의 높이와 너비를 각각 7인치와 6.25인치로 조정합니다. 정확한 크기를 지정하려면 **속성** 창의 **위치**에서 **너비** 및 **높이** 속성의 값을 입력합니다.
  
    > [!NOTE]  
    > 이 보고서에서는 Letter(8.5 X11) 용지 크기와 1인치 여백을 사용합니다. 목록 상자의 높이가 9인치보다 크거나 너비가 6.5인치보다 클 경우 빈 페이지가 생성될 수 있습니다.  
  
2.  목록 상자 안을 클릭하고 목록 맨 위의 막대를 마우스 오른쪽 단추로 클릭한 다음 **테이블릭스 속성**을 클릭합니다.  
  
    ![report-builder-free-form-tablix-properties](../reporting-services/media/report-builder-free-form-tablix-properties.png) 
  
3.  **데이터 집합 이름** 드롭다운 목록에서 **ListDataset**을 선택합니다.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  목록 안을 마우스 오른쪽 단추로 클릭한 다음 **사각형 속성**을 클릭합니다.  
  
6.  **일반** 탭에서 **뒤에 페이지 나누기 추가** 확인란을 선택합니다.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-add-a-new-row-group-and-to-delete-the-details-group"></a>새 행 그룹을 추가하고 세부 정보 그룹을 삭제하려면  
  
1.  행 그룹 창에서 세부 정보 그룹을 마우스 오른쪽 단추로 클릭하고 **그룹 추가**를 가리킨 다음 **부모 그룹**을 클릭합니다.  
  
    ![report-builder-free-form-add-parent-group](../reporting-services/media/report-builder-free-form-add-parent-group.png)  
  
2.  **그룹화 방법** 목록에서 다음을 선택합니다. `[Territory].`  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    `[Territory]` 셀을 포함하는 열이 목록에 추가됩니다.
  
4.  목록에서 Territory 열을 마우스 오른쪽 단추로 클릭한 다음 **열 삭제**를 클릭합니다.  
  
    ![report-builder-free-form-delete-columns](../reporting-services/media/report-builder-free-form-delete-columns.png)
  
5.  **열만 삭제**를 선택합니다.  
  
6.  행 그룹 창에서 **세부 정보** 그룹 > **그룹 삭제**를 마우스 오른쪽 단추로 클릭합니다.  
   
7.  **그룹만 삭제**를 선택합니다.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Graphics"></a>3. 그래픽 요소 추가  
목록 데이터 영역의 장점 중 하나는 테이블 형식 레이아웃으로 제한하지 않고 사각형 및 입력란과 같은 보고서 항목을 어느 곳에나 추가할 수 있다는 점입니다. 색으로 채워진 사각형과 같은 그래픽을 추가하여 보고서의 모양을 돋보이게 할 수 있습니다.  
  
### <a name="to-add-graphic-elements-to-the-report"></a>보고서에 그래픽 요소를 추가하려면  
  
1.  **삽입** 탭에서 **사각형**을 선택합니다. 

2. 목록의 왼쪽 위를 클릭하고 마우스를 끌어 사각형의 높이와 너비를 각각 7인치와 3.5인치로 조정합니다. 정확한 크기를 지정하려면 **속성** 창의 **위치**에서 **너비** 및 **높이**의 값을 입력합니다.
  
2.  사각형 > **사각형 속성**을 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **채우기** 탭을 클릭합니다.  
  
4.  **채우기 색**에서 **연한 회색**을 선택합니다.  
   
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
이제 보고서의 왼쪽에 다음 그림과 같이 연한 회색 사각형으로 구성된 세로 그래픽이 있습니다.  
  
![report-builder-free-form-gray-rectangle](../reporting-services/media/report-builder-free-form-gray-rectangle.png)
 
## <a name="Text"></a>4. 자유 형식 텍스트 추가  
입력란을 추가하여 각 보고서 페이지와 데이터 필드에서 반복되는 정적 텍스트를 표시할 수 있습니다.  
  
### <a name="to-add-text-to-the-report"></a>보고서에 텍스트를 추가하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  **삽입** 탭 > **텍스트 상자**로 이동합니다. 이전에 추가한 사각형 안에 있는 목록의 왼쪽 위를 클릭하고 마우스를 끌어 입력란의 너비와 높이를 각각 3.45인치와 5인치로 조정합니다.  
  
3.  입력란에 커서를 놓고 **Newsletter for** 를 입력합니다. 다음 단계에서 추가할 필드의 텍스트를 구분하기 위해 "for" 단어 뒤에 공백을 포함합니다.   
  
    ![뉴스레터 제목 텍스트 추가](../reporting-services/media/tutorial-newsletterfor.png "뉴스레터 제목 텍스트 추가")  
  
4.  보고서 데이터 창의 ListDataSet에서 `[Territory]` 필드를 입력란으로 끌어 "Newsletter for" 뒤에 놓습니다.  
  
    ![report-builder-free-form-territory-field](../reporting-services/media/report-builder-free-form-territory-field.png)
  
5.  텍스트와 `[Territory]` 필드를 선택합니다.  
  
6.  **홈** 탭 > **글꼴**에서 다음을 선택합니다. 
  
    *  **Segoe Semibold**.
    *  **20pt**.
    *  **토마토**.  
  
9. 3단계에서 입력한 텍스트 아래에 커서를 놓고 **Hello** 를 입력한 후 단어 뒤에 공백을 추가하여 텍스트와 다음 단계에서 추가할 필드를 구분합니다.  
 
10. 보고서 데이터 창의 ListDataSet에서 `[FullName]` 필드를 입력란으로 끌어 "Hello" 뒤에 놓은 다음 쉼표(,)를 입력합니다.  
   
11. 이전 단계에서 추가한 텍스트를 선택합니다.
  
12. **홈** 탭 > **글꼴**에서 다음을 선택합니다. 
  
    *  **Segoe Semibold**.
    *  **16pt**.
    *  **검정**.  
   
15. 9-13단계에서 추가한 텍스트 아래에 커서를 놓고 다음과 같은 의미 없는 텍스트를 복사하여 붙여넣습니다.  
  
    ```  
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin sed dolor in ipsum pulvinar egestas. Sed sed lacus at leo ornare ultricies. Vivamus velit risus, euismod nec sodales gravida, gravida in dui. Etiam ullamcorper elit vitae justo fermentum ut ullamcorper augue sodales. 
    Ut placerat, nisl quis feugiat adipiscing, nibh est aliquet est, mollis faucibus mauris lectus quis arcu. In mollis tincidunt lacinia. In vitae erat ut lorem tincidunt luctus. Curabitur et magna nunc, sit amet adipiscing nisi. Nulla rhoncus elementum orci nec tincidunt. 
    Aliquam imperdiet cursus erat vel tincidunt. Donec et neque ac urna rutrum sodales. In id purus et nisl dignissim dapibus. Sed rhoncus metus at felis feugiat eu tempor dolor vehicula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam faucibus consectetur diam eu pellentesque.   
 
    ```  
  
16. 방금 추가한 텍스트를 선택합니다.  
  
17.  **홈** 탭 > **글꼴**에서 다음을 선택합니다. 
  
      *  **맑은 고딕**.
      *  **10pt**.
      *  **검정**.  
 
20. 입력란에 커서를 놓고 의미 없는 텍스트 아래에 **Congratulations on your total sales of**를 입력한 후 단어 뒤에 공백을 추가하여 텍스트와 다음 단계에서 추가할 필드를 구분합니다. 
  
21. Sales 필드를 입력란으로 끌어 이전 단계에서 입력한 텍스트 뒤에 배치한 다음 느낌표(!)를 입력합니다.  

25. 방금 추가한 텍스트와 필드를 선택합니다.  
  
17.  **홈** 탭 > **글꼴**에서 다음을 선택합니다. 
  
      *  **Segoe Semibold**.
      *  **16pt**.
      *  **검정**.  
  
22. `[Sales]` 필드만 선택하고 필드 > **식**을 마우스 오른쪽 단추로 클릭합니다.  
  
23. **식** 상자에서 다음과 같이 Sum 함수를 포함하도록 식을 변경합니다.  
  
    ```  
    =Sum(Fields!Sales.value)  
    ```  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    ![report-builder-free-form-text-box](../reporting-services/media/report-builder-free-form-text-box.png)
 
29. `[Sum(Sales)]`을 선택한 상태로 **홈** 탭 > **숫자** 그룹 > **통화**로 이동합니다.  
  
30. "제목을 추가하려면 클릭하십시오." 텍스트가 있는 입력란을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
31. 목록 상자를 선택합니다. 두 개의 양방향 화살표를 선택하고 페이지의 맨 위로 이동합니다.  

    ![report-builder-drag-list](../reporting-services/media/report-builder-drag-list.png)
  
32. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
보고서에 정적 테스트가 표시되고 각 보고서 페이지에 지역과 관련된 데이터가 포함됩니다. Sales의 서식이 통화로 지정됩니다.  
  
![report-builder-newsletter-page-preview](../reporting-services/media/report-builder-newsletter-page-preview.png)
  
## <a name="Table"></a>5. 테이블을 추가하여 Sales 세부 정보 표시  
새 테이블 및 행렬 마법사를 사용하여 자유 형식 보고서에 테이블을 추가합니다. 마법사를 완료한 후에는 합계를 표시할 행을 수동으로 추가합니다.  
  
### <a name="to-add-a-table"></a>테이블을 추가하려면  
  
1.  **삽입** 탭 > **데이터 영역** 영역 > **테이블** > **테이블 마법사**로 이동합니다.  
  
2.  **데이터 집합 선택** 페이지에서 **ListDataset** > **다음**을 클릭합니다.  
  
4.  **필드 정렬** 페이지에서 **사용 가능한 필드** 의 Product 필드를 **값**으로 끌어옵니다.  
  
5.  SalesDate, Quantity 및 Sales에 대해 3단계를 반복합니다. SalesDate는 Product 아래에 배치하고, Quantity는 SalesDate 아래에 배치하고, Sales는SalesDate 아래에 배치합니다.  
  
6.  **다음**을 클릭합니다.  
  
7.  **레이아웃 선택** 페이지에서 테이블의 레이아웃을 확인합니다.  
  
    테이블은 단순합니다. 5개의 열로 구성되며 행 또는 열 그룹이 없습니다. 그룹이 없기 때문에 그룹과 관련된 레이아웃 옵션은 사용할 수 없습니다. 이 자습서의 뒷부분에서 합계를 포함하도록 테이블을 수동으로 업데이트할 것입니다.  
  
8.  **다음**을 클릭합니다.  
  
9. **마침**을 클릭합니다.  
  
11. 테이블을 4단원에서 추가한 입력란 아래로 끌어옵니다.  
  
    > [!NOTE]  
    > 테이블이 목록 상자 안, 회색 사각형 안에 있는지 확인합니다.  
  
12. 테이블을 선택한 상태로 **행 그룹** 창에서 **세부 정보** > **합계 추가** > **다음 이후**를 마우스 오른쪽 단추로 클릭합니다.  
  
    ![report-builder-free-form-table-totals](../reporting-services/media/report-builder-free-form-table-totals.png)
  
13. Product 열의 셀을 선택하고 **Total**을 입력합니다.

    ![report-builder-free-form-type-total](../reporting-services/media/report-builder-free-form-type-total.png)

12. [SalesDate] 필드를 선택합니다. **홈** 탭 > **숫자**에서 **기본값**을 **날짜**로 변경합니다.

13. [Sum(Sales)] 필드를 선택합니다. **홈** 탭 > **숫자**에서 **기본값**을 **통화**로 변경합니다.

**실행** 을 클릭하여 보고서를 미리 봅니다.  
  
보고서에 판매 세부 정보 및 합계가 포함된 테이블이 표시됩니다.  
  
![report-builder-free-form-with-table](../reporting-services/media/report-builder-free-form-with-table.png)
   
## <a name="Save"></a>6. 보고서 저장  
보고서를 보고서 서버, SharePoint 라이브러리 또는 컴퓨터에 저장할 수 있습니다.  
  
이 자습서에서는 보고서를 보고서 서버에 저장합니다. 보고서 서버에 액세스할 수 없는 경우에는 보고서를 컴퓨터에 저장하십시오.  
  
### <a name="to-save-the-report-on-a-report-server"></a>보고서를 보고서 서버에 저장하려면  
  
1.  **보고서 작성기** 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
2.  **최근에 사용한 사이트 및 서버**를 클릭합니다.  
  
3.  보고서를 저장할 수 있는 권한을 가진 보고서 서버의 이름을 선택하거나 입력합니다.  
  
    "보고서 서버에 연결하는 중"이라는 메시지가 나타납니다. 연결되면 보고서 서버 관리자가 보고서의 기본 위치로 지정한 보고서 폴더의 내용이 표시됩니다.  
  
4.  **이름**에서 기본 이름을 **SalesInformationByTerritory**로 바꿉니다.  
  
5.  **저장**을 클릭합니다.  
  
보고서가 보고서 서버에 저장됩니다. 연결된 보고서 서버의 이름이 창 아래쪽에 있는 상태 표시줄에 나타납니다.  
  
### <a name="to-save-the-report-on-your-computer"></a>컴퓨터에 보고서를 저장하려면  
  
1.  **보고서 작성기** 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
2.  **바탕 화면**, **내 문서**또는 **내 컴퓨터**를 클릭한 다음 보고서를 저장할 폴더를 찾습니다.  
  
3.  **이름**에서 기본 이름을 **SalesInformationByTerritory**로 바꿉니다.  
  
4.  **저장**을 클릭합니다.  
  
## <a name="Line"></a>7. (선택 사항) 선을 추가하여 보고서 영역 구분  
선을 추가하여 보고서의 편집 영역과 세부 정보 영역을 구분합니다.  
  
### <a name="to-add-a-line"></a>선을 추가하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  **삽입** 탭 > **보고서 항목** > **선**으로 이동합니다.  
  
3.  4단원에서 추가한 자유 형식 입력란 아래에 선을 그립니다.  
  
4.  선을 클릭하고 **홈** 탭 > **테두리**에서 다음을 선택합니다.
     * **너비** 를 선택한 다음 **3** pt를 선택합니다.
     * **색** 을 선택한 다음 **토마토**를 선택합니다.  
  
## <a name="Visualization"></a>8. (옵션) 요약 데이터 시각화 추가  
사각형은 보고서가 렌더링되는 방식을 제어하는 데 유용합니다. 원형 및 세로 막대형 차트를 사각형 내에 배치하여 보고서가 원하는 방식으로 렌더링되도록 합니다.  
  
### <a name="to-add-a-rectangle"></a>사각형을 추가하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  **삽입** 탭 > **보고서 항목** >  **사각형**으로 이동합니다. 테이블 오른쪽의 목록 상자 안에서 사각형을 끌어 사각형의 너비와 높이를 각각 약 2.25인치와 7.9인치로 조정합니다.  
  
3.  새 사각형을 선택한 상태로 속성 창에서 **BorderColor LightGrey**, **BorderStyle 실선**, **BorderWidth 2pt**로 지정합니다. 

4. 사각형과 테이블의 위쪽을 맞춥니다.  
  
## <a name="to-add-a-pie-chart"></a>원형 차트를 추가하려면  
  
1.  **삽입** 탭 > **데이터 시각화** > **차트** > **차트 마법사**로 이동합니다.  
  
2.  **데이터 집합 선택** 페이지에서 **ListDataset** > **다음**을 클릭합니다.  
  
3.  **원형** > **다음**을 클릭합니다.  
  
4.  차트 필드 정렬 페이지에서 Product를 **범주**로 끌어옵니다.  
  
5.  Quantity를 **값**으로 끌어온 후 **다음**을 클릭합니다.  
  
6.  **마침**을 클릭합니다.  
  
8.  보고서의 왼쪽 위에 나타나는 차트의 너비와 높이를 각각 약 2.25인치와 3.6인치로 조정합니다.  
  
9. 차트를 사각형 안으로 끌어옵니다.  
   
10. 차트 제목을 선택하고 **Product Quantities Sold**를 입력합니다.  
  
12. **홈** 탭 > **글꼴**에서 제목을 다음과 같이 조정합니다.
    * **글꼴** **Segoe UI Semibold**을 참조하세요.
    * **크기** **12pt**을 참조하세요.
    * **색** **검정**을 참조하세요.  

13. 범례 > **범례 속성**을 마우스 오른쪽 단추로 클릭합니다.

14. **일반** 탭의 **범례 위치**에서 맨 아래에 있는 가운데 점을 선택합니다. 
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

16. 필요한 경우 마우스를 끌어 차트 영역의 높이를 늘립니다.

     ![report-builder-free-form-pie](../reporting-services/media/report-builder-free-form-pie.png)
  
## <a name="to-add-a-column-chart"></a>세로 막대형 차트를 추가하려면  
  
1.  **삽입** 탭 > **데이터 시각화** > **차트** > **차트 마법사**로 이동합니다.  
  
2.  **데이터 집합 선택** 페이지에서 **ListDataset**을 클릭하고 **다음**을 클릭합니다.  
  
3.  **세로 막대형**을 클릭하고 **다음**을 클릭합니다.  
  
4.  **차트 필드 정렬** 페이지에서 Product 필드를 **범주**로 끌어옵니다.  
  
5.  Sales를 **값** 으로 끌어온 후 **다음**을 클릭합니다.  
  
    세로 축에 값이 표시됩니다.  
  
6.  **마침**을 클릭합니다.  
  
    세로 막대형 차트가 보고서의 왼쪽 위 모퉁이에 추가됩니다.  
  
8.  차트의 너비와 높이를 각각 약 2.25인치와 4인치로 조정합니다.  
  
9. 차트를 원형 차트 아래의 사각형 안으로 끌어옵니다.  
   
10. 차트 제목을 선택하고 **Product Sales**를 입력합니다.  
  
12. **홈** 탭 > **글꼴**에서 제목을 다음과 같이 조정합니다.
    * **글꼴** **Segoe UI Semibold**을 참조하세요.
    * **크기** **12pt**을 참조하세요.
    * **색** **검정**을 참조하세요.  
  
15. 범례를 마우스 오른쪽 단추로 클릭한 다음 **범례 삭제**를 클릭합니다.  
  
    > [!NOTE]  
    > 범례를 제거하면 차트가 작을 때 차트를 읽기 쉬워집니다.  
  
    ![report-builder-free-form-column](../reporting-services/media/report-builder-free-form-column.png)

12. 차트 축을 선택하고 *홈** 탭 > **숫자** > **통화**로 이동합니다.

13. 숫자에 달러만 표시되고 센트는 표시되지 않도록 **소수 자릿수 줄이기** 를 두 번 선택합니다.      
### <a name="to-verify-the-charts-are-inside-the-rectangle"></a>차트가 사각형 내에 있는지 확인하려면  

사각형을 보고서 페이지에 있는 다른 항목의 컨테이너로 사용할 수 있습니다. 자세한 내용은 [사각형을 컨테이너로 사용](../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)을 참조하세요.
  
1.  이 단원의 앞부분에서 만들어 차트를 추가한 사각형을 선택합니다.  
  
    속성 창의 **Name** 속성에 사각형의 이름이 표시됩니다.  
  
    ![report-builder-free-form-rectangle-name](../reporting-services/media/report-builder-free-form-rectangle-name.png) 
  
2.  원형 차트를 클릭합니다.  
  
3.  **속성** 창에서 **Parent** 속성에 사각형의 이름이 포함되는지 확인합니다.  
  
     ![report-builder-free-form-pie-parent](../reporting-services/media/report-builder-free-form-pie-parent.png) 
  
4.  세로 막대형 차트를 클릭하고 3단계를 반복합니다.  
  
    > [!NOTE]  
    > 차트가 사각형 내에 없으면 렌더링된 보고서에 차트가 함께 표시되지 않습니다.  
  
### <a name="to-make-the-charts-the-same-size"></a>차트의 크기를 동일하게 하려면  
  
1.  원형 차트를 선택하고 Ctrl 키를 누른 다음 세로 막대형 차트를 선택합니다.  
  
2.  두 차트를 모두 선택한 상태로 > **레이아웃** > **같은 너비로**를 마우스 오른쪽 단추를 클릭합니다.  
  
    > [!NOTE]  
    > 선택한 모든 항목의 너비는 처음 클릭한 항목의 너비에 따라 결정됩니다.  
  
3.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
이제 보고서의 원형 차트 및 세로 막대형 차트에 요약 판매 데이터가 표시됩니다.  
  

  
## <a name="next-steps"></a>Next Steps  
자유 형식 보고서를 만드는 방법에 대한 자습서를 마쳤습니다.  
  
목록에 대한 자세한 내용은 다음을 참조하세요. 
* [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md) 
* [목록을 사용하여 송장 및 양식 만들기](../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)
* [테이블릭스 데이터 영역 셀, 행 및 열&#40;보고서 작성기&#41; 및 SSRS](../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
쿼리 디자이너에 대한 자세한 내용은 [쿼리 디자이너&#40;보고서 작성기&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9) 및 [텍스트 기반 쿼리 디자이너 사용자 인터페이스&#40;보고서 작성기&#41;](../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[보고서 작성기 자습서](../reporting-services/report-builder-tutorials.md) 
  

