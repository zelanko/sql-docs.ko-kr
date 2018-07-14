---
title: AMO 데이터 마이닝 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data mining [AMO]
- AMO, data mining
- Analysis Management Objects, data mining
ms.assetid: e4108825-b722-417c-9647-ab30ce35e549
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dbea4d55066e2de5061d75c2b40092b84e8008ba
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171644"
---
# <a name="amo-data-mining-classes"></a>AMO 데이터 마이닝 클래스
  데이터 마이닝 클래스는 데이터 마이닝 개체를 만들고, 수정하고, 삭제하고, 처리하는 데 사용됩니다. 데이터 마이닝 개체 작업에는 데이터 마이닝 구조 만들기, 데이터 마이닝 모델을 만들기 및 모델 처리가 포함됩니다.  
  
 및에 대 한 환경을 설정 하는 방법에 대 한 자세한 내용은 <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource>, 및 <xref:Microsoft.AnalysisServices.DataSourceView> 개체를 참조 하십시오 [AMO 기본 클래스](amo-fundamental-classes.md)합니다.  
  
 AMO(Analysis Management Objects)에서 개체를 정의하려면 올바른 컨텍스트를 설정하도록 각 개체에 대해 여러 속성을 설정해야 합니다. OLAP 및 데이터 마이닝 개체와 같이 복잡한 개체는 길고 세부적인 코드 작업이 필요합니다.  
  
  
 다음 그림에서는 이 항목에 설명된 클래스의 관계를 보여 줍니다.  
  
 ![AMO 데이터 마이닝 클래스](../../../analysis-services/dev-guide/media/amo-dataminingclasses.gif "AMO 데이터 마이닝 클래스")  
  
##  <a name="MiningStructure"></a> MiningStructure 개체  
 마이닝 구조는 마이닝 모델의 컨테이너입니다. 이 구조에는 마이닝 모델에서 사용 가능한 열이 모두 정의되어 있습니다. 각 마이닝 모델에는 구조에 정의된 열 집합의 고유한 열이 정의되어 있습니다.  
  
 단순 <xref:Microsoft.AnalysisServices.MiningStructure> 개체는 기본 정보, 데이터 원본 뷰, 하나 이상의 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>, 0개 이상의 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 및 <xref:Microsoft.AnalysisServices.MiningModelCollection>으로 구성되어 있습니다.  
  
 기본 정보에는 <xref:Microsoft.AnalysisServices.MiningStructure> 개체의 이름 및 ID(내부 식별자)가 포함됩니다.  
  
 <xref:Microsoft.AnalysisServices.DataSourceView> 개체는 마이닝 구조의 기본 데이터 모델을 유지합니다.  
  
 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>은 단일 값을 가지는 열 또는 특성입니다.  
  
 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>은 각 사례에 대한 여러 값을 가지는 열 또는 특성입니다.  
  
 <xref:Microsoft.AnalysisServices.MiningModelCollection>에는 동일한 데이터를 기반으로 작성된 모든 마이닝 모델이 포함됩니다.  
  
 <xref:Microsoft.AnalysisServices.MiningStructure> 개체를 데이터베이스의 <xref:Microsoft.AnalysisServices.MiningStructureCollection>에 추가한 다음 Update 메서드를 사용하여 서버로 업데이트하면 <xref:Microsoft.AnalysisServices.MiningStructure> 개체가 만들어집니다.  
  
 <xref:Microsoft.AnalysisServices.MiningStructure> 개체를 제거하려면 <xref:Microsoft.AnalysisServices.MiningStructure> 개체의 Drop 메서드를 사용하여 삭제해야 합니다. 컬렉션에서 <xref:Microsoft.AnalysisServices.MiningStructure> 개체를 제거해도 서버에는 영향을 주지 않습니다.  
  
 <xref:Microsoft.AnalysisServices.MiningStructure>는 고유 프로세스 메서드를 사용하여 처리될 수 있으며, 부모 개체에서 고유 프로세스 메서드를 사용하여 자체적으로 처리할 때 처리될 수도 있습니다.  
  
### <a name="columns"></a>열  
 열 모델에 대 한 데이터를 저장 및 사용에 따라 다른 유형일 수 있습니다: 키, 입력, 예측 가능, 또는 InputPredictable 합니다. Predictable 열은 마이닝 모델의 작성 대상입니다.  
  
 AMO에서 단일 값 열은 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>이라고 합니다. 여러 값 열은 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>이라고 합니다.  
  
