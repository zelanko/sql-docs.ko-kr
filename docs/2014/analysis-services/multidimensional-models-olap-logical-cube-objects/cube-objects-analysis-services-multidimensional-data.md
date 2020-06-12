---
title: Cube 개체 (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], objects
ms.assetid: 5cee362e-3f95-4467-bc6c-29b1518ecbf3
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0e6dfb75be696ab26893e668b99dc36c7340f86c
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545315"
---
# <a name="cube-objects-analysis-services---multidimensional-data"></a>큐브 개체(Analysis Services - 다차원 데이터)
    
## <a name="introducing-cube-objects"></a>큐브 개체 소개  
 단순 <xref:Microsoft.AnalysisServices.Cube> 개체는 기본 정보, 차원 및 측정값 그룹으로 구성 됩니다. 기본 정보에는 큐브의 이름, 큐브의 기본 측정값, 데이터 원본, 스토리지 모드 등이 포함됩니다.  
  
 Dimensions 컬렉션에는 데이터베이스 차원 컬렉션의 큐브에 사용되는 실제 차원 집합이 포함되어 있습니다. 모든 차원은 큐브에서 참조되기 전에 데이터베이스의 차원 컬렉션에 정의되어야 합니다. 전용 차원은에서 사용할 수 없습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 측정값 그룹은 큐브에 있는 측정값의 집합으로, 공용 데이터 원본 뷰와 차원의 공통 집합이 있는 측정값의 컬렉션입니다. 측정값 그룹은 측정값의 처리 단위이므로 개별적으로 처리하고 검색할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|||  
|-|-|  
|항목||  
|[동작&#40;Analysis Services - 다차원 데이터&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[Aggregations and Aggregation Designs](aggregations-and-aggregation-designs.md)||  
|[계산](calculations.md)||  
|[큐브 셀 Analysis Services 다차원 데이터를 &#40;&#41;](cube-cells-analysis-services-multidimensional-data.md)||  
|[큐브 속성](cube-properties-multidimensional-model-programming.md)||  
|[큐브 저장소 &#40;Analysis Services 다차원 데이터&#41;](cube-storage-analysis-services-multidimensional-data.md)||  
|[큐브 번역](cube-translations.md)||  
|[차원 관계](dimension-relationships.md)||  
|[다차원 모델의 KPI&#40;핵심 성과 지표&#41;](../multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[측정값 및 측정값 그룹](../multidimensional-models/measures-and-measure-groups.md)||  
|[파티션&#40;Analysis Services - 다차원 데이터&#41;](partitions-analysis-services-multidimensional-data.md)||  
|[큐브 뷰](perspectives.md)||  
  
  
