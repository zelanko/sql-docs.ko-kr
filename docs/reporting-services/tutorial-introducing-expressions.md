---
title: "자습서: 식 소개 | Microsoft Docs"
ms.custom: ""
ms.date: "09/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 2d05ef4c-5f91-48b2-8795-f0a201a0b3cc
caps.latest.revision: 14
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 14
---
# 자습서: 식 소개
이 [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)] 자습서에서는 일반적인 함수 및 연산자와 함께 식을 사용하여 강력하고 유연한 페이지가 매겨진 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 보고서를 만듭니다. 

이름 값을 연결하고, 별도의 데이터 집합에서 값을 조회하고, 필드 값에 따라 서로 다른 색을 표시하는 등의 작업을 수행하는 식을 작성합니다.  
  
보고서에는 줄무늬가 있으며 흰색 행과 컬러 행이 번갈아 표시됩니다. 보고서에는 흰색이 아닌 행의 색을 선택하기 위한 매개 변수가 포함됩니다.  
  
다음 그림은 만들려는 보고서와 비슷한 보고서를 보여 줍니다.  
  
![보고서-작성기-식-자습서-브라우저 내](../reporting-services/media/report-builder-expression-tutorial-in-browser.png) 
  
이 자습서에 소요되는 예상 시간: 30분  
  
## 요구 사항  
요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md)을 참조하세요.  
  
## <a name="Setup"></a>1. 테이블 또는 행렬 마법사에서 테이블 보고서 및 데이터 집합 만들기  
이 섹션에서는 테이블 보고서, 데이터 원본 및 데이터 집합을 만듭니다. 테이블의 레이아웃을 지정할 때는 몇몇 필드만 포함하고, 마법사를 완료한 후 열을 수동으로 추가합니다. 마법사를 사용하면 손쉽게 테이블의 레이아웃을 지정할 수 있습니다.  
  
> [!NOTE]  
> 이 자습서의 쿼리에는 데이터 값이 포함되어 있으므로 외부 데이터 원본이 필요하지 않습니다. 따라서 쿼리가 상당히 길어집니다. 비즈니스 환경에서는 쿼리에 데이터가 포함되지 않을 것입니다. 이 자습서의 쿼리는 학습용으로만 제공됩니다.  
  
### 테이블 보고서를 만들려면  
  
