---
title: 다 대 다 관계 및 다 대 다 관계 속성 정의 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f0a8ee2b6ee9bb7d53234b6b21974978543bc4c2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="define-a-many-to-many-relationship-and-many-to-many-relationship-properties"></a>다 대 다 관계 및 다 대 다 관계 속성 정의
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  이 항목에서는 Analysis Services의 다 대 다 차원에 대해 설명하고 이러한 차원을 사용하는 경우와 만드는 방법도 살펴봅니다.  
  
## <a name="introduction"></a>소개  
 Analysis Services는 다 대 다 차원을 지원하여 표준 별모양 스키마에서 설명할 수 있는 것보다 복잡한 분석을 가능하게 합니다. 표준 별모양 스키마에서는 모든 차원이 팩트 테이블과 일 대 다 관계를 맺고 있습니다. 각 팩트는 하나의 차원 멤버에 조인되고 단일 차원 멤버는 여러 팩트와 연결됩니다.  
  
 다 대 다는 팩트(계정 잔액 등)이 동일한 차원의 여러 멤버와 연결될 수 있도록 하여(공동 계정의 잔액이 공동 계정의 예금주 둘 이상에 할당될 수 있음) 이러한 모델링 제한을 제거합니다.  
  
 개념적으로 Analysis Services의 다 대 다 차원 관계는 관계형 모델의 다 대 다 관계와 동일하며 같은 종류의 시나리오를 지원합니다. 다 대 다의 일반적인 예는 다음과 같습니다.  
  
-   학생들이 많은 과목에 등록되고 각 과목에 많은 학생이 있습니다.  
  
-   의사들에게 많은 환자가 있고 환자들에게 많은 의사가 있습니다.  
  
-   고객들이 많은 은행 계정을 갖고 있고 은행 계정들이 둘 이상의 고객에게 속할 수도 있습니다.  
  
-   Adventure Works에서는 많은 고객이 제품을 구매하는 다양한 이유를 갖고 있으며 판매 이유가 많은 주문과 연결될 수 있습니다.  
  
 분석 측면에서 다 대 다 관계의 이점은 차원 관계에 비해 개수나 합계를 정확히 표현한다는 것입니다. 이는 일반적으로 특정 차원 멤버에 대한 계산을 수행할 때 중복 개수를 제거하여 이루어집니다. 이 점을 명확히 하기 위해 둘 이상의 범주에 속하는 제품이나 서비스를 예로 들어보겠습니다. 범주별로 서비스 수를 세는 경우 두 범주에 모두 속하는 서비스가 각 범주에 포함되게 하려고 합니다. 이와 동시에 제공하는 서비스의 수를 과장하지는 않으려고 합니다. 다 대 다 차원 관계를 지정하면 범주나 서비스별로 쿼리할 때 올바른 결과를 얻을 가능성이 높습니다. 그러나 이렇게 되려면 항상 철저한 테스트가 필요합니다.  
  
 구조적 측면에서 볼 때 다 대 다 차원 관계를 만드는 것은 관계형 데이터 모델에서 다 대 다를 만들 수 있는 방법과 유사합니다. 관계형 모델이 *접합 테이블* 을 사용하여 행 연결을 저장하는 반면에 다차원 모델은 *중간 측정값 그룹*을 사용합니다. 중간 측정값 그룹은 여러 차원의 멤버를 매핑하는 테이블을 나타내는 용어입니다.  
  
 시각적으로 다 대 다 차원 관계는 큐브 다이어그램에 나타나지 않습니다. 대신 차원 용도 탭을 사용하여 모델에서 다 대 다 관계를 신속하게 식별할 수 있습니다. 다 대 다 관계는 다음 아이콘으로 표시됩니다.  
  
 ![차원 용도의 다 대 다 아이콘](../../analysis-services/multidimensional-models/media/ssas-m2m-icondimusage.png "다 대 다 차원 용도의 아이콘")  
  
 단추를 클릭하여 관계 정의 대화 상자를 연 다음 관계 유형이 다 대 다인지 확인하고 관계에서 사용되는 중간 측정값 그룹을 확인합니다.  
  
 ![차원 용도의 관계 단추가](../../analysis-services/multidimensional-models/media/ssas-m2m-btndimusage.png "차원 용도의 관계 정의 단추")  
  
 이후의 섹션들에서는 다 대 다 차원을 설정하고 모엘 동작을 테스트하는 방법을 알아봅니다. 먼저 추가 정보를 검토하거나 자습서를 살펴보려면 이 문서 끝에 있는 **자세한 정보** 를 참조하십시오.  
  
