---
title: "큐브 개체 (Analysis Services-다차원 데이터) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- cubes [Analysis Services], objects
ms.assetid: 5cee362e-3f95-4467-bc6c-29b1518ecbf3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 018739c4f8da237c1a90a101b96888a8583349be
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="cube-objects-analysis-services---multidimensional-data"></a>큐브 개체(Analysis Services - 다차원 데이터)
    
## <a name="introducing-cube-objects"></a>큐브 개체 소개  
 간단한 <xref:Microsoft.AnalysisServices.Cube> 개체를 구성: 기본 정보, 차원 및 측정값 그룹입니다. 기본 정보에는 큐브의 이름, 큐브의 기본 측정값, 데이터 원본, 저장소 모드 등이 포함됩니다.  
  
 Dimensions 컬렉션에는 데이터베이스 차원 컬렉션의 큐브에 사용되는 실제 차원 집합이 포함되어 있습니다. 모든 차원은 큐브에서 참조되기 전에 데이터베이스의 차원 컬렉션에 정의되어야 합니다. 사용할 수 없는 개인 차원을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다.  
  
 측정값 그룹은 큐브에 있는 측정값의 집합으로, 공용 데이터 원본 뷰와 차원의 공통 집합이 있는 측정값의 컬렉션입니다. 측정값 그룹은 측정값의 처리 단위이므로 개별적으로 처리하고 검색할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|||  
|-|-|  
|항목||  
|[동작&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[집계 및 집계 디자인](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)||  
|[계산](../../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)||  
|[큐브 셀 &#40; Analysis Services-다차원 데이터 &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-cells-analysis-services-multidimensional-data.md)||  
|[큐브 속성-다차원 모델 프로그래밍](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-properties-multidimensional-model-programming.md)||  
|[큐브 저장소 &#40; Analysis Services-다차원 데이터 &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)||  
|[큐브 번역](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md)||  
|[차원 관계](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)||  
|[다차원 모델의 KPI&#40;핵심 성과 지표&#41;](../../analysis-services/multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[측정값 및 측정값 그룹](../../analysis-services/multidimensional-models/measures-and-measure-groups.md)||  
|[파티션&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)||  
|[큐브 뷰](../../analysis-services/multidimensional-models-olap-logical-cube-objects/perspectives.md)||  
  
  