1.  컴퓨터, [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 웹 포털 또는 SharePoint 통합 모드에서 [보고서 작성기를 시작](../reporting-services/report-builder/start-report-builder.md)합니다.  
  
    **새 보고서 또는 데이터 집합** 대화 상자가 열립니다.  
  
    **새 보고서 또는 데이터 집합** 대화 상자가 표시되지 않는 경우 **파일** 메뉴 > **새로 만들기**를 클릭합니다.  
  
2.  왼쪽 창에 **새 보고서** 가 선택되어 있는지 확인합니다.  
  
3.  오른쪽 창에서 **테이블 또는 행렬 마법사**를 클릭합니다.  
  
4.  **데이터 집합 선택** 페이지에서 **데이터 집합 만들기** > **다음**을 클릭합니다.  
  
6.  **데이터 원본에 대한 연결 선택** 페이지에서 **SQL Server** 형식의 데이터 원본을 선택합니다. 목록에서 데이터 원본을 선택하거나 보고서 서버를 찾아 선택합니다.  

    > [!NOTE]  
    > 적절한 권한만 있으면 선택하는 데이터 원본은 중요하지 않습니다. 데이터를 데이터 원본에서 가져오는 것은 아니기 때문입니다. 자세한 내용은 [데이터에 연결하는 다른 방법&#40;보고서 작성기&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)을 참조하세요.  
  
7.  **다음**을 클릭합니다.  
  
8.  **쿼리 디자인** 페이지에서 **텍스트로 편집**을 클릭합니다.  
  
9. 쿼리 창에 다음 쿼리를 붙여 넣습니다.  
  
    ```  
    SELECT 'Lauren' AS FirstName,'Johnson' AS LastName, 'American Samoa' AS StateProvince, 1 AS CountryRegionID,'Female' AS Gender, CAST(9996.60 AS money) AS YTDPurchase, CAST('2015-6-10' AS date) AS LastPurchase  
    UNION SELECT'Warren' AS FirstName, 'Pal' AS LastName, 'New South Wales' AS StateProvince, 2 AS CountryRegionID, 'Male' AS Gender, CAST(5747.25 AS money) AS YTDPurchase, CAST('2015-7-3' AS date) AS LastPurchase  
    UNION SELECT 'Fernando' AS FirstName, 'Ross' AS LastName, 'Alberta' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(9248.15 AS money) AS YTDPurchase, CAST('2015-10-17' AS date) AS LastPurchase  
    UNION SELECT 'Rob' AS FirstName, 'Caron' AS LastName, 'Northwest Territories' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(742.50 AS money) AS YTDPurchase, CAST('2015-4-29' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Bailey' AS LastName, 'British Columbia' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(1147.50 AS money) AS YTDPurchase, CAST('2015-6-15' AS date) AS LastPurchase  
    UNION SELECT  'Bridget' AS FirstName, 'She' AS LastName, 'Hamburg' AS StateProvince, 4 AS CountryRegionID, 'Female' AS Gender, CAST(7497.30 AS money) AS YTDPurchase, CAST('2015-5-10' AS date) AS LastPurchase  
    UNION SELECT 'Alexander' AS FirstName, 'Martin' AS LastName, 'Saxony' AS StateProvince, 4 AS CountryRegionID, 'Male' AS Gender, CAST(2997.60 AS money) AS YTDPurchase, CAST('2015-11-19' AS date) AS LastPurchase  
    UNION SELECT 'Yolanda' AS FirstName, 'Sharma' AS LastName ,'Micronesia' AS StateProvince, 5 AS CountryRegionID, 'Female' AS Gender, CAST(3247.95 AS money) AS YTDPurchase, CAST('2015-8-23' AS date) AS LastPurchase  
    UNION SELECT 'Marc' AS FirstName, 'Zimmerman' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1200.00 AS money) AS YTDPurchase, CAST('2015-11-16' AS date) AS LastPurchase  
    UNION SELECT 'Katherine' AS FirstName, 'Abel' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Female' AS Gender, CAST(2025.00 AS money) AS YTDPurchase, CAST('2015-12-1' AS date) AS LastPurchase  
    UNION SELECT 'Nicolas' as FirstName, 'Anand' AS LastName, 'Seine (Paris)' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1425.00 AS money) AS YTDPurchase, CAST('2015-12-11' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Peters' AS LastName, 'England' AS StateProvince, 12 AS CountryRegionID, 'Male' AS Gender, CAST(887.50 AS money) AS YTDPurchase, CAST('2015-8-15' AS date) AS LastPurchase  
    UNION SELECT 'Alison' AS FirstName, 'Nath' AS LastName, 'Alaska' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(607.50 AS money) AS YTDPurchase, CAST('2015-10-13' AS date) AS LastPurchase  
    UNION SELECT 'Grace' AS FirstName, 'Patterson' AS LastName, 'Kansas' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(1215.00 AS money) AS YTDPurchase, CAST('2015-10-18' AS date) AS LastPurchase  
    UNION SELECT 'Bobby' AS FirstName, 'Sanchez' AS LastName, 'North Dakota' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(6191.00 AS money) AS YTDPurchase, CAST('2015-9-17' AS date) AS LastPurchase  
    UNION SELECT 'Charles' AS FirstName, 'Reed' AS LastName, 'Nebraska' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8772.00 AS money) AS YTDPurchase, CAST('2015-8-27' AS date) AS LastPurchase  
    UNION SELECT 'Orlando' AS FirstName, 'Romeo' AS LastName, 'Texas' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8578.00 AS money) AS YTDPurchase, CAST('2015-7-29' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2015-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2015-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2015-11-30' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2015-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2015-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2015-11-30' AS date) AS LastPurchase  
    ```  

  
10. 쿼리 디자이너 도구 모음에서 **실행**(**!**)을 클릭합니다. 결과 집합에는 FirstName, LastName, StateProvince, CountryRegionID, Gender, YTDPurchase 및 LastPurchase 열에 23행의 데이터가 표시됩니다.  

    ![보고서-작성기-식-자습서-쿼리를-텍스트로](../reporting-services/media/report-builder-expression-tutorial-query-as-text.png)
  
11. **다음**을 클릭합니다.  
  
12. **필드 정렬** 페이지에서 다음 필드를 지정된 순서에 따라 **사용 가능한 필드** 목록에서 **값** 목록으로 끌어옵니다.  
  
    -   StateProvince   
    -   CountryRegionID  
    -   LastPurchase  
    -   YTDPurchase  
  
    CountryRegionID 및 YTDPurchase는 숫자 데이터를 포함하므로 SUM 집계가 기본적으로 적용되지만 이러한 합계를 구하지 않으려고 합니다.  
   
13. **값** 목록에서 **CountryRegionID**를 마우스 오른쪽 단추로 클릭하고 **Sum** 확인란을 선택 취소합니다.  
  
    Sum은 더 이상 CountryRegionID에 적용되지 않습니다.  
  
14. **값** 목록에서 **YTDPurchase**를 마우스 오른쪽 단추로 클릭하고 **Sum** 옵션을 클릭합니다.  
  
    Sum은 더 이상 YTDPurchase에 적용되지 않습니다.  
    
    ![보고서-작성기-식-합계를 구하지 않음](../reporting-services/media/report-builder-expression-not-sum.png)
  
15. **다음**을 클릭합니다.  
  
16. **레이아웃 선택** 페이지의 모든 기본 설정을 유지하고 **다음**을 클릭합니다.  

    ![보고서-작성기-식-자습서-레이아웃-선택](../reporting-services/media/report-builder-expression-tutorial-choose-layout.png)
  
17. **마침**을 클릭합니다.  
  
## <a name="UpdateNames"></a>2. 데이터 원본 및 데이터 집합의 기본 이름 업데이트  
  
### 데이터 원본의 기본 이름을 업데이트하려면  
  
1.  보고서 데이터 창에서 **데이터 원본** 폴더를 확장합니다.  
  
2.  **DataSource1**을 마우스 오른쪽 단추로 클릭하고 **데이터 원본 속성**을 클릭합니다.  
  
3.  **이름** 상자에 **ExpressionsDataSource**를 입력합니다.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### 데이터 집합의 기본 이름을 업데이트하려면  
  
1.  보고서 데이터 창에서 **데이터 집합** 폴더를 확장합니다.  
  
2.  **DataSet1**을 마우스 오른쪽 단추로 클릭하고 **데이터 집합 속성**을 클릭합니다.  

    ![보고서-작성기-식-자습서-데이터 집합-이름 바꾸기](../reporting-services/media/report-builder-expression-tutorial-rename-dataset.png)
  
3.  **이름** 상자에 **Expressions**를 입력합니다.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Concatenate"></a>3. 이름 및 성 표시  
이 섹션에서는 이름과 성을 포함하는 이름으로 계산되는 식에서 **Left** 함수와 **Concatenate**(**&**) 연산자를 사용합니다. 단계별로 식을 작성하거나 절차에서 단계를 건너뛰고 자습서의 식을 복사하여 **식** 대화 상자에 붙여넣을 수 있습니다.   
  
1.  **StateProvince** 열을 마우스 오른쪽 단추로 클릭하고 **열 삽입**을 가리킨 다음 **왼쪽**을 클릭합니다.  
  
    새 열이 **StateProvince** 열의 왼쪽에 추가됩니다. 
    
    ![보고서-작성기-식-자습서-열-삽입](../reporting-services/media/report-builder-expression-tutorial-insert-column.png) 
  
2.  새 열의 제목을 클릭하고 **Name**을 입력합니다.  
  
3.  **Name** 열의 데이터 셀을 마우스 오른쪽 단추로 클릭하고 **식**을 클릭합니다.  

    ![보고서-작성기-식-자습서-식-삽입](../reporting-services/media/report-builder-expression-tutorial-insert-expression.png)
  
4.  **식** 대화 상자에서 **일반 함수**를 확장하고 **텍스트**를 클릭합니다.  
  
5.  **항목** 목록에서 **Left**를 두 번 클릭합니다.  
  
    **Left** 함수가 식에 추가됩니다.  
    
    ![보고서-작성기-식-자습서-left-함수](../reporting-services/media/report-builder-expression-tutorial-left-function.png)
  
6.  **범주** 목록에서 **필드(식)**를 클릭합니다.  
  
7.  **값** 목록에서 **FirstName**을 두 번 클릭합니다.  
  
8.  **, 1)**을 입력합니다.  
  
    이 식은 **FirstName** 값에서 가장 왼쪽의 한 자를 추출합니다.  
  
9. **&". "&**를 입력합니다.  

    그러면 식 뒤에 마침표와 공백이 하나씩 추가됩니다.
  
10. **값** 목록에서 **LastName**을 두 번 클릭합니다.  
  
    완성된 식은 다음과 같습니다. `=Left(Fields!FirstName.Value, 1) &". "& Fields!LastName.Value`  
    
    ![보고서-작성기-식-자습서-이름-식-완성](../reporting-services/media/report-builder-expression-tutorial-complete-name-expression.png)
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. **실행** 을 클릭하여 보고서를 미리 봅니다.  

## <a name="DateFormat"></a>(선택 사항) 날짜 및 통화 열과 머리글 행 서식 지정  
이 섹션에서는 날짜가 포함된 **Last Purchase** 열과 통화가 포함된 YTDPurchase 열의 서식을 지정합니다. 머리글 행의 서식도 지정합니다.  
  
### 날짜 열의 서식을 지정하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  **Last Purchase** 열에서 데이터 셀을 선택하고 **홈** 탭 > **숫자** 섹션에서 **날짜**를 선택합니다.  

    ![보고서-작성기-식-자습서-날짜-서식](../reporting-services/media/report-builder-expression-tutorial-date-format.png)
  
3.  또한 **숫자** 섹션에서 **자리 표시자 스타일** 옆에 있는 화살표를 클릭하고 **보기 값**을 선택합니다. 

    ![보고서-작성기-식-자습서-보기-값](../reporting-services/media/report-builder-expression-tutorial-sample-values.png)

    이제 선택한 서식의 예를 확인할 수 있습니다. 
  
### 통화 열의 서식을 지정하려면

- **YTDPurchase** 열에서 데이터 셀을 선택하고 **숫자** 섹션에서 **통화 기호**를 선택합니다.
 
### 열 머리글의 서식을 지정하려면

1. 열 머리글의 행을 선택합니다.

2. **홈** 탭 > **단락** 섹션에서 **왼쪽**을 선택합니다. 

    ![보고서-작성기-식-자습서-머리글-서식 지정](../reporting-services/media/report-builder-expression-tutorial-format-headings.png)

3. **실행** 을 클릭하여 보고서를 미리 봅니다. 

다음은 지금까지 서식을 지정한 날짜, 통화 및 열 머리글이 적용된 보고서입니다.

![보고서-작성기-식-자습서-서식 지정-미리 보기](../reporting-services/media/report-builder-expression-tutorial-preview-formatted.png)

  
## <a name="Gender"></a>4. 색을 사용하여 성별 표시  
이 섹션에서는 색을 추가하여 사람의 성별을 표시합니다. 새 열을 추가하여 색을 표시한 다음 Gender 필드의 값에 따라 열에 나타나는 색을 결정합니다.  
  
보고서를 줄무늬 보고서로 만들 때 해당 테이블 셀에 적용한 색을 유지하려면 사각형을 추가한 다음 사각형에 배경색을 추가합니다.  
    
 
### M/F 열을 추가하려면  
  
1.  **Name** 열을 마우스 오른쪽 단추로 클릭하고 **열 삽입**을 가리킨 다음 **왼쪽**을 클릭합니다.  
  
    새 열이 **Name** 열의 왼쪽에 추가됩니다.  
  
2.  새 열의 머리글을 클릭하고 **M/F**를 입력합니다.  
  
### 사각형을 추가하려면  
  
1.   **삽입** 탭에서 **사각형**을 클릭한 다음 **M/F** 열의 데이터 셀을 클릭합니다.  
  
     셀에 사각형이 추가됩니다.  
     
     ![보고서-작성기-식-자습서-사각형-삽입](../reporting-services/media/report-builder-expression-tutorial-insert-rectangle.png)
  
2. **M/F**와 **Name** 사이의 열 구분선을 끌어 **M/F** 열을 더 좁게 만듭니다.

    ![보고서-작성기-식-자습서-열-좁히기](../reporting-services/media/report-builder-expression-tutorial-narrow-column.png)
  
### 색을 사용하여 성별을 표시하려면  
  
1.  **M/F** 열에서 데이터 셀의 사각형을 마우스 오른쪽 단추로 클릭하고 **사각형 속성**을 클릭합니다.  
  
2.  **사각형 속성** 대화 상자 > **채우기** 탭에서 **채우기 색** 옆에 있는 식 **fx** 단추를 클릭합니다.  
  
3.  **식** 대화 상자에서 **일반 함수**를 확장하고 **프로그램 흐름**을 클릭합니다.  
  
4.  **항목** 목록에서 **Switch**를 두 번 클릭합니다.  
  
5.  **범주** 목록에서 **필드(식)**를 클릭합니다.  
  
6.  **값** 목록에서 **Gender**를 두 번 클릭합니다.  
  
7.  **="Male",**를 입력합니다(쉼표 포함).

8. **범주** 목록에서 **상수**를 클릭하고 **값** 상자에서 **수레국화 청색**을 클릭합니다.

    ![보고서-작성기-식-자습서-색-식-수레국화-청색](../reporting-services/media/report-builder-expression-tutorial-color-expression-cornflower-blue.png)

9. 그 뒤에 쉼표를 입력합니다. 
  
5.  **범주** 목록에서 **필드(식)**를 클릭하고 **값** 목록에서 **Gender**를 두 번 클릭합니다.  
  
7.  **="Female",**를 입력합니다(쉼표 포함). 

8. **범주** 목록에서 **상수**를 클릭하고 **값** 상자에서 **토마토**를 클릭합니다.

13. 그 뒤에 닫는 괄호 **)**를 입력합니다. 
  
    완성된 식은 다음과 같습니다. `=Switch(Fields!Gender.Value ="Male", "CornflowerBlue",Fields!Gender.Value ="Female","Tomato")`  
    
    ![보고서-작성기-식-자습서-색-식-완성](../reporting-services/media/report-builder-expression-tutorial-color-expression-complete.png)
  