#### <a name="scalarminingstructurecolumn"></a>ScalarMiningStructureColumn  
 단순 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn> 개체는 기본 정보, 형식, 내용 및 데이터 바인딩으로 구성되어 있습니다.  
  
 기본 정보에는 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>의 이름 및 ID(내부 식별자)가 포함됩니다.  
  
 값의 데이터 형식: LONG, BOOLEAN, 텍스트, DOUBLE 날짜입니다.  
  
 엔진은 내용을 통해 열의 모델링 방법을 알 수 있습니다. 값은: 불연속, Continuous, Discretized, 정렬, Cyclical, 확률, Variance, StdDev은 ProbabilityVariance, ProbabilityStdDev, 지원, 키입니다.  
  
 데이터 바인딩은 데이터 원본 뷰 요소를 사용하여 데이터 마이닝 열을 기본 데이터 모델과 연결합니다.  
  
 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>을 부모 <xref:Microsoft.AnalysisServices.MiningStructureCollection>에 추가한 다음 Update 메서드를 사용하여 부모 <xref:Microsoft.AnalysisServices.MiningStructure> 개체를 서버로 업데이트하면 해당 개체가 만들어집니다.  
  
 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>을 제거하려면 부모 <xref:Microsoft.AnalysisServices.MiningStructure>의 컬렉션에서 해당 개체를 제거한 후 Update 메서드를 사용하여 부모 <xref:Microsoft.AnalysisServices.MiningStructure> 개체를 서버로 업데이트해야 합니다.  
  
#### <a name="tableminingstructurecolumn"></a>TableMiningStructureColumn  
 단순 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 개체는 기본 정보 및 스칼라 열로 구성되어 있습니다.  
  
 기본 정보에는 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>의 이름 및 ID(내부 식별자)가 포함됩니다.  
  
 스칼라 열은 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>입니다.  
  
 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>을 부모 <xref:Microsoft.AnalysisServices.MiningStructure> 컬렉션에 추가한 다음 Update 메서드를 사용하여 부모 <xref:Microsoft.AnalysisServices.TableMiningStructureColumn> 개체를 서버로 업데이트하면 해당 개체가 만들어집니다.  
  
 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>을 제거하려면 부모 <xref:Microsoft.AnalysisServices.MiningStructure>의 컬렉션에서 해당 개체를 제거한 후 Update 메서드를 사용하여 부모 <xref:Microsoft.AnalysisServices.MiningStructure> 개체를 서버로 업데이트해야 합니다.  
  
##  <a name="MiningModel"></a> MiningModel 개체  
 <xref:Microsoft.AnalysisServices.MiningModel>은 사용할 구조의 열, 사용할 알고리즘 및 모델을 조정하는 특정 매개 변수(옵션)를 선택할 수 있는 개체입니다. 예를 들어, 동일한 알고리즘을 사용하는 동일한 마이닝 구조의 여러 마이닝 모델을 정의해야 할 수 있습니다. 한 모델에 있는 마이닝 구조의 일부 열을 무시하려면 해당 열을 다른 모델에서 입력으로 사용하고 세 번째 모델에서 입력 및 예측으로 사용합니다. 이 방법은 한 마이닝 모델에서는 열을 연속 열로 처리하고 다른 모델에서는 열을 불연속화 열로 처리하는 경우에 유용합니다.  
  
 단순 <xref:Microsoft.AnalysisServices.MiningModel> 개체는 기본 정보, 알고리즘 정의 및 열로 구성되어 있습니다.  
  
 기본 정보에는 마이닝 모델의 이름 및 ID(내부 식별자)가 포함됩니다.  
  
 알고리즘 정의는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 제공하는 표준 알고리즘 또는 서버에 설정된 사용자 지정 알고리즘을 참조합니다.  
  
 열은 알고리즘 및 용도 정의에 따라 사용되는 열의 컬렉션입니다.  
  
 <xref:Microsoft.AnalysisServices.MiningModel> 개체를 데이터베이스의 <xref:Microsoft.AnalysisServices.MiningModelCollection>에 추가한 다음 Update 메서드를 사용하여 서버로 업데이트하면 <xref:Microsoft.AnalysisServices.MiningModel>이 만들어집니다.  
  
 <xref:Microsoft.AnalysisServices.MiningModel>을 제거하려면 <xref:Microsoft.AnalysisServices.MiningModel>의 Drop 메서드를 사용하여 삭제해야 합니다. 컬렉션에서 <xref:Microsoft.AnalysisServices.MiningModel>을 제거해도 서버에는 영향을 주지 않습니다.  
  
 <xref:Microsoft.AnalysisServices.MiningModel>은 만들어진 후 고유 프로세스 메서드를 사용하여 처리될 수 있으며, 부모 개체가 고유 프로세스 메서드를 사용하여 자체적으로 처리할 때 처리될 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.AnalysisServices>   
 [AMO 기본 클래스](amo-fundamental-classes.md)   
 [AMO 데이터 마이닝 개체 프로그래밍](programming-amo-data-mining-objects.md)   
 [AMO 클래스 소개](amo-classes-introduction.md)   
 [논리적 아키텍처 &#40;Analysis Services-다차원 데이터&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [데이터베이스 개체 &#40;Analysis Services-다차원 데이터&#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
