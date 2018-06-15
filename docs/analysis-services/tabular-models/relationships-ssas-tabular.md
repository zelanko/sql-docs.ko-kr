---
title: 관계 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b704b7e2fdc299006d77e08314d2b16ffd750a0a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34045307"
---
# <a name="relationships"></a>관계 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  테이블 형식 모델에서 관계는 두 데이터 테이블 간의 연결입니다. 관계는 두 테이블의 데이터 간에 상관 관계를 설정합니다. 예를 들어 Customers 테이블과 Orders 테이블을 연결하여 각 주문에 연결된 고객 이름을 표시할 수 있습니다.  
  
 테이블 가져오기 마법사를 사용하여 동일한 데이터 원본에서 가져오기를 수행할 경우 가져오기로 선택한 테이블(데이터 원본에서)에 이미 있는 관계가 모델에 다시 만들어집니다. 다이어그램 뷰의 모델 디자이너 또는 관계 관리 대화 상자를 사용하여 자동으로 검색된 관계와 다시 만들어진 관계를 볼 수 있습니다. 또한 다이어그램 뷰의 모델 디자이너나 관계 만들기 또는 관계 관리 대화 상자를 사용하여 수동으로 테이블 간에 새로운 관계를 만들 수도 있습니다.  
  
 가져오는 동안 자동으로 만들어졌거나 수동으로 만든 테이블 간에 관계를 정의하면 관련 열을 사용하여 데이터를 필터링하고 관련 테이블의 값을 조회할 수 있습니다.  
  
> [!TIP]  
>  모델에 여러 관계가 포함된 경우 다이어그램 뷰를 사용하면 테이블 간의 새 관계를 만들고 시각화하는 데 도움이 됩니다.  
  
  
##  <a name="what"></a> 이점  
 관계는 각 테이블에 있는 하나 이상의 열에 기반을 둔 두 데이터 테이블 간의 연결입니다. 관계가 어떤 점에서 유용한지 궁금하다면 여러분이 기업에서 고객 주문 데이터를 추적하는 업무를 담당하고 있다고 가정해 보십시오. 관계를 사용하면 다음과 같은 구조를 지닌 단일 테이블에서 모든 데이터를 추적할 수 있습니다.  
  
|CustomerID|이름|EMail|DiscountRate|OrderID|OrderDate|Product|수량|  
|----------------|----------|-----------|------------------|-------------|---------------|-------------|--------------|  
|1.|Ashton|chris.ashton@contoso.com|.05|256|2010-01-07|Compact Digital|11|  
|1.|Ashton|chris.ashton@contoso.com|.05|255|2010-01-03|SLR Camera|15|  
|2|Jaworski|michal.jaworski@contoso.com|.10|254|2010-01-03|Budget Movie-Maker|27|  
  
 이 접근 방법도 나쁘지 않지만 이 경우 각 주문에 대해 고객의 전자 메일 주소와 같은 중복 데이터가 다량 저장될 수 있습니다. 저장 비용은 저렴하지만 전자 메일 주소가 변경될 경우 해당 고객에 대한 모든 행을 업데이트해야 합니다. 데이터를 여러 테이블로 분할하고 해당 테이블 간에 관계를 정의하면 이러한 문제를 해결할 수 있습니다. 사용 하는 방법 이것이 *관계형 데이터베이스* SQL server. 예를 들어 모델로 가져온 데이터베이스에서 다음과 같은 세 개의 관련 테이블을 사용하여 주문 데이터를 나타낼 수 있습니다.  
  
### <a name="customers"></a>Customers  
  
|[CustomerID]|이름|EMail|  
|--------------------|----------|-----------|  
|1.|Ashton|chris.ashton@contoso.com|  
|2|Jaworski|michal.jaworski@contoso.com|  
  
### <a name="customerdiscounts"></a>CustomerDiscounts  
  
|[CustomerID]|DiscountRate|  
|--------------------|------------------|  
|1.|.05|  
|2|.10|  
  
### <a name="orders"></a>Orders  
  