## <a name="create-a-many-to-many-dimension"></a>다 대 다 차원 만들기  
 간단한 다 대 다 관계에는 다 대 다 카디널리티가 있는 두 차원, 멤버 연결을 저장하기 위한 중간 측정값 그룹 및 총 매출 합계, 은행 계정 잔액 등의 측정 가능한 데이터가 포함된 팩트 측정값 그룹이 포함됩니다.  
  
 다 대 다 관계의 차원은 DSV에 대응하는 테이블이 있을 수도 있으며, 이 경우 모델의 각 차원이 데이터 원본의 기존 테이블을 기반으로 합니다. 반대로 모델의 차원은 DSV에 있는 더 적거나 서로 다른 물리적 테이블에서 파생될 수도 있습니다. Sales Reasons 및 Sales Orders를 적절한 예로 사용하여 Adventure Works 예제 큐브에서는 DSV에서 대응하는 물리적 항목 없이 모델 전용 데이터 구조로 존재하는 차원을 사용하는 다 대 다 관계를 보여 줍니다. Sales Order 차원은 기본 데이터 원본의 차원 테이블이 아니라 팩트 테이블을 기반으로 합니다.  
  
 다음 절차에서는 다 대 다 관계에 참여하는 엔터티를 이미 알고 있다고 가정합니다. 자세한 내용은 **자세한 정보** 를 참조하십시오.  
  
 다 대 다 관계를 만드는 데 사용되는 단계를 보여주기 위해 이 절차에서는 Adventure Works 예제 큐브에서 다 대 다 관계 중 하나를 다시 만듭니다. 원본 데이터(즉, Adventure Works 예제 데이터 웨어하우스)가 관계형 데이터베이스 엔진 인스턴스에 설치되어 있는 경우 다음 단계를 수행할 수 있습니다.  
  
#### <a name="step-1-verify-dsv-relationships"></a>1단계: DSV 관계 확인  
  
1.  SQL Server Data Tools의 다차원 프로젝트에서 SQL Server 데이터베이스 엔진 인스턴스에 호스팅된 Adventure Works DW 2012 관계형 데이터 웨어하우스를 데이터 원본으로 만듭니다.  
  
2.  다음 기존 테이블을 사용하여 데이터 원본 뷰를 만듭니다.  
  
    -   FactInternetSales  
  
    -   FactInternetSalesReason  
  
    -   DimSalesReason  
  
3.  다 대 다 관계에서 사용하려는 모든 테이블이 기본 키 관계를 통해 DSV에서 관련되어 있는지 확인합니다. 이 작업은 이후 단계에서 중간 측정값 그룹에 대한 연결을 설정하기 위해 필요합니다.  
  
    > [!NOTE]  
    >  기본 데이터 원본에서 기본 및 외래 키 관계를 제공하지 않는 경우 DSV에서 수동으로 관계를 만들 수 있습니다. 자세한 내용은 [데이터 원본 뷰에서 논리적 관계 정의&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md)를 참조하세요.  
  
     다음 예제에서는 이 절차에서 사용되는 테이블이 기본 키를 사용하여 연결되어 있음을 확인합니다.  
  
     ![관련된 테이블을 표시 하는 DSV](../../analysis-services/multidimensional-models/media/ssas-m2m-dsvpkeys.PNG "관련된 테이블을 표시 하는 DSV")  
  
#### <a name="step-2-create-dimensions-and-measure-groups"></a>2단계: 차원 및 측정값 그룹 만들기  
  
1.  SQL Server Data Tools의 다차원 프로젝트에서 **차원** 을 마우스 오른쪽 단추로 클릭하고 **새 차원**을 선택합니다.  
  
2.  기존 **DimSalesReason**테이블을 기반으로 새 차원을 만듭니다. 원본을 지정할 때 기본값을 모두 적용합니다.  
  
     특성의 경우 모두 선택합니다.  
  
     ![새 차원에 특성 목록](../../analysis-services/multidimensional-models/media/ssas-m2m-dimsalesreason.PNG "새 차원에 특성 목록")  
  
3.  기존 Fact Internet Sales 테이블을 기반으로 두 번째 차원을 만듭니다. 이 테이블은 팩트 테이블이지만 Sales Order 정보를 포함하고 있습니다. 이 정보를 사용하여 Sales Order 차원을 만들 것입니다.  
  
4.  원본 정보 지정에서 이름 열을 지정해야 한다는 경고가 표시됩니다. **SalesOrderNumber** 를 이름으로 선택합니다.  
  
     ![이름 열을 표시 하는 sales Order 차원](../../analysis-services/multidimensional-models/media/ssas-m2m-dimsalesordersource.PNG "이름 열을 표시 하는 Sales Order 차원")  
  
