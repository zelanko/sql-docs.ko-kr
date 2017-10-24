---
title: "측정값 및 측정값 그룹 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- measure groups [Analysis Services]
- measures [Analysis Services], about measures
- OLAP objects [Analysis Services], measures
- aggregate functions [Analysis Services]
- granularity
- measure groups [Analysis Services], about measure groups
- measures [Analysis Services]
- aggregations [Analysis Services], measures
- fact tables [Analysis Services]
ms.assetid: 4f0122f9-c3a5-4172-ada3-5bc5f7b1cc9a
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bd15969978480e68505747609332f6224355a22f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="measures-and-measure-groups"></a>측정값 및 측정값 그룹
  큐브에는 *측정값 그룹* 의 *측정값*, 비즈니스 논리 및 측정값이 제공하는 숫자 데이터를 평가하기 위한 컨텍스트를 제공하는 차원 컬렉션이 포함됩니다. 측정값과 측정값 그룹은 둘 다 큐브의 필수 구성 요소입니다. 큐브는 최소 하나의 측정값과 측정값 그룹 없이는 존재할 수 없습니다.  
  
 이 항목에서는 [Measures](#bkmk_measure) 및 [Measure Groups](#bkmk_mg)에 대해 설명합니다. 또한 측정값 및 측정값 그룹을 만들고 구성하는 절차 단계에 대한 링크가 들어 있는 다음 표도 제공됩니다.  
  
|**링크**|**Description**|  
|--------------|---------------------|  
|[다차원 모델의 측정값 및 측정값 그룹 만들기](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|측정값과 측정값 그룹을 만들기 위한 몇 가지 접근 방식 중 하나를 선택합니다.|  
|[측정값 속성 구성](../../analysis-services/multidimensional-models/configure-measure-properties.md)|큐브 마법사를 사용하여 큐브를 시작한 경우 집계 방법을 변경하고, 데이터 형식을 적용하며, 클라이언트 응용 프로그램에서 측정값의 표시 유형을 설정하거나, 값이 집계되기 전에 데이터를 조작하기 위한 측정값 식을 추가해야 할 수 있습니다.|  
|[측정값 그룹 속성 구성](../../analysis-services/multidimensional-models/configure-measure-group-properties.md)|다차원 모델에서 측정값 그룹은 원본 데이터 웨어하우스의 팩트 테이블과 같습니다. 측정값 그룹의 속성을 통해 측정값 그룹 수준에서 전체적으로 작동하는 캐싱 동작, 저장소 및 처리 지시문을 지정할 수 있습니다. 파티션 구성은 부분적으로 측정값 그룹 개체에 대해 설정하는 속성에 의해 결정됩니다.|  
|[집계 함수 사용](../../analysis-services/multidimensional-models/use-aggregate-functions.md)|측정값에 할당될 수 있는 집계 방법을 이해합니다.|  
|[반가산적 동작 정의](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md)|반가산적 동작은 일부 차원에 대해서만 유효하고 나머지 다른 차원에 대해서는 유효하지 않은 집계를 의미합니다. 일반적인 예로는 은행 계좌 잔액을 들 수 있습니다. 잔액을 고객 및 지역별로 집계하고자 하지만 시간별로 집계하고자 하지는 않을 것입니다. 예를 들어 연속적으로 며칠간 동일한 계좌의 잔액을 더하지는 않을 것입니다. 반가산적 동작을 정의하려면 비즈니스 인텔리전스 추가 마법사를 사용합니다.|  
|[연결된 측정값 그룹](../../analysis-services/multidimensional-models/linked-measure-groups.md)|동일한 데이터베이스 또는 다른 Analysis Services 데이터베이스에 있는 다른 큐브의 기존 측정값 그룹의 용도를 변경합니다.|  
  
##  <a name="bkmk_measure"></a> Measures  
 측정값은 집계할 수 있는 측정 가능한 데이터(대개 숫자)를 포함하는 열을 나타냅니다. 측정값은 통화 용어(예: 수익, 이익률 또는 비용) 또는 개수(재고 수준, 직원 수, 고객 수 또는 주문 수)나 비즈니스 논리를 통합하는 더 복잡한 계산으로 표현된 조직 활동의 일부 측면을 나타냅니다.  
  
 모든 큐브는 하나 이상의 측정값을 포함해야 하지만 대부분의 큐브는 많은 수의 측정값을 포함하며 경우에 따라 그 수가 수백 개에 이르기도 합니다. 구조적으로 하나의 측정값은 흔히 팩트 테이블 하나의 원본 열 하나에 매핑되며, 해당 열은 측정값을 로드하는 데 사용되는 값을 제공합니다. 또는 MDX를 사용하여 측정값을 정의할 수도 있습니다.  
  
 측정값은 컨텍스트를 구분하며, 쿼리에 포함되는 모든 차원 멤버에 의해 결정되는 컨텍스트에서 숫자 데이터에 대해 작동합니다. 예를 들어 **Reseller Sales** 를 계산하는 측정값은 **Sum** 연산자에 의해 지원되며 쿼리에 포함된 각 차원 멤버의 판매액을 더합니다. 쿼리가 개별 제품을 지정하든 범주로 롤업하든 시간 또는 지리로 분할되든 관계없이 측정값은 쿼리에 포함된 차원에 대해 유효한 연산을 생성해야 합니다.  
  
 이 예제에서 **Reseller Sales** 는 **Sales Territory** 계층을 따라 다양한 수준으로 집계됩니다.  
  
 ![측정값과 차원이 호출 된 피벗 테이블](../../analysis-services/multidimensional-models/media/ssas-keyconcepts-pivot1-measures-dimensions.png "측정값과 차원이 호출 된 피벗 테이블")  
  
 측정값은 숫자 원본 데이터가 포함된 팩트 테이블이 쿼리에 사용된 차원 테이블에 대한 포인터도 포함하는 경우에 유효한 결과를 생성합니다. Reseller Sales 예제를 사용할 경우, 판매액을 저장하는 각 행이 제품 테이블, 날짜 테이블 또는 판매 지역 테이블에 대한 포인터도 저장하면 해당 차원의 멤버를 포함하는 쿼리는 올바르게 해결됩니다.  
  
 측정값이 쿼리에 사용된 차원과 관련이 없는 경우 어떻게 될까요? 일반적으로 Analysis Services는 기본 측정값을 보여 주며, 값은 모든 멤버에 대해 동일합니다. 이 예제에서 고객이 온라인 카탈로그를 사용하여 발생한 직접 판매를 측정하는 **Internet Sales**는 판매 조직과 관계가 없습니다.  
  
 ![값을 측정 하는 반복을 보여 주는 피벗 테이블](../../analysis-services/multidimensional-models/media/ssas-unrelatedmeasure.PNG "값을 측정 하는 반복을 보여 주는 피벗 테이블")  
  
 클라이언트 응용 프로그램에서 이러한 동작이 발생할 확률을 최소화하기 위해 동일한 데이터베이스 내에 여러 큐브 또는 큐브 뷰를 만들어 각 큐브 또는 큐브 뷰가 관련 개체만 포함하도록 할 수 있습니다. 확인해야 할 관계는 측정값 그룹(팩트 테이블에 매핑됨)과 차원 간의 관계입니다.  
  
##  <a name="bkmk_mg"></a> Measure Groups  
 큐브에서 측정값은 기본 팩트 테이블에 의해 측정값 그룹으로 그룹화됩니다. 측정값 그룹은 차원과 측정값을 연결하는 데 사용됩니다. 측정값 그룹은 집계 동작으로 고유 카운트를 가지고 있는 측정값에도 사용됩니다. 고유 카운트 측정값을 자체 측정값 그룹에 각각 배치하면 집계 동작이 최적화됩니다.  
  
 단순 <xref:Microsoft.AnalysisServices.MeasureGroup> 개체는 그룹 이름, 저장소 모드 및 처리 모드와 같은 기본 정보로 구성됩니다. 또한 이러한 개체는 측정값 그룹의 구성을 형성하는 측정값, 차원 및 파티션과 같은 해당 구성 요소도 포함합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델의 큐브](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)   
 [다차원 모델의 측정값 및 측정값 그룹 만들기](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)  
  
  

