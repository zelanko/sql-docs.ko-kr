---
title: '2 단원: 데이터 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 13c3a8cc-b1db-4aba-ad9b-038b7971be8d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9e18298e152089f361faa839228415909133663f
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543455"
---
# <a name="lesson-2-add-data"></a>2단원: 데이터 추가
  이 섹션에서는 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 의 테이블 가져오기 마법사를 사용하여 AdventureWorksDW SQL Database에 연결하고, 데이터를 선택하고, 미리 보고 필터링한 다음 해당 데이터를 모델 작업 영역으로 가져옵니다.  
  
 테이블 가져오기 마법사를 사용하여 Access, SQL, Oracle, Sybase, Informix, DB2, Teradata 등 다양한 관계형 원본에서 데이터를 가져올 수 있습니다. 이러한 각 관계형 원본에서 데이터를 가져오는 단계는 아래에 설명된 과정과 매우 비슷합니다. 또한 저장 프로시저를 사용하여 데이터를 선택할 수 있습니다.  
  
 데이터를 가져오는 방법 및 데이터를 가져올 수 있는 다양한 종류의 데이터 원본에 대한 자세한 내용은 [데이터 원본&#40;SSAS 테이블 형식&#41;](data-sources-ssas-tabular.md)을 참조하세요.  
  
 이 단원을 완료하기 위한 예상 시간: **20분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원의 작업을 수행 하기 전에 이전 단원인 [1 단원: 새 테이블 형식 모델 프로젝트 만들기](lesson-1-create-a-new-tabular-model-project.md)를 완료 해야 합니다.  
  
## <a name="create-a-connection"></a>연결 만들기  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2012-database"></a>AdventureWorksDW2012 데이터베이스에 대한 연결을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **데이터 원본에서 가져오기**를 클릭합니다.  
  
     그러면 데이터 원본에 대한 연결을 설정하는 과정을 안내하는 테이블 가져오기 마법사가 시작됩니다. **데이터 원본에서 가져오기** 가 회색으로 나타나면 **솔루션 탐색기** 에서 **Model.bim** 을 두 번 클릭하여 디자이너에서 모델을 엽니다.  
  
2.  **테이블 가져오기 마법사**의 **관계형 데이터베이스**에서 **Microsoft SQL Server**를 클릭한 후 **다음**을 클릭합니다.  
  
3.  **Microsoft SQL Server 데이터베이스에 연결** 페이지의 **연결 이름**에을 입력 `Adventure Works DB from SQL` 합니다.  
  
4.  **서버 이름**에 AdventureWorksDW 데이터베이스가 설치되어 있는 서버의 이름을 입력합니다.  
  
5.  **데이터베이스 이름** 필드에서 아래쪽 화살표를 클릭하고 **AdventureWorksDW**를 선택한 후 **다음**을 클릭합니다.  
  
6.  **가장 정보** 페이지에서 데이터를 가져와 처리할 때 Analysis Services가 데이터 원본에 연결하는 데 사용할 자격 증명을 지정해야 합니다. **특정 Windows 사용자 이름 및 암호** 가 선택되어 있는지 확인하고 **사용자 이름** 및 **암호**에 Windows 로그온 자격 증명을 입력한 후 **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  Windows 사용자 계정과 암호를 사용하면 데이터 원본에 가장 안전하게 연결할 수 있습니다. 자세한 내용은 [가장&#40;SSAS 테이블 형식&#41;](tabular-models/impersonation-ssas-tabular.md)을 참조하세요.  
  
7.  **데이터를 가져오는 방법 선택** 페이지에서 **데이터를 가져올 테이블 및 뷰를 목록에서 선택** 이 선택되어 있는지 확인합니다. **다음** 을 클릭하여 원본 데이터베이스에 있는 모든 원본 테이블 목록을 표시할 수 있도록 테이블 및 뷰를 목록에서 선택하려고 합니다.  
  
8.  **테이블 및 뷰 선택** 페이지에서 **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**및 **FactInternetSales**테이블의 확인란을 선택합니다.  
  
9. 모델의 테이블에 알아보기 쉬운 이름을 지정하려고 합니다. **DimCustomer** 의 **이름**열에서 셀을 클릭합니다. 나이 고객에서 "Dim"을 제거 하 여 테이블의 이름을 바꿉니다.  
  
10. 다른 테이블의 이름을 바꿉니다.  
  
    |원본 이름|친숙한 이름|  
    |-----------------|-------------------|  
    |FactOnlineSales|날짜|  
    |DimGeography|Geography|  
    |DimProduct|Product|  
    |DimProductCategory|제품 범주|  
    |DimProductSubcategory|Product Subcategory|  
    |FactInternetSales|Internet Sales|  
  
     **마침** 을 클릭하지 **마십시오**.  
  
 데이터베이스에 연결하여 가져올 테이블을 선택하고 테이블에 이름을 지정했으므로 다음 섹션인 [가져오기 전에 테이블 데이터 필터링](#FilterData)으로 이동합니다.  
  
##  <a name="filter-the-table-data"></a><a name="FilterData"></a>테이블 데이터 필터링  
 데이터베이스에서 가져온 DimCustomer 테이블에는 원래 SQL Server Adventure Works 데이터베이스의 데이터 하위 집합이 포함되어 있습니다. 필요 하지 않은 행 중 일부는 행 필터를 사용할 수 없습니다. 가능하면 모델에 사용되는 메모리 내 공간을 절약하기 위해 사용하지 않을 데이터는 필터링하려고 합니다.  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>가져오기 전에 테이블 데이터를 필터링하려면  
  
1.  **Customer** 테이블에 대한 행을 선택하고 **미리 보기 및 필터**를 클릭합니다. DimCustomer 원본 테이블의 모든 열이 표시된 상태로 **선택한 테이블 미리 보기** 창이 열립니다.  
  
2.  다음 열의 맨 위에 있는 확인란의 선택을 취소합니다.  
  
    |Customer|  
    |--------------|  
    |**SpanishEducation**|  
    |**FrenchEducation**|  
    |**SpanishOccupation**|  
    |**FrenchOccupation**|  
  
     이러한 열의 값은 인터넷 매출 분석과 관련이 없으므로 가져올 필요가 없습니다. 필요 없는 열을 제거하면 모델의 크기가 작아집니다.  
  
3.  이외의 다른 열이 모두 선택되어 있는지 확인하고 **확인**을 클릭합니다.  
  
     이제 적용 된 **필터** 라는 단어가 **Customer** 행의 **필터 세부 정보** 열에 표시 되는지 확인 합니다. 이 링크를 클릭 하면 방금 적용 한 필터에 대 한 텍스트 설명이 표시 됩니다.  
  
4.  나머지 각 테이블에서 다음 열에 대한 확인란의 선택을 취소하여 테이블을 필터링합니다.  
  
    |날짜|  
    |----------|  
    |**DateKey**|  
    |**SpanishDayNameOfWeek**|  
    |**FrenchDayNameOfWeek**|  
    |**SpanishMonthName**|  
    |**FrenchMonthName**|  
  
    |Geography|  
    |---------------|  
    |**SpanishCountryRegionName**|  
    |**FrenchCountryRegionName**|  
    |**IpAddressLocator**|  
  
    |Product|  
    |-------------|  
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
  
    |제품 범주|  
    |----------------------|  
    |**SpanishProductCategoryName**|  
    |**FrenchProductCategoryName**|  
  
    |Product Subcategory|  
    |-------------------------|  
    |**SpanishProductSubcategoryName**|  
    |**FrenchProductSubcategoryName**|  
  
    |Internet Sales|  
    |--------------------|  
    |**OrderDateKey**|  
    |**DueDateKey**|  
    |**ShipDateKey**|  
  
 데이터를 미리 보고 필요 없는 데이터를 필터링했으므로 이제 데이터를 가져올 수 있습니다. 다음 섹션인 **선택한 테이블 및 열 데이터 가져오기**로 이동합니다.  
  
##  <a name="import-the-selected-tables-and-column-data"></a><a name="Import"></a>선택한 테이블 및 열 데이터 가져오기  
 이제 선택한 데이터를 가져올 수 있습니다. 마법사에서는 테이블 데이터와 함께 테이블 간 관계를 가져옵니다. 앞에서 지정한 이름의 새 테이블과 열이 모델에 생성되고 필터링한 데이터는 가져오지 않습니다.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>선택한 테이블 및 열 데이터를 가져오려면  
  
1.  선택 항목을 검토합니다. 잘못된 항목이 없으면 **마침**을 클릭합니다.  
  
     데이터를 가져오는 동안 인출된 행의 수가 마법사에 표시됩니다. 데이터를 모두 가져오면 성공을 나타내는 메시지가 표시됩니다.  
  
    > [!TIP]  
    >   가져온 테이블 간에 자동으로 생성된 관계를 보려면 **데이터 준비** 행에서 **자세히**를 클릭합니다.  
  
2.  **닫기**를 클릭합니다.  
  
     마법사가 닫히고 모델 디자이너가 표시됩니다. 각 테이블이 모델 디자이너에 새 테이블로 추가되어 있습니다.  
  
## <a name="save-the-model-project"></a>모델 프로젝트를 저장합니다.  
 모델 프로젝트를 자주 저장하도록 해야 합니다.  
  
#### <a name="to-save-the-model-project"></a>모델 프로젝트를 저장하려면  
  
-   [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **파일** 메뉴를 클릭한 다음 **모두 저장**을 클릭합니다.  
  
## <a name="next-step"></a>다음 단계  
 이 자습서를 계속하려면 다음 단원인 [3단원: 열 이름 바꾸기](rename-columns.md)로 이동하세요.  
  
  