5.  마법사의 다음 페이지에서 특성을 선택합니다. 이 예에서는 **SalesOrderNumber**만 선택하면 됩니다.  
  
     ![판매 주문 차원 보여 주는 특성 목록](../../analysis-services/multidimensional-models/media/ssas-m2m-dimsalesorderattrib.PNG "Sales order 차원 보여 주는 특성 목록")  
  
6.  차원에 대해 일관성 있는 명명 규칙을 사용하기 위해 차원의 이름을 **Dim Sales Orders**로 바꿉니다.  
  
     ![차원 이름 바꾸기를 표시 하는 마법사 페이지](../../analysis-services/multidimensional-models/media/ssas-m2m-dimsalesorders.PNG "차원 이름 바꾸기를 표시 하는 마법사 페이지")  
  
7.  **큐브** 를 마우스 오른쪽 단추로 클릭하고 **새 큐브**를 선택하세요.  
  
8.  측정값 그룹 테이블에서 **FactInternetSales** 및 **FactInternetSalesReason**을 선택합니다.  
  
     **FactInternetSales** 는 큐브에서 사용하려는 측정값을 포함하고 있기 때문에 선택하고, **FactInternetSalesReason** 은 판매 주문과 판매 이유의 관계를 설정하는 멤버 연결 데이터를 제공하는 중간 측정값 그룹이기 때문에 선택합니다.  
  
9. 각 팩트 테이블의 측정값을 선택합니다.  
  
     모델을 단순하게 만들기 위해 모든 측정값을 지운 다음 목록 아래쪽에서 **Sales Amount** 및 **Fact Internet Sales Count** 만 선택합니다. **FactInternetSalesReason** 은 측정값을 하나만 포함하므로 자동으로 선택됩니다.  
  
10. 차원 목록에 **Dim Sales Reason** 및 **Dim Sales Orders**가 표시됩니다.  
  
     새 차원 선택 페이지에서 **Fact Internet Sales Dimension**의 새 차원을 만들라는 메시지가 마법사에 표시됩니다. 이 차원은 필요하지 않으므로 목록에서 지워도 됩니다.  
  
11. 큐브의 이름을 지정하고 **마침**을 클릭합니다.  
  
#### <a name="step-3-define-many-to-many-relationship"></a>3단계: 다 대 다 관계 정의  
  
1.  큐브 디자이너에서 차원 용도 탭을 클릭합니다. **Dim Sales Reason** 및 **Fact Internet Sales**간에 이미 다 대 다 관계가 있음을 확인합니다. 이전에 설명한 대로 다음 아이콘은 다 대 다 관계를 나타냅니다.  
  
     ![차원 용도의 다 대 다 아이콘](../../analysis-services/multidimensional-models/media/ssas-m2m-icondimusage.png "다 대 다 차원 용도의 아이콘")  
  
2.  **Dim Sales Reason** 과 **Fact Internet Sales**간의 교집합 셀을 클릭한 다음 단추를 클릭하여 관계 정의 대화 상자를 엽니다.  
  
     이 대화 상자가 다 대 다 관계를 지정하는 데 사용됨을 확인할 수 있습니다. 일반 관계가 있는 차원을 대신 추가한 경우에는 이 대화 상자를 사용하여 다 대 다로 변경할 수 있습니다.  
  
     ![차원 용도의 관계 단추가](../../analysis-services/multidimensional-models/media/ssas-m2m-btndimusage.png "차원 용도의 관계 정의 단추")  
  
3.  Analysis Services 다차원 인스턴스에 프로젝트를 배포합니다. 다음 단계에서는 Excel에서 큐브를 탐색하여 동작을 확인합니다.  
  
## <a name="testing-many-to-many"></a>다 대 다 테스트  
 큐브에서 다 대 다 관계를 정의하는 경우 쿼리가 예상되는 결과를 반환하는지 확인하기 위해 반드시 테스트를 거쳐야 합니다. 최종 사용자가 사용할 클라이언트 응용 프로그램을 사용하여 큐브를 테스트해야 합니다. 다음 절차에서는 Excel을 사용하여 큐브에 연결하고 쿼리 결과를 확인합니다.  
  
#### <a name="browse-the-cube-in-excel"></a>Excel에서 큐브 탐색  
  
1.  프로젝트를 배포한 다음 큐브를 탐색하여 집계가 유효한지 확인합니다.  
  
2.  Excel에서 **데이터** | **기타 원본** | **Analysis Services**를 클릭합니다. 서버의 이름을 입력하고 데이터베이스와 큐브를 선택합니다.  
  
3.  다음과 같은 피벗 테이블을 만듭니다.  
  
    -   **Sales Amount** 를 값으로 사용함  
  
    -   열에서**Sales Reason Name** 을 사용함  
  
    -   행에서**Sales Order Number** 를 사용함  
  
