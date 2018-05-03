---
title: '2 단원: 데이터 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 06/19/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 13c3a8cc-b1db-4aba-ad9b-038b7971be8d
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5976c7113de52fa34611d0809f525ddd74c1a861
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-2-add-data"></a>2단원: 데이터 추가
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

이 단원에서는 SSDT 테이블 가져오기 마법사를 사용 하 여 AdventureWorksDW SQL 샘플 데이터베이스에 연결, 데이터 선택, 미리 보기 및 데이터를 필터링 및 다음의 모델 작업 영역에 데이터를 가져와야 하 합니다.  
  
테이블 가져오기 마법사를 사용하여 Access, SQL, Oracle, Sybase, Informix, DB2, Teradata 등 다양한 관계형 원본에서 데이터를 가져올 수 있습니다. 이러한 각 관계형 원본에서 데이터를 가져오는 단계는 아래에 설명된 과정과 매우 비슷합니다. 또한 저장된 프로시저를 사용 하 여 데이터를 선택할 수 있습니다. 데이터를 다양 한 유형의 데이터 원본에서 가져올 수 가져오기에 대 한 자세한 참조 [데이터 소스](../analysis-services/tabular-models/data-sources-ssas-tabular.md)합니다.  
  
이 단원에 소요되는 예상 시간: **20분**  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행하려면 이전 단원인 [1단원: 새 테이블 형식 모델 프로젝트를 만들기](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)를 완료해야 합니다.  
  
## <a name="create-a-connection"></a>연결 만들기  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2014-database"></a>에 대 한 연결을 만들려면 한 AdventureWorksDW2014 데이터베이스  
  
1.  테이블 형식 모델 탐색기에서 마우스 오른쪽 단추로 클릭 **데이터 원본** > **데이터 원본에서 가져오기**합니다.  
  
    데이터 원본에 대 한 연결을 설정 하는 과정을 안내 하는 테이블 가져오기 마법사가 시작 됩니다. 테이블 형식 모델 탐색기가 보이지 않으면 두 번 클릭 **Model.bim** 에 **솔루션 탐색기** 를 모델 디자이너에서 엽니다. 
    
    ![로-테이블 형식-2 단원-시간이](../analysis-services/media/as-tabular-lesson2-tme.png) 

    참고: 1400 호환성 수준에서 모델을 만들려는 경우 테이블 가져오기 마법사는 대신 새로운 데이터 가져오기 환경을 표시 됩니다. 대화 상자, 다음 단계는 약간 다릅니다 나타나지만 여전히 함께 진행할 수 있습니다. 
  
2.  테이블 가져오기 마법사에서 아래 **관계형 데이터베이스**, 클릭 **Microsoft SQL Server** > **다음**합니다.  
  
3.  **Microsoft SQL Server 데이터베이스에 연결** 페이지의 **연결 이름**에 **Adventure Works DB from SQL**을 입력합니다.  
  
4.  **서버 이름**를 AdventureWorksDW 데이터베이스를 설치한 서버의 이름을 입력 합니다.  
  
5.  에 **데이터베이스 이름** 필드를 선택한 **AdventureWorksDW**, 클릭 하 고 **다음**합니다.  
  
    ![로-테이블 형식-2 단원-tiw-이름](../analysis-services/media/as-tabular-lesson2-tiw-name.png)
  
6.  **가장 정보** 페이지에서 데이터를 가져와 처리할 때 Analysis Services가 데이터 원본에 연결하는 데 사용할 자격 증명을 지정해야 합니다. **특정 Windows 사용자 이름 및 암호** 가 선택되어 있는지 확인하고 **사용자 이름** 및 **암호**에 Windows 로그온 자격 증명을 입력한 후 **다음**을 클릭합니다.  
  
    > [!NOTE]  
    > Windows 사용자 계정과 암호를 사용하면 데이터 원본에 가장 안전하게 연결할 수 있습니다. 자세한 내용은 참조 [가장](../analysis-services/tabular-models/impersonation-ssas-tabular.md)합니다.  
  
