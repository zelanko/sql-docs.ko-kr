---
title: 보고서에 연계 매개 변수 추가(보고서 작성기) | Microsoft Docs
description: 보고서 작성기의 보고서에서 연계 매개 변수를 사용하여 대량의 보고서 데이터를 관리하는 방법을 알아봅니다.
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 3a22eec3-57a7-478e-b6fc-102a9dbe0591
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fba193af6ef9f76c50f33ffa45a7bc668a0edead
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364665"
---
# <a name="add-cascading-parameters-to-a-report-report-builder-and-ssrs"></a>보고서에 연계 매개 변수 추가(보고서 작성기 및 SSRS)
  연계 매개 변수를 사용하면 대량의 보고서 데이터를 관리할 수 있습니다. 한 매개 변수의 값 목록이 다른 매개 변수에서 선택한 값에 따라 달라지는 관련 매개 변수 집합을 정의할 수 있습니다. 예를 들어 첫 번째 매개 변수가 제품 범주 목록을 나타내는 독립적인 매개 변수이고 사용자가 범주를 선택하면 두 번째 매개 변수가 첫 번째 매개 변수의 값에 종속됩니다. 즉, 두 번째 매개 변수의 값이 선택된 범위 내 하위 범주의 목록으로 업데이트됩니다. 사용자가 보고서를 볼 때 범주 및 하위 범주 매개 변수 모두에 대한 값으로 보고서 데이터가 필터링됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 연계 매개 변수를 만들려면 먼저 데이터 세트 쿼리를 정의하고 필요한 각 연계 매개 변수에 대한 쿼리 매개 변수를 추가합니다. 또한 각 연계 매개 변수마다 별도의 데이터 세트를 만들어 사용 가능한 값을 제공해야 합니다. 자세한 내용은 [보고서 매개 변수의 사용 가능한 값 추가, 변경 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md)를 참조하세요.  
  
 목록 뒷부분의 매개 변수에 대한 데이터 세트 쿼리에는 목록 앞부분의 각 매개 변수에 대한 참조가 포함되므로 연계 매개 변수에서는 순서가 중요합니다. 보고서 데이터 창의 매개 변수 순서에 따라 런타임에 보고서에 매개 변수 쿼리가 나타나는 순서가 결정되며 따라서 사용자가 각각의 연속된 매개 변수 값을 선택하는 순서가 결정됩니다.  
  
 여러 값을 갖는 연계 매개 변수를 만들고 모두 선택 기능을 포함하는 방법은 [모두 선택 다중값 연계 매개 변수를 만드는 방법](https://go.microsoft.com/fwlink/?LinkId=184757)을 참조하십시오.  
  
## <a name="to-create-the-main-dataset-with-a-query-that-includes-multiple-related-parameters"></a>관련된 여러 매개 변수가 포함된 쿼리가 있는 기본 데이터 세트를 만들려면  
  
1.  보고서 데이터 창에서 데이터 원본을 마우스 오른쪽 단추로 클릭한 다음, **데이터 세트 추가** 를 클릭합니다.  
  
2.  **이름** 에 데이터 세트의 이름을 입력합니다.  
  
3.  **데이터 원본** 에서 데이터 원본의 이름을 선택하거나 **새로 만들기** 를 클릭하여 데이터 원본을 새로 만듭니다.  
  
4.  **쿼리 유형** 에서 선택된 데이터 원본에 대한 쿼리 유형을 선택합니다. 이 항목에서는 **텍스트** 쿼리 유형을 사용합니다.  
  
5.  **쿼리** 에서 이 보고서의 데이터를 검색하는 데 사용할 쿼리를 입력합니다. 쿼리에는 다음 부분이 포함되어야 합니다.  
  
    1.  데이터 원본 필드의 목록. 예를 들어 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 SELECT 문은 해당 테이블 또는 뷰의 데이터베이스 열 이름 목록을 지정합니다.  
  
    2.  각 연계 매개 변수당 하나의 쿼리 매개 변수. 쿼리 매개 변수는 쿼리에서 포함하거나 제외할 값을 지정하여 데이터 원본에서 검색되는 데이터를 제한합니다. 일반적으로 쿼리 매개 변수는 쿼리의 제약 조건 절에 넣습니다. 예를 들어 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 문에서는 WHERE 절에 쿼리 매개 변수를 넣습니다.  
  
6.  **실행** ( **!** )을 클릭합니다. 쿼리 매개 변수를 넣은 다음 쿼리를 실행하면 쿼리 매개 변수에 해당하는 보고서 매개 변수가 자동으로 생성됩니다.  
  
    > [!NOTE]  
    >  처음 쿼리를 실행할 때 쿼리 매개 변수의 순서에 따라 보고서에서 매개 변수가 생성되는 순서가 결정됩니다. 순서를 변경하려면 [보고서 매개 변수의 순서 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)을 참조하세요.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 다음으로는 독립 매개 변수에 대한 값을 제공하는 데이터 세트를 만듭니다.  
  
## <a name="to-create-a-dataset-to-provide-values-for-an-independent-parameter"></a>독립 매개 변수에 대한 값을 제공하는 데이터 세트를 만들려면  
  
1.  보고서 데이터 창에서 데이터 원본을 마우스 오른쪽 단추로 클릭한 다음, **데이터 세트 추가** 를 클릭합니다.  
  
2.  **이름** 에 데이터 세트의 이름을 입력합니다.  
  
3.  **데이터 원본** 에서 이름이 1단계에서 선택한 데이터 원본의 이름인지 확인합니다.  
  
4.  **쿼리 유형** 에서 선택된 데이터 원본에 대한 쿼리 유형을 선택합니다. 이 항목에서는 **텍스트** 쿼리 유형을 사용합니다.  
  
5.  **쿼리** 에서 이 매개 변수에 대한 값을 검색하는 데 사용할 쿼리를 입력합니다. 독립 매개 변수에 대한 쿼리에는 일반적으로 쿼리 매개 변수가 포함되지 않습니다. 예를 들어 모든 범주 값을 제공하는 매개 변수에 대한 쿼리를 만들려면 다음과 비슷한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용할 수 있습니다.  
  
    ```  
    SELECT DISTINCT <column name> FROM <table>  
    ```  
  
     SELECT DISTINCT 명령은 지정된 테이블의 지정된 열에서 각각의 고유값을 가져올 수 있도록 결과 집합에서 중복 값을 제거합니다.  
  
     **실행** ( **!** )을 클릭합니다. 결과 집합은 이 첫 번째 매개 변수에 사용 가능한 값을 표시합니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 다음으로는 이 데이터 세트를 사용하여 런타임에 사용 가능한 값을 채우는 첫 번째 매개 변수의 속성을 설정합니다.  
  
## <a name="to-set-available-values-for-a-report-parameter"></a>보고서 매개 변수에 사용 가능한 값을 설정하려면  
  
1.  보고서 데이터 창의 매개 변수 폴더에서 첫 번째 매개 변수를 마우스 오른쪽 단추로 클릭한 다음 **매개 변수 속성** 을 클릭합니다.  
  
2.  **이름** 에서 매개 변수 이름이 올바른지 확인합니다.  
  
3.  **사용 가능한 값** 을 클릭합니다.  
  
4.  **쿼리에서 값 가져오기** 를 클릭합니다. 세 개의 필드가 나타납니다.  
  
5.  **데이터 세트** 의 드롭다운 목록에서, 이전 절차에서 만든 데이터 세트의 이름을 클릭합니다.  
  
6.  **값** 필드에서 매개 변수 값을 제공하는 필드의 이름을 클릭합니다.  
  
7.  **레이블** 필드에서 매개 변수 레이블을 제공하는 필드의 이름을 클릭합니다.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 다음으로, 종속 매개 변수의 값을 제공하는 데이터 세트를 만듭니다.  
  
## <a name="to-create-a-dataset-to-provide-values-for-a-dependent-parameter"></a>종속 매개 변수의 값을 제공하는 데이터 세트를 만들려면  
  
1.  보고서 데이터 창에서 데이터 원본을 마우스 오른쪽 단추로 클릭한 다음, **데이터 세트 추가** 를 클릭합니다.  
  
2.  **이름** 에 데이터 세트의 이름을 입력합니다.  
  
3.  **데이터 원본** 에서 이름이 1단계에서 선택한 데이터 원본의 이름인지 확인합니다.  
  
4.  **쿼리 유형** 에서 선택된 데이터 원본에 대한 쿼리 유형을 선택합니다. 이 항목에서는 **텍스트** 쿼리 유형을 사용합니다.  
  
5.  **쿼리** 에서 이 매개 변수에 대한 값을 검색하는 데 사용할 쿼리를 입력합니다. 종속 매개 변수에 대한 쿼리에는 일반적으로 이 매개 변수가 종속된 각 매개 변수에 대한 쿼리 매개 변수가 포함됩니다. 예를 들어 범주(독립 매개 변수)에 대해 모든 하위 범주(종속 매개 변수) 값을 제공하는 매개 변수에 대한 쿼리를 만들려면 다음과 비슷한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용할 수 있습니다.  
  
    ```  
    SELECT DISTINCT Subcategory FROM <table>   
    WHERE (Category = @Category)  
    ```  
  
     WHERE 절에서, Category는 \<table>의 필드 이름이며 @Category는 쿼리 매개 변수입니다. 이 문은 @Category에 지정된 범주에 대한 하위 범주의 목록을 생성합니다. 런타임에 이 값은 사용자가 동일한 이름의 보고서 매개 변수에 대해 선택한 값으로 채워집니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 그런 다음, 이 데이터 세트를 사용하여 런타임에 사용 가능한 값을 채우는 두 번째 매개 변수의 속성을 설정합니다.  
  
## <a name="to-set-available-values-for-the-second-parameter"></a>두 번째 매개 변수에 사용 가능한 값을 설정하려면  
  
1.  보고서 데이터 창의 매개 변수 폴더에서 첫 번째 매개 변수를 마우스 오른쪽 단추로 클릭한 다음 **매개 변수 속성** 을 클릭합니다.  
  
2.  **이름** 에서 매개 변수 이름이 올바른지 확인합니다.  
  
3.  **사용 가능한 값** 을 클릭합니다.  
  
4.  **쿼리에서 값 가져오기** 를 클릭합니다.  
  
5.  **데이터 세트** 의 드롭다운 목록에서, 이전 절차에서 만든 데이터 세트의 이름을 클릭합니다.  
  
6.  **값** 필드에서 매개 변수 값을 제공하는 필드의 이름을 클릭합니다.  
  
7.  **레이블** 필드에서 매개 변수 레이블을 제공하는 필드의 이름을 클릭합니다.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-test-the-cascading-parameters"></a>연계 매개 변수를 테스트하려면  
  
1.  **실행** 을 클릭합니다.  
  
2.  첫 번째 매개 변수인 독립 매개 변수의 드롭다운 목록에서 값을 선택합니다.  
  
     보고서 처리기가 다음 매개 변수에 대한 데이터 세트 쿼리를 실행하고 첫 번째 매개 변수에 선택한 값을 전달합니다. 두 번째 매개 변수의 드롭다운 목록이 첫 번째 매개 변수 값에 따라 선택된 사용 가능한 값으로 채워집니다.  
  
3.  두 번째 매개 변수인 종속 매개 변수의 드롭다운 목록에서 값을 선택합니다.  
  
     마지막 매개 변수를 선택한 뒤에는 사용자가 선택 사항을 변경할 수 있도록 보고서가 자동으로 실행되지 않습니다.  
  
4.  **보고서 보기** 를 클릭합니다. 선택한 매개 변수에 따라 보고서가 업데이트됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 매개 변수 추가, 변경 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [자습서: 보고서에 매개 변수 추가&#40;보고서 작성기&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [보고서 작성기 자습서](../../reporting-services/report-builder-tutorials.md)   
 [데이터 세트 필터, 데이터 영역 필터 및 그룹 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