4.  결과를 분석합니다. 예제 데이터를 사용하고 있기 때문에 처음에는 모든 판매 주문에 동일한 값이 있는 것처럼 보입니다. 그러나 아래로 스크롤하면 데이터 변화를 확인할 수 있습니다.  
  
     어느 정도 내려가면 주문 번호 **SO5382**에 대한 판매액과 판매 이유를 찾을 수 있습니다. 이 특정 주문의 총합계는 **539.99**이고 이 주문에 할당된 구매 이유에는 Promotion, Other 및 Price가 포함되어 있습니다.  
  
     ![다 대 다 집계를 표시 한 Excel 워크시트](../../analysis-services/multidimensional-models/media/ssas-m2m-excel.png "다 대 다 집계를 표시 한 Excel 워크시트")  
  
     주문의 판매액은 올바르게 계산되었습니다. 즉, 전체 주문의 판매액은 **539.99** 입니다. **539.99** 가 각 이유에 표시되어 있지만 모든 세 이유의 값에 대한 합계가 계산되지 않아서 총합계가 잘못된 값으로 커지지 않았습니다.  
  
     왜 처음부터 판매액을 각 판매 이유 아래에 넣지 않았을까요? 그것은 바로 각 이유에 할당할 수 있는 판매액을 식별할 수 있도록 하기 위해서입니다.  
  
5.  워크시트의 아래로 스크롤합니다. 이제 총합계뿐만 아니라 다른 이유에 비해 Price가 고객 구매의 가장 중요한 이유인 것을 쉽게 확인할 수 있습니다.  
  
     ![다 대 다에서 합계를 표시 하는 Excel 통합 문서](../../analysis-services/multidimensional-models/media/ssas-m2m-excelgrandtotal.png "다 대 다에서 합계를 표시 하는 Excel 통합 문서")  
  
#### <a name="tips-for-handling-unexpected-query-results"></a>예기치 않은 쿼리 결과 처리 시 유용한 정보  
  
1.  쿼리에서 의미 있는 결과를 반환하지 않는 개수와 같은 측정값을 중간 측정값 그룹에서 숨깁니다. 이렇게 하면 의미 없는 데이터를 생성하는 집계를 사용하지 않게 됩니다. 측정값을 숨기려면 차원 디자이너에서 특성에 대한 **표시 유형** 을 **False** 로 설정합니다.  
  
2.  제공하려는 분석 환경을 지원하는 차원과 측정값의 하위 집합을 사용하기 위해 큐브 뷰를 만듭니다. 경우에 따라 함께 제대로 작동하지 않는 많은 측정값 그룹과 차원이 큐브에 포함되어 있을 수 있습니다. 함께 사용하려는 차원과 측정값 그룹을 분리하면 보다 예측 가능한 결과를 얻을 수 있습니다.  
  
3.  모델을 변경한 후 배포하고 다시 연결하는 작업을 항상 잊지 말고 수행합니다. Excel에서 피벗 테이블 분석 리본의 새로 고침 단추를 사용합니다.  
  
4.  연결된 측정값 그룹을 여러 다 대 다 관계에서 사용하지 마십시오. 특히 해당 관계가 서로 다른 큐브에 있는 경우에 사용하지 마십시오. 사용하면 모호한 집계가 발생할 수 있습니다. 자세한 내용은 [다 대 다 관계가 포함된 큐브의 연결된 측정값에 대한 잘못된 집계](http://social.technet.microsoft.com/wiki/contents/articles/22911.incorrect-amounts-for-linked-measures-in-cubes-containing-many-to-many-relationships-ssas-troubleshooting.aspx)를 참조하세요.  
  
##  <a name="bkmk_Learn"></a> Learn more  
 개념을 완전히 이해하는 데 유용한 추가 정보를 얻으려면 다음 링크를 사용하십시오.  
  
 [다 대 다 혁명 2.0](http://go.microsoft.com/fwlink/?LinkId=324760)  
  
 [자습서: SQL Server Analysis Services의 다 대 다 차원 예제](http://go.microsoft.com/fwlink/?LinkId=324761)  
  
## <a name="see-also"></a>관련 항목:  
 [차원 관계](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Analysis Services 다차원 모델링 자습서에 대 한 예제 데이터 및 프로젝트 설치](../../analysis-services/install-sample-data-and-projects.md)   
 [Analysis Services 프로젝트 & #40; 배포 SSDT & #41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)   
 [다차원 모델의 큐브 뷰](../../analysis-services/multidimensional-models/perspectives-in-multidimensional-models.md)  
  
  