7.  **데이터를 가져오는 방법 선택** 페이지에서 **데이터를 가져올 테이블 및 뷰를 목록에서 선택** 이 선택되어 있는지 확인합니다. **다음** 을 클릭하여 원본 데이터베이스에 있는 모든 원본 테이블 목록을 표시할 수 있도록 테이블 및 뷰를 목록에서 선택하려고 합니다.  
  
8.  **테이블 및 뷰 선택** 페이지에서 **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**및 **FactInternetSales**테이블의 확인란을 선택합니다.  
  
    **마침** 을 클릭하지 **마십시오**.  
  
## <a name="FilterData"></a>Filter the table data  
가져오는 샘플 데이터베이스에서 DimCustomer 테이블은 원본 SQL Server Adventure Works 데이터베이스의 데이터 하위 집합을 포함 합니다. 좀 더를 모델로 가져올 때 필요 하지 않은 DimCustomer 테이블에서 열을 필터링 합니다. 가능 하면 모델에서 사용 하는 메모리에 공간을 절약할 수는 사용 되지 않게 하는 데이터를 필터링 합니다.  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>가져오기 전에 테이블 데이터를 필터링하려면  
  
1.  행을 선택 하 고 **DimCustomer** 테이블을 마우스 클릭 **미리 보기 및 필터**합니다. DimCustomer 원본 테이블의 모든 열이 표시된 상태로 **선택한 테이블 미리 보기** 창이 열립니다.  
  
2.  다음 열의 맨 위에 있는 확인란의 선택을 취소합니다. **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**을 참조하세요. 

    ![로-테이블 형식-2 단원-tiw-일반](../analysis-services/media/as-tabular-lesson2-tiw-clear.png)
  
    이러한 열의 값은 인터넷 매출 분석과 관련이 없으므로 가져올 필요가 없습니다. 불필요 한 열을 제거 하면 모델 보다 작고 효율적인 있습니다.  
  
3.  이외의 다른 열이 모두 선택되어 있는지 확인하고 **확인**을 클릭합니다.  
  
    라는 단어가 **적용 된 필터** 에 표시 됩니다는 **필터 세부 정보** 열에는 **DimCustomer** 행; 클릭 하면 해당 링크의 텍스트 설명이 표시 됩니다는 방금 적용 필터입니다.  
    
    ![로-테이블 형식-2 단원-적용 된-필터](../analysis-services/media/as-tabular-lesson2-applied-filters.png)
    
  
4.  나머지 각 테이블에서 다음 열에 대한 확인란의 선택을 취소하여 테이블을 필터링합니다.  
    
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
  
      |열|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Import the selected tables and column data  
미리 보기 하 고 불필요 한 데이터를 필터링 했으므로 나머지 않을 데이터를 가져올 수 있습니다. 마법사에서는 테이블 데이터와 함께 테이블 간 관계를 가져옵니다. 새 테이블 및 열에 모델 만들어지며 필터링 하는 데이터를 가져올 수 없습니다.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>선택한 테이블 및 열 데이터를 가져오려면  
  
1.  선택 항목을 검토합니다. 잘못 된 항목이 없으면, 클릭 **마침**합니다.  
  
    데이터를 가져오는 동안 인출된 행의 수가 마법사에 표시됩니다. 데이터를 모두 가져오면 성공을 나타내는 메시지가 표시됩니다.  
    
    ![로-테이블 형식-2 단원-성공](../analysis-services/media/as-tabular-lesson2-success.png) 
  
    > [!TIP]  
    > 가져온 테이블 간에 자동으로 생성된 관계를 보려면 **데이터 준비** 행에서 **자세히**를 클릭합니다. 
  
2.  **닫기**를 클릭합니다.  
  
    마법사가 닫히고 모델 디자이너가 이제 가져온된 테이블을 표시 합니다. 
  
## <a name="save-your-model-project"></a>모델 프로젝트를 저장 합니다.  
모델 프로젝트를 자주 저장 하는 것이 유용 합니다.  
  
#### <a name="to-save-the-model-project"></a>모델 프로젝트를 저장하려면  
  
-   Click **파일** > **모두 저장**을 참조하세요.  
  
## <a name="whats-next"></a>다음 단계
다음 단원으로 이동: [3 단원: 날짜 테이블로 표시](../analysis-services/lesson-3-mark-as-date-table.md)합니다.

  
  
