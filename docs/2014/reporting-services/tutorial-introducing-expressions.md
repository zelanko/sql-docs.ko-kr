---
title: '자습서: 식 소개 | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2d05ef4c-5f91-48b2-8795-f0a201a0b3cc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 79563abac2c6a9ed64dff93667ff3d3966b70bc5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098851"
---
# <a name="tutorial-introducing-expressions"></a>자습서: 식 소개
  식은 강력하고 융통성 있는 보고서를 만드는 데 도움이 됩니다. 이 자습서에서는 일반 함수와 연산자를 사용하는 식을 만들고 구현하는 방법을 배웁니다. **식** 대화 상자를 사용 하 여 이름 값을 연결 하 고, 별도의 데이터 집합에서 값을 조회 하 고, 필드 값에 따라 다른 그림을 표시 하는 식을 작성 합니다.  
  
 보고서에는 가로줄무늬가 있으며 흰색 행과 다른 색 행이 번갈아 표시됩니다. 보고서에는 흰색이 아닌 행의 색을 선택하기 위한 매개 변수가 포함됩니다.  
  
 다음 그림에서는 만들려는 보고서와 비슷한 보고서를 보여 줍니다.  
  
 ![rs_ExpressionsTutorial](../../2014/tutorials/media/rs-expressionstutorial.gif "rs_ExpressionsTutorial")  
  
##  <a name="what-you-will-learn"></a><a name="BackToTop"></a>학습 내용  
 이 자습서에서는 다음 작업 방법을 배웁니다.  
  