12. **확인**을 클릭한 다음 다시 **확인**을 클릭하여 **사각형 속성** 대화 상자를 닫습니다.  
  
14. **실행** 을 클릭하여 보고서를 미리 봅니다.  

    ![보고서-작성기-식-자습서-미리 보기-m-f-열](../reporting-services/media/report-builder-expression-tutorial-preview-m-f-column.png)

### 색 사각형의 서식을 지정하려면

1. **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  

16. **M/F** 열에서 사각형을 선택합니다. 속성 창의 테두리 섹션에서 다음 속성을 설정합니다.

    - BorderColor = 흰색
    - BorderStyle = 실선
    - BorderWidth = 5pt
    
    ![보고서-작성기-식-자습서-서식-m-f-열](../reporting-services/media/report-builder-expression-tutorial-format-m-f-column.png)

18. **실행**을 클릭하여 보고서를 다시 미리 봅니다. 이번에는 색 블록 주위에 공백이 있습니다.

    ![보고서-작성기-식-자습서-서식 지정-m-f-열-미리 보기](../reporting-services/media/report-builder-expression-tutorial-preview-formatted-m-f-column.png)  
  
## <a name="Lookup"></a>5. CountryRegion 이름 조회  
이 섹션에서는 CountryRegion 데이터 집합을 만들고 **Lookup** 함수를 사용하여 국가/지역의 식별자 대신 국가/지역의 이름을 표시합니다.  
  
