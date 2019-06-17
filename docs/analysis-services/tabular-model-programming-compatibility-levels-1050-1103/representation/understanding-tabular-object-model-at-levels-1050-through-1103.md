---
title: 테이블 형식 개체 모델 수준 1050-1103 이해 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ad3963cd7b0b2b40e6b3a08cab68ad809378bff1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63025387"
---
# <a name="understanding-tabular-object-model-at-levels-1050-through-1103"></a>1050~1103 수준에서 테이블 형식 개체 모델 이해
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]

  테이블 형식 모델은 테이블, 관계, 계층, 큐브 뷰, 측정값 및 핵심 성과의 논리적 표현입니다. 이 섹션에서는 AMO를 사용한 내부 구현에 대해 소개합니다. 참조 [Analysis Management Objects를 사용 하 여 개발 &#40;AMO&#41; ](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo) AMO를 사용한 적이 없는 경우.  
  
 여기에 사용되는 접근 방법은 하향식이며, 테이블 형식 모델의 모든 관련 개체가 논리적으로 AMO 개체 및 필요한 상호 작용이나 설명된 워크플로에 매핑됩니다. AMO to Tabular 예제의 AMO를 사용 하 여 테이블 형식 모델을 만들려면 소스 코드 샘플은 Codeplex에서 사용할 수 있습니다. 예제 코드 관련 중요 정보: 예제 코드는 여기에서 설명한 논리적 개념에 대한 지원으로만 제공되며 프로덕션 환경에서 사용해서는 안 됩니다. 예제는 지원 또는 보증 없이 제공됩니다.  
  
## <a name="database-representation"></a>데이터베이스 표현  
 데이터베이스는 테이블 형식 모델의 컨테이너 개체를 제공하며 테이블 형식 모델의 모든 개체는 데이터베이스에 포함됩니다. AMO 개체를 기준으로 데이터베이스 표현은 `xref:Microsoft.AnalysisServices.Database`과 일 대 일 매핑 관계를 가지며 그 밖의 주요 AMO 개체는 필수 항목이 아닙니다. 모델링을 수행할 때 AMO 데이터베이스 개체에 포함된 개체를 모두 사용할 수 있다는 의미는 아닙니다.  
  
 참조 [데이터베이스 표현을&#40;테이블 형식&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/database-representation-tabular.md) 에 대 한 자세한 내용은 데이터베이스 표현을 만들고 조작 하는 방법입니다.  
  
## <a name="connection-representation"></a>연결 표현  
 연결은 테이블 형식 모델 솔루션에 포함할 데이터와 모델 자체 간에 관계를 설정합니다. AMO 개체를 기준으로 연결은 `xref:Microsoft.AnalysisServices.DataSource`과 일 대 일 매핑 관계를 가지며 그 밖의 주요 AMO 개체는 필수 항목이 아닙니다. 모델링을 수행할 때 AMO 데이터 원본 개체에 포함된 개체를 모두 사용할 수 있다는 의미는 아닙니다.  
  
 참조 [연결 표현 &#40;테이블 형식&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/connection-representation-tabular.md) 에 대 한 자세한 내용은 데이터 원본 표현을 만들고 조작 하는 방법입니다.  
  
## <a name="table-representation"></a>테이블 표현  
 테이블은 데이터베이스의 데이터를 포함하는 데이터베이스 개체입니다. AMO 개체를 기준으로 테이블은 일 대 다 매핑 관계를 가지며 다음 AMO 개체를 사용 하 여 테이블을 나타냅니다: `xref:Microsoft.AnalysisServices.DataSourceView`, `xref:Microsoft.AnalysisServices.Dimension`를 `xref:Microsoft.AnalysisServices.Cube`, `xref:Microsoft.AnalysisServices.CubeDimension`를 `xref:Microsoft.AnalysisServices.MeasureGroup` 및 `xref:Microsoft.AnalysisServices.Partition` 가 주된 필수 개체입니다. 그러나 모델링을 수행할 때 앞에서 말한 AMO 개체의 모든 포함 된 개체 수를 의미 하지는 것이 반드시 합니다.  
  
 참조 [테이블 표시 &#40;테이블 형식&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-representation-tabular.md) 에 대 한 자세한 내용은 테이블 표현을 만들고 조작 하는 방법입니다.  
  
### <a name="calculated-column-representation"></a>계산 열 표현  
 계산 열은 테이블의 열을 생성하는 평가 식이며 테이블의 각 행에 대해 새 값이 계산 열에 계산 및 저장됩니다. AMO 개체를 기준으로 계산된 된 열 일 대 다 매핑 관계를 있습니다. 계산된 열은 `xref:Microsoft.AnalysisServices.Dimension` AMO 개체를 사용하여 나타납니다. `xref:Microsoft.AnalysisServices.MeasureGroup`가 주된 필수 개체입니다. 모델링을 수행할 때 앞에서 말한 AMO 개체의 포함된 개체를 모두 사용할 수 있다는 의미는 아닙니다.  
  
 참조 [계산 열 표현을 &#40;테이블 형식&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-calculated-column-representation.md) 에 대 한 자세한 내용은 계산된 열 표현을 만들고 조작 하는 방법입니다.  
  
### <a name="calculated-measure-representation"></a>계산 측정값 표현  
 계산 측정값은 모델이 배포된 후 요청 시 평가되는 저장 식입니다. AMO 개체를 기준으로 계산 측정값은 일 대 다 매핑 관계를 가지며 계산된 열은 `xref:Microsoft.AnalysisServices.MdxScript.Commands%2A` AMO 개체를 사용하여 나타납니다. `xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A`가 주된 필수 개체입니다. 모델링을 수행할 때 앞에서 말한 AMO 개체의 포함된 개체를 모두 사용할 수 있다는 의미는 아닙니다.  
  
> [!NOTE]  
>  `xref:Microsoft.AnalysisServices.Measure` 개체는 테이블 형식 모델의 계산 측정값과 아무런 관계가 없으며 테이블 형식 모델에서 지원되지 않습니다.  
  
 참조 [계산 측정값 표현 &#40;테이블 형식&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-calculated-measure-representation.md) 에 대 한 자세한 내용은 계산된 측정값 표현을 만들고 조작 하는 방법입니다.  
  
### <a name="hierarchy-representation"></a>계층 표현  
 계층은 최종 사용자에게 풍부한 드릴업 및 드릴다운 환경을 제공하는 메커니즘입니다. AMO 개체를 기준으로 계층 표현은 `xref:Microsoft.AnalysisServices.Hierarchy`과 일 대 일 매핑 관계를 가지며 그 밖의 주요 AMO 개체는 필수 항목이 아닙니다. 테이블 형식 모델링을 수행할 때 AMO 데이터베이스 개체에 포함된 개체를 모두 사용할 수 있다는 의미는 아닙니다.  
  
 참조 [계층 표현 &#40;테이블 형식&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-hierarchy-representation.md) 에 대 한 자세한 내용은 계층 표현을 만들고 조작 하는 방법입니다.  
  
### <a name="key-performance-indicator--kpi--representation"></a>핵심 성과 지표 표현을-KPI  
 KPI는 기본 측정값으로 정의된 값을 대상 값과 비교하여 값 성과를 측정하는 데 사용됩니다. AMO 개체를 기준으로 KPI 표현은 일 대 다 매핑 관계를 가지며 다음 AMO 개체를 사용 하 여 KPI 표시 됩니다. `xref:Microsoft.AnalysisServices.MdxScript.Commands%2A` 및 `xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A` 가 주된 필수 개체입니다.  모델링을 수행할 때 앞에서 말한 AMO 개체의 포함된 개체를 모두 사용할 수 있다는 의미는 아닙니다.  
  
> [!NOTE]  
>  `xref:Microsoft.AnalysisServices.Kpi` 개체는 테이블 형식 모델의 KPI와 아무런 관계가 없다는 것도 중요한 차이점입니다. 또한 이러한 개체는 테이블 형식 모델에서 지원되지 않습니다.  
  
 참조 [키 성능 지표 표현을 &#40;테이블 형식&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-key-performance-indicator-representation.md) 에 대 한 자세한 내용은 KPI 표현을 만들고 조작 하는 방법입니다.  
  
### <a name="partition-representation"></a>파티션 표현  
 운영을 위해 테이블을 나눌 수 있습니다 다른 하위 집합에 폼 테이블은 서로 결합 하는 경우는 행입니다. 각각의 하위 집합은 테이블의 파티션입니다. AMO 개체를 기준으로 파티션 표현은 `xref:Microsoft.AnalysisServices.Partition`과 일 대 일 매핑 관계를 가지며 그 밖의 주요 AMO 개체는 필수 항목이 아닙니다. 모델링을 수행할 때 AMO 데이터베이스 개체에 포함된 개체를 모두 사용할 수 있다는 의미는 아닙니다.  
  
 참조 [파티션 표현 &#40;테이블 형식&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-partition-representation.md) 에 대 한 자세한 내용은 파티션 표현을 만들고 조작 하는 방법입니다.  
  
## <a name="relationship-representation"></a>관계 표현  
 관계는 두 테이블 데이터 간의 연결입니다. 관계는 두 테이블의 데이터 간에 상관 관계를 설정합니다.  
  
 테이블 형식 모델에서는 두 테이블 간에 여러 관계를 정의할 수 있습니다. 두 테이블 간에 여러 관계가 정의되어 있는 경우 하나의 관계만 기본 활성 관계로 정의할 수 있습니다. 나머지 모든 관계는 비활성 관계입니다.  
  
 AMO 개체를 기준으로 모든 비활성 관계는 `xref:Microsoft.AnalysisServices.Relationship`과 일 대 일 매핑 관계를 가지며 그 밖의 주요 AMO 개체는 필수 항목이 아닙니다. 활성 관계에 대해서는 기타 요구 사항이 있으며 `xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension`에 대한 매핑 역시 필수입니다. 모델링을 수행할 때 AMO 관계 또는 referenceMeasureGroupDimension 개체에 포함된 개체를 모두 사용할 수 있다는 의미는 아닙니다.  
  
 참조 [관계 표현을 &#40;테이블 형식&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/relationship-representation-tabular.md) 에 대 한 자세한 내용은 관계 표현을 만들고 조작 하는 방법입니다.  
  
## <a name="perspective-representation"></a>큐브 뷰 표현  
 큐브 뷰는 모델을 간소화하거나 집중시키는 메커니즘입니다. AMO 개체를 기준으로 관계 표현은 `xref:Microsoft.AnalysisServices.Perspective`와 일 대 일 매핑 관계를 가지며 그 밖의 주요 AMO 개체는 필수 항목이 아닙니다. 테이블 형식 모델링을 수행할 때 AMO 큐브 뷰 개체에 포함 된 모든 개체 수를 의미 하지는 두는 것이 반드시 합니다.  
  
 참조 [큐브 뷰 표현 &#40;테이블 형식&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/perspective-representation-tabular.md) 대 한 큐브 뷰 표현을 만들고 조작 하는 방법에 자세한 내용은 합니다.  
  
> [!WARNING]  
>  큐브 뷰는 보안 메커니즘이 아니므로 다른 인터페이스를 통해 큐브 뷰 밖에 있는 개체에 계속 액세스할 수 있습니다.  
  
  
