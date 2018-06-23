---
title: '자습서: 보고서에 매개 변수 추가(보고서 작성기) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eab34ec4-b3ad-4a76-95cc-07b2f75ee6d7
caps.latest.revision: 9
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 230cd7bcbadf9e51ba248ffa34851335977cb0ad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182208"
---
# <a name="tutorial-add-a-parameter-to-your-report-report-builder"></a>자습서: 보고서에 매개 변수 추가(보고서 작성기)
  보고서에 매개 변수를 추가하면 사용자가 데이터 원본이나 보고서에서 보고서 데이터를 필터링할 수 있습니다. 보고서 매개 변수는 데이터 집합 쿼리에 포함하는 각 쿼리 매개 변수에 대해 자동으로 만들어집니다. 매개 변수 데이터 형식에 따라 보고서 뷰 도구 모음에 매개 변수가 표시되는 방식이 결정됩니다.  
  
 ![rs_tut_Parameter](../../2014/tutorials/media/rs-tut-parameter.gif "rs_tut_Parameter")  
  
##  <a name="BackToTop"></a> 학습 내용  
 이 자습서에서는 다음 작업 방법을 배웁니다.  
  
1.  [테이블 또는 행렬 마법사에서 행렬 보고서 및 데이터 집합 만들기](#Setup)  
  
2.  [구성 데이터, 레이아웃 및 스타일 선택 테이블 또는 행렬 마법사에서](#CompleteWizard)  
  
3.  [보고서 매개 변수를 만드는 쿼리 매개 변수 추가](#Query)  
  
4.  [보고서 매개 변수의 기본 데이터 형식 및 기타 속성 변경](#ChangeDefaultProperties)  
  
    1.  [사용 가능한 값을 제공할 데이터 집합을 추가 및 표시 이름](#AddDataset)  
  
    2.  [값의 드롭다운 목록을 만드는 데 사용 가능한 값 지정](#AvailableValues)  
  
    3.  [보고서가 자동으로 실행 되도록 기본값 지정](#DefaultValues)  
  
    4.  [이름/값 쌍이 있는 데이터 집합에서 값 조회](#NameValue)  
  
5.  [보고서에 선택한 매개 변수 값을 표시 합니다.](#Expression)  
  
6.  [필터에서 보고서 매개 변수를 사용 합니다.](#Filter)  
  
7.  [여러 값을 허용 하도록 보고서 매개 변수 변경](#Multivalued)  
  
8.  [조건부 표시 유형에 대 한 부울 매개 변수를 추가 합니다.](#Boolean)  
  
9. [보고서 제목 추가](#Title)  
  
10. [보고서 저장](#Save)  
  
> [!NOTE]  
>  이 자습서에서 마법사의 단계는 하나의 절차로 통합됩니다. 보고서 서버를 찾고, 데이터 원본을 선택하고, 데이터 집합을 만드는 방법에 대한 단계별 지침은 이 시리즈의 첫 번째 자습서인 [자습서: 기본 테이블 보고서 만들기&#40;보고서 작성기&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)를 참조하세요.  
  
 이 자습서에 소요되는 예상 시간: 25분  
  
## <a name="requirements"></a>요구 사항  
 요구 사항에 대한 자세한 내용은 [자습서의 필수 조건&#40;보고서 작성기&#41;](../reporting-services/report-builder-tutorials.md)을 참조하세요.  
  
##  <a name="Setup"></a> 1. 테이블 또는 행렬 마법사에서 행렬 보고서 및 데이터 집합 만들기  
 행렬 보고서, 데이터 원본 및 데이터 집합을 만듭니다.  
  
> [!NOTE]  
>  이 자습서의 쿼리에는 데이터 값이 포함되어 있으므로 외부 데이터 원본이 필요하지 않습니다. 따라서 쿼리가 상당히 길어집니다. 비즈니스 환경에서는 쿼리에 데이터가 포함되지 않을 것입니다. 이 자습서의 쿼리는 학습용으로만 제공됩니다.  
  
#### <a name="to-create-a-new-matrix-report"></a>새 행렬 보고서를 만들려면  
  
1.  클릭 **시작**, 가리킨 **프로그램**, 가리킨 [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] **보고서 작성기**, 클릭 하 고 **보고서 작성기**합니다.  
  
     **시작** 대화 상자가 나타납니다.  
  
    > [!NOTE]  
    >  **시작** 대화 상자가 나타나지 않으면 **보고서 작성기** 단추에서 **새로 만들기**를 클릭합니다.  
  
2.  왼쪽된 창의 확인 **보고서** 을 선택 합니다.  
  
3.  오른쪽 창에서 **테이블 또는 행렬 마법사**를 클릭합니다.  
  
4.  **만들기**를 클릭합니다.  
  
5.  **데이터 집합 선택** 페이지에서 **데이터 집합 만들기**를 클릭합니다.  
  
6.  **다음**을 클릭합니다.  
  
7.  **데이터 원본에 대한 연결 선택** 페이지에서 **SQL Server** 형식의 데이터 원본을 선택합니다. 목록에서 데이터 원본을 선택하거나 보고서 서버를 찾아 선택합니다.  
  
8.  **다음**을 클릭합니다.  
  
9. **쿼리 디자인** 페이지에서 **텍스트로 편집**을 클릭합니다.  
  
10. 쿼리 창에 다음 쿼리를 붙여 넣습니다.  
  
    ```  
    ;WITH CTE (StoreID, Subcategory, Quantity)   
    AS (  
    SELECT 200 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 2002 AS Quantity  
    UNION SELECT  200 AS StoreID, 'Camcorders' AS Subcategory, 1954 AS Quantity  
    UNION SELECT  200 AS StoreID, 'Accessories' AS Subcategory, 1895 AS Quantity  
    UNION SELECT  199 AS StoreID, 'Digital Cameras' AS Subcategory, 1849 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 1579 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Camcorders' AS Subcategory, 1561 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Digital Cameras' AS Subcategory, 1553 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Accessories' AS Subcategory, 1534 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Accessories' AS Subcategory, 1755 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Camcorders' AS Subcategory, 1631 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 1772 AS Quantity)  
    SELECT StoreID, Subcategory, Quantity  
    FROM CTE  
    ```  
  
     이 쿼리는 공통 테이블 식 안에 있는 몇 가지 [!INCLUDE[tsql](../includes/tsql-md.md)] SELECT 문의 결과를 결합하여 Contoso 예제 데이터베이스의 단순화된 데이터에 따라 값을 지정합니다. Contoso 판매량 데이터는 소비자 제품에 대한 해외 판매량 데이터를 나타냅니다. 이 자습서에서는 카메라 판매량 데이터를 사용합니다. 하위 범주는 디지털 카메라, 디지털 SLR(Single Lens Reflex) 카메라, 캠코더 및 액세서리를 나타냅니다.  
  
     이 쿼리는 상점 식별자, 판매 항목 하위 범주 및 세 상점의 판매 주문에 대한 주문 수량을 포함하는 열 이름을 지정합니다. 이 쿼리에서 상점 이름은 결과 집합에 포함되는 데이터가 아닙니다. 이 자습서의 뒷부분에 나오는 별도의 데이터 집합에서 상점 식별자에 해당하는 상점 이름을 조회할 수 있습니다.  
  
     이 쿼리에는 쿼리 매개 변수가 포함되어 있지 않습니다. 이 자습서의 뒷부분에서 쿼리 매개 변수를 추가합니다.  
  
11. 쿼리 디자이너 도구 모음에서 **실행** (**!**)을 클릭합니다. 결과 집합은 11 개의 4 개 매장에서 각 하위 범주에 대 한 판매 항목 수량을 표시 하는 데이터 행을 표시 하 고 다음 열이 포함: StoreID, Subcategory, Quantity 합니다.  
  
12. **다음**을 클릭합니다.  
  
##  <a name="CompleteWizard"></a> 2. 테이블 또는 행렬 마법사에서 데이터 구성 및 레이아웃과 스타일 선택  
 이 마법사를 사용하여 데이터를 표시할 시작 디자인을 제공할 수 있습니다. 이 마법사의 미리 보기 창에서는 테이블 또는 행렬 디자인을 완료하기 전에 데이터 그룹화의 결과를 시각화할 수 있습니다.  
  
#### <a name="to-organize-data-into-groups"></a>데이터를 그룹으로 구성하려면  
  
1.  **필드 정렬** 페이지에서 Subcategory를 **행 그룹**으로 끌어옵니다.  
  
2.  StoreID를 **열 그룹**으로 끌어옵니다.  
  
3.  Quantity를 **값**으로 끌어옵니다.  
  
     하위 범주로 그룹화된 행에 판매 수량 값을 구성했습니다. 각 상점마다 하나의 열이 있습니다.  
  
4.  **다음**을 클릭합니다.  
  
5.  에 **레이아웃 선택** 페이지의 **옵션**, 되어 있는지 확인 **부분합 및 총합계 표시** 을 선택 합니다.  
  
     보고서를 실행하면 마지막 열에 모든 상점에 대한 각 하위 범주의 총 수량이 표시되고 마지막 행에 각 상점에 대한 모든 하위 범주의 총 수량이 표시됩니다.  
  
6.  **다음**을 클릭합니다.  
  
7.  에 **스타일 선택** 페이지의 스타일 창에서 스타일을 선택 합니다.  
  
8.  **마침**을 클릭합니다.  
  
     디자인 화면에 행렬이 추가됩니다. 행렬에는 열 3개와 행 3개가 표시됩니다. 첫 번째 행의 셀 내용은 Subcategory, [StoreID] 및 Total입니다. 두 번째 행의 셀 내용에는 하위 범주, 각 상점의 판매 항목 수량 및 모든 상점에 대한 각 하위 범주의 총 수량을 나타내는 식이 포함됩니다. 마지막 행의 셀에는 각 상점의 총합계가 표시됩니다.  
  
9. 행렬을 클릭하고 첫 번째 열의 가장자리로 마우스를 이동한 후 핸들을 잡고 열 너비를 확장합니다.  
  
10. **실행** 을 클릭하여 보고서를 미리 봅니다.  
  
 보고서가 보고서 서버에서 실행되고 보고서 처리가 수행된 시간과 제목이 표시됩니다.  
  
 이 경우 열 머리글에는 상점 이름이 아닌 상점 식별자가 표시됩니다. 나중에 상점 식별자/상점 이름 쌍이 포함된 데이터 집합에서 상점 이름을 조회하는 식을 추가합니다.  
  
##  <a name="Query"></a> 3. 쿼리 매개 변수를 추가하여 보고서 매개 변수 만들기  
 쿼리 매개 변수를 쿼리에 추가하면 보고서 작성기가 이름, 프롬프트 및 데이터 형식에 대한 기본 속성을 사용하여 단일 값 보고서 매개 변수를 자동으로 만듭니다.  
  
#### <a name="to-add-a-query-parameter"></a>쿼리 매개 변수를 추가하려면  
  
1.  디자인 뷰로 전환합니다.  
  
2.  보고서 데이터 창에서 **데이터 집합** 폴더를 확장하고 **DataSet1**을 마우스 오른쪽 단추로 클릭한 다음 **쿼리**를 클릭합니다.  
  
3.  다음 추가 [!INCLUDE[tsql](../includes/tsql-md.md)] `WHERE` 쿼리의 마지막 줄으로 절:  
  
    ```  
    WHERE StoreID = (@StoreID)  
    ```  
  
     `WHERE` 쿼리 매개 변수로 지정 된 상점 식별자에 검색된 데이터를 제한 하는 절 *@StoreID*합니다.  
  
4.  쿼리 디자이너 도구 모음에서 **실행** (**!**)을 클릭합니다. **쿼리 매개 변수 정의** 대화 상자가 열리고 쿼리 매개 변수 *@StoreID*의 값을 입력하라는 메시지가 나타납니다.  
  
5.  **매개 변수 값**에 **200**을 입력합니다.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     결과 집합에는 상점 식별자 **200**에 대한 Accessories, Camcorders 및 Digital SLR Cameras의 판매 수량이 표시됩니다.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  보고서 데이터 창에서 **매개 변수** 폴더를 확장합니다.  
  
 이제 보고서 매개 변수 라는 *@StoreID*합니다. 기본적으로 매개 변수는 데이터 형식이 **텍스트**합니다. 상점 식별자가 정수이므로 다음 절차에서 데이터 형식을 Integer로 변경합니다.  
  
##  <a name="ChangeDefaultProperties"></a> 4. 보고서 매개 변수의 기본 데이터 형식 및 기타 속성 변경  
 보고서 매개 변수를 만든 후 속성의 기본값을 조정할 수 있습니다.  
  
#### <a name="to-change-the-default-data-type-for-a-report-parameter"></a>보고서 매개 변수의 기본 데이터 형식을 변경하려면  
  
1.  아래에 있는 보고서 데이터 창에는 **매개 변수** 노드를 마우스 오른쪽 단추로 클릭 *@StoreID*, 클릭 하 고 **매개 변수 속성**합니다.  
  
2.  프롬프트에 입력 **Store identifier?** 보고서를 실행할 때 이 텍스트가 보고서 뷰어 도구 모음에 표시됩니다.  
  
3.  **데이터 형식**의 드롭다운 목록에서 **정수**를 선택합니다.  
  
4.  대화 상자의 나머지 기본값을 적용합니다.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  보고서를 미리 봅니다. 에 대 한 프롬프트를 표시 하는 보고서 뷰어 *@StoreID*합니다.  
  
7.  보고서 뷰어 도구 모음에서 Store ID 옆에 **200**을 입력한 다음 **보고서 보기**를 클릭합니다.  
  
##  <a name="AddDataset"></a> 4a 합니다. 사용 가능한 값과 표시 이름을 제공하는 데이터 집합 추가  
 선택할 값에 대한 드롭다운 목록을 만들어 사용자가 매개 변수에 대한 유효한 값만 입력하도록 할 수 있습니다. 지정한 목록이나 데이터 집합의 값을 사용할 수 있습니다. 쿼리에 매개 변수에 대한 참조가 포함되지 않은 데이터 집합에서 사용 가능한 값을 제공해야 합니다.  
  
#### <a name="to-create-a-dataset-for-valid-values-for-a-parameter"></a>매개 변수에 대한 유효한 값의 데이터 집합을 만들려면  
  
1.  디자인 뷰로 전환합니다.  
  
2.  보고서 데이터 창에서 **데이터 집합** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **데이터 집합 추가**를 클릭합니다.  
  
3.  **이름**에 **Stores**를 입력합니다.  
  
4.  선택 된 **내 보고서에 포함 된 데이터 집합을 사용 하 여** 옵션입니다.  
  
5.  **데이터 소스**, 드롭 다운 목록에서 첫 번째 절차에서 만든 데이터 원본을 선택 합니다.  
  
6.  **쿼리 유형**에서 **텍스트** 가 선택되어 있는지 확인합니다.  
  
7.  **쿼리**에 다음 텍스트를 붙여넣습니다.  
  
    ```  
    SELECT 200 AS StoreID, 'Contoso Catalog Store' as StoreName  
    UNION SELECT 199 AS StoreID, 'Contoso North America Online Store' as StoreName  
    UNION SELECT 307 AS StoreID, 'Contoso Asia Online Store' as StoreName  
    UNION SELECT 306 AS StoreID, 'Contoso Europe Online Store' as StoreName  
    ```  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     보고서 데이터 창의 **Stores** 데이터 집합 노드 아래에 StoreID 및 StoreName 필드가 표시됩니다.  
  
##  <a name="AvailableValues"></a> 4b 합니다. 드롭다운 값 목록을 만드는 데 사용 가능한 값 지정  
 사용 가능한 값을 제공하는 데이터 집합을 만든 후 보고서 속성을 변경하여 보고서 뷰어 도구 모음의 유효한 값의 드롭다운 목록을 채우는 데 사용할 데이터 집합과 필드를 지정해야 합니다.  
  
#### <a name="to-provide-available-values-for-a-parameter-from-a-dataset"></a>데이터 집합의 매개 변수에 사용 가능한 값을 제공하려면  
  
1.  보고서 데이터 창에서 매개 변수를 마우스 오른쪽 단추로 *@StoreID*, 클릭 하 고 **매개 변수 속성**합니다.  
  
2.  **사용 가능한 값**을 클릭한 다음 **쿼리에서 값 가져오기**를 클릭합니다.  
  
3.  **데이터 집합**의 드롭다운 목록에서 **Stores**를 클릭합니다.  
  
4.  **값 필드**의 드롭다운 목록에서 StoreID를 클릭합니다.  
  
5.  **레이블 필드**의 드롭다운 목록에서 StoreName을 클릭합니다. 이 레이블 필드는 값의 표시 이름을 지정합니다.  
  
6.  **일반**을 클릭합니다.  
  
7.  프롬프트에 입력 **Store name?**  
  
     사용자가 이제 상점 식별자 대신 상점 이름의 목록에서 선택하게 됩니다. 매개 변수가 상점 이름이 아닌 상점 식별자를 기반으로 하기 때문에 매개 변수 데이터 형식은 **Integer** 로 유지됩니다.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. 보고서를 미리 봅니다.  
  
     보고서 뷰어 도구 모음에서 매개 변수 입력란은 이제 보여 주는 드롭다운 목록이  **\<값 선택 >** 합니다.  
  
10. 드롭다운 목록에서 Contoso Catalog Store를 선택한 다음 **보고서 보기**합니다.  
  
 보고서에는 상점 식별자 **200**에 대한 Accessories, Camcorders 및 Digital SLR Cameras의 판매 수량이 표시됩니다.  
  
##  <a name="DefaultValues"></a> 4 코어입니다. 보고서가 자동으로 실행되도록 기본값 지정  
 보고서가 자동으로 실행되도록 각 매개 변수의 기본값을 지정할 수 있습니다.  
  
#### <a name="to-specify-a-default-value-from-a-dataset"></a>데이터 집합에서 기본값을 지정하려면  
  
1.  디자인 뷰로 전환합니다.  
  
2.  보고서 데이터 창에서 *@StoreID*을 마우스 오른쪽 단추로 클릭한 다음 **매개 변수 속성**를 참조하세요.  
  
3.  클릭 **기본값**, 클릭 하 고 **쿼리에서 값 가져오기**합니다.  
  
4.  **데이터 집합**의 드롭다운 목록에서 **Stores**를 클릭합니다.  
  
5.  **값 필드**의 드롭다운 목록에서 StoreID를 클릭합니다.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  보고서를 미리 봅니다.  
  
 에 대 한 *@StoreID*, 보고서 뷰어에 "Contoso North America Online Store" 값을 표시 합니다. 이 결과 데이터 집합에 대해 집합에서 첫 번째 값은 **저장소**합니다. 보고서에는 상점 식별자 **199**에 대한 Digital Cameras의 판매 수량이 표시됩니다.  
  
#### <a name="to-specify-a-custom-default-value"></a>사용자 지정 기본값을 지정하려면  
  
1.  디자인 뷰로 전환합니다.  
  
2.  보고서 데이터 창에서 *@StoreID*을 마우스 오른쪽 단추로 클릭한 다음 **매개 변수 속성**를 참조하세요.  
  
3.  클릭 **기본값**를 클릭 하 고 **값을 지정**, 클릭 하 고 **추가**합니다. 새 값 행이 추가됩니다.  
  
4.  **값**에 **200**을 입력합니다.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  보고서를 미리 봅니다.  
  
 에 대 한 *@StoreID*, 보고서 뷰어에 "Contoso Catalog Store" 값을 표시 합니다. 이 상점 식별자에 대 한 표시 이름을 **200**합니다. 보고서에는 상점 식별자 **200**에 대한 Accessories, Camcorders 및 Digital SLR Cameras의 판매 수량이 표시됩니다.  
  
##  <a name="NameValue"></a> 4d 합니다. 이름/값 쌍이 있는 데이터 집합에서 값 조회  
 데이터 집합에는 식별자 및 해당 이름 필드가 포함되어 있을 수 있습니다. 식별자만 있는 경우 이름/값 쌍이 포함된 만든 데이터 집합에서 해당 이름을 조회할 수 있습니다.  
  
#### <a name="to-look-up-a-value-from-a-dataset"></a>데이터 집합에서 값을 조회하려면  
  
1.  디자인 뷰로 전환합니다.  
  
2.  디자인 화면에서 행렬에 있는 첫 번째 행의 열 머리글에서 `[StoreID]` 를 마우스 오른쪽 단추로 클릭한 다음 **식**을 클릭합니다.  
  
3.  식 창에서 시작 부분의 `equals`(=)를 제외한 텍스트를 모두 삭제합니다.  
  
4.  **범주**에서 **일반 함수**를 확장하고 **기타**를 클릭합니다. 항목 창에 함수 집합이 표시됩니다.  
  
5.  항목에서 **조회**를 두 번 클릭합니다. 식 창에 `=Lookup(`이 표시됩니다. 예제 창에 Lookup 구문 예가 표시됩니다.  
  
6.  다음 식을 입력합니다. `=Lookup(Fields!StoreID.Value,Fields!StoreID.Value,Fields!StoreName.Value,"Stores")`  
  
     Lookup 함수가 StoreID의 값을 사용하여 "Stores" 데이터 집합에서 조회한 다음 StoreName 값을 반환합니다.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     상점 열 머리글에 복잡 한 식에 대 한 표시 텍스트 포함:  **< \<Expr >>** 합니다.  
  
8.  보고서를 미리 봅니다.  
  
 각 페이지의 맨 위 입력란에 상점 식별자 대신 상점 이름이 표시됩니다.  
  
##  <a name="Expression"></a> 5. 보고서에 선택한 매개 변수 값 표시  
 사용자가 보고서에 대해 궁금한 사항이 있는 경우 사용자가 선택한 매개 변수 값을 알면 도움이 됩니다. 각 매개 변수에 대해 사용자가 선택한 값을 보고서에 유지할 수 있습니다. 입력란의 매개 변수를 페이지 바닥글에 표시하는 것이 한 가지 방법입니다.  
  
#### <a name="to-display-the-selected-parameter-value-and-label-on-a-page-footer"></a>선택한 매개 변수 값 및 레이블을 페이지 바닥글에 표시하려면  
  
1.  디자인 뷰로 전환합니다.  
  
2.  페이지 바닥글을 마우스 오른쪽 단추로 클릭, 가리킨 **삽입**, 클릭 하 고 **텍스트 상자**합니다. 입력란을 타임스탬프가 있는 입력란 옆으로 끌어옵니다. 입력란의 측면 핸들을 잡고 너비를 확장합니다  
  
3.  보고서 데이터 창에서 *@StoreID* 매개 변수를 입력란으로 끌어옵니다. 입력란에 `[@StoreID]`가 표시됩니다.  
  
4.  매개 변수 레이블을 표시하려면 삽입 커서가 기존 식 뒤에 나타날 때까지 입력란을 클릭하고 공백을 입력한 다음 매개 변수의 또 다른 복사본을 보고서 데이터 창에서 입력란으로 끌어옵니다. 입력란에 `[@StoreID] [@StoreID]`가 표시됩니다.  
  
5.  첫 번째 식을 마우스 오른쪽 단추로 클릭 하 고 클릭 **식**합니다. **식** 대화 상자가 열립니다. `Value` 텍스트를 `Label`로 바꿉니다.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     `[@StoreID.Label] [@StoreID]`텍스트가 표시됩니다.  
  
7.  보고서를 미리 봅니다.  
  
##  <a name="Filter"></a> 6. 필터에서 보고서 매개 변수 사용  
 필터를 사용하면 외부 데이터 원본에서 검색된 데이터 중 보고서에 사용할 데이터를 제어할 수 있습니다. 사용자가 표시할 데이터를 제어할 수 있도록 하기 위해 행렬에 대한 필터에 보고서 매개 변수를 포함할 수 있습니다.  
  
#### <a name="to-specify-a-parameter-in-a-matrix-filter"></a>행렬 필터에서 매개 변수를 지정하려면  
  
1.  디자인 뷰로 전환합니다.  
  
2.  행렬에서 행 또는 열 머리글 핸들을 마우스 오른쪽 단추로 클릭한 다음 **테이블릭스 속성**을 클릭합니다.  
  
3.  **필터**를 클릭한 다음 **추가**를 클릭합니다. 새 필터 행이 나타납니다.  
  
4.  **식**의 드롭다운 목록에서 데이터 집합 필드 StoreID를 선택합니다. 데이터 형식에 **Integer**가 표시됩니다. 식 값이 데이터 집합 필드이면 데이터 형식이 자동으로 설정됩니다.  
  
5.  **연산자**, 있는지 `equals` (=)을 선택 합니다.  
  
6.  **값**에 `[@StoreID]`를 입력합니다. `[@StoreID]` 는 `=Parameters!StoreID.Value`를 나타내는 단순 식 구문입니다.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  보고서를 미리 봅니다.  
  
     행렬에 "Contoso Catalog Store"에 대한 데이터만 표시됩니다.  
  
9. 보고서 뷰어 도구 모음에서 **Store name?** 으로 **Contoso Asia Online Store**를 선택한 다음 **보고서 보기**를 클릭합니다.  
  
 행렬에 선택한 상점에 해당하는 데이터가 표시됩니다.  
  
##  <a name="Multivalued"></a> 7. 여러 값을 허용하도록 보고서 매개 변수 변경  
 매개 변수를 단일 값 매개 변수에서 다중값 매개 변수로 변경하려면 필터를 비롯해 매개 변수에 대한 참조가 포함된 모든 식과 쿼리를 변경해야 합니다. 다중값 매개 변수는 값 배열입니다. 데이터 집합 쿼리에서 쿼리 구문을 통해 한 값의 값 집합 포함 여부를 테스트해야 합니다. 보고서 식에서 식 구문은 개별 값이 아닌 값 배열에 액세스해야 합니다.  
  
#### <a name="to-change-a-parameter-from-single-to-multivalued"></a>매개 변수를 단일 값 매개 변수에서 다중값 매개 변수로 변경하려면  
  
1.  디자인 뷰로 전환합니다.  
  
2.  보고서 데이터 창에서 *@StoreID*을 마우스 오른쪽 단추로 클릭한 다음 **매개 변수 속성**를 참조하세요.  
  
3.  **다중 값 허용**을 선택합니다.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  보고서 데이터 창에서 **데이터 집합** 폴더를 확장하고 **DataSet1**을 마우스 오른쪽 단추로 클릭한 다음 **쿼리**를 클릭합니다.  
  
6.  변경 `equals` (=)를 `IN` 에 [!INCLUDE[tsql](../includes/tsql-md.md)] `WHERE` 절에 쿼리의 마지막 줄:  
  
    ```  
    WHERE StoreID IN (@StoreID)  
    ```  
  
     `IN` 연산자는 값의 값 집합 포함 여부를 테스트합니다.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  행렬에서 행 또는 열 머리글 핸들을 마우스 오른쪽 단추로 클릭한 다음 **테이블릭스 속성**을 클릭합니다.  
  
9. **필터**를 클릭합니다.  
  
10. **연산자**에서 **In**을 선택합니다.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. 페이지 바닥글에 매개 변수가 표시되는 입력란에서 모든 텍스트를 삭제합니다.  
  
13. 입력란을 마우스 오른쪽 단추로 클릭한 다음 **식**을 클릭합니다. 다음 식을 입력합니다. `=Join(Parameters!StoreID.Label, ", ")`  
  
     이 식은 사용자가 선택한 모든 상점 이름을 연결합니다.  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
15. 방금 만든 후 다음 명령을 입력 하는 식 앞에 텍스트 상자에는 클릭: 매개 변수 값이 선택: 합니다.  
  
16. 보고서를 미리 봅니다.  
  
17. Store Name? 옆의 드롭다운 목록을 클릭합니다.  
  
     각각의 유효한 값이 확인란 옆에 나타납니다.  
  
18. **모두 선택**을 클릭한 다음 **보고서 보기**를 클릭합니다.  
  
     보고서에 모든 상점에 대한 모든 하위 범주의 판매 수량이 표시됩니다.  
  
19. 드롭다운 목록에서 **모두 선택** 을 클릭하여 목록을 지우고 "Contoso Catalog Store"와 "Contoso Asia Online Store"를 차례로 클릭한 다음 **보고서 보기**를 클릭합니다.  
  
##  <a name="Boolean"></a> 8입니다. 조건부 표시에 대한 부울 매개 변수 추가  
  
#### <a name="to-add-a-boolean-parameter"></a>부울 매개 변수를 추가하려면  
  
1.  디자인 화면의 보고서 데이터 창에서 **매개 변수**를 마우스 오른쪽 단추로 클릭한 다음 **매개 변수 추가**를 클릭합니다.  
  
2.  **이름**에 ShowSelections를 입력합니다.  
  
3.  **프롬프트**에 Show selections?를 입력합니다.  
  
4.  **데이터 형식**, 드롭 다운 목록에서 클릭 **부울**합니다.  
  
5.  **기본값**을 클릭합니다.  
  
6.  **값 지정**을 클릭한 다음 **추가**를 클릭합니다.  
  
7.  **값**에 **False**를 입력합니다.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-set-visibility-based-on-a-boolean-parameter"></a>부울 매개 변수에 따라 표시 유형을 설정하려면  
  
1.  디자인 화면에서 매개 변수 값이 표시되는 페이지 바닥글의 입력란을 마우스 오른쪽 단추로 클릭한 다음 **입력란 속성**을 클릭합니다.  
  
2.  **표시 유형**을 클릭합니다.  
  
3.  **식에 따라 표시 또는 숨기기**옵션을 선택한 다음 **Fx**식 단추를 클릭합니다.  
  
4.  다음 식을 입력합니다. `=Not Parameters!ShowSelections.Value`  
  
     입력란의 표시 유형 옵션은 Hidden 속성을 사용하여 제어됩니다. 매개 변수를 선택할 경우 Hidden 속성이 False이고 입력란이 표시되도록 `Not` 연산자를 적용합니다.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  보고서를 미리 봅니다.  
  
     매개 변수 선택 항목이 표시되는 입력란이 나타나지 않습니다.  
  
8.  보고서 뷰어 도구 모음에서 옆에 **Show selections**, 클릭 `True`합니다.  
  
9. 보고서를 미리 봅니다.  
  
 페이지 바닥글의 입력란에 선택한 모든 상점 이름이 표시됩니다.  
  
##  <a name="Title"></a> 9입니다. 보고서 제목 추가  
  
#### <a name="to-add-a-report-title"></a>보고서 제목을 추가하려면  
  
1.  디자인 화면에서 **제목을 추가하려면 클릭하십시오.** 를 클릭합니다.  
  
2.  Parameterized Product Sales를 입력한 다음 입력란 바깥쪽을 클릭합니다.  
  
##  <a name="Save"></a> 10입니다. 보고서 저장  
  
#### <a name="to-save-the-report-on-a-report-server"></a>보고서를 보고서 서버에 저장하려면  
  
1.  **보고서 작성기** 단추에서 **다른 이름으로 저장**을 클릭합니다.  
  
2.  **최근에 사용한 사이트 및 서버**를 클릭합니다.  
  
3.  보고서를 저장할 수 있는 권한을 가진 보고서 서버의 이름을 선택하거나 입력합니다.  
  
     **보고서 서버에 연결하는 중**이라는 메시지가 나타납니다. 연결되면 보고서 서버 관리자가 보고서의 기본 위치로 지정한 보고서 폴더의 내용이 표시됩니다.  
  
4.  **이름**에서 기본 이름을 Parameterized Sales Report로 바꿉니다.  
  
5.  **저장**을 클릭합니다.  
  
 보고서가 보고서 서버에 저장됩니다. 연결된 보고서 서버는 창 아래쪽에 있는 상태 표시줄에 나타납니다.  
  
## <a name="next-steps"></a>다음 단계  
 보고서에 매개 변수를 추가하는 방법에 대한 연습을 완료했습니다. 매개 변수에 대한 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](report-design/report-parameters-report-builder-and-report-designer.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [자습서 &#40;보고서 작성기&#41;](report-builder-tutorials.md)   
 [SQL Server 2014의 보고서 작성기](report-builder/report-builder-in-sql-server-2016.md)  
  
  