### CountryRegion 데이터 집합을 만들려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  보고서 데이터 창에서 **새로 만들기**를 클릭하고 **데이터 집합**을 클릭합니다.  
  
3.  **데이터 집합 속성에서 **내 보고서에 포함된 데이터 집합 사용**을 클릭합니다.  
  
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
  
9. **실행**(**!**)을 클릭하여 쿼리를 실행합니다.  
  
    쿼리 결과는 국가/지역 식별자와 이름입니다.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. **확인**을 다시 클릭하여 **데이터 집합 속성** 대화 상자를 닫습니다.  

     이제 **보고서 데이터** 열에 두 번째 데이터 집합이 있습니다.
  
### CountryRegion 데이터 집합에서 값을 조회하려면  
  
1.  **Country Region ID** 열 머리글을 클릭하고 **Country Region**을 읽도록 텍스트 **ID**를 삭제합니다.  
  
2.  **Country Region** 열의 데이터 셀을 마우스 오른쪽 단추로 클릭하고 **식**을 클릭합니다.  
  
3.  처음 등호(=)를 제외하고 식을 삭제합니다.  
  
    나머지 식은 다음과 같습니다. `=`  
  
4.  **식** 대화 상자에서 **일반 함수**를 확장하고 **기타**를 클릭한 다음 **항목** 목록에서 **조회**를 두 번 클릭합니다.  
  