1.  [테이블 또는 행렬 마법사에서 테이블 보고서 및 데이터 세트 만들기](#Setup)  
  
2.  [데이터 원본 및 데이터 세트의 기본 이름 업데이트](#UpdateNames)  
  
3.  [이름, 이니셜 및 성 표시](#Concatenate)  
  
4.  [이미지를 사용하여 성별 표시](#Gender)  
  
5.  [CountryRegion 이름 조회](#Lookup)  
  
6.  [마지막 구입 이후 일수 계산](#Count)  
  
7.  [표시기를 사용하여 판매량 비교 표시](#Indicator)  
  
8.  [보고서를 "녹색 막대" 보고서로 만들기](#GreenBar)  
  
### <a name="other-optional-steps"></a>기타 선택적 단계  
  
-   [날짜 열 서식 지정](#DateFormat)  
  
-   [보고서 제목 추가](#Title)  
  
-   [보고서 저장](#Save)  
  
 이 자습서에 소요되는 예상 시간: 30분  
  
## <a name="requirements"></a>요구 사항  
 요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/report-builder-tutorials.md)을 참조하세요.  
  
##  <a name="1-create-a-table-report-and-dataset-from-the-table-or-matrix-wizard"></a><a name="Setup"></a>1. 테이블 또는 행렬 마법사에서 테이블 보고서 및 데이터 집합 만들기  
 테이블 보고서, 데이터 원본 및 데이터 세트를 만듭니다. 테이블의 레이아웃을 지정할 때는 몇몇 필드만 포함하고, 마법사를 완료한 후 열을 수동으로 추가합니다. 마법사에서는 손쉽게 테이블의 레이아웃을 지정하고 스타일을 적용할 수 있습니다.  
  
> [!NOTE]  
>  이 자습서의 쿼리에는 데이터 값이 포함되어 있으므로 외부 데이터 원본이 필요하지 않습니다. 따라서 쿼리가 상당히 길어집니다. 비즈니스 환경에서는 쿼리에 데이터가 포함되지 않을 것입니다. 이 자습서의 쿼리는 학습용으로만 제공됩니다.  
  
> [!NOTE]  
>  이 자습서에서 마법사의 단계는 하나의 절차로 통합됩니다. 보고서 서버를 찾고, 데이터 원본을 선택하고, 데이터 세트를 만드는 방법에 대한 단계별 지침은 이 시리즈의 첫 번째 자습서인 [자습서: 기본 테이블 보고서 만들기&#40;보고서 작성기&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)을 참조하세요.  
  
#### <a name="to-create-a-new-table-report"></a>새 테이블 보고서를 만들려면  
  
1.  **시작**을 클릭 하 고 **프로그램**, [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] **보고서 작성기**을 차례로 가리킨 다음 **보고서 작성기**를 클릭 합니다.  
  
     **시작** 대화 상자가 나타납니다.  
  
    > [!NOTE]  
    >  **시작** 대화 상자가 나타나지 않으면 **보고서 작성기** 단추에서 **새로 만들기**를 클릭합니다.  
  
    > [!NOTE]  
    >  보고서 작성기 ClickOnce 버전을 사용 하는 것을 선호 하는 경우 보고서 관리자를 열고 **보고서 작성기**를 클릭 하거나, 보고서와 같은 Reporting Services 내용 유형이 설정 된 SharePoint 사이트로 이동 하 고 공유 문서 라이브러리의 **문서** 탭에 있는 **새 문서** 메뉴에서 **보고서 작성기 보고서** 를 클릭 합니다.  
  
2.  왼쪽 창에 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **테이블 또는 행렬 마법사**를 클릭합니다.  
  
4.  **데이터 세트 선택** 페이지에서 **데이터 세트 만들기**를 클릭합니다.  
  
5.  **다음**을 클릭합니다.  
  
6.  **데이터 원본에 대한 연결 선택** 페이지에서 **SQL Server**형식의 데이터 원본을 선택합니다. 목록에서 데이터 원본을 선택하거나 보고서 서버를 찾아 선택합니다.  
  
7.  **다음**을 클릭합니다.  
  
8.  **쿼리 디자인** 페이지에서 **텍스트로 편집**을 클릭합니다.  
  
9. 쿼리 창에 다음 쿼리를 붙여 넣습니다.  
  
    ```  
    SELECT 'Lauren' AS FirstName,'Johnson' AS LastName, 'American Samoa' AS StateProvince, 1 AS CountryRegionID,'Unknown' AS Gender, CAST(9996.60 AS money) AS YTDPurchase, CAST('2010-6-10' AS date) AS LastPurchase  
    UNION SELECT'Warren' AS FirstName, 'Pal' AS LastName, 'New South Wales' AS StateProvince, 2 AS CountryRegionID, 'Male' AS Gender, CAST(5747.25 AS money) AS YTDPurchase, CAST('2010-7-3' AS date) AS LastPurchase  
    UNION SELECT 'Fernando' AS FirstName, 'Ross' AS LastName, 'Alberta' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(9248.15 AS money) AS YTDPurchase, CAST('2010-10-17' AS date) AS LastPurchase  
    UNION SELECT 'Rob' AS FirstName, 'Caron' AS LastName, 'Northwest Territories' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(742.50 AS money) AS YTDPurchase, CAST('2010-4-29' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Bailey' AS LastName, 'British Columbia' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(1147.50 AS money) AS YTDPurchase, CAST('2010-6-15' AS date) AS LastPurchase  
    UNION SELECT  'Bridget' AS FirstName, 'She' AS LastName, 'Hamburg' AS StateProvince, 4 AS CountryRegionID, 'Female' AS Gender, CAST(7497.30 AS money) AS YTDPurchase, CAST('2010-5-10' AS date) AS LastPurchase  
    UNION SELECT 'Alexander' AS FirstName, 'Martin' AS LastName, 'Saxony' AS StateProvince, 4 AS CountryRegionID, 'Male' AS Gender, CAST(2997.60 AS money) AS YTDPurchase, CAST('2010-11-19' AS date) AS LastPurchase  
    UNION SELECT 'Yolanda' AS FirstName, 'Sharma' AS LastName ,'Micronesia' AS StateProvince, 5 AS CountryRegionID, 'Female' AS Gender, CAST(3247.95 AS money) AS YTDPurchase, CAST('2010-8-23' AS date) AS LastPurchase  
    UNION SELECT 'Marc' AS FirstName, 'Zimmerman' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1200.00 AS money) AS YTDPurchase, CAST('2010-11-16' AS date) AS LastPurchase  
    UNION SELECT 'Katherine' AS FirstName, 'Abel' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Female' AS Gender, CAST(2025.00 AS money) AS YTDPurchase, CAST('2010-12-1' AS date) AS LastPurchase  
    UNION SELECT 'Nicolas' as FirstName, 'Anand' AS LastName, 'Seine (Paris)' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1425.00 AS money) AS YTDPurchase, CAST('2010-12-11' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Peters' AS LastName, 'England' AS StateProvince, 12 AS CountryRegionID, 'Male' AS Gender, CAST(887.50 AS money) AS YTDPurchase, CAST('2010-8-15' AS date) AS LastPurchase  
    UNION SELECT 'Alison' AS FirstName, 'Nath' AS LastName, 'Alaska' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(607.50 AS money) AS YTDPurchase, CAST('2010-10-13' AS date) AS LastPurchase  
    UNION SELECT 'Grace' AS FirstName, 'Patterson' AS LastName, 'Kansas' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(1215.00 AS money) AS YTDPurchase, CAST('2010-10-18' AS date) AS LastPurchase  
    UNION SELECT 'Bobby' AS FirstName, 'Sanchez' AS LastName, 'North Dakota' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(6191.00 AS money) AS YTDPurchase, CAST('2010-9-17' AS date) AS LastPurchase  
    UNION SELECT 'Charles' AS FirstName, 'Reed' AS LastName, 'Nebraska' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8772.00 AS money) AS YTDPurchase, CAST('2010-8-27' AS date) AS LastPurchase  
    UNION SELECT 'Orlando' AS FirstName, 'Romeo' AS LastName, 'Texas' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8578.00 AS money) AS YTDPurchase, CAST('2010-7-29' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2010-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2010-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2010-11-30' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2010-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2010-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2010-11-30' AS date) AS LastPurchase  
    ```  
  
     이 쿼리에서는 생일, 이름, 성, 시/도, 국가/지역 식별자, 성별 및 구매량 연간 누계를 포함하는 열 이름을 지정합니다.  
  
10. 쿼리 디자이너 도구 모음에서 **실행** (**!**)을 클릭 합니다. 결과 집합에는 20행의 데이터가 표시되고 FirstName, LastName, StateProvince, CountryRegionID, Gender, YTDPurchase 및 LastPurchase 열이 포함됩니다.  
  
11. **다음**을 클릭합니다.  
  
12. **필드 정렬** 페이지에서 다음 필드를 지정된 순서에 따라 **사용 가능한 필드** 목록에서 **값** 목록으로 끌어옵니다.  
  
    -   StateProvince  
  
    -   CountryRegionID  
  
    -   LastPurchase  
  
    -   YTDPurchase  
  
     CountryRegionID 및 YTDPurchase는 숫자 데이터를 포함하므로 SUM 집계가 기본적으로 적용됩니다.  
  
    > [!NOTE]  
    >  FirstName 및 LastName 필드는 포함되지 않으며, 이후 단계에서 두 필드를 추가합니다.  
  
13. **값** 목록에서를 마우스 오른쪽 단추로 클릭 `CountryRegionID` 하 고 **Sum** 옵션을 클릭 합니다.  
  
     Sum은 더 이상 CountryRegionID에 적용되지 않습니다.  
  
14. **값** 목록에서 **YTDPurchase** 를 마우스 오른쪽 단추로 클릭하고 **Sum** 옵션을 클릭합니다.  
  
     Sum은 더 이상 YTDPurchase에 적용되지 않습니다.  
  
15. **다음**을 클릭합니다.  
  
16. **레이아웃 선택** 페이지에서 **다음**을 클릭합니다.  
  
17. **스타일 선택** 페이지에서 **슬레이트**를 클릭 한 다음 **마침**을 클릭 합니다.  
  
##  <a name="2-update-default-names-of-the-data-source-and-dataset"></a><a name="UpdateNames"></a>2. 데이터 원본 및 데이터 집합의 기본 이름 업데이트  
  
#### <a name="to-update-the-default-name-of-the-data-source"></a>데이터 원본의 기본 이름을 업데이트하려면  
  
1.  보고서 데이터 창에서 **데이터 원본**을 확장합니다.  
  
2.  **DataSource1** 을 마우스 오른쪽 단추로 클릭하고 **데이터 원본 속성**을 클릭합니다.  
  
3.  **이름** 상자에 **ExpressionsDataSource**를 입력합니다.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-update-the-default-name-of-the-dataset"></a>데이터 세트의 기본 이름을 업데이트하려면  
  
1.  보고서 데이터 창에서 **데이터 세트**를 확장합니다.  
  
2.  **DataSet1**을 마우스 오른쪽 단추로 클릭하고 **데이터 세트 속성**을 클릭합니다.  
  
3.  **이름** 상자에 **Expressions**를 입력합니다.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="3-display-first-name-initial-and-last-name"></a><a name="Concatenate"></a>3. 이름, 이니셜 및 성 표시  
 이니셜과 성을 포함하는 이름으로 계산되는 식에서 **Left** 함수와 **Concatenate**(**&**) 연산자를 사용합니다. 단계별로 식을 작성하거나 절차에서 단계를 건너뛰고 자습서의 식을 복사하여 **식** 대화 상자에 붙여넣을 수 있습니다.  
  
#### <a name="to-add-the-name-column"></a>Name 열을 추가하려면  
  
1.  **StateProvince** 열을 마우스 오른쪽 단추로 클릭하고 **열 삽입**을 가리킨 다음 **왼쪽**을 클릭합니다.  
  
     새 열이 **StateProvince** 열의 왼쪽에 추가됩니다.  
  
2.  새 열의 제목을 클릭하고 **Name**을 입력합니다.  
  
3.  **Name** 열의 데이터 셀을 마우스 오른쪽 단추로 클릭하고 **식**을 클릭합니다.  
  
4.  **식** 대화 상자에서 **일반 함수**를 확장하고 **텍스트**를 클릭합니다.  
  
5.  **항목** 목록에서 **Left**를 두 번 클릭합니다.  
  
     **Left** 함수가 식에 추가됩니다.  
  
6.  **범주** 목록에서 **필드(식)** 를 클릭합니다.  
  
7.  **값** 목록에서 **FirstName**을 두 번 클릭합니다.  
  
8.  **, 1)** 을 입력합니다.  
  
     이 식은 **FirstName** 값에서 가장 왼쪽의 한 자를 추출합니다.  
  
9. **&" "&** 를 입력합니다.  
  
10. **값** 목록에서 **LastName**을 두 번 클릭합니다.  
  
     완성된 식은 다음과 같습니다. `=Left(Fields!FirstName.Value, 1) &" "& Fields!LastName.Value`  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
##  <a name="4-use-images-to-display-gender"></a><a name="Gender"></a>4. 이미지를 사용 하 여 성별 표시  
 이미지를 사용하여 사용자의 성별을 표시하고 제3의 이미지를 사용하여 알 수 없는 성별 값을 식별합니다. 보고서에 세 개의 숨겨진 이미지와 새 열을 추가하여 이미지를 표시한 다음 Gender 필드의 값에 따라 열에 나타나는 이미지를 결정합니다.  
  
 보고서를 가로줄무늬가 있는 보고서로 만들 때 이미지가 포함된 테이블 셀에 색을 적용하려면 사각형을 추가한 다음 이미지를 사각형에 추가합니다. 배경색을 사각형에 적용할 수 있지만 이미지에는 적용할 수 없기 때문에 사각형을 사용해야 합니다.  
  
 이 자습서에서는 Windows와 함께 설치된 이미지를 사용하지만 사용 가능한 어떠한 이미지라도 사용할 수 있습니다. 포함 이미지를 사용하지만 포함 이미지가 로컬 컴퓨터나 보고서 서버에 설치되어 있지 않아도 됩니다.  
  
#### <a name="to-add-images-to-the-report-body"></a>보고서 본문에 이미지를 추가하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  리본의 **삽입** 탭에서 **이미지**를 클릭한 다음 보고서 본문에서 테이블 아래를 클릭합니다.  
  
     **이미지 속성** 대화 상자가 열립니다.  
  
3.  **가져오기**를 클릭하고 C:\Users\Public\Public Pictures\Sample Pictures로 이동합니다.  
  
4.  Penguins.JPG를 클릭하고 **열기**를 클릭합니다.  
  
     **이미지 속성** 대화 상자에서 **표시 유형**을 클릭한 다음 **숨기기** 옵션을 클릭합니다.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  2~5단계를 반복하되 Koala.JPG를 선택합니다.  
  
7.  2~5단계를 반복하되 Tulips.JPG를 선택합니다.  
  
#### <a name="to-add-the-gender-column"></a>Gender 열을 추가하려면  
  
1.  **Name** 열을 마우스 오른쪽 단추로 클릭하고 **열 삽입**을 가리킨 다음 **오른쪽**을 클릭합니다.  
  
     새 열이 **Name** 열의 오른쪽에 추가됩니다.  
  
2.  새 열의 제목을 클릭하고 **Gender**를 입력합니다.  
  
#### <a name="to-add-a-rectangle"></a>사각형을 추가하려면  
  
-   리본의 **삽입** 탭에서 **사각형**을 클릭한 다음 **Gender** 열의 데이터 셀을 클릭합니다.  
  
     셀에 사각형이 추가됩니다.  
  
#### <a name="to-add-an-image-to-the-rectangle"></a>사각형에 이미지를 추가하려면  
  
1.  사각형을 마우스 오른쪽 단추로 클릭하고 **삽입**을 가리킨 다음 **이미지**를 클릭합니다.  
  
2.  **이미지 속성** 대화 상자에서 **이 이미지 사용** 옆의 아래쪽 화살표를 클릭하고 추가한 이미지 중 하나(예: Penguins.JPG)를 선택합니다.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-use-images-to-show-gender"></a>이미지를 사용하여 성별을 표시하려면  
  
1.  **Gender** 열에서 데이터 셀의 이미지를 마우스 오른쪽 단추로 클릭하고 **이미지 속성**을 클릭합니다.  
  
2.  **이미지 속성** 대화 상자에서 **이 이미지 사용** 입력란 옆에 있는 식 단추(**fx**)를 클릭합니다.  
  
3.  **식** 대화 상자에서 **일반 함수** 를 확장하고 **프로그램 흐름**을 클릭합니다.  
  
4.  **항목** 목록에서 **Switch**를 두 번 클릭합니다.  
  
5.  **범주** 목록에서 **필드(식)** 를 클릭합니다.  
  
6.  **값** 목록에서 **Gender**를 두 번 클릭합니다.  
  
7.  **="Male", "Koala",** 를 입력합니다.  
  
8.  **값** 목록에서 **Gender**를 두 번 클릭합니다.  
  
9. **="Female", "Penguins",** 를 입력합니다.  
  
10. **값** 목록에서 **Gender**를 두 번 클릭합니다.  
  
11. **="Unknown", "Tulips")** 를 입력합니다.  
  
     완성된 식은 다음과 같습니다. `=Switch(Fields!Gender.Value ="Male", "Koala",Fields!Gender.Value ="Female","Penguins",Fields!Gender.Value ="Unknown","Tulips")`  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. **확인**을 다시 클릭하여 **이미지 속성** 대화 상자를 닫습니다.  
  
14. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
##  <a name="5-look-up-countryregion-name"></a><a name="Lookup"></a>5. CountryRegion 이름 조회  
 CountryRegion 데이터 세트를 만들고 **Lookup** 함수를 사용하여 국가/지역의 식별자 대신 국가/지역의 이름을 표시합니다.  
  
#### <a name="to-create-the-countryregion-dataset"></a>CountryRegion 데이터 세트를 만들려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  보고서 데이터 창에서 **새로 만들기**를 클릭한 다음, **데이터 세트**를 클릭합니다.  
  
3.  **내 보고서에 포함된 데이터 집합 사용**을 클릭합니다.  
  
4.  **데이터 원본** 목록에서 ExpressionsDataSource를 선택합니다.  
  
5.  **이름** 상자에 **CountryRegion**을 입력합니다.  
  
6.  **텍스트** 쿼리 유형이 선택되어 있는지 확인한 다음 **쿼리 디자이너**를 클릭합니다.  
  
7.  **텍스트로 편집**을 클릭합니다.  
  
8.  쿼리 창에 다음 쿼리를 복사하여 붙여 넣습니다.  
  
    ```  
    SELECT 1 AS ID, 'American Samoa' AS CountryRegion  
    UNION SELECT 2 AS CountryRegionID, 'Australia' AS CountryRegion  
    UNION SELECT 3 AS ID, 'Canada' AS CountryRegion  
    UNION SELECT 4 AS ID, 'Germany' AS CountryRegion  
    UNION SELECT 5 AS ID, 'Micronesia' AS CountryRegion  
    UNION SELECT 6 AS ID, 'France' AS CountryRegion  
    UNION SELECT 7 AS ID, 'United States' AS CountryRegion  
    UNION SELECT 8 AS ID, 'Brazil' AS CountryRegion  
    UNION SELECT 9 AS ID, 'Mexico' AS CountryRegion  
    UNION SELECT 10 AS ID, 'Japan' AS CountryRegion  
    UNION SELECT 10 AS ID, 'Australia' AS CountryRegion  
    UNION SELECT 12 AS ID, 'United Kingdom' AS CountryRegion  
    ```  
  
9. **실행** (**!**)을 클릭 하 여 쿼리를 실행 합니다.  
  
     쿼리 결과는 국가/지역 식별자와 이름입니다.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. **확인**을 다시 클릭하여 **데이터 세트 속성** 대화 상자를 닫습니다.  
  
#### <a name="to-look-up-values-in-the-countryregion-dataset"></a>CountryRegion 데이터 세트에서 값을 조회하려면  
  
1.  **Country Region ID** 열 제목을 클릭하고 텍스트 ID를 삭제합니다.  
  
2.  **Country Region** 열의 데이터 셀을 마우스 오른쪽 단추로 클릭하고 **식**을 클릭합니다.  
  
3.  처음 등호(=)를 제외하고 식을 삭제합니다.  
  
     나머지 식은 다음과 같습니다. `=`  
  
4.  **식** 대화 상자에서 **일반 함수**를 확장하고 **기타**를 클릭합니다.  
  
5.  **항목** 목록에서 **Lookup**을 두 번 클릭합니다.  
  
6.  **범주** 목록에서 **필드(식)** 를 클릭합니다.  
  
7.  **값** 목록에서를 두 번 클릭 `CountryRegionID`합니다.  
  
8.  `CountryRegionID.Value` 바로 뒤에 커서가 없으면 커서를 그곳에 둡니다.  
  
9. 오른쪽 괄호를 삭제한 다음 **,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")** 을 입력합니다.  
  
     완성된 식은 다음과 같습니다. `=Lookup(Fields!CountryRegionID.Value,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")`  
  
     **Lookup** 함수의 구문에서는 CountryRegion 데이터 세트에서 CountryRegionID 및 ID 간의 조회를 지정합니다. 여기에서는 CountryRegion 값을 반환하며 이 값은 CountryRegion 데이터 세트에도 있습니다.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
##  <a name="6-count-days-since-last-purchase"></a><a name="Count"></a>6. 마지막 구매 이후 일 수 계산  
 열을 추가한 다음 **Now** 함수 또는 `ExecutionTime` 기본 제공 전역 변수를 사용 하 여 사용자의 마지막 구매 이후 오늘 까지의 일 수를 계산 합니다.  
  
#### <a name="to-add-the-days-ago-column"></a>Days Ago 열을 추가하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  **Last Purchase** 열을 마우스 오른쪽 단추로 클릭하고 **열 삽입**을 가리킨 다음 **오른쪽**을 클릭합니다.  
  
     새 열이 **Last Purchase** 열의 오른쪽에 추가됩니다.  
  
3.  열 머리글에서 **Days Ago**를 입력합니다.  
  
4.  **Days Ago** 열의 데이터 셀을 마우스 오른쪽 단추로 클릭하고 **식**을 클릭합니다.  
  
5.  **식** 대화 상자에서 **일반 함수**를 확장하고 **날짜 및 시간**을 클릭합니다.  
  
6.  **항목** 목록에서 **DateDiff**를 두 번 클릭합니다.  
  
7.  `DateDiff(` 바로 뒤에 커서가 없으면 커서를 그곳에 둡니다.  
  
8.  **"d",** 를 입력합니다.  
  
9. **범주** 목록에서 **필드(식)** 를 클릭합니다.  
  
10. **값** 목록에서 **LastPurchase**를 두 번 클릭합니다.  
  
11. `Fields!LastPurchase.Value` 바로 뒤에 커서가 없으면 커서를 그곳에 둡니다.  
  
12. 유형 **,**  
  
13. **범주** 목록에서 **날짜 및 시간**을 다시 클릭합니다.  
  
14. **항목** 목록에서 **Now**를 두 번 클릭합니다.  
  
    > [!WARNING]  
    >  프로덕션 보고서의 경우, 보고서의 정보 행에서와 같이 보고서가 렌더링되면서 여러 번 계산되는 식에서 **Now** 함수를 사용하면 안 됩니다. **Now** 의 값은 행마다 변경되고 서로 다른 값이 식의 계산 결과에 영향을 미치므로 조금씩 일치하지 않는 결과가 발생합니다. 대신 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 제공하는 `ExecutionTime` 전역 변수를 사용해야 합니다.  
  
15. `Now(` 바로 뒤에 커서가 없으면 커서를 그곳에 둡니다.  
  
16. 왼쪽 괄호를 삭제한 다음 **)** 를 입력합니다.  
  
     완성된 식은 다음과 같습니다. `=DateDiff("d", Fields!LastPurchase.Value, Now)`  
  
17. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="7-use-an-indicator-to-show-sales-comparison"></a><a name="Indicator"></a>7. 표시기를 사용 하 여 판매 비교 표시  
 새 열을 추가 하 고 표시기를 사용 하 여 연간 연간 누계 (YTD) 구매가 평균 YTD 구매를 초과 하는지 여부를 표시 합니다. **Round** 함수는 값에서 소수를 제거합니다.  
  
 표시기와 그 상태의 구성에는 많은 단계가 필요합니다. 원하는 경우 "표시기를 구성 하려면" 절차에서 앞으로 건너뛰고이 자습서의 완성 된 식을 복사 하 여 **식** 대화 상자에 붙여 넣을 수 있습니다.  
  
#### <a name="to-add-the--or---avg-sales-column"></a>+ or - AVG Sales 열을 추가하려면  
  
1.  **YTD Purchase** 열을 마우스 오른쪽 단추로 클릭하고 **열 삽입**을 가리킨 다음 **오른쪽**을 클릭합니다.  
  
     새 열이 **YTD Purchase** 열의 오른쪽에 추가됩니다.  
  
2.  열의 제목을 클릭하고 **+ or - AVG Sales**를 입력합니다.  
  
#### <a name="to-add-an-indicator"></a>표시기를 추가하려면  
  
1.  리본의 **삽입** 탭에서 **표시기**를 클릭한 다음 **+ or - AVG Sales** 열의 데이터 셀을 클릭합니다.  
  
     **표시기 유형 선택** 대화 상자가 열립니다.  
  
2.  아이콘 집합의 **방향** 그룹에서 회색 화살표 3개로 구성된 집합을 클릭합니다.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-configure-the-indicator"></a>표시기를 구성하려면  
  
1.  표시기를 마우스 오른쪽 단추로 클릭하고 **표시기 속성**을 클릭한 다음 **값 및 상태**를 클릭합니다.  
  
2.  **값** 입력란 옆의 식 단추( **fx** )를 클릭합니다.  
  
3.  **식** 대화 상자에서 **일반 함수**를 확장하고 **수치 연산**을 클릭합니다.  
  
4.  **항목** 목록에서 **Round**를 두 번 클릭합니다.  
  
5.  **범주** 목록에서 **필드(식)** 를 클릭합니다.  
  
6.  **값** 목록에서 **YTDPurchase**를 두 번 클릭합니다.  
  
7.  `Fields!YTDPurchase.Value` 바로 뒤에 커서가 없으면 커서를 그곳에 둡니다.  
  
8.  입력할**-**  
  
9. **일반 함수**를 다시 확장하고 **집계**를 클릭합니다.  
  
10. **항목** 목록에서 **Avg**를 두 번 클릭합니다.  
  
11. **범주** 목록에서 **필드(식)** 를 클릭합니다.  
  
12. **값** 목록에서 **YTDPurchase**를 두 번 클릭합니다.  
  
13. `Fields!YTDPurchase.Value` 바로 뒤에 커서가 없으면 커서를 그곳에 둡니다.  
  
14. **, "Expressions"))** 를 입력합니다.  
  
     완성된 식은 다음과 같습니다. `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions"))`  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. **상태 단위** 상자에서 **숫자**를 선택합니다.  
  
17. 아래쪽 화살표가 있는 행에서 **시작** 값의 입력란 오른쪽에 있는 **fx** 단추를 클릭합니다.  
  
18. **식** 대화 상자에서 **일반 함수**를 확장하고 **수치 연산**을 클릭합니다.  
  
19. **항목** 목록에서 **Round**를 두 번 클릭합니다.  
  
20. **범주** 목록에서 **필드(식)** 를 클릭합니다.  
  
21. **값** 목록에서 **YTDPurchase**를 두 번 클릭합니다.  
  
22. `Fields!YTDPurchase.Value` 바로 뒤에 커서가 없으면 커서를 그곳에 둡니다.  
  
23. 입력할**-**  
  
24. **일반 함수**를 다시 확장하고 **집계**를 클릭합니다.  
  
25. **항목** 목록에서 **Avg**를 두 번 클릭합니다.  
  
26. **범주** 목록에서 **필드(식)** 를 클릭합니다.  
  
27. **값** 목록에서 **YTDPurchase**를 두 번 클릭합니다.  
  
28. `Fields!YTDPurchase.Value` 바로 뒤에 커서가 없으면 커서를 그곳에 둡니다.  
  
29. **, "Expressions")) < 0**을 입력합니다.  
  
     완성된 식은 다음과 같습니다. `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) < 0`  
  
30. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
31. **끝** 값의 입력란에 **0**을 입력합니다.  
  
32. 옆쪽 화살표가 있는 행을 클릭하고 **삭제**를 클릭합니다.  
  
33. 위쪽 화살표가 있는 행에서 **시작** 상자에 **0**을 입력합니다.  
  
34. **끝** 값의 입력란 오른쪽에 있는 **fx** 단추를 클릭합니다.  
  
35. **식** 대화 상자에서 식을 만듭니다.`=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) >0`  
  
36. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
37. **확인** 을 다시 클릭하여 **표시기 속성** 대화 상자를 닫습니다.  
  
38. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
##  <a name="8-make-the-report-a-green-bar-report"></a><a name="GreenBar"></a>8. 보고서를 "녹색 막대" 보고서로 만들기  
 가로줄무늬가 있는 보고서로 만들기 위해 매개 변수를 사용하여 보고서의 행에 번갈아 적용할 색을 지정합니다.  
  
#### <a name="to-add-a-parameter"></a>매개 변수를 추가하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  **보고서 데이터** 창에서 **매개 변수** 를 마우스 오른쪽 단추로 클릭하고 **매개 변수 추가**를 클릭합니다.  
  
     **보고서 매개 변수 속성** 대화 상자가 열립니다.  
  
3.  **프롬프트**에 **Choose color**를 입력합니다.  
  
4.  **이름**에 **RowColor**를 입력합니다.  
  
5.  왼쪽 창에서 **사용 가능한 값**을 클릭합니다.  
  
6.  **값 지정**을 클릭합니다.  
  
7.  **추가**를 클릭합니다.  
  
8.  **레이블** 상자에 **Yellow**를 입력합니다.  
  
9. **값** 상자에 **Yellow**를 입력합니다.  
  
10. **추가**를 클릭합니다.  
  
11. **레이블** 상자에 **Green**을 입력합니다.  
  
12. **값** 상자에 **PaleGreen**을 입력합니다.  
  
13. **추가**를 클릭합니다.  
  
14. **레이블** 상자에 **Blue**를 입력합니다.  
  
15. **값** 상자에 **LightBlue**를 입력합니다.  
  
16. **추가**를 클릭합니다.  
  
17. **레이블** 상자에 **Pink**를 입력합니다.  
  
18. **값** 상자에 **Pink**를 입력합니다.  
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-apply-alternating-colors-to-detail-rows"></a>정보 행에 색을 번갈아 적용하려면  
  
1.  리본의 **보기** 탭을 클릭하고 **속성**이 선택되어 있는지 확인합니다.  
  
2.  **Name** 열의 데이터 셀을 클릭하고 Shift 키를 누릅니다.  
  
3.  행의 다른 셀을 차례로 클릭합니다.  
  
4.  속성 창에서 **BackgroundColor**를 클릭합니다.  
  
     속성 창에 속성이 범주별로 표시되어 있으면 **Fill** 범주에서 **BackgroundColor**를 찾을 수 있습니다.  
  
5.  아래쪽 화살표를 클릭한 다음 **식**을 클릭합니다.  
  
6.  **식** 대화 상자에서 **일반 함수**를 확장하고 **프로그램 흐름**을 클릭합니다.  
  
7.  **항목** 목록에서 **IIf**를 두 번 클릭합니다.  
  
8.  **일반 함수**를 확장하고 **집계**를 클릭합니다.  
  
9. **항목** 목록에서 **RunningValue**를 두 번 클릭합니다.  
  
10. **범주** 목록에서 **필드(식)** 를 클릭합니다.  
  
11. **값** 목록에서 **FirstName**을 두 번 클릭합니다.  
  
12. `Fields!FirstName.Value` 바로 뒤에 커서가 없으면 커서를 그곳에 두고 **,** 를 입력합니다.  
  
13. **일반 함수**를 확장하고 **집계**를 클릭합니다.  
  
14. **항목** 목록에서 **Count**를 두 번 클릭합니다.  
  
15. `Count(` 바로 뒤에 커서가 없으면 커서를 그곳에 둡니다.  
  
16. 왼쪽 괄호를 삭제 한 다음 **, "Expressions")를** 입력 합니다.  
  
    > [!NOTE]  
    >  식은 데이터 행 수를 셀 데이터 세트의 이름입니다.  
  
17. **연산자**를 확장하고 **산술**을 클릭합니다.  
  
18. **항목** 목록에서 **Mod**를 두 번 클릭합니다.  
  
19. `Mod` 바로 뒤에 커서가 없으면 커서를 그곳에 둡니다.  
  
20. **2 =0,** 를 입력합니다.  
  
    > [!IMPORTANT]  
    >  숫자 2를 입력하기 전에 공백을 포함해야 합니다.  
  
21. **매개 변수** 를 클릭하고 **값** 목록에서 **RowColor**를 두 번 클릭합니다.  
  
22. `Parameters!RowColor.Value` 바로 뒤에 커서가 없으면 커서를 그곳에 둡니다.  
  
23. **, "White")를 입력 합니다** .  
  
     완성된 식은 다음과 같습니다. `=IIf(RunningValue(Fields!FirstName.Value,Count, "Expressions") Mod 2 =0, Parameters!RowColor.Value, "White")`  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="run-the-report"></a>보고서 실행  
  
1.  **홈** 탭에 없으면 **홈**을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  **실행**을 클릭합니다.  
  
3.  **색 선택** 드롭다운 목록에서 보고서에 표시될 흰색이 아닌 막대의 색을 선택합니다.  
  
4.  **보고서 보기**를 클릭합니다.  
  
     보고서가 렌더링되고 선택한 배경이 행에 번갈아 표시됩니다.  
  
##  <a name="optional-format-date-column"></a><a name="DateFormat"></a>필드 날짜 열 서식 지정  
 날짜가 포함된 **Last Purchase** 열의 서식을 지정합니다.  
  
#### <a name="to-format-date-column"></a>날짜 열의 서식을 지정하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  **Last Purchase** 열의 데이터 셀을 마우스 오른쪽 단추로 클릭하고 **입력란 속성**을 클릭합니다.  
  
3.  **입력란 속성** 대화 상자에서 **숫자**, **날짜**, **\*1/31/2000** 형식을 차례로 클릭합니다.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="optional-add-a-report-title"></a><a name="Title"></a>필드 보고서 제목 추가  
 보고서에 제목을 추가합니다.  
  
#### <a name="to-add-a-report-title"></a>보고서 제목을 추가하려면  
  
1.  디자인 화면에서 **제목을 추가하려면 클릭하십시오.** 를 클릭합니다.  
  
2.  **Sales Comparison Summary**를 입력한 다음 입력란 바깥쪽을 클릭합니다.  
  
3.  **Sales Comparison Summary**가 들어 있는 입력란을 마우스 오른쪽 단추로 클릭하고 **입력란 속성**을 클릭합니다.  
  
4.  **입력란 속성** 대화 상자에서 **글꼴**을 클릭합니다.  
  
5.  **크기** 목록에서 **18pt**를 선택합니다.  
  
6.  **색** 목록에서 **회색**을 선택합니다.  
  
7.  **굵게** 및 **기울임꼴**을 선택합니다.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="optional-save-the-report"></a><a name="Save"></a>필드 보고서 저장  
 보고서를 보고서 서버, SharePoint 라이브러리 또는 컴퓨터에 저장할 수 있습니다. 자세한 내용은 [보고서 저장&#40;보고서 작성기&#41;](report-builder/saving-reports-report-builder.md)을 참조하세요.  
  
 이 자습서에서는 보고서를 보고서 서버에 저장합니다. 보고서 서버에 액세스할 수 없는 경우에는 보고서를 컴퓨터에 저장하십시오.  
  
#### <a name="to-save-the-report-to-a-report-server"></a>보고서를 보고서 서버에 저장하려면  
  
1.  **보고서 작성기** 단추에서 다른 **이름으로 저장**을 클릭 합니다.  
  
2.  **최근에 사용한 사이트 및 서버**를 클릭합니다.  
  
3.  보고서를 저장할 수 있는 권한을 가진 보고서 서버의 이름을 선택하거나 입력합니다.  
  
     "보고서 서버에 연결하는 중"이라는 메시지가 나타납니다. 연결되면 보고서 서버 관리자가 기본 보고서 위치로 지정한 보고서 폴더의 내용이 표시됩니다.  
  
4.  **이름**에서 기본 이름을 **Sales Comparison Summary**로 바꿉니다.  
  
5.  **저장**을 클릭합니다.  
  
 보고서가 보고서 서버에 저장됩니다. 연결된 보고서 서버의 이름이 창 아래쪽에 있는 상태 표시줄에 나타납니다.  
  
#### <a name="to-save-the-report-to-your-computer"></a>컴퓨터에 보고서를 저장하려면  
  
1.  **보고서 작성기** 단추에서 다른 **이름으로 저장**을 클릭 합니다.  
  
2.  **바탕 화면**, **내 문서**또는 **내 컴퓨터**를 클릭한 다음 보고서를 저장할 폴더를 찾습니다.  
  
3.  **이름**에서 기본 이름을 **Sales Comparison Summary**로 바꿉니다.  
  
4.  **저장**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [식&#40;보고서 작성기 및 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [보고서 작성기 및 SSRS &#40;표시기&#41;](report-design/indicators-report-builder-and-ssrs.md)   
 [이미지, 텍스트 상자, 사각형 및 선 &#40;보고서 작성기 및 SSRS&#41;](report-design/rectangles-and-lines-report-builder-and-ssrs.md)   
 [테이블 &#40;보고서 작성기 및 SSRS&#41;](report-design/tables-report-builder-and-ssrs.md)   
 [보고서 &#40;보고서 작성기 및 SSRS&#41;에 데이터를 추가 합니다.](report-data/report-datasets-ssrs.md)  
  
  