|[CustomerID]|OrderID|OrderDate|Product|수량|  
|--------------------|-------------|---------------|-------------|--------------|  
|1.|256|2010-01-07|Compact Digital|11|  
|1.|255|2010-01-03|SLR Camera|15|  
|2|254|2010-01-03|Budget Movie-Maker|27|  
  
 이러한 테이블을 동일한 데이터베이스에서 가져오는 경우, 테이블 가져오기 마법사에서는 [대괄호] 안에 있는 열을 기준으로 테이블 간의 관계를 검색하여 모델 디자이너에서 이러한 관계를 재현할 수 있습니다. 자세한 내용은 이 항목의 [관계 자동 검색 및 유추](#detection) 를 참조하십시오. 여러 원본에서 테이블을 가져오는 경우 수동으로 만들 수 있습니다 관계에 설명 된 대로 [테이블 두 간의 관계를 만들](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)합니다.  
  
### <a name="columns-and-keys"></a>열 및 키  
 관계는 동일한 데이터가 포함된 각 테이블의 열에 기반을 둡니다. 예를 들어 Customers 테이블과 Orders 테이블은 둘 모두 고객 ID가 저장된 열을 포함하기 때문에 서로 관련시킬 수 있습니다. 이 항목의 예에서는 열 이름이 같지만 반드시 같아야 할 필요는 없습니다. 한 열은 이름이 CustomerID이고 다른 열은 이름이 CustomerNumber일 수 있습니다. Orders 테이블의 모든 행에 Customers 테이블에 저장되어 있는 ID만 있으면 됩니다.  
  
 관계형 데이터베이스에는 일반적으로 특수 속성을 가진 열로 나타나는 여러 가지 유형의 *키*가 있습니다. 관계형 데이터베이스에는 다음 네 가지 유형의 키를 사용할 수 있습니다.  
  
-   *기본 키*: 테이블의 행을 고유하게 식별합니다(예: Customers 테이블의 CustomerID).  
  
-   *대체 키* (또는 *후보 키*): 기본 키가 아닌 고유 열입니다. 예를 들어 Employees 테이블에 직원 ID와 주민 등록 번호가 저장될 수 있으며 둘 모두 고유합니다.  
  
-   *외래 키*: 다른 테이블의 고유 열을 참조하는 열입니다(예: Customers 테이블의 CustomerID를 참조하는 Orders 테이블의 CustomerID).  
  
-   *복합 키*: 두 개 이상의 열로 구성된 키입니다. 테이블 형식 모델에서는 복합 키가 지원되지 않습니다. 자세한 내용은 이 항목의 "복합 키 및 조회 열"을 참조하십시오.  
  
 테이블 형식 모델에서는 기본 키 또는 대체 키를 *관련 조회 열*또는 그냥 *조회 열*이라고 합니다. 테이블에 기본 키와 대체 키가 둘 다 있으면 둘 중 하나를 조회 열로 사용할 수 있습니다. 외래 키는 *원본 열* 또는 그냥 *열*이라고 합니다. 이 항목의 예에서는 Orders 테이블의 CustomerID(열)와 Customers 테이블의 CustomerID(조회 열) 간에 관계가 정의됩니다. 관계형 데이터베이스에서 데이터를 가져오는 경우 기본적으로 모델 디자이너에서는 한 테이블에서 외래 키를 선택하고 다른 테이블에서 해당되는 기본 키를 선택합니다. 그러나 조회 열에 대한 고유 값을 가지는 열이면 모두 사용할 수 있습니다.  
  
### <a name="types-of-relationships"></a>관계 유형  
 Customers와 Orders 간의 관계는 *일 대 다 관계*입니다. 모든 고객은 여러 개의 주문을 가질 수 있지만 각 주문은 여러 고객을 가질 수 없습니다. 관계의 유형에는 *일 대 일* 과 *다 대 다*가 있습니다. 각 고객에 대해 단일 할인율을 정의하는 CustomerDiscounts 테이블은 Customers 테이블과 일 대 일 관계에 있습니다. 다 대 다 관계의 예로는 Products 및 Customers 간의 직접적인 관계를 들 수 있습니다. 이 관계에서 고객은 여러 개의 제품을 구입할 수 있고 한 제품을 여러 명의 고객이 구입할 수도 있습니다. 모델 디자이너는 사용자 인터페이스에서 다 대 다 관계를 지원하지 않습니다. 자세한 내용은 이 항목에 있는 "[다 대 다 관계](#bkmk_many_to_many)"를 참조하십시오.  
  
 다음 표에서는 세 테이블 간의 관계를 보여 줍니다.  
  
|관계|형식|조회 열|열|  
|------------------|----------|-------------------|------------|  
|Customers-CustomerDiscounts|일 대 일|Customers.CustomerID|CustomerDiscounts.CustomerID|  
|Customers-Orders|일 대 다|Customers.CustomerID|Orders.CustomerID|  
  
### <a name="relationships-and-performance"></a>관계와 성능  
 관계를 만든 후에 모델 디자이너에서는 일반적으로 새로 만든 관계의 테이블에 있는 열을 사용하는 모든 수식을 다시 계산해야 합니다. 데이터의 양이 많거나 관계가 복잡하면 처리에 시간이 걸릴 수 있습니다.  
  
##  <a name="requirements"></a> Requirements for relationships  
 모델 디자이너에서 관계를 만들 때 따라야 할 몇 가지 요구 사항이 있습니다.  
  
### <a name="single-active-relationship-between-tables"></a>테이블 간 단일 활성 관계  
 관계가 여러 개 있으면 테이블 간의 종속성이 모호해질 수 있습니다. 정확한 계산을 만들려면 한 테이블에서 다음 테이블로 연결되는 단일 경로가 필요합니다. 따라서 각 테이블 쌍 사이에는 하나의 활성 관계만 있을 수 있습니다. 예를 들어 AdventureWorks DW 2012에서 DimDate 테이블에는 FactInternetSales 테이블의 세 가지 다른 열인 OrderDate, DueDate 및 ShipDate와 관련된 DateKey 열이 포함되어 있습니다. 이러한 테이블을 가져오려는 경우 첫 번째 관계는 성공적으로 만들어지지만 같은 열에 적용되는 연속된 관계에 대해 다음 오류가 나타나게 됩니다.  
  
 \* 관계: 테이블 [열 1]-> 테이블 [열 2]-상태: 오류-이유: 테이블 간에 관계를 만들 수 없습니다 \<표 1 > 및 \<표 2 >. 두 테이블 간에는 하나의 직접 또는 간접 관계만 존재합니다.  
  
 테이블이 두 개 있고 이 테이블 간에 여러 관계가 있는 경우 조회 열을 포함하는 테이블의 여러 복사본을 가져와서 각 테이블 쌍 간에 하나의 관계를 만들어야 합니다.  
  
 테이블 간에 많은 비활성 관계가 있을 수 있습니다. 테이블 사이에서 사용할 경로는 쿼리 시간에 보고하는 클라이언트에 의해 지정됩니다.  
  
### <a name="one-relationship-for-each-source-column"></a>각 원본 열에 하나의 관계 사용  
 원본 열은 여러 관계에 참여할 수 없습니다. 특정 열을 한 관계의 원본 열로 이미 사용했지만 해당 열을 사용하여 다른 테이블의 다른 관련 조회 열에 연결하려는 경우 열의 복사본을 만든 다음 해당 열을 새 관계에 사용할 수 있습니다.  
  
 계산 열에 DAX 수식을 사용하면 동일한 값을 가진 열의 복사본을 쉽게 만들 수 있습니다. 자세한 내용은 참조 [계산 열 만들기](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md)합니다.  
  
### <a name="unique-identifier-for-each-table"></a>각 테이블의 고유 식별자  
 각 테이블에는 해당 테이블의 각 행을 고유하게 식별하는 단일 열이 있어야 합니다. 이 열을 대개 기본 키라고 합니다.  
  
### <a name="unique-lookup-columns"></a>고유 조회 열  
 조회 열의 데이터 값은 고유해야 합니다. 즉, 열에 중복된 값이 있으면 안 됩니다. 테이블 형식 모델에서 null 및 빈 문자열은 공백과 동일하며 이는 고유 데이터 값입니다. 이는 조회 열에 Null 값을 여러 개 포함할 수 없음을 의미합니다.  
  
### <a name="compatible-data-types"></a>호환되는 데이터 형식  
 원본 열과 조회 열의 데이터 형식이 호환되어야 합니다. 데이터 형식에 대 한 자세한 내용은 참조 [지원 되는 데이터 형식](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md)합니다.  
  
### <a name="composite-keys-and-lookup-columns"></a>복합 키 및 조회 열  
 테이블 형식 모델에서는 복합 키를 사용할 수 없습니다. 즉, 테이블의 각 행을 고유하게 식별하는 열이 항상 하나여야 합니다. 복합 키를 기반으로 하는 기존 관계를 가진 테이블을 가져오는 경우 테이블 가져오기 마법사는 해당 관계를 테이블 형식 모델에서 만들 수 없으므로 이 관계를 무시합니다.  
  
 모델 디자이너에서 두 테이블 간의 관계를 만들려고 하고 기본 키 및 외래 키를 정의하는 열이 여러 개 있는 경우 먼저 이들 값을 결합하여 단일 키 열을 만든 후 관계를 만들어야 합니다. 이 작업을 데이터를 가져오기 전에 수행하거나 모델 디자이너에서 계산 열을 만들어 수행할 수 있습니다.  
  
###  <a name="bkmk_many_to_many"></a> Many-to-Many relationships  
 테이블 형식 모델에서는 다 대 다 관계를 지원하지 않으므로 모델 디자이너에서 *접합 테이블* 을 추가할 수 없습니다. 하지만 DAX 함수를 사용하여 다 대 다 관계를 모델링할 수 있습니다.  
  
 또한 동일한 목적을 달성하는 경우 양방향 교차 필터 설정을 시도할 수 있습니다. 경우에 따라 여러 테이블 관계 간에 필터 컨텍스트를 유지 하는 필터 간을 통해 다 대 다 관계의 요구 사항이 충족 될 수입니다. 자세한 내용은 [SQL Server 2016 Analysis Services의 테이블 형식 모델에 대한 양방향 교차 필터](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) 를 참조하세요.  
  
### <a name="self-joins-and-loops"></a>자체 조인 및 루프  
 자체 조인은 테이블 형식 모델 테이블에서 허용되지 않습니다. 자체 조인은 테이블 자체의 재귀적 관계입니다. 자체 조인은 주로 부모-자식 계층을 정의하는 데 사용됩니다. 예를 들어 Employees 테이블을 자체에 조인하여 기업의 관리 체인을 보여 주는 계층을 만들 수 있습니다.  
  
 모델 디자이너에서는 모델의 관계 사이에 루프를 만들 수 없습니다. 즉, 다음과 같은 관계 집합은 금지됩니다.  
  
 테이블 1, 열 a - 테이블 2, 열 f  
  
 테이블 2, 열 f - 테이블 3, 열 n  
  
 테이블 3, 열 n - 테이블 1, 열 a  
  
 루프를 초래하는 관계를 만들려고 하면 오류가 발생합니다.  
  
##  <a name="detection"></a> Inference of relationships  
 경우에 따라 테이블 간의 관계가 자동으로 연결됩니다. 예를 들어 아래에서 처음 두 테이블 집합 간에 관계를 만들면 다른 두 테이블 간에 관계가 존재하는 것으로 유추되어 관계가 자동으로 만들어집니다.  
  
 Products와 Category -- 수동으로 관계 생성  
  
 Category와 SubCategory -- 수동으로 관계 생성  
  
 Products와 SubCategory -- 관계가 유추됨  
  
 관계가 자동으로 연결되려면 위와 같이 관계가 한 방향으로 형성되어야 합니다. 예를 들어 처음에 Sales와 Products 간에 관계를 만들고 Sales와 Customers 간에 관계를 만들었다면 관계는 유추되지 않습니다. 이는 Products와 Customers 간의 관계가 다 대 다 관계이기 때문입니다.  
  
##  <a name="bkmk_detection"></a> Detection of relationships when importing data  
 관계형 데이터 원본 테이블에서 가져오는 경우 테이블 가져오기 마법사는 원본 스키마 데이터를 기반으로 원본 테이블에서 기존 관계를 검색합니다. 관련 테이블을 가져오는 경우 해당 관계가 모델에서 중복됩니다.  
  
##  <a name="bkmk_manually_create"></a> Manually create relationships  
 단일 관계형 데이터 원본의 테이블 간 대부분의 관계는 자동으로 검색되고 테이블 형식 모델에 만들어지는 데 반해 모델 테이블 간 관계를 수동으로 만들어야 하는 인스턴스도 많습니다.  
  
 모델에 있는 데이터의 원본이 여러 개인 경우 수동으로 관계를 만들어야 할 가능성이 많습니다. 예를 들어 관계형 데이터 원본에서 Customers, CustomerDiscounts 및 Orders 테이블을 가져올 수 있습니다. 원본의 이러한 테이블 간에 있는 관계는 자동으로 모델에 만들어집니다. 그런 다음 다른 원본의 다른 테이블을 추가할 수 있습니다. 예를 들어 icrosoft Excel 통합 문서의 Geography 테이블에서 영역 데이터를 가져올 수 있습니다. 그런 다음 Customers 테이블의 열과 Geography 테이블 간 관계를 수동으로 만들 수 있습니다.  
  
 다이어그램 뷰의 모델 디자이너나 관계 관리 대화 상자를 사용하여 테이블 형식 모델에 관계를 수동으로 만들 수 있습니다. 다이어그램 뷰는 테이블을 그래픽 형식의 관계도와 함께 표시합니다. 한 테이블의 열을 클릭한 다음 다른 테이블로 커서를 끌어 테이블 간에 올바른 순서로 쉽게 관계를 만들 수 있습니다. 관계 관리 대화 상자에는 간단한 테이블 형식으로 테이블 간의 관계가 표시됩니다. 수동으로 관계를 만드는 방법을 알아보려면 참조 [테이블 두 간의 관계를 만들](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)합니다.  
  
##  <a name="bkmk_dupl_errors"></a> Duplicate values and other errors  
 관계에 사용할 수 없는 열을 선택하면 열 옆에 빨간색 X가 나타납니다. 오류 아이콘 위에 커서를 두면 문제에 대한 자세한 정보를 제공하는 메시지가 표시됩니다. 다음과 같은 문제로 인해 선택된 열 간에 관계를 만들지 못할 수 있습니다.  
  
|문제 또는 메시지|해결 방법|  
|------------------------|----------------|  
|선택한 두 열 모두에 중복되는 값이 들어 있기 때문에 관계를 만들 수 없습니다.|올바른 관계를 만들려면 선택한 한 쌍의 열 중 최소 하나의 열에 고유 값만 들어 있어야 합니다.<br /><br /> 열을 편집하여 중복을 제거하거나 고유 값이 들어 있는 열이 **관련 조회 열**로 사용되도록 열의 순서를 반대로 할 수 있습니다.|  
|열에 null 또는 빈 값이 포함되어 있습니다.|null 값이 있으면 데이터 열을 서로 조인할 수 없습니다. 모든 행에 대해 관계에서 사용되는 두 열 모두에 값이 있어야 합니다.|  
  
##  <a name="bkmk_related_tasks"></a> Related tasks  
  
|항목|Description|  
|-----------|-----------------|  
|[두 테이블 간에 관계 만들기](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)|두 테이블 간의 관계를 수동으로 만드는 방법을 설명합니다.|  
|[관계 삭제](../../analysis-services/tabular-models/delete-relationships-ssas-tabular.md)|관계를 삭제하는 방법과 관계를 삭제할 경우에 발생하는 결과를 설명합니다.|  
|[SQL Server 2016 Analysis Services의 테이블 형식 모델에 대한 양방향 교차 필터](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)|관련된 테이블에 대한 양방향 교차 필터링을 설명합니다. 한 테이블 관계의 필터 컨텍스트는 테이블이 관련되고 양방향 교차 필터가 정의되는 경우 두 번째 테이블 관계를 통해 쿼리할 때 사용할 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [테이블 및 열](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [데이터 가져오기](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)  
  
  