6.  **범주** 목록에서 **필드(식)**를 클릭하고 **값** 목록에서 **CountryRegionID**를 두 번 클릭합니다.  
  
8.  `CountryRegionID.Value` 바로 뒤에 커서를 놓고 **,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")**을 입력합니다.  
  
    완성된 식은 다음과 같습니다. `=Lookup(Fields!CountryRegionID.Value,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")`  
  
    **Lookup** 함수의 구문에서는 식 데이터 집합의 CountryRegionID와 CountryRegion 데이터 집합에서 CountryRegion 값을 반환하는 CountryRegion 데이터 집합의 ID 사이에 조회를 지정합니다.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
## <a name="Count"></a>6. 마지막 구입 이후 일수 계산  
이 섹션에서는 열을 추가한 다음 **Now** 함수 또는 `ExecutionTime` 기본 제공 전역 변수를 사용하여 고객의 마지막 구매 이후 오늘까지의 일수를 계산합니다.  
  
### Days Ago 열을 추가하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  **Last Purchase** 열을 마우스 오른쪽 단추로 클릭하고 **열 삽입**을 가리킨 다음 **오른쪽**을 클릭합니다.  
  
    새 열이 **Last Purchase** 열의 오른쪽에 추가됩니다.  
  
3.  열 머리글에서 **Days Ago**를 입력합니다.  
  
4.  **Days Ago** 열의 데이터 셀을 마우스 오른쪽 단추로 클릭하고 **식**을 클릭합니다.  
  
