---
title: 'Analysis Services 자습서 단원 2: 데이터 가져오기 | Microsoft Docs'
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
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38007204"
---
# <a name="get-data"></a>데이터 가져오기

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서 사용 하 여 **데이터 가져오기** AdventureWorksDW 예제 데이터베이스에 연결할 데이터, 미리 보기 및 필터를 선택 하 고 다음 모델 작업 영역으로 가져옵니다.  
  
가져올 데이터를 사용 하 여 다양 한 원본에서에서 데이터를 가져올 수 있습니다. 파워 쿼리 M 수식을 사용 하 여 데이터를 쿼리할 수 있습니다 또는 [네이티브 SQL 쿼리 식](../tabular-models/ssas-import-query.md)합니다.

> [!NOTE]
> 이 자습서의 작업 및 이미지를 온-프레미스 서버에서 AdventureWorksDW2014 데이터베이스에 연결을 표시 합니다. 경우에 따라 Azure SQL Data Warehouse에 AdventureWorksDW 데이터베이스를 다른 개체 표시 될 수 있습니다. 그러나 이러한는 근본적으로 동일 합니다.
  
이 단원에 소요되는 예상 시간: **10분**  
  
## <a name="prerequisites"></a>사전 요구 사항  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [1 단원: 새 테이블 형식 모델 프로젝트를 만들](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)합니다.  
  
## <a name="create-a-connection"></a>연결 만들기  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw-database"></a>AdventureWorksDW 데이터베이스에 대 한 연결을 만들려면  
  
1.  **테이블 형식 모델 탐색기**를 마우스 오른쪽 단추로 클릭 **데이터 원본** > **데이터 원본에서 가져오기**합니다.  
  
    그러면 **데이터 가져오기**, 하는 과정을 안내 데이터 원본에 연결 합니다. 테이블 형식 모델 탐색기에 표시 되지 않으면 **솔루션 탐색기**를 두 번 클릭 **Model.bim** 를 모델 디자이너에서 엽니다. 
    
    ![as-lesson2-getdata](../tutorial-tabular-1400/media/as-lesson2-getdata.png)
  
2.  데이터 가져오기 **데이터베이스** > **SQL Server Database** > **Connect**합니다.  
  
3.  에 **SQL Server 데이터베이스** 대화 상자에서 **서버**AdventureWorksDW 데이터베이스를 설치한 서버의 이름을 입력 하 고 클릭 **연결**합니다.  

4.  자격 증명을 입력 하는 메시지가 표시 되 면 Analysis Services를 가져오고 데이터를 처리할 때 데이터 원본에 연결 하는 자격 증명을 지정 해야 합니다. **가장 모드**를 선택 **계정 가장**, 그런 다음 자격 증명을 입력 한 다음 클릭 **Connect**합니다. 암호 만료 되지 않습니다 여기서 계정을 사용 하는 것이 좋습니다.

    ![as-lesson2-account](../tutorial-tabular-1400/media/as-lesson2-account.png)
  
    > [!NOTE]  
    > Windows 사용자 계정과 암호를 사용하면 데이터 원본에 가장 안전하게 연결할 수 있습니다.
  
5.  탐색 창에서 선택 합니다 **AdventureWorksDW** 데이터베이스를 선택한 다음 클릭 **확인**합니다. 이 데이터베이스에 연결을 만듭니다. 
  
6.  탐색 창에서 다음 테이블에 대 한 확인란을 선택 합니다. **DimCustomer**, **DimDate**를 **DimGeography**, **DimProduct**,  **DimProductCategory**하십시오 **DimProductSubcategory**, 및 **FactInternetSales**합니다.  

    ![as-lesson2-select-tables](../tutorial-tabular-1400/media/as-lesson2-select-tables.png)
  
확인을 클릭 하면 쿼리 편집기가 열립니다. 다음 섹션에서 가져오려는 데이터만 선택 합니다.

  
## <a name="filter-the-table-data"></a>테이블 데이터 필터링  

AdventureWorksDW 예제 데이터베이스의 테이블에는 모델에 포함할 필요가 없는 데이터를 가집니다. 가능 하면 모델에 사용 되는 메모리 내 공간 절약을 위해 불필요 한 데이터를 필터링 하려고 합니다. 필터링 할 테이블의 열 중 일부는 가져오지 작업 영역 데이터베이스나 모델 데이터베이스에 배포한 후. 
  
#### <a name="to-filter-the-table-data-before-importing"></a>가져오기 전에 테이블 데이터를 필터링 하려면  
  
1.  쿼리 편집기에서 선택 합니다 **DimCustomer** 테이블입니다. 데이터 원본 (AdventureWorksDW 샘플 데이터베이스)에서 DimCustomer 테이블 뷰가 나타납니다. 
  
2.  다중 선택 (Ctrl + 클릭) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**하십시오 **FrenchOccupation**, 다음 마우스 오른쪽 단추를 클릭 **열 제거**합니다. 

    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-columns.png)
  
    이러한 열의 값은 인터넷 매출 분석과 관련이 없으므로 가져올 필요가 없습니다. 보다 작고 효율적인 모델을 사용 하면 불필요 한 열을 제거 합니다.  

    > [!TIP]
    > 실수를 하는 경우의 단계를 삭제 하 여 백업할 수 있습니다 **적용 된 단계**합니다.   
    
    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-step.png)

  
4.  각 테이블에는 다음 열을 제거 하 여 나머지 테이블을 필터링 합니다.  
    
    **DimDate**
    
      |Column|  
      |--------|  
      |**DateKey**|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |Column|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |Column|  
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
  
      |Column|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |Column|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      열을 제거 합니다.
  
## <a name="Import"></a>Import the selected tables and column data  

미리 보기를 했으므로 불필요 한 데이터를 필터링 했으므로 나머지 하려는 데이터를 가져올 수 있습니다. 마법사에서는 테이블 데이터와 함께 테이블 간 관계를 가져옵니다. 새 테이블 및 열을 모델에서 만든 및 필터링 하는 데이터를 가져오지 않습니다.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>선택한 테이블 및 열 데이터를 가져오려면  
  
1.  선택 항목을 검토합니다. 잘못 된 항목이 없으면, 클릭 **가져오기**합니다. 데이터 처리 대화 상자를 작업 영역 데이터베이스에 데이터 원본에서 가져올 데이터의 상태를 표시 합니다.
  
    ![as-lesson2-success](../tutorial-tabular-1400/media/as-lesson2-success.png) 
  
2.  **닫기**를 클릭합니다.  

  
## <a name="save-your-model-project"></a>모델 프로젝트를 저장 합니다.  

모델 프로젝트를 자주 저장 하는 것이 반드시 합니다.  
  
#### <a name="to-save-the-model-project"></a>모델 프로젝트를 저장하려면  
  
-   Click **파일** > **모두 저장**을 참조하세요.  
  
## <a name="whats-next"></a>다음 단계

[3 단원: 날짜 테이블로 표시](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)합니다.

  
  
