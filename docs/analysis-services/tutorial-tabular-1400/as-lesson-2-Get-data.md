---
title: 'Analysis Services 자습서 2 단원: 데이터 가져오기 | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9adeebfbd3c49761adb816a7d28472a61ffca5cc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="get-data"></a>데이터 가져오기

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는 사용 하 여 **데이터 가져오기** AdventureWorksDW 예제 데이터베이스에 연결할 데이터, 미리 보기 및 필터를 선택 하 고 다음 모델 작업 영역으로 가져옵니다.  
  
가져올 데이터를 사용 하 여 다양 한 원본에서에서 데이터를 가져올 수 있습니다. 파워 쿼리 M 수식 식을 사용 하 여 데이터를 쿼리할 수 있습니다 또는 [네이티브 SQL 쿼리 식](../tabular-models/ssas-import-query.md)합니다.

> [!NOTE]
> 작업 및 이미지가이 자습서에서는 온-프레미스 서버에서 AdventureWorksDW2014 데이터베이스에 연결 하려면 표시 됩니다. 경우에 따라 Azure SQL 데이터 웨어하우스에 대 한 AdventureWorksDW 데이터베이스에는 서로 다른 개체 이면 표시할 수 있습니다. 그러나 서로 근본적으로 동일 합니다.
  
이 단원에 소요되는 예상 시간: **10분**  
  
## <a name="prerequisites"></a>필수 구성 요소  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [1 단원: 새 테이블 형식 모델 프로젝트 만들기](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)합니다.  
  
## <a name="create-a-connection"></a>연결 만들기  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw-database"></a>AdventureWorksDW 데이터베이스에 연결을 만들려면  
  
1.  **테이블 형식 모델 탐색기**를 마우스 오른쪽 단추로 클릭 **데이터 원본** > **데이터 원본에서 가져오기**합니다.  
  
    그러면 **데이터 가져오기**를 안내 하는 데이터 원본에 연결 합니다. 테이블 형식 모델 탐색기에 표시 되지 않는 경우 **솔루션 탐색기**를 두 번 클릭 **Model.bim** 를 모델 디자이너에서 엽니다. 
    
    ![as-lesson2-getdata](../tutorial-tabular-1400/media/as-lesson2-getdata.png)
  
2.  데이터 가져오기에서 클릭 **데이터베이스** > **SQL Server 데이터베이스** > **연결**합니다.  
  
3.  에 **SQL Server 데이터베이스** 대화에 **서버**AdventureWorksDW 데이터베이스를 설치한 서버의 이름을 입력 한 다음 클릭 **연결**합니다.  

4.  를 자격 증명을 입력 하 라는 메시지가 가져오고 데이터를 처리할 때 데이터 원본에 연결 하는 데 사용 하 여 Analysis Services 자격 증명을 지정 해야 합니다. **가장 모드**선택, **가장 계정**, 다음 자격 증명을 입력 하 고 클릭 **연결**합니다. 계정을 사용 하면 암호 만료 되지 않는 것이 좋습니다.

    ![as-lesson2-account](../tutorial-tabular-1400/media/as-lesson2-account.png)
  
    > [!NOTE]  
    > Windows 사용자 계정과 암호를 사용하면 데이터 원본에 가장 안전하게 연결할 수 있습니다.
  
5.  탐색 창의 선택 된 **AdventureWorksDW** 데이터베이스를 선택한 다음 클릭 **확인**합니다. 이 데이터베이스에 연결을 만듭니다. 
  
6.  탐색 창에서 다음 테이블에 대 한 확인란을 선택: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, 및 **FactInternetSales**합니다.  

    ![as-lesson2-select-tables](../tutorial-tabular-1400/media/as-lesson2-select-tables.png)
  
확인을 클릭 한 후 쿼리 편집기가 열립니다. 다음 섹션에서 가져올 데이터에만 선택할 수 있습니다.

  
## <a name="filter-the-table-data"></a>테이블 데이터 필터링  

AdventureWorksDW 예제 데이터베이스의 테이블에는 모델에 포함할 필요가 없는 데이터를 가집니다. 가능 하면 모델에 사용 되는 메모리 내 공간 절약을 위해 불필요 한 데이터를 필터링 하려고 합니다. 하지 가져온 작업 영역 데이터베이스 또는 model 데이터베이스에 배포 된 후 되므로 일부 테이블의 열을에서 필터링 합니다. 
  
#### <a name="to-filter-the-table-data-before-importing"></a>가져오기 전에 테이블 데이터를 필터링 하려면  
  
1.  쿼리 편집기에서 선택 된 **DimCustomer** 테이블입니다. 데이터 원본 (AdventureWorksDW 예제 데이터베이스)에서 DimCustomer 테이블 보기가 나타납니다. 
  
2.  다중 선택 (Ctrl + 클릭) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**를 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **열 제거**합니다. 

    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-columns.png)
  
    이러한 열의 값은 인터넷 매출 분석과 관련이 없으므로 가져올 필요가 없습니다. 보다 작고 효율적인 모델을 사용 하면 불필요 한 열을 제거 합니다.  

    > [!TIP]
    > 단계를 삭제 하 여 백업할 수를 실수 하는 경우 **적용 된 단계**합니다.   
    
    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-step.png)

  
4.  각 테이블에는 다음과 같은 열을 제거 하 여 나머지 테이블을 필터링 합니다.  
    
    **DimDate**
    
      |열|  
      |--------|  
      |**DateKey**|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |열|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |열|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |열|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |열|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      제거 된 열이 없습니다.
  
## <a name="Import"></a>Import the selected tables and column data  

미리 보기 하 고 불필요 한 데이터를 필터링 했으므로 나머지 않을 데이터를 가져올 수 있습니다. 마법사에서는 테이블 데이터와 함께 테이블 간 관계를 가져옵니다. 필터링 하는 데이터를 가져올 수는 및 모델에 새 테이블 및 열 만들어집니다.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>선택한 테이블 및 열 데이터를 가져오려면  
  
1.  선택 항목을 검토합니다. 잘못 된 항목이 없으면, 클릭 **가져오기**합니다. 데이터 처리 대화 상자를 작업 영역 데이터베이스에 사용자 데이터 원본에서 가져올 데이터의 상태를 표시 합니다.
  
    ![as-lesson2-success](../tutorial-tabular-1400/media/as-lesson2-success.png) 
  
2.  **닫기**를 클릭합니다.  

  
## <a name="save-your-model-project"></a>모델 프로젝트를 저장 합니다.  

모델 프로젝트를 자주 저장 하는 것이 유용 합니다.  
  
#### <a name="to-save-the-model-project"></a>모델 프로젝트를 저장하려면  
  
-   Click **파일** > **모두 저장**을 참조하세요.  
  
## <a name="whats-next"></a>다음 단계

[3 단원: 날짜 테이블로 표시](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)합니다.

  
  