5.  **식** 대화 상자에서 **일반 함수**를 확장하고 **날짜 및 시간**을 클릭합니다.  
  
6.  **항목** 목록에서 **DateDiff**를 두 번 클릭합니다.  
  
7.  `DateDiff(` 바로 뒤에 **"d",**를 입력합니다(따옴표 "" 및 쉼표 포함). 
  
9. **범주** 목록에서 **필드(식)**를 클릭하고 **값** 목록에서 **LastPurchase**를 두 번 클릭합니다.  
  
11. `Fields!LastPurchase.Value` 바로 뒤에 **,**(쉼표)를 입력합니다. 
  
13. **범주** 목록에서 **날짜 및 시간**을 다시 클릭하고 **항목** 목록에서 **Now**를 두 번 클릭합니다.  
  
    > [!WARNING]  
    > 프로덕션 보고서의 경우, 보고서의 정보 행에서와 같이 보고서가 렌더링되면서 여러 번 계산되는 식에서 **Now** 함수를 사용하면 안 됩니다. **Now**의 값은 행마다 변경되고 서로 다른 값이 식의 계산 결과에 영향을 미치므로 조금씩 일치하지 않는 결과가 발생합니다. 대신 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 제공하는 `ExecutionTime` 전역 변수를 사용하세요.  
  
15. `Now(` 뒤에 있는 왼쪽 괄호를 삭제한 다음 오른쪽 괄호 **)**를 입력합니다.  
  
    완성된 식은 다음과 같습니다. `=DateDiff("d", Fields!LastPurchase.Value, Now)`  
    
    ![보고서-작성기-식-자습서-마지막-구매-후-날짜](../reporting-services/media/report-builder-expression-tutorial-date-since-last-purchase.png)
  
17. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

11. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
## <a name="Indicator"></a>7. 표시기를 사용하여 판매량 비교 표시  
이 섹션에서는 새 열을 추가하고 표시기를 사용하여 사용자의 구매량 YTD(연간 누계)가 평균 구매량 YTD보다 크거나 작은지를 표시합니다. **Round** 함수는 값에서 소수를 제거합니다.  
  
표시기와 해당 상태를 구성하려면 여러 단계를 수행해야 합니다. 원하는 경우 "표시기를 구성하려면" 절차에서 단계를 건너뛰고 이 자습서의 완성된 식을 복사하여 **식** 대화 상자에 붙여넣을 수 있습니다.  
  
### + or - AVG Sales 열을 추가하려면  
  
1.  **YTD Purchase** 열을 마우스 오른쪽 단추로 클릭하고 **열 삽입**을 가리킨 다음 **오른쪽**을 클릭합니다.  
  
    새 열이 **YTD Purchase** 열의 오른쪽에 추가됩니다.  
  
2.  열 머리글을 클릭하고 **+ or - AVG Sales**를 입력합니다.  
  
### 표시기를 추가하려면  
  
1.  **삽입** 탭에서 **표시기**를 클릭한 다음 **+ or - AVG Sales** 열의 데이터 셀을 클릭합니다.  
  
    **표시기 유형 선택** 대화 상자가 열립니다.  
  
2.  아이콘 집합의 **방향** 그룹에서 회색 화살표 3개로 구성된 집합을 클릭합니다.  

    ![보고서-작성기-식-자습서-표시기-선택](../reporting-services/media/report-builder-expression-tutorial-select-indicator.png)
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### 표시기를 구성하려면  
  
1.  표시기를 마우스 오른쪽 단추로 클릭하고 **표시기 속성**을 클릭한 다음 **값 및 상태**를 클릭합니다.  
  
2.  **값** 입력란 옆의 식 단추(**fx**)를 클릭합니다.  
  
3.  **식** 대화 상자에서 **일반 함수**를 확장하고 **수치 연산**을 클릭합니다.  
  
4.  **항목** 목록에서 **Round**를 두 번 클릭합니다.  
  
5.  **범주** 목록에서 **필드(식)**를 클릭하고 **값** 목록에서 **YTDPurchase**를 두 번 클릭합니다.  
  
7.  `Fields!YTDPurchase.Value` 바로 뒤에 **-**(빼기 기호)를 입력합니다. 
  
9. **일반 함수**를 다시 확장하고 **집계**를 클릭한 다음 **항목** 목록에서 **Avg**를 두 번 클릭합니다.  
  
11. **범주** 목록에서 **필드(식)**를 클릭하고 **값** 목록에서 **YTDPurchase**를 두 번 클릭합니다.  
  
13. `Fields!YTDPurchase.Value` 바로 뒤에 **, "Expressions"))**를 입력합니다.  
  
    완성된 식은 다음과 같습니다. `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions"))`  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. **상태 단위** 상자에서 **숫자**를 선택합니다.  
  
