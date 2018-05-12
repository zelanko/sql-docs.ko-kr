---
title: AMO OLAP 클래스 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: amo
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1d457c26a0b2d33058a5eb496825a6dc03dbc71
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="amo-olap-classes"></a>AMO OLAP 클래스
  AMO(Analysis Management Objects) OLAP 클래스를 사용하면 큐브 및 차원과 KPI(핵심 성과 지표), 동작, 자동 관리 캐싱 등의 관련 개체를 손쉽게 만들고 수정, 삭제 및 처리할 수 있습니다.  
  
 AMO 프로그래밍 환경 설정에 대 한 자세한 내용은 데이터베이스 액세스 또는 데이터를 정의 하는 서버와 연결할 원본 및 데이터 원본 뷰 표시 방법 [AMO 기본 클래스](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [차원 개체](#Dimensions)  
  
-   [큐브 개체](#Cubes)  
  
-   [MeasureGroup 개체](#MeasureGroups)  
  
-   [파티션 개체](#Partition)  
  
-   [AggregationDesign 개체](#AggregationDesign)  
  
-   [Aggregation 개체](#Aggregation)  
  
-   [동작 개체](#Action)  
  
-   [KPI 개체](#KPI)  
  
-   [Perspective 개체](#Perspective)  
  
-   [번역 개체](#Translation)  
  
-   [ProactiveCaching 개체](#ProactiveCaching)  
  
 다음 그림에서는 이 항목에 설명된 클래스의 관계를 보여 줍니다.  
  
 ![AMO의 OLAP 클래스](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-olapclasses.gif "AMO의 OLAP 클래스")  
  
## <a name="basic-classes"></a>기본 클래스  
  
###  <a name="Dimensions"></a> 차원 개체  
 부모 데이터베이스의 차원 컬렉션에 차원을 추가한 다음 Update 메서드를 사용하여 해당 <xref:Microsoft.AnalysisServices.Dimension> 개체를 서버로 업데이트하면 차원이 만들어집니다.  
  
 차원을 제거 하려면의 Drop 메서드를 사용 하 여 삭제 해야에 <xref:Microsoft.AnalysisServices.Dimension>합니다. Remove 메서드를 사용하여 데이터베이스의 차원 컬렉션에서 <xref:Microsoft.AnalysisServices.Dimension>을 제거하면 해당 차원이 서버에서는 삭제되지 않고 AMO 개체 모델에서만 삭제됩니다.  
  
 <xref:Microsoft.AnalysisServices.Dimension> 개체를 만든 후 이 개체를 처리할 수 있습니다. <xref:Microsoft.AnalysisServices.Dimension>은 해당 개체의 Process 메서드를 사용하여 처리하거나, 부모 개체가 처리될 때 부모 개체의 Process 메서드를 사용하여 처리할 수 있습니다.  
  
 사용할 수 있는 메서드 및 속성에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.Dimension>의 <xref:Microsoft.AnalysisServices>를 참조하십시오.  
  
###  <a name="Cubes"></a> 큐브 개체  
 부모 데이터베이스의 큐브 컬렉션에 큐브를 추가한 다음 Update 메서드를 사용하여 해당 <xref:Microsoft.AnalysisServices.Cube> 개체를 서버로 업데이트하면 큐브가 만들어집니다. 큐브의 Update 메서드에는 큐브의 수정된 모든 개체가 이 업데이트 동작을 통해 서버로 업데이트되도록 하는 UpdateOptions.ExpandFull 매개 변수가 포함될 수 있습니다.  
  
 큐브를 제거하려면 <xref:Microsoft.AnalysisServices.Cube>의 Drop 메서드를 사용하여 삭제해야 합니다. 컬렉션에서 큐브를 제거해도 서버에는 영향을 주지 않습니다.  
  
 <xref:Microsoft.AnalysisServices.Cube> 개체를 만든 후 이 개체를 처리할 수 있습니다. <xref:Microsoft.AnalysisServices.Cube>는 해당 개체의 Process 메서드를 사용하여 처리하거나, 부모 개체가 처리될 때 부모 개체의 Process 메서드를 사용하여 처리할 수 있습니다.  
  
 사용할 수 있는 메서드 및 속성에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.Cube>의 <xref:Microsoft.AnalysisServices>를 참조하십시오.  
  
###  <a name="MeasureGroups"></a> MeasureGroup 개체  
 큐브의 측정값 그룹 컬렉션에 측정값 그룹을 추가한 다음 Update 메서드를 사용하여 해당 <xref:Microsoft.AnalysisServices.MeasureGroup> 개체를 서버로 업데이트하면 측정값 그룹이 만들어집니다. <xref:Microsoft.AnalysisServices.MeasureGroup> 개체는 해당 개체의 Drop 메서드를 사용하여 제거할 수 있습니다.  
  
 <xref:Microsoft.AnalysisServices.MeasureGroup> 개체를 만든 후 이 개체를 처리할 수 있습니다. <xref:Microsoft.AnalysisServices.MeasureGroup>은 해당 개체의 Process 메서드를 사용하여 처리하거나, 부모 개체가 처리될 때 부모 개체의 Process 메서드를 사용하여 처리할 수 있습니다.  
  
 사용할 수 있는 메서드 및 속성에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.MeasureGroup>의 <xref:Microsoft.AnalysisServices>를 참조하십시오.  
  
###  <a name="Partition"></a> 파티션 개체  
 <xref:Microsoft.AnalysisServices.Partition> 개체를 부모 측정값 그룹의 파티션 컬렉션에 추가한 다음 Update 메서드를 사용하여 서버의 <xref:Microsoft.AnalysisServices.Partition> 개체를 업데이트하면 해당 개체가 만들어집니다. <xref:Microsoft.AnalysisServices.Partition> 개체는 Drop 메서드를 사용하여 제거할 수 있습니다.  
  
 사용할 수 있는 메서드 및 속성에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.Partition>의 <xref:Microsoft.AnalysisServices>를 참조하십시오.  
  
###  <a name="AggregationDesign"></a> AggregationDesign 개체  
 <xref:Microsoft.AnalysisServices.AggregationDesign> 개체에서 AggregationDesign 메서드를 사용하여 집계 디자인을 생성할 수 있습니다.  
  
 사용할 수 있는 메서드 및 속성에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.AggregationDesign>의 <xref:Microsoft.AnalysisServices>를 참조하십시오.  
  
###  <a name="Aggregation"></a> Aggregation 개체  
 <xref:Microsoft.AnalysisServices.Aggregation> 개체를 부모 측정값 그룹의 집계 디자인 컬렉션에 추가한 다음 Update 메서드를 사용하여 서버의 부모 측정값 그룹 개체를 업데이트하면 해당 개체가 만들어집니다. 집계는 Remove 메서드나 RemoveAt 메서드를 사용하여 <xref:Microsoft.AnalysisServices.AggregationCollection>에서 제거할 수 있습니다.  
  
 사용할 수 있는 메서드 및 속성에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.Aggregation>의 <xref:Microsoft.AnalysisServices>를 참조하십시오.  
  
## <a name="advanced-classes"></a>고급 클래스  
 고급 클래스에서는 큐브 작성 및 탐색 이외의 추가 OLAP 기능을 제공합니다. 다음 목록에서는 몇 가지 고급 클래스와 해당 클래스의 이점을 설명합니다.  
  
-   Action 클래스 - 큐브의 특정 영역을 탐색할 때 활성 응답을 만드는 데 사용됩니다.  
  
-   KPI 클래스 - KPI(핵심 성과 지표)는 데이터 값 간의 비교 분석을 가능하게 해 줍니다.  
  
-   Perspective 클래스 - 사용자가 자신에게 중요한 항목에 집중할 수 있도록 단일 큐브에 대한 선택된 뷰를 제공합니다.  
  
-   Translation 클래스 - 큐브를 사용자 로캘에 맞게 사용자 지정할 수 있도록 합니다.  
  
-   ProactiveCaching 클래스 - MOLAP 저장소의 뛰어난 성능과 ROLAP 저장소의 즉시성을 균형 있게 조정해 주며 일정에 따른 파티션 처리 기능을 제공합니다.  
  
 AMO는 이 향상된 동작에 대한 정의를 설정하는 데 사용되지만 실제 환경은 이러한 향상된 클래스를 모두 구현하는 탐색 클라이언트에 의해 정의됩니다.  
  
###  <a name="Action"></a> 동작 개체  
 <xref:Microsoft.AnalysisServices.Action> 개체를 큐브의 동작 컬렉션에 추가한 다음 Update 메서드를 사용하여 <xref:Microsoft.AnalysisServices.Cube> 개체를 서버로 업데이트하면 Action 개체가 만들어집니다. 큐브의 Update 메서드에는 큐브의 수정된 모든 개체가 이 업데이트 동작을 통해 서버로 업데이트되도록 하는 UpdateOptions.ExpandFull 매개 변수가 포함될 수 있습니다.  
  
 <xref:Microsoft.AnalysisServices.Action> 개체를 제거하려면 컬렉션에서 해당 개체를 제거한 후 부모 큐브를 업데이트해야 합니다.  
  
 해당 동작을 클라이언트에서 사용하려면 먼저 큐브를 업데이트하고 처리해야 합니다.  
  
 사용할 수 있는 메서드 및 속성에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.Action>의 <xref:Microsoft.AnalysisServices>를 참조하십시오.  
  
###  <a name="KPI"></a> Kpi 개체  
 <xref:Microsoft.AnalysisServices.Kpi> 개체를 큐브의 KPI 컬렉션에 추가한 다음 Update 메서드를 사용하여 <xref:Microsoft.AnalysisServices.Cube> 개체를 서버로 업데이트하면 Kpi 개체가 만들어집니다. 큐브의 Update 메서드에는 큐브의 수정된 모든 개체가 이 업데이트 동작을 통해 서버로 업데이트되도록 하는 UpdateOptions.ExpandFull 매개 변수가 포함될 수 있습니다.  
  
 <xref:Microsoft.AnalysisServices.Kpi> 개체를 제거하려면 컬렉션에서 해당 개체를 제거한 후 부모 큐브를 업데이트해야 합니다.  
  
 KPI를 사용하려면 먼저 큐브를 업데이트하고 처리해야 합니다.  
  
 사용할 수 있는 메서드 및 속성에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.Kpi>의 <xref:Microsoft.AnalysisServices>를 참조하십시오.  
  
###  <a name="Perspective"></a> Perspective 개체  
 <xref:Microsoft.AnalysisServices.Perspective> 개체를 큐브의 큐브 뷰 컬렉션에 추가한 다음 Update 메서드를 사용하여 해당 <xref:Microsoft.AnalysisServices.Cube> 개체를 서버로 업데이트하면 Perspective 개체가 만들어집니다. 큐브의 Update 메서드에는 큐브의 수정된 모든 개체가 이 업데이트 동작을 통해 서버로 업데이트되도록 하는 UpdateOptions.ExpandFull 매개 변수가 포함될 수 있습니다.  
  
 <xref:Microsoft.AnalysisServices.Perspective> 개체를 제거하려면 컬렉션에서 해당 개체를 제거한 후 부모 큐브를 업데이트해야 합니다.  
  
 큐브 뷰를 사용하려면 먼저 큐브를 업데이트하고 처리해야 합니다.  
  
 사용할 수 있는 메서드 및 속성에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.Perspective>의 <xref:Microsoft.AnalysisServices>를 참조하십시오.  
  
###  <a name="Translation"></a> 번역 개체  
 <xref:Microsoft.AnalysisServices.Translation> 개체를 원하는 개체의 번역 컬렉션에 추가한 다음 Update 메서드를 사용하여 가장 가까이 있는 주요 부모 개체를 서버로 업데이트하면 Translation 개체가 만들어집니다. 가장 가까이 있는 부모 개체의 Update 메서드에는 수정된 모든 자식 개체가 이 업데이트 동작을 통해 서버로 업데이트되도록 하는 UpdateOptions.ExpandFull 매개 변수가 포함될 수 있습니다.  
  
 <xref:Microsoft.AnalysisServices.Translation> 개체를 제거하려면 컬렉션에서 해당 개체를 제거한 후 가장 가까이 있는 부모 개체를 업데이트해야 합니다.  
  
 사용할 수 있는 메서드 및 속성에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.Translation>의 <xref:Microsoft.AnalysisServices>를 참조하십시오.  
  
###  <a name="ProactiveCaching"></a> ProactiveCaching 개체  
 차원 또는 파티션의 자동 관리 캐싱 개체 컬렉션에 <xref:Microsoft.AnalysisServices.ProactiveCaching> 개체를 추가한 다음 Update 메서드를 사용하여 차원 또는 파티션 개체를 서버로 업데이트하면 ProactiveCaching 개체가 만들어집니다.  
  
 <xref:Microsoft.AnalysisServices.ProactiveCaching> 개체를 제거하려면 컬렉션에서 해당 개체를 제거한 후 부모 개체를 업데이트해야 합니다.  
  
 자동 관리 캐싱을 사용하려면 먼저 차원 또는 파티션을 업데이트하고 처리해야 합니다.  
  
 사용할 수 있는 메서드 및 속성에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.ProactiveCaching>의 <xref:Microsoft.AnalysisServices>를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.AnalysisServices>   
 [AMO 클래스 소개](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO OLAP 기본 개체 프로그래밍](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-basic-objects.md)   
 [AMO OLAP 고급 개체 프로그래밍](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-advanced-objects.md)   
 [논리적 아키텍처 & #40; Analysis Services-다차원 데이터 & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [데이터베이스 개체 & #40; Analysis Services-다차원 데이터 & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
