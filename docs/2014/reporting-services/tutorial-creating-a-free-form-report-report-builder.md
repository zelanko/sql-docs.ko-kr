---
title: '자습서: 자유 형식 보고서 만들기(보고서 작성기) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 87288b59-faf2-4b1d-a8e4-a7582baedf2f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 332c67f47c8096cbeb5a94c4e2a288cd532038cf
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66098946"
---
# <a name="tutorial-creating-a-free-form-report-report-builder"></a>자습서: 자유 형식 보고서 (보고서 작성기) 만들기
  이 자습서에서는 양식 편지와 유사한 SSRS 자유 형식 보고서를 만드는 방법을 배웁니다. 입력란, 이미지 및 다른 데이터 영역이 있는 양식을 만들기 위해 보고서 항목을 정렬할 수 있습니다.  
  
 이 자습서에서 만드는 보고서는 자습서에 포함된 샘플 판매 데이터를 기반으로 합니다. 이 보고서에서는 정보가 지역별로 그룹화되고 지역의 판매 관리자 이름과 세부 및 요약 판매 정보가 표시됩니다. 목록 데이터 영역을 자유 형식 보고서의 기초로 사용한 다음, 이미지가 있는 장식 패널, 데이터가 삽입된 정적 텍스트, 세부 정보를 표시할 테이블, 요약 정보를 표시할 원형 및 세로 막대형 차트(선택 사항) 등을 추가합니다.  
  
##  <a name="BackToTop"></a> 학습할 내용  
 이 자습서에서는 다음 작업 방법을 배웁니다.  
  
