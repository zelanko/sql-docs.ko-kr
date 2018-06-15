---
title: 양방향 교차 필터 테이블 형식 모델에서 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 89c3aee1bb762a5725e3242c88284d07abdb8de7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044877"
---
# <a name="bi-directional-cross-filters-in-tabular-models"></a>테이블 형식 모델에서 양방향 교차 필터
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  SQL Server 2016의 새로운 기능에는 테이블 형식 모델에서 *양방향 교차 필터* 를 사용하는 기본 제공 접근 방식이 있습니다. 이 방식을 사용하면 테이블 관계에서 필터 컨텍스트를 전파하기 위한 수동 DAX 해결 방법이 필요 없습니다.  
  
 개념을 해당 구성 요소로 세분화해 보겠습니다. *교차 필터링* 은 관련 테이블의 값에 따라 테이블에 대한 필터 컨텍스트를 설정하는 기능이고, *양방향* 은 테이블 관계의 반대편에 있는 두 번째 관련 테이블로 필터 컨텍스트를 전달하는 것입니다. 이름에서 알 수 있듯이 한 방향이 아니라 관계의 양방향으로 분할할 수 있습니다.  내부적으로 양방향 필터링은 필터 컨텍스트를 확장하여 데이터의 상위 집합을 쿼리합니다.  
  
 ![SSAS-BIDI-1-Filteroption](../../analysis-services/tabular-models/media/ssas-bidi-1-filteroption.PNG "SSAS-BIDI-1-Filteroption")  
  
 두 가지가의 교차 필터: 단방향과 양방향 필터링 합니다. 단방향은 해당 관계에서 팩트 테이블과 차원 테이블 간의 기존 다 대 일 필터 방향입니다. 양방향은 두 관계 모두에 공통적인 하나의 테이블을 사용하여 하나의 관계에 대한 필터 컨텍스트를 다른 테이블 관계에 대한 필터 컨텍스트로 사용할 수 있도록 해주는 교차 필터입니다.  
  
 **FactOnlineSales** 에 대한 외래 키 관계가 있는 **DimDate** 및 **DimProduct**의 경우 양방향 교차 필터는 **FactOnlineSales-to-DimDate** 와 **FactOnlineSales-to-DimProduct** 를 동시에 사용하는 것과 같습니다.  
  
 양방향 교차 필터는 과거에 테이블 형식 개발자와 PowerPivot 개발자의 해결 과제였던 다 대 다 쿼리 디자인 문제를 손쉽게 해결할 수 있습니다. 테이블 형식 모델과 Powerpivot 모델의 다 대 다 관계에 대해 DAX 해결 방법을 사용한 경우 양방향 필터를 적용하여 예상된 결과가 생성되는지 확인할 수 있습니다.  
  
 양방향 교차 필터를 만들 때 다음 사항에 유의해야 합니다.  
  
-   양방향 필터를 사용하기 전에 검토가 필요합니다.  
  
     모든 위치에서 양방향 필터를 사용하는 경우 예상치 못한 방식으로 데이터가 과도하게 필터링될 수 있습니다.  또한 둘 이상의 잠재적 쿼리 경로를 만들어 의도치 않게 모호성을 발생시킬 수 있습니다. 이러한 문제를 모두 방지하려면 단방향 필터와 양방향 필터의 조합을 사용하도록 계획하세요.  
  
-   증분 테스트를 수행하여 각 필터 변경 내용이 모델에 미치는 영향을 확인합니다. [Excel에서 분석](../../analysis-services/tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md) 은 증분 테스트에 적합합니다. 하나의 모범 사례로, 다른 보고 클라이언트를 사용하여 정기적으로 테스트하는 것이 좋습니다.  
  
> [!NOTE]  
>  CTP 3.2부터 SSDT에는 양방향 교차 필터를 자동으로 시도할지 여부를 결정하는 기본값이 포함되어 있습니다. 기본적으로 양방향 필터를 사용하도록 설정한 경우 SSDT는 모델이 테이블 관계 체인을 통해 하나의 쿼리 경로를 명확히 나타내는 경우에만 양방향 필터링을 사용합니다.  
  
