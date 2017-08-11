---
title: "(보고서 작성기 및 SSRS) 보고서에 연계 매개 변수를 추가 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3a22eec3-57a7-478e-b6fc-102a9dbe0591
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d8efc7a0b7120faa53a63bd07c51029a1b379f9e
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="add-cascading-parameters-to-a-report-report-builder-and-ssrs"></a>보고서에 연계 매개 변수 추가(보고서 작성기 및 SSRS)
  연계 매개 변수를 사용하면 대량의 보고서 데이터를 관리할 수 있습니다. 한 매개 변수의 값 목록이 다른 매개 변수에서 선택한 값에 따라 달라지는 관련 매개 변수 집합을 정의할 수 있습니다. 예를 들어 첫 번째 매개 변수가 제품 범주 목록을 나타내는 독립적인 매개 변수이고 사용자가 범주를 선택하면 두 번째 매개 변수가 첫 번째 매개 변수의 값에 종속됩니다. 즉, 두 번째 매개 변수의 값이 선택된 범위 내 하위 범주의 목록으로 업데이트됩니다. 사용자가 보고서를 볼 때 범주 및 하위 범주 매개 변수 모두에 대한 값으로 보고서 데이터가 필터링됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 연계 매개 변수를 만들려면 먼저 데이터 집합 쿼리를 정의하고 필요한 각 연계 매개 변수에 대한 쿼리 매개 변수를 추가합니다. 또한 각 연계 매개 변수마다 별도의 데이터 집합을 만들어 사용 가능한 값을 제공해야 합니다. 자세한 내용은 참조 [추가, 변경 또는 보고서 매개 변수 &#40;에 대 한 사용 가능한 값 삭제 보고서 작성기 및 SSRS &#41; ](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md).  
  
 목록 뒷부분의 매개 변수에 대한 데이터 집합 쿼리에는 목록 앞부분의 각 매개 변수에 대한 참조가 포함되므로 연계 매개 변수에서는 순서가 중요합니다. 보고서 데이터 창의 매개 변수 순서에 따라 런타임에 보고서에 매개 변수 쿼리가 나타나는 순서가 결정되며 따라서 사용자가 각각의 연속된 매개 변수 값을 선택하는 순서가 결정됩니다.  
  
 여러 값을 갖는 연계 매개 변수를 만들고 모두 선택 기능을 포함하는 방법은 [모두 선택 다중값 연계 매개 변수를 만드는 방법](http://go.microsoft.com/fwlink/?LinkId=184757)을 참조하십시오.  
  
## <a name="to-create-the-main-dataset-with-a-query-that-includes-multiple-related-parameters"></a>관련된 여러 매개 변수가 포함된 쿼리가 있는 기본 데이터 집합을 만들려면  
  
1.  보고서 데이터 창에서 데이터 원본을 마우스 오른쪽 단추로 클릭한 다음 **데이터 집합 추가**를 클릭합니다.  
  
2.  **이름**에 데이터 집합의 이름을 입력합니다.  
  
3.  **데이터 원본**에서 데이터 원본의 이름을 선택하거나 **새로 만들기** 를 클릭하여 데이터 원본을 새로 만듭니다.  
  
4.  **쿼리 유형**에서 선택된 데이터 원본에 대한 쿼리 유형을 선택합니다. 이 항목에서는 **텍스트** 쿼리 유형을 사용합니다.  
  
5.  **쿼리**에서 이 보고서의 데이터를 검색하는 데 사용할 쿼리를 입력합니다. 쿼리에는 다음 부분이 포함되어야 합니다.  
  
    1.  데이터 원본 필드의 목록. 예를 들어 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 SELECT 문은 해당 테이블 또는 뷰의 데이터베이스 열 이름 목록을 지정합니다.  
  
    2.  각 연계 매개 변수당 하나의 쿼리 매개 변수. 쿼리 매개 변수는 쿼리에서 포함하거나 제외할 값을 지정하여 데이터 원본에서 검색되는 데이터를 제한합니다. 일반적으로 쿼리 매개 변수는 쿼리의 제약 조건 절에 넣습니다. 예를 들어 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 문에서는 WHERE 절에 쿼리 매개 변수를 넣습니다. 자세한 내용은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SQL Server 온라인 설명서 [의](http://go.microsoft.com/fwlink/?linkid=120955)설명서에 있는 "WHERE 및 HAVING을 사용하여 행 필터링"을 참조하십시오.  
  
6.  **실행** (**!**)을 클릭합니다. 쿼리 매개 변수를 넣은 다음 쿼리를 실행하면 쿼리 매개 변수에 해당하는 보고서 매개 변수가 자동으로 생성됩니다.  
  
    > [!NOTE]  
    >  처음 쿼리를 실행할 때 쿼리 매개 변수의 순서에 따라 보고서에서 매개 변수가 생성되는 순서가 결정됩니다. 순서를 변경 하려면 참조 [보고서 매개 변수 &#40;의 순서를 변경 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 다음으로는 독립 매개 변수에 대한 값을 제공하는 데이터 집합을 만듭니다.  
  
## <a name="to-create-a-dataset-to-provide-values-for-an-independent-parameter"></a>독립 매개 변수에 대한 값을 제공하는 데이터 집합을 만들려면  
  
1.  보고서 데이터 창에서 데이터 원본을 마우스 오른쪽 단추로 클릭한 다음 **데이터 집합 추가**를 클릭합니다.  
  
2.  **이름**에 데이터 집합의 이름을 입력합니다.  
  
3.  **데이터 원본**에서 이름이 1단계에서 선택한 데이터 원본의 이름인지 확인합니다.  
  
4.  **쿼리 유형**에서 선택된 데이터 원본에 대한 쿼리 유형을 선택합니다. 이 항목에서는 **텍스트** 쿼리 유형을 사용합니다.  
  
5.  **쿼리**에서 이 매개 변수에 대한 값을 검색하는 데 사용할 쿼리를 입력합니다. 독립 매개 변수에 대한 쿼리에는 일반적으로 쿼리 매개 변수가 포함되지 않습니다. 예를 들어 모든 범주 값을 제공하는 매개 변수에 대한 쿼리를 만들려면 다음과 비슷한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용할 수 있습니다.  
  
    ```  
    SELECT DISTINCT <column name> FROM <table>  
    ```  
  
     SELECT DISTINCT 명령은 지정된 테이블의 지정된 열에서 각각의 고유값을 가져올 수 있도록 결과 집합에서 중복 값을 제거합니다.  
  
     **실행** (**!**)을 클릭합니다. 결과 집합은 이 첫 번째 매개 변수에 사용 가능한 값을 표시합니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 다음으로는 이 데이터 집합을 사용하여 런타임에 사용 가능한 값을 채우는 첫 번째 매개 변수의 속성을 설정합니다.  
  
## <a name="to-set-available-values-for-a-report-parameter"></a>보고서 매개 변수에 사용 가능한 값을 설정하려면  
  
1.  보고서 데이터 창의 매개 변수 폴더에서 첫 번째 매개 변수를 마우스 오른쪽 단추로 클릭한 다음 **매개 변수 속성**을 클릭합니다.  
  
2.  **이름**에서 매개 변수 이름이 올바른지 확인합니다.  
  
3.  **사용 가능한 값**을 클릭합니다.  
  
4.  **쿼리에서 값 가져오기**를 클릭합니다. 세 개의 필드가 나타납니다.  
  
5.  **데이터 집합**의 드롭다운 목록에서, 이전 절차에서 만든 데이터 집합의 이름을 클릭합니다.  
  
6.  **값** 필드에서 매개 변수 값을 제공하는 필드의 이름을 클릭합니다.  
  
7.  **레이블** 필드에서 매개 변수 레이블을 제공하는 필드의 이름을 클릭합니다.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 다음으로는 종속 매개 변수의 값을 제공하는 데이터 집합을 만듭니다.  
  
## <a name="to-create-a-dataset-to-provide-values-for-a-dependent-parameter"></a>종속 매개 변수의 값을 제공하는 데이터 집합을 만들려면  
  
1.  보고서 데이터 창에서 데이터 원본을 마우스 오른쪽 단추로 클릭한 다음 **데이터 집합 추가**를 클릭합니다.  
  
2.  **이름**에 데이터 집합의 이름을 입력합니다.  
  
3.  **데이터 원본**에서 이름이 1단계에서 선택한 데이터 원본의 이름인지 확인합니다.  
  
4.  **쿼리 유형**에서 선택된 데이터 원본에 대한 쿼리 유형을 선택합니다. 이 항목에서는 **텍스트** 쿼리 유형을 사용합니다.  
  
5.  **쿼리**에서 이 매개 변수에 대한 값을 검색하는 데 사용할 쿼리를 입력합니다. 종속 매개 변수에 대한 쿼리에는 일반적으로 이 매개 변수가 종속된 각 매개 변수에 대한 쿼리 매개 변수가 포함됩니다. 예를 들어 범주(독립 매개 변수)에 대해 모든 하위 범주(종속 매개 변수) 값을 제공하는 매개 변수에 대한 쿼리를 만들려면 다음과 비슷한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용할 수 있습니다.  
  
    ```  
    SELECT DISTINCT Subcategory FROM <table>   
    WHERE (Category = @Category)  
    ```  
  
     WHERE 절에 범주는에서 필드의 이름을 \<테이블 > 및 @Category 쿼리 매개 변수입니다. 이 문은에 지정 된 범주에 대 한 하위 범주의 목록을 생성 @Category합니다. 런타임에 이 값은 사용자가 동일한 이름의 보고서 매개 변수에 대해 선택한 값으로 채워집니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 다음으로는 이 데이터 집합을 사용하여 런타임에 사용 가능한 값을 채우는 두 번째 매개 변수의 속성을 설정합니다.  
  
## <a name="to-set-available-values-for-a-report-parameter"></a>보고서 매개 변수에 사용 가능한 값을 설정하려면  
  
1.  보고서 데이터 창의 매개 변수 폴더에서 첫 번째 매개 변수를 마우스 오른쪽 단추로 클릭한 다음 **매개 변수 속성**을 클릭합니다.  
  
2.  **이름**에서 매개 변수 이름이 올바른지 확인합니다.  
  
3.  **사용 가능한 값**을 클릭합니다.  
  
4.  **쿼리에서 값 가져오기**를 클릭합니다.  
  
5.  **데이터 집합**의 드롭다운 목록에서, 이전 절차에서 만든 데이터 집합의 이름을 클릭합니다.  
  
6.  **값** 필드에서 매개 변수 값을 제공하는 필드의 이름을 클릭합니다.  
  
7.  **레이블** 필드에서 매개 변수 레이블을 제공하는 필드의 이름을 클릭합니다.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-test-the-cascading-parameters"></a>연계 매개 변수를 테스트하려면  
  
1.  **실행**을 클릭합니다.  
  
2.  첫 번째 매개 변수인 독립 매개 변수의 드롭다운 목록에서 값을 선택합니다.  
  
     보고서 처리기가 다음 매개 변수에 대한 데이터 집합 쿼리를 실행하고 첫 번째 매개 변수에 선택한 값을 전달합니다. 두 번째 매개 변수의 드롭다운 목록이 첫 번째 매개 변수 값에 따라 선택된 사용 가능한 값으로 채워집니다.  
  
3.  두 번째 매개 변수인 종속 매개 변수의 드롭다운 목록에서 값을 선택합니다.  
  
     마지막 매개 변수를 선택한 뒤에는 사용자가 선택 사항을 변경할 수 있도록 보고서가 자동으로 실행되지 않습니다.  
  
4.  **보고서 보기**를 클릭합니다. 선택한 매개 변수에 따라 보고서가 업데이트됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 매개 변수 추가, 변경 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [보고서 매개 변수 사용 &#40; 보고서 작성기 및 보고서 디자이너 &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [자습서: 보고서 &#40; 매개 변수 추가 보고서 작성기 &#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [보고서 작성기 자습서](../../reporting-services/report-builder-tutorials.md)   
 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 &#40; 추가 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [보고서는 데이터 집합 및 공유 데이터 집합 &#40; 포함 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