-   [빈 보고서, 데이터 원본 및 데이터 집합 만들기](#BlankReport)  
  
-   [추가 하 고 목록 구성](#List)  
  
-   [그래픽 추가](#Graphics)  
  
-   [자유 형식 텍스트 추가](#Text)  
  
-   [세부 정보를 표시할 테이블 추가](#Table)  
  
-   [데이터 서식 지정](#Format)  
  
-   [보고서 저장](#Save)  
  
### <a name="other-optional-steps"></a>기타 선택적 단계  
  
-   [보고서 영역 구분 하는 줄을 추가 합니다.](#Line)  
  
-   [요약 데이터 시각화 추가](#Visualization)  
  
 이 자습서를 완료 하는 시간을 예상 합니다. 20분.  
  
## <a name="requirements"></a>요구 사항  
 요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/report-builder-tutorials.md)을 참조하세요.  
  
##  <a name="BlankReport"></a> 1. 빈 보고서, 데이터 원본 및 데이터 세트 만들기  
  
> [!NOTE]  
>  이 자습서에서 쿼리는 데이터 값을 포함하므로 보고서에는 외부 데이터 원본이 필요하지 않습니다. 이러한 종류의 내부 데이터의 사용은 학습 목적으로는 훌륭하지만 이 방식으로 만드는 쿼리는 길어집니다. 을 참조하십시오.  
  
#### <a name="to-create-a-blank-report"></a>빈 보고서를 만들려면  
  
1.  **시작**을 클릭하고 **프로그램**, **Microsoft SQL Server 2012 보고서 작성기**를 차례로 가리킨 다음 **보고서 작성기**를 클릭합니다.  
  
    > [!NOTE]  
    >  **시작** 대화 상자가 나타나야 합니다. 이 대화 상자가 나타나지 않으면 보고서 작성기 단추에서 **새로 만들기**를 클릭합니다.  
  
2.  **시작** 대화 상자의 왼쪽 창에서 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **빈 보고서**를 클릭합니다.  
  
#### <a name="to-create-a-new-data-source"></a>새 데이터 원본을 만들려면  
  
1.  보고서 데이터 창에서 **새로 만들기**를 클릭하고 **데이터 원본**을 클릭합니다.  
  
2.  에 `Name` 상자에 입력 합니다. **ListDataSource**  
  
3.  **내 보고서에 포함된 연결 사용**을 클릭합니다.  
  
4.  연결 형식이 Microsoft SQL Server인지 확인한 다음 **연결 문자열** 상자에 다음을 입력합니다. **데이터 원본 = \<servername>**  
  
     \<서버 이름 >에는 SQL Server 데이터베이스 엔진 인스턴스의 설치 된 컴퓨터를 지정 하는 예제 Report001, 합니다. 보고서 데이터는 SQL Server 데이터베이스에서 추출되지 않았으므로 데이터베이스 이름을 포함하지 않아야 합니다. 지정된 서버의 기본 데이터베이스는 쿼리를 구문 분석하는 데 사용됩니다.  
  
5.  **자격 증명**을 클릭하고 SQL Server 데이터베이스 엔진의 인스턴스에 연결해야 하는 자격 증명을 입력합니다.  
  
6.  **확인**을 클릭합니다.  
  
#### <a name="to-create-a-new-dataset"></a>새 데이터 세트를 만들려면  
  
1.  보고서 데이터 창에서 **새로 만들기**를 클릭한 다음, **데이터 세트**를 클릭합니다.  
  
2.  에 `Name` 상자에 입력 합니다. **ListDataset.**  
  
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
  
7.  실행 아이콘을 클릭하여 쿼리를 실행합니다.  
  
     쿼리 결과는 보고서에 표시할 수 있는 데이터입니다.  
  
     ![쿼리 디자이너](../../2014/tutorials/media/tutorial-querydesigner.png "쿼리 디자이너")  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="List"></a> 2. 목록 추가 및 구성  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 테이블, 행렬 및 목록이라는 세 가지 데이터 영역 템플릿을 제공합니다. 이러한 템플릿은 모두 테이블릭스 데이터 영역을 기반으로 합니다.  
  
 이 자습서에서는 목록을 사용하여 회보와 유사한 보고서에 판매 지역에 대한 판매 정보를 표시합니다. 이 정보는 지역별로 그룹화됩니다. 데이터를 지역별로 그룹화하는 새 행 그룹을 추가한 다음 기본 제공된 세부 정보 행 그룹을 삭제합니다. 목록 템플릿은 자유 형식 보고서를 만드는 데 이상적입니다. 자세한 내용은 [나열 &#40;보고서 작성기 및 SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)합니다.  
  
> [!NOTE]  
>  이 보고서에서는 Letter(8.5 X11) 용지 크기와 1인치 여백을 사용합니다. 보고서 페이지의 높이가 9인치보다 크거나 너비가 6 1/2인치보다 클 경우 빈 페이지가 생성될 수 있습니다.  
  
#### <a name="to-add-a-list"></a>목록을 추가하려면  
  
1.  리본 메뉴의 **삽입** 탭에 있는 **데이터 영역** 영역에서 **목록** 을 클릭하고 보고서 본문 안으로 목록을 끌어옵니다. 목록의 높이와 너비를 각각 7인치와 6.25인치로 만듭니다.  
  
2.  목록 안을 클릭하고 목록 맨 위를 마우스 오른쪽 단추로 클릭한 다음 **테이블릭스 속성**을 클릭합니다.  
  
     ![추가 목록](../../2014/tutorials/media/tutorial-addinglistwithnumbers.png "추가 목록")  
  
3.  **데이터 집합 이름** 드롭다운 목록에서 **ListDataset**을 선택합니다.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  목록 안을 마우스 오른쪽 단추로 클릭한 다음 **사각형 속성**을 클릭합니다.  
  
     ![사각형 속성 명령](../../2014/tutorials/media/tutorial-rectanglepropertiescommand.png "사각형 속성 명령")  
  
6.  **일반** 탭에서 **뒤에 페이지 나누기 추가** 확인란을 선택합니다.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-add-a-new-row-group-and-to-delete-the-details-group"></a>새 행 그룹을 추가하고 세부 정보 그룹을 삭제하려면  
  
1.  행 그룹 창에서 세부 정보 그룹을 마우스 오른쪽 단추로 클릭하고 **그룹 추가**를 가리킨 다음 **부모 그룹**을 클릭합니다.  
  
     ![상위 그룹 명령](../../2014/tutorials/media/tutorial-parentgroupcommand.png "상위 그룹 명령")  
  
2.  드롭다운 목록에서 `[Territory].`를 선택합니다.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     열이 목록에 추가됩니다. 이 열에는 `[Territory].` 셀이 있습니다  
  
4.  목록에서 Territory 열을 마우스 오른쪽 단추로 클릭한 다음 **열 삭제**를 클릭합니다.  
  
     ![열 삭제](../../2014/tutorials/media/tutorial-deletecolumnscommand.png "열 삭제")  
  
5.  **열만 삭제**를 클릭합니다.  
  
     ![열 삭제 대화 상자](../../2014/tutorials/media/tutorial-deletecolumnsdialog.png "열 삭제 대화 상자")  
  
6.  행 그룹 창에서 **세부 정보** 그룹을 마우스 오른쪽 단추로 클릭한 다음 **그룹 삭제**를 클릭합니다.  
  
     ![세부 정보 그룹 삭제](../../2014/tutorials/media/tutorial-deletedetailsgroup.png "세부 정보 그룹 삭제")  
  
7.  **그룹만 삭제**를 클릭합니다.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Graphics"></a> 3. 그래픽 추가  
 목록 데이터 영역을 사용할 경우의 장점 중 하나는 테이블 형식 레이아웃으로 제한하지 않고 사각형 및 입력란과 같은 보고서 항목을 어느 곳에나 추가할 수 있다는 점입니다. 색으로 채워진 사각형과 같은 그래픽을 추가하여 보고서의 모양을 돋보이게 할 수 있습니다.  
  
#### <a name="to-add-graphic-elements-to-the-report"></a>보고서에 그래픽 요소를 추가하려면  
  
1.  에 **삽입** 탭 리본 메뉴 클릭 **사각형**을 목록의 왼쪽된 위 모퉁이를 사각형을 끕니다. 사각형의 높이와 너비를 각각 7인치와 1인치로 만듭니다.  
  
2.  사각형을 마우스 오른쪽 단추로 클릭한 다음 **사각형 속성**을 클릭합니다.  
  
3.  **채우기** 탭을 클릭합니다.  
  
4.  **채우기 색** 드롭다운 목록에서 **다른 색**을 클릭한 다음 **진한 회색** 을 선택합니다.  
  
     ![채우기 색을 선택](../../2014/tutorials/media/tutorial-selectfillcolorwithnumbers.png "선택 채우기 색")  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 이제 보고서의 왼쪽에 진한 회색 사각형으로 구성된 세로 그래픽이 있습니다.  
  
##  <a name="Text"></a> 4. 자유 형식 텍스트 추가  
 입력란에는 각 보고서 페이지와 데이터 필드에서 반복되는 정적 텍스트가 포함됩니다.  
  
#### <a name="to-add-text-to-the-report"></a>보고서에 텍스트를 추가하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  리본 메뉴의 **삽입** 탭에서 **입력란**을 클릭한 다음 입력란을 목록의 왼쪽 상단으로 끌어 이전에 추가한 사각형 안에 배치합니다. 입력란의 높이와 너비를 각각 3인치와 5인치로 만듭니다.  
  
3.  입력란의 위쪽에 커서를 놓은 다음 입력: **Newsletter for**.  
  
     ![뉴스레터 제목 텍스트 추가](../../2014/tutorials/media/tutorial-newsletterfor.png "뉴스레터 제목 텍스트 추가")  
  
    > [!NOTE]  
    >  "for" 단어 뒤에 추가 공백을 포함해야 합니다. 이 공백은 텍스트와 다음 단계에서 추가할 필드를 구분합니다.  
  
4.  Territory 필드를 입력란으로 끌어 3단계에서 입력한 텍스트 뒤에 배치합니다.  
  
     ![영역 필드 추가](../../2014/tutorials/media/tutorial-addterritorialfield.png "영역 추가 필드")  
  
5.  모든 텍스트를 선택하고 마우스 오른쪽 단추를 클릭한 다음 **텍스트 속성**을 클릭합니다.  
  
6.  **글꼴** 탭을 클릭합니다.  
  
7.  **글꼴** 목록에서 **Times New Roman**을 선택하고 **크기** 에서 **20pt**를 선택한 다음 **색** 에서 **빨강**을 선택합니다.  
  
     ![텍스트 속성](../../2014/tutorials/media/tutorial-textpropertieswithnumbers.png "텍스트 속성")  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 형식과 3 단계에서 입력 한 텍스트 아래에 커서를 배치 합니다. **Hello** 합니다.  
  
    > [!NOTE]  
    >  "Hello" 단어 뒤에 추가 공백을 포함해야 합니다. 이 공백은 텍스트와 다음 단계에서 추가할 필드를 구분합니다.  
  
10. FullName 필드를 입력란으로 끌어 9단계에서 입력한 텍스트 뒤에 배치한 다음 쉼표(,)를 입력합니다.  
  
     ![전체 이름 필드 추가](../../2014/tutorials/media/tutorial-addfullnamefield.png "Full Name 추가 필드")  
  
11. 9-10단계에서 추가한 텍스트를 선택하고 마우스 오른쪽 단추를 클릭한 다음 **텍스트 속성**을 클릭합니다.  
  
12. **글꼴** 탭을 클릭합니다.  
  
13. **글꼴** 목록에서 **Times New Roman**을 선택하고 **크기** 에서 **16pt**를 선택한 다음 **색** 에서 **검정** 을 선택합니다.  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
15. 9-13단계에서 추가한 텍스트 아래에 커서를 놓고 다음의 예제 텍스트를 복사하여 붙여 넣습니다.  
  
    ```  
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin sed dolor in ipsum pulvinar egestas. Sed sed lacus at leo ornare ultricies. Vivamus velit risus, euismod nec sodales gravida, gravida in dui. Etiam ullamcorper elit vitae justo fermentum ut ullamcorper augue sodales. Ut placerat, nisl quis feugiat adipiscing, nibh est aliquet est, mollis faucibus mauris lectus quis arcu. In mollis tincidunt lacinia. In vitae erat ut lorem tincidunt luctus. Curabitur et magna nunc, sit amet adipiscing nisi. Nulla rhoncus elementum orci nec tincidunt. Aliquam imperdiet cursus erat vel tincidunt. Donec et neque ac urna rutrum sodales. In id purus et nisl dignissim dapibus. Sed rhoncus metus at felis feugiat eu tempor dolor vehicula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam faucibus consectetur diam eu pellentesque.   
    Nulla facilisi. Proin ligula enim, porta ut tincidunt id, adipiscing sit amet eros. Ut purus sem, bibendum et vulputate sit amet, facilisis eget magna. Sed aliquam erat non erat eleifend hendrerit. Ut a ligula est, sit amet eleifend enim. Ut et nisl enim, sit amet adipiscing augue. Vivamus eu arcu ac libero posuere elementum. Integer condimentum bibendum venenatis. Integer odio tellus, feugiat in pellentesque semper, interdum nec sem. Sed cursus euismod sem, ut elementum sapien placerat vel.   
    ```  
  
16. 15단계에서 추가한 텍스트를 선택하고 마우스 오른쪽 단추를 클릭한 다음 **텍스트 속성**을 클릭합니다.  
  
17. **글꼴** 탭을 클릭합니다.  
  
18. **글꼴** 목록에서 **Arial**을 선택하고 **크기** 에서 **10pt**를 선택한 다음 **색상** 에서 **검정**을 선택합니다.  
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     ![뉴스레터 텍스트 추가](../../2014/tutorials/media/tutorial-newslettertext.png "뉴스레터 텍스트 추가")  
  
20. 15 단계에서 붙여 넣은 텍스트 아래에 커서를 놓고 입력 합니다. **축에 총 판매량에** 입니다.  
  
    > [!NOTE]  
    >  "of" 단어 뒤에 추가 공백을 포함해야 합니다. 이 공백은 텍스트와 다음 단계에서 추가할 필드를 구분합니다.  
  
21. Sales 필드를 입력란으로 끌어 20단계에서 입력한 텍스트 뒤에 배치한 다음 느낌표(!)를 입력합니다.  
  
22. Sales 필드를 강조 표시, 필드를 마우스 오른쪽 단추로 클릭 하 고, 클릭 **식**합니다.  
  
23. 식 상자에서 다음과 같이 Sum 함수를 포함하도록 식을 변경합니다.  
  
    ```  
    =Sum(Fields!Sales.value)  
    ```  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     ![판매량 필드에 식을 추가](../../2014/tutorials/media/tutorial-addexpressiontosalesfield.png "판매량 필드에 식 추가")  
  
25. 20-23단계에서 추가한 텍스트를 선택하고 마우스 오른쪽 단추를 클릭한 다음 **텍스트 속성**을 클릭합니다.  
  
26. **글꼴** 탭을 클릭합니다.  
  
27. **글꼴** 목록에서 **Times New Roman**을 선택하고 **크기** 에서 **16pt**를 선택한 다음 **색** 에서 **빨강**을 선택합니다.  
  
28. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
29. `[Sum(Sales)]` 를 선택하고 **홈** 탭의 **숫자** 그룹에서 **통화** 단추를 클릭합니다.  
  
     ![추가 통화 기호](../../2014/tutorials/media/tutorial-addcurrencysymbol.png "통화 기호 추가")  
  
30. "제목을 추가하려면 클릭하십시오." 텍스트가 있는 입력란을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
31. 목록 상자를 선택하고 화살표 키를 사용하여 페이지의 위쪽으로 이동합니다.  
  
32. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 보고서에 정적 테스트가 표시되고 각 보고서 페이지에 지역과 관련된 데이터가 포함됩니다. Sales의 서식이 통화로 지정됩니다.  
  
 ![뉴스레터 미리 보기](../../2014/tutorials/media/tutorial-newsletters.png "뉴스레터 미리 보기")  
  
##  <a name="Table"></a> 5. 테이블을 추가하여 Sales 세부 정보 표시  
 새 테이블 및 행렬 마법사를 사용하여 자유 형식 보고서에 테이블을 추가합니다. 마법사를 완료한 후에는 합계를 표시할 행을 수동으로 추가합니다.  
  
#### <a name="to-add-a-table"></a>테이블을 추가하려면  
  
1.  리본 메뉴의 **삽입** 탭에 있는 **데이터 영역** 영역에서 **테이블**을 클릭한 다음 **테이블 마법사**를 클릭합니다.  
  
2.  데이터 세트 선택 페이지에서 **ListDataset**을 클릭합니다.  
  
3.  **다음**을 클릭합니다.  
  
4.   **필드 정렬** 페이지에서 **사용 가능한 필드** 의 Product 필드를 **값**으로 끌어옵니다.  
  
5.  SalesDate, Quantity 및 Sales에 대해 4단계를 반복합니다. SalesDate는 Product 아래에 배치하고, Quantity는 SalesDate 아래에 배치하고, Sales는SalesDate 아래에 배치합니다.  
  
6.  **다음**을 클릭합니다.  
  
7.  **레이아웃 선택** 페이지에서 테이블의 레이아웃을 확인합니다.  
  
     이 테이블은 매우 간단하여 5개의 열로 구성되며 행 또는 열 그룹이 없습니다. 그룹이 없기 때문에 그룹과 관련된 레이아웃 옵션은 사용할 수 없습니다. 이 자습서의 뒷부분에서 합계를 포함하도록 테이블을 수동으로 업데이트할 것입니다.  
  
8.  **다음**을 클릭합니다.  
  
9. **스타일 선택** 페이지의 **스타일** 창에서 **Slate**를 선택합니다.  
  
10. **마침**을 클릭합니다.  
  
11. 테이블을 4단원에서 추가한 입력란 아래로 끌어옵니다.  
  
    > [!NOTE]  
    >  테이블이 목록 내에 표시되는지 확인합니다.  
  
12. 테이블이 선택되었는지 확인한 다음 행 그룹 창에서 세부 정보를 마우스 오른쪽 단추로 클릭하고 **합계 추가**를 가리킨 다음 **뒤**를 클릭합니다.  
  
     ![보고서 합계 추가](../../2014/tutorials/media/tutorial-addtotal.png "보고서 합계 추가")  
  
13. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 보고서에 판매 세부 정보 및 합계가 포함된 테이블이 표시됩니다.  
  
 ![보고서의 판매량 합계](../../2014/tutorials/media/tutorial-reportsalestotals.png "보고서의 판매량 합계")  
  
##  <a name="Format"></a> 6. 데이터 서식 지정  
 숫자 데이터의 서식을 통화로 지정하고 날짜의 서식을 날짜와 시간으로 지정합니다.  
  
#### <a name="to-format-fields-table"></a>필드 테이블의 형식을 지정하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 전환합니다.  
  
2.  `[Sum(SalesSales)]` 이 들어 있는 테이블 셀을 클릭하고 **홈** 탭의 **숫자** 그룹에서 **통화** 단추를 클릭합니다.  
  
     ![판매 합계에 통화 기호를 추가](../../2014/tutorials/media/tutorial-sumsales-currencysymbol.png "판매 합계에 통화 기호 추가")  
  
3.  `[SalesDate]` 가 들어 있는 셀을 클릭하고 **숫자** 그룹의 드롭다운 목록에서 **날짜**를 선택합니다.  
  
4.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 이제 보고서에 서식이 지정된 데이터가 표시되므로 보다 쉽게 읽을 수 있습니다.  
  
 ![보고서의 판매량 합계를 포맷](../../2014/tutorials/media/tutorial-reportsalestotals-formatted.png "형식 보고서의 판매량 합계")  
  
##  <a name="Save"></a> 7. 보고서 저장  
 보고서를 보고서 서버, SharePoint 라이브러리 또는 컴퓨터에 저장할 수 있습니다. 보고서를 실행하고 **내보내기** 메뉴에서 형식을 선택하여 보고서를 Word 및 PDF 등의 다양한 형식으로 내보낼 수도 있습니다.  
  
 이 자습서에서는 보고서를 보고서 서버에 저장합니다. 보고서 서버에 액세스할 수 없는 경우에는 보고서를 컴퓨터에 저장하십시오.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>보고서를 보고서 서버에 저장하려면  
  
1.  **보고서 작성기** 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
2.  **최근에 사용한 사이트 및 서버**를 클릭합니다.  
  
3.  보고서를 저장할 수 있는 권한을 가진 보고서 서버의 이름을 선택하거나 입력합니다.  
  
     "보고서 서버에 연결하는 중"이라는 메시지가 나타납니다. 연결되면 보고서 서버 관리자가 보고서의 기본 위치로 지정한 보고서 폴더의 내용이 표시됩니다.  
  
4.  `Name`를 사용 하 여 기본 이름을 바꿀 **SalesInformationByTerritory**합니다.  
  
5.  **저장**을 클릭합니다.  
  
 보고서가 보고서 서버에 저장됩니다. 연결된 보고서 서버의 이름이 창 아래쪽에 있는 상태 표시줄에 나타납니다.  
  
#### <a name="to-save-the-report-on-your-computer"></a>컴퓨터에 보고서를 저장하려면  
  
1.  **보고서 작성기** 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
2.  **바탕 화면**, **내 문서**또는 **내 컴퓨터**를 클릭한 다음 보고서를 저장할 폴더를 찾습니다.  
  
3.  `Name`를 사용 하 여 기본 이름을 바꿀 **SalesInformationByTerritory**합니다.  
  
4.  **저장**을 클릭합니다.  
  
##  <a name="Line"></a> 8. (선택 사항) 선을 추가하여 보고서 영역 구분  
 선을 추가하여 보고서의 편집 영역과 세부 정보 영역을 구분합니다.  
  
#### <a name="to-add-a-line"></a>선을 추가하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  리본 메뉴의 **삽입** 탭에 있는 **보고서 항목** 영역에서 **선**을 클릭합니다.  
  
3.  4단원에서 추가한 자유 형식 입력란 아래로 선을 끌어옵니다.  
  
4.  선을 클릭합니다.  
  
5.  **홈** 탭을 클릭합니다.  
  
6.  **테두리** 영역에서 너비를 **4 1/2** pt로 선택하고 색을 **빨강**으로 선택합니다.  
  
     ![보고서에 줄을 추가](../../2014/tutorials/media/tutorial-reportwithline.png "보고서에 선 추가")  
  
##  <a name="Visualization"></a> 9. (선택 사항) 요약 데이터 시각화 추가  
 사각형은 보고서가 렌더링되는 방식을 제어하는 데 유용합니다. 원형 및 세로 막대형 차트를 사각형 내에 배치하여 보고서가 원하는 방식으로 렌더링되도록 합니다.  
  
#### <a name="to-add-a-rectangle"></a>사각형을 추가하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  리본 메뉴의 **삽입** 탭에 있는 **보고서 항목** 영역에서 **사각형**을 클릭한 다음 사각형을 테이블 오른쪽의 목록 안으로 끌어옵니다. 사각형의 너비와 높이를 각각 2인치와 4인치로 만듭니다.  
  
3.  사각형과 테이블의 위쪽을 맞춥니다.  
  
#### <a name="to-add-a-pie-chart"></a>원형 차트를 추가하려면  
  
1.  리본 메뉴의 **삽입** 탭에 있는 **데이터 시각화** 영역에서 **차트** 를 클릭한 다음 **차트 마법사**를 클릭합니다.  
  
2.  데이터 세트 선택 페이지에서 **ListDataset**을 클릭한 후, **다음**을 클릭합니다.  
  
3.  **원형**을 클릭하고 **다음**을 클릭합니다.  
  
4.  차트 필드 정렬 페이지에서 Product를 **범주**로 끌어옵니다.  
  
5.  Quantity를 끌어 옵니다 **값**를 클릭 하 고 **다음**합니다.  
  
6.  **스타일 선택** 페이지의 **스타일** 창에서 **Slate**를 선택합니다.  
  
7.  **마침**을 클릭합니다.  
  
8.  보고서의 왼쪽 위 모퉁이에 나타나는 차트의 높이와 너비를 각각 1 1/2인치와 2인치로 조정합니다.  
  
9. 차트를 사각형 안으로 끌어옵니다.  
  
     ![원형 차트 추가](../../2014/tutorials/media/tutorial-addpiechart.png "원형 차트 추가")  
  
10. 차트 제목을 마우스 오른쪽 단추로 클릭한 다음 **제목 속성**을 클릭합니다.  
  
11. 에 **차트 제목 속성** 대화 상자의 제목 입력란에서: **Product Quantities Sold**.  
  
12. **글꼴** 탭을 클릭하고 **크기** 목록에서 **10pt**를 클릭합니다.  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-add-a-column-chart"></a>세로 막대형 차트를 추가하려면  
  
1.  리본 메뉴의 **삽입** 탭에 있는 **데이터 시각화** 영역에서 **차트** 를 클릭한 다음 **차트 마법사**를 클릭합니다.  
  
2.  **데이터 집합 선택** 페이지에서 **ListDataset**을 클릭하고 **다음**을 클릭합니다.  
  
3.  **세로 막대형**을 클릭하고 **다음**을 클릭합니다.  
  
4.  차트 필드 정렬 페이지에서 Product 필드를 끌어 **범주**합니다.  
  
5.  Sales를 **값** 으로 끌어온 후 **다음**을 클릭합니다.  
  
     세로 축에 값이 표시됩니다.  
  
6.  **스타일 선택** 페이지의 **스타일** 창에서 **Slate**를 선택합니다.  
  
7.  **마침**을 클릭합니다.  
  
     세로 막대형 차트가 보고서의 왼쪽 위 모퉁이에 추가됩니다.  
  
8.  차트의 너비와 높이를 모두 2인치로 조정합니다.  
  
9. 차트를 원형 차트 아래의 사각형 안으로 끌어옵니다.  
  
     ![추가 세로 막대형 차트](../../2014/tutorials/media/tutorial-addcolumnchart.png "세로 막대형 차트 추가")  
  
10. 차트 제목을 마우스 오른쪽 단추로 클릭한 다음 **제목 속성**을 클릭합니다.  
  
11. 에 **차트 제목 속성** 대화 상자의 제목 입력란에서: **Product Sales**.  
  
12. **글꼴** 탭을 클릭하고 **크기** 목록에서 **10pt**를 클릭한 다음 **확인**을 클릭합니다.  
  
13. 세로 막대형 차트에서 세로 축을 마우스 오른쪽 단추로 클릭한 다음 **축 제목 표시**의 선택을 취소합니다.  
  
14. 가로 축에 대해 13단계를 반복합니다.  
  
15. 범례를 마우스 오른쪽 단추로 클릭한 다음 **범례 삭제**를 클릭합니다.  
  
    > [!NOTE]  
    >  차트 크기가 작은 경우 축 제목 및 범례를 제거하면 차트를 더 쉽게 읽을 수 있습니다.  
  
 ![차트 제목 변경 및 축 제목 제거](../../2014/tutorials/media/tutorial-columnchart-newtitle-noaxistitle.png "차트 제목 변경 및 축 제목 제거")  
  
#### <a name="to-verify-the-charts-are-inside-the-rectangle"></a>차트가 사각형 내에 있는지 확인하려면  
  
1.  이 단원의 앞부분에서 추가한 사각형을 클릭합니다.  
  
     속성 창의 `Name` 속성에 사각형의 이름이 표시됩니다.  
  
     ![사각형의 이름이](../../2014/tutorials/media/tutorial-rectanglename.png "사각형의 이름")  
  
2.  원형 차트를 클릭합니다.  
  
3.  에 **속성** 창 확인는 `Parent` 속성에 사각형의 이름이 포함 되어 있습니다.  
  
     ![원형 차트에 대 한 속성을 부모](../../2014/tutorials/media/tutorial-piechart-parentproperty.png "부모 원형 차트에 대 한 속성")  
  
4.  세로 막대형 차트를 클릭하고 2~3단계를 반복합니다.  
  
    > [!NOTE]  
    >  차트가 사각형 내에 없으면 렌더링된 보고서에 차트가 함께 표시되지 않습니다.  
  
#### <a name="to-make-the-charts-the-same-size"></a>차트의 크기를 동일하게 하려면  
  
1.  원형 차트를 클릭하고 Ctrl 키를 누른 다음 세로 막대형 차트를 클릭합니다.  
  
2.  두 차트를 모두 선택한 상태로 마우스 오른쪽 단추를 클릭한 다음 **레이아웃**을 가리키고 **같은 너비로**를 클릭합니다.  
  
     ![차트 너비를 동일 하 게](../../2014/tutorials/media/tutorial-makechartssamewidth.png "차트 너비를 동일 하 게")  
  
    > [!NOTE]  
    >  선택한 모든 항목의 너비는 처음 클릭한 항목의 너비에 따라 결정됩니다.  
  
3.  **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 이제 보고서의 원형 차트 및 세로 막대형 차트에 요약 판매 데이터가 표시됩니다.  
  
 ![SSRS 자습서, 자유 형식 보고서](../../2014/tutorials/media/tutorial-reportfinal.png "SSRS 자습서, 자유 형식 보고서")  
  
## <a name="more-information"></a>추가 정보  
 목록에 대 한 자세한 내용은 참조 하세요. [테이블, 행렬 및 목록 &#40;보고서 작성기 및 SSRS&#41;](report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)를 [나열 &#40;보고서 작성기 및 SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)하십시오 [테이블 릭 스 데이터 영역 &#40;보고서 작성기 및 SSRS&#41;](report-design/tablix-data-region-areas-report-builder-and-ssrs.md), 및 [테이블 릭 스 데이터 영역 셀, 행 및 열 &#40;보고서 작성기&#41; 및 SSRS](report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 쿼리 디자이너에 대한 자세한 내용은 [쿼리 디자이너&#40;보고서 작성기&#41;](../../2014/reporting-services/query-designers-report-builder.md) 및 [텍스트 기반 쿼리 디자이너 사용자 인터페이스&#40;보고서 작성기&#41;](report-data/text-based-query-designer-user-interface-report-builder.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [자습서 &#40;보고서 작성기&#41;](report-builder-tutorials.md)   
 [SQL Server 2014의 보고서 작성기](report-builder/report-builder-in-sql-server-2016.md)  
  
  