17. 아래쪽 화살표가 있는 행에서 **시작** 값의 입력란 오른쪽에 있는 **fx** 단추를 클릭합니다.  

    ![보고서-작성기-식-자습서-표시기-시작](../reporting-services/media/report-builder-expression-tutorial-indicator-start.png)
  
18. **식** 대화 상자에서 **일반 함수**를 확장하고 **수치 연산**을 클릭합니다.  
  
19. **항목** 목록에서 **Round**를 두 번 클릭합니다.  
  
20. **범주** 목록에서 **필드(식)**를 클릭하고 **값** 목록에서 **YTDPurchase**를 두 번 클릭합니다.  
  
22. `Fields!YTDPurchase.Value` 바로 뒤에 **-**(빼기 기호)를 입력합니다. 
  
24. **일반 함수**를 다시 확장하고 **집계**를 클릭한 다음 **항목** 목록에서 **Avg**를 두 번 클릭합니다.  
  
26. **범주** 목록에서 **필드(식)**를 클릭하고 **값** 목록에서 **YTDPurchase**를 두 번 클릭합니다.  
  
28. `Fields!YTDPurchase.Value` 바로 뒤에 **, "Expressions")) < 0**을 입력합니다.  
  
    완성된 식은 다음과 같습니다. `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) < 0`  
  
30. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
31. **끝** 값의 입력란에 **0**을 입력합니다.  
  
32. 옆쪽 화살표가 있는 행을 클릭하고 **삭제**를 클릭합니다.  

    ![보고서-작성기-식-자습서-표시기-상태-삭제](../reporting-services/media/report-builder-expression-tutorial-delete-indicator-state.png)
    
    이제 위쪽 또는 아래쪽 이렇게 두 개의 화살표만 있습니다.
  
33. 위쪽 화살표가 있는 행에서 **시작** 상자에 **0**을 입력합니다.  
  
34. **끝** 값의 입력란 오른쪽에 있는 **fx** 단추를 클릭합니다.  
  
35. **식** 대화 상자에서 **100**을 삭제하고 다음 식을 만듭니다. `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) >0`  
  
36. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
37. **확인**을 다시 클릭하여 **표시기 속성** 대화 상자를 닫습니다.  
  
38. **실행** 을 클릭하여 보고서를 미리 봅니다.  

    ![보고서-작성기-식-자습서-표시기-미리 보기](../reporting-services/media/report-builder-expression-tutorial-preview-indicator.png)
  
## <a name="GreenBar"></a>8. 줄무늬 보고서 만들기  
보고서 구독자가 보고서의 번갈아 표시되는 행에 적용할 색을 지정하여 줄무늬 보고서를 만들 수 있도록 매개 변수를 만듭니다.  
  
### 매개 변수를 추가하려면  
  
1.  **디자인** 을 클릭하여 디자인 뷰로 돌아갑니다.  
  
2.  **보고서 데이터** 창에서 **매개 변수**를 마우스 오른쪽 단추로 클릭하고 **매개 변수 추가**를 클릭합니다.  

    ![보고서-작성기-식-자습서-매개 변수-추가](../reporting-services/media/report-builder-expression-tutorial-add-parameter.png)
  
    **보고서 매개 변수 속성** 대화 상자가 열립니다.  
  
3.  **프롬프트**에 **Choose color**를 입력합니다.  
  
4.  **이름**에 **RowColor**를 입력합니다.  
  
5.  **사용 가능한 값** 탭에서 **값 지정**을 클릭합니다.  
  
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

    ![보고서-작성기-식-자습서-사용 가능한-매개 변수](../reporting-services/media/report-builder-expression-tutorial-parameter-available.png)
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### 정보 행에 색을 번갈아 적용하려면  
  
1.   자체 배경색이 있는 **M/F** 열의 셀을 제외한 데이터 행의 모든 셀을 선택합니다.  

     ![보고서-작성기-식-자습서-줄무늬-선택](../reporting-services/media/report-builder-expression-tutorial-select-banded.png)
  
4.  속성 창에서 **BackgroundColor**를 클릭합니다. 

     속성 창이 표시되지 않으면 **보기** 탭에서 **속성** 상자를 선택합니다.  
  
    속성 창에서 속성이 범주별로 나열된 경우 **기타** 범주에서 **BackgroundColor**를 찾을 수 있습니다.  
  
5.  아래쪽 화살표를 클릭한 다음 **식**을 클릭합니다.  

    ![보고서-작성기-식-자습서-줄무늬-색-속성](../reporting-services/media/report-builder-expression-tutorial-banded-color-property.png)
  