## <a name="set-the-default"></a>기본값 설정  
 단일 방향 필터가 기본값입니다. 디자이너에서 만든 모든 새 프로젝트 또는 모델 자체(프로젝트가 이미 있는 경우)에 대한 기본값을 변경할 수 있습니다.  
  
 프로젝트 수준에서는 프로젝트를 만들 때 설정이 평가되므로 기본값을 양방향으로 변경하면 다음 프로젝트를 만들 때 선택 항목의 효과가 표시됩니다.  
  
1.  SSDT에서 **도구** > **옵션** > **Analysis Services 테이블 형식 디자이너** > **새 프로젝트 설정**을 선택합니다.  
  
2.  **기본 필터 방향** 을 **단일 방향** 또는 **양방향**으로 설정합니다.  
  
 또는 모델에 대한 기본값을 변경할 수 있습니다.  
  
1.  솔루션 탐색기에서 **Model.bim** > **속성** 을 선택합니다.  
  
2.  **기본 필터 방향** 을 **단일 방향** 또는 **양방향**으로 설정합니다.  
  
## <a name="walkthrough-an-example"></a>예제 연습  
 양방향 교차 필터링의 가치를 이해하려면 예제를 사용하는 것이 가장 좋습니다. 기본적으로 만들어진 교차 필터와 카디널리티를 반영하는 [ContosoRetailDW](http://www.microsoft.com/en-us/download/details.aspx?id=18279)의 다음 데이터 집합을 고려해 보겠습니다.  
  
 ![SSAS-BIDI-2-Model](../../analysis-services/tabular-models/media/ssas-bidi-2-model.PNG "SSAS-BIDI-2-Model")  
  
> [!NOTE]  
>  기본적으로 데이터를 가져오는 동안 팩트 테이블과 관련 차원 테이블 간의 외래 키와 기본 키 관계에서 파생된 다 대 일 구성에 대한 테이블 관계가 만들어집니다.  
  
 필터 방향은 차원 테이블에서 팩트 테이블 방향입니다. 프로 모션, 제품, 날짜, 고객 및 고객 지리는 모두 몇 가지 측정값의 집계를 생성하는 유효한 필터이며, 실제 값은 사용된 차원에 따라 달라집니다.  
  
 ![ssas-bidi-3-defaultrelationships](../../analysis-services/tabular-models/media/ssas-bidi-3-defaultrelationships.PNG "ssas-bidi-3-defaultrelationships")  
  
 이 간단한 별모양 스키마에서는 Excel에서의 테스트를 통해 행과 열의 차원 테이블에서 가운데 **FactOnlineSales** 테이블에 있는 **Sum of Sales** 측정값에 제공된 집계 데이터로의 흐름을 필터링할 때 데이터가 적절히 조각화되는지 확인합니다.  
  
 ![ssas-bidi-4-excelSumSales](../../analysis-services/tabular-models/media/ssas-bidi-4-excelsumsales.PNG "ssas-bidi-4-excelSumSales")  
  
 측정값을 팩트 테이블에서 가져오고 필터 컨텍스트가 팩트 테이블에서 종료되는 경우 이 모델에 대한 집계가 올바르게 필터링됩니다. 그러나 다른 곳에서 측정값(예: 제품 또는 고객 테이블의 고유 개수 또는 프로모션 테이블의 평균 할인)을 만들고 기존 필터 컨텍스트를 해당 측정값으로 확장하려는 경우에는 어떻게 될까요?  
  
 **DimProducts** 의 고유 개수를 피벗 테이블에 추가하여 확인해 보겠습니다. **Count Products**의 반복되는 값에 유의하세요. 얼핏 보기에 누락된 테이블 관계처럼 보이지만 이 예제의 모델에서는 모든 관계가 완전히 정의되고 활성 상태인 것을 볼 수 있습니다. 이 예제에서는 제품 테이블의 행에 날짜 필터가 없기 때문에 반복되는 값이 발생합니다.  
  
 ![ssas-bidi-5-prodcount-nofilter](../../analysis-services/tabular-models/media/ssas-bidi-5-prodcount-nofilter.png "ssas-bidi-5-prodcount-nofilter")  
  
 **FactOnlineSales** 와 **DimProduct**간의 양방향 교차 필터를 추가한 후에는 제품 테이블의 행이 제조업체와 날짜별로 올바르게 필터링됩니다.  
  
 ![ssas-bidi-6-prodcount-withfilter](../../analysis-services/tabular-models/media/ssas-bidi-6-prodcount-withfilter.png "ssas-bidi-6-prodcount-withfilter")  
  
## <a name="learn-step-by-step"></a>자세한 단계별  
 이 연습을 단계별로 수행하여 양방향 교차 필터를 체험할 수 있습니다. 단계를 따르려면 다음이 필요합니다.  
  
-   SQL Server 2016 Analysis Services 인스턴스, 테이블 형식 모드, 최신 CTP 릴리스  
  
-   [Visual Studio 2015용 SQL Server Data Tools(SSDT)](http://go.microsoft.com/fwlink/p/?LinkID=627574), 최신 CTP와 함께 공동 출시  
  
-   [ContosoRetailDW](http://www.microsoft.com/en-us/download/details.aspx?id=18279)  
  
-   이 데이터에 대한 읽기 권한  
  
-   Excel(Excel에서 분석에 사용)  
  
### <a name="create-a-project"></a>프로젝트 만들기  
  
1.  Visual Studio 2015용 SQL Server Data Tools를 시작합니다.  
  
2.  **파일** > **새로 만들기** > **프로젝트** > **Analysis Services 테이블 형식 모델**을 클릭합니다.  
  
3.  테이블 형식 모델 디자이너에서 작업 영역 데이터베이스를 테이블 형식 서버 모드의 SQL Server 2016 Preview Analysis Services 인스턴스로 설정합니다.  
  
4.  모델 호환성 수준이 설정 되어 있는지 확인 **SQL Server 2016 RTM (1200)** 이상.  
  
     **확인**을 클릭해 프로젝트를 만듭니다.  
  
### <a name="add-data"></a>데이터 추가  
  
1.  **모델** > **데이터 원본에서 가져오기** > **Microsoft SQL Server**를 클릭합니다.  
  
2.  서버, 데이터베이스 및 인증 방법을 지정합니다.  
  
3.  ContosoRetailDW 데이터베이스를 선택합니다.  
  
4.  **다음**을 클릭합니다.  
  
5.  테이블 선택에서 ctrl 키를 누른 채 다음 테이블을 선택합니다.  
  
    -   DimProduct  
  
    -   DimCustomer  
  
    -   FactOnlineSales  
  
    -   DimGeography  
  
    -   DimPromotion  
  
     이제 모델에서 보다 쉽게 읽을 수 있도록 이름을 편집할 수 있습니다.  
  
     ![ssas-bidi-7-ImportData](../../analysis-services/tabular-models/media/ssas-bidi-7-importdata.PNG "ssas-bidi-7-ImportData")  
  
6.  데이터를 가져옵니다.  
  
 오류가 발생하는 경우 데이터베이스에 연결하는 데 사용된 계정에 Contoso 데이터 웨어하우스에 대한 읽기 권한이 있는 SQL Server 로그인이 있는지 확인합니다. 원격 연결에서 SQL Server에 대한 방화벽의 포트 구성을 확인할 수도 있습니다.  
  
### <a name="review-default-table-relationships"></a>기본 테이블 관계 검토  
 다이어그램 뷰로 전환합니다( **모델** > **모델 뷰** > **다이어그램 뷰**). 카디널리티 및 활성 관계가 시각적으로 표시됩니다. 모든 관계는 임의의 두 관련 테이블 간에 일 대 다 관계입니다.  
  
 ![SSAS-BIDI-2-Model](../../analysis-services/tabular-models/media/ssas-bidi-2-model.PNG "SSAS-BIDI-2-Model")  
  
 또는 **테이블** > **관계 관리** 를 클릭하여 테이블 레이아웃으로 동일한 정보를 볼 수 있습니다.  
  
 ![ssas-bidi-3-defaultrelationships](../../analysis-services/tabular-models/media/ssas-bidi-3-defaultrelationships.PNG "ssas-bidi-3-defaultrelationships")  
  
### <a name="create-measures"></a>측정값 만들기  
 차원 데이터의 다양한 측면으로 판매량 합계를 구하는 집계가 필요합니다. **DimProduct** 에서 제품 수를 계산하는 측정값을 만든 다음 지정된 연도, 지정된 지역 또는 고객 유형별로 판매된 제품 수를 보여 주는 제품 머천다이징 분석에 이를 사용할 수 있습니다.  
  
1.  **모델** > **모델 뷰** > **다이어그램 뷰**를 클릭합니다.  
  
2.  **FactOnlineSales**를 클릭합니다.  
  
3.  **SalesAmount** 열을 선택합니다.  
  
4.  **열** > **자동 합계** > **합계** 를 클릭하여 판매량에 대한 측정값을 만듭니다.  
  
5.  **DimProduct**를 클릭합니다.  
  
6.  **ProductKeycolumn**을 선택합니다.  
  
7.  **열** > **자동 합계** > **DistinctCount** 를 클릭하여 고유한 제품에 대한 측정값을 만듭니다.  
  
### <a name="analyze-in-excel"></a>Excel에서 분석  
  
1.  **모델** > **Excel에서 분석** 을 클릭하여 모든 데이터를 피벗 테이블로 가져옵니다.  
  
2.  필드 목록에서 방금 만든 두 측정값을 선택합니다.  
  
3.  **제품** > **제조업체**를 선택합니다.  
  
4.  **날짜** > **역년**을 선택합니다.  
  
 판매량이 예상대로 연도 및 제조업체별로 분할됩니다. 이는 **FactOnlineSales**, **DimProduct**및 **DimDate** 간의 기본 필터 컨텍스트가 관계의 '다' 쪽 측정값에 대해 올바르게 작동하기 때문입니다.  
  
 이와 동시에 판매량과 동일한 필터 컨텍스트에서 제품 수가 선택되지 않는 것을 볼 수 있습니다. 제품 수는 제조업체(제조업체와 제품 수가 둘 다 동일한 테이블에 있음)별로 올바르게 필터링되지만 날짜 필터는 제품 수로 전파되지 않습니다.  
  
### <a name="change-the-cross-filter"></a>교차 필터 변경  
  
1.  모델로 돌아가 **테이블** > **관계 관리**를 선택합니다.  
  
2.  **FactOnlineSales** 와 **DimProduct**간의 관계를 편집합니다.  
  
     필터 방향을 두 테이블 모두로 변경합니다.  
  
3.  설정을 저장합니다.  
  
4.  통합 문서에서 **새로 고침** 을 클릭하여 모델을 다시 읽습니다.  
  
 이제 제품 수와 판매량 둘 다 동일한 필터 컨텍스트( **DimProducts** 의 제조업체뿐 아니라 **DimDate**의 역년을 포함)로 필터링된 것을 볼 수 있습니다.  
  
## <a name="next-steps"></a>다음 단계  
 양방향 교차 필터가 언제 어떻게 시행 착오를 일으킬 수 있는지를 이해하면 사용자의 시나리오에서 양방향 교차 필터가 작동하는 방식을 알 수 있습니다. 때때로 기본 제공 동작으로 부족하여 DAX 계산에서 대체해야 작업을 완료할 수 있는 경우가 있습니다. **참고 항목** 섹션에 이 주제에 대한 추가 리소스를 제공하는 여러 링크가 나와 있습니다.  
  
 실제로 교차 필터링은 일반적으로 다 대 다 구문을 통해서만 배달되는 데이터 탐색 형식을 지원할 수 있습니다. 양방향 교차 필터링은 다 대 다 구문이 아니라는 점을 인식해야 합니다.  이 릴리스의 테이블 형식 모델 디자이너에서는 실제 다 대 다 테이블 구성이 지원되지 않는 상태로 유지됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Power BI Desktop에서 관계 만들기 및 관리](https://support.powerbi.com/knowledgebase/articles/464155-create-and-manage-relationships-in-power-bi-desktop)   
 [Powerpivot과 테이블 형식 모델에서 간단한 다 다 대 다 관계를 처리 하는 방법의 실제 예](http://social.technet.microsoft.com/wiki/contents/articles/22202.a-practical-example-of-how-to-handle-simple-many-to-many-relationships-in-power-pivotssas-tabular-models.aspx)   
 [DAX를 활용 하 여 다 대 다 관계를 확인 하 고 교차 테이블 필터링](http://blog.gbrueckl.at/2012/05/resolving-many-to-many-relationships-leveraging-dax-cross-table-filtering/)   
 [다 대 다 혁명 (SQLBI 블로그)](http://www.sqlbi.com/articles/many2many/)  
  
  