6.  **식** 대화 상자에서 **일반 함수**를 확장하고 **프로그램 흐름**을 클릭합니다.  
  
7.  **항목** 목록에서 **IIf**를 두 번 클릭합니다.  
  
8.  **일반 함수**에서 **기타**를 클릭하고 **항목** 목록에서 **RowNumber**를 두 번 클릭합니다.  

9. **RowNumber(** 바로 뒤에 **Nothing) MOD 2,**를 입력합니다.
  
8. **매개 변수**를 클릭하고 **값** 목록에서 **RowColor**를 두 번 클릭합니다.  
  
22. `Parameters!RowColor.Value` 바로 뒤에 **, "White")**를 입력합니다.  
  
    완성된 식은 다음과 같습니다. `=IIF(RowNumber(Nothing) MOD 2, Parameters!RowColor.Value, “White”)`  
    
    ![보고서-작성기-식-자습서-줄무늬-색-식](../reporting-services/media/report-builder-expression-tutorial-banded-color-expressn.png)
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### 보고서 실행  
  
1.  **홈** 탭에서 **실행**을 클릭합니다.  

    이제 보고서를 실행할 때 흰색이 아닌 줄무늬의 색을 선택한 후에야 보고서가 표시됩니다.
  
3.  **색 선택** 목록에서 보고서에 사용할 흰색이 아닌 줄무늬의 색을 선택합니다.  
    
    ![보고서-작성기-식-자습서-색-선택](../reporting-services/media/report-builder-expression-tutorial-select-color.png)
  
4.  **보고서 보기**를 클릭합니다.  
  
    보고서가 렌더링되고 선택한 배경이 행에 번갈아 표시됩니다. 
    
    ![보고서-작성기-식-자습서-줄무늬-미리 보기](../reporting-services/media/report-builder-expression-tutorial-preview-banded.png) 
  
## <a name="Title"></a>(선택 사항) 보고서 제목 추가  
보고서에 제목을 추가합니다.  
  
### 보고서 제목을 추가하려면  
  
1.  디자인 화면에서 **제목을 추가하려면 클릭하십시오.**를 클릭합니다.  
  
2.  **판매 비교 요약**을 입력한 다음 텍스트를 선택합니다.  
  
3.  **홈** 탭의 **글꼴** 상자에서 다음을 설정합니다.

    -  크기 = 18
    -  색 = 회색
    -  굵게
  
4.  **홈** 탭에서 **실행**을 클릭합니다.  
  
3.  보고서에 사용할 흰색이 아닌 줄무늬의 색을 선택한 다음 **보고서 보기**를 클릭합니다.  
  
## <a name="Save"></a>(선택 사항) 보고서 저장  
보고서를 보고서 서버, SharePoint 라이브러리 또는 컴퓨터에 저장할 수 있습니다. 자세한 내용은 [보고서 저장&#40;보고서 작성기&#41;](../reporting-services/report-builder/saving-reports-report-builder.md)을 참조하세요.  
  
이 자습서에서는 보고서를 보고서 서버에 저장합니다. 보고서 서버에 액세스할 수 없는 경우에는 보고서를 컴퓨터에 저장하십시오.  
  
### 보고서를 보고서 서버에 저장하려면  
  
1.  **파일** 메뉴에서 **다른 이름으로 저장**을 선택합니다.  
  
2.  **최근에 사용한 사이트 및 서버**를 클릭합니다.  
  
3.  보고서를 저장할 수 있는 권한을 가진 보고서 서버의 이름을 선택하거나 입력합니다.  
  
    "보고서 서버에 연결하는 중"이라는 메시지가 나타납니다. 연결되면 보고서 서버 관리자가 기본 보고서 위치로 지정한 보고서 폴더의 내용이 표시됩니다.  
  
4.  보고서 이름을 지정하고 **저장**을 클릭합니다.  
  
보고서가 보고서 서버에 저장됩니다. 연결된 보고서 서버의 이름이 창 아래쪽에 있는 상태 표시줄에 나타납니다.

이제 보고서 구독자가 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 웹 포털에서 보고서를 볼 수 있습니다.

![보고서-작성기-식-자습서-최종-브라우저 내](../reporting-services/media/report-builder-expression-tutorial-final-in-browser.png)

   
## 관련 항목:  
[식&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
[식 예&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
[표시기&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
[이미지, 입력란, 사각형 및 선&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/images-text-boxes-rectangles-and-lines-report-builder-and-ssrs.md)  
[테이블&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-design/tables-report-builder-and-ssrs.md)  
[보고서 데이터 집합&#40;SSRS&#41;](../reporting-services/report-data/report-datasets-ssrs.md)  
  
  
  
