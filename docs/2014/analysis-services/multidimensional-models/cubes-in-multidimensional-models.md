---
title: 다차원 모델의 큐브 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLAP objects [Analysis Services], cubes
- cubes [Analysis Services], about cubes
- cubes [Analysis Services]
- OLAP [Analysis Services], cubes
ms.assetid: e0f7acf3-4b07-41fc-a5fc-ac30b4a56c54
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca5da5ea8dfb22adc6e038f9dc54740e5102aad0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237733"
---
# <a name="cubes-in-multidimensional-models"></a>다차원 모델의 큐브
  큐브는 분석 목적의 정보를 포함하는 다차원 구조이며, 큐브의 주요 구성 요소는 차원과 측정값입니다. 차원은 조각화 및 분석에 사용할 큐브의 구조를 정의하고, 측정값은 최종 사용자에게 의미가 있는 집계된 숫자 값을 제공합니다. 논리적 구조인 큐브를 사용하면 클라이언트 응용 프로그램에서는 마치 값이 큐브의 셀에 포함되어 있고 가능한 모든 요약된 값에 대해 셀이 정의되어 있는 것처럼 측정값의 값을 검색할 수 있습니다. 큐브의 셀은 차원 멤버의 교차에 의해 정의되며 해당 특정 교차 지점에 있는 측정값의 집계된 값을 포함합니다.  
  
## <a name="benefits-of-using-cubes"></a>큐브 사용의 이점  
 큐브를 사용하면 분석을 위한 모든 관련 데이터를 한 곳에 저장할 수 있습니다.  
  
## <a name="components-of-cubes"></a>큐브의 구성 요소  
 큐브는 다음 요소로 구성됩니다.  
  
|요소|Description|  
|-------------|-----------------|  
|차원|[다차원 모델의 차원](dimensions-in-multidimensional-models.md)|  
|측정값 및 측정값 그룹|[다차원 모델의 측정값 및 측정값 그룹 만들기](create-measures-and-measure-groups-in-multidimensional-models.md)|  
|파티션|[다차원 모델의 파티션](partitions-in-multidimensional-models.md)|  
|큐브 뷰|[다차원 모델의 큐브 뷰](perspectives-in-multidimensional-models.md)|  
|계층 구조|[사용자 정의 계층 만들기](user-defined-hierarchies-create.md)|  
|동작|[다차원 모델의 동작](actions-in-multidimensional-models.md)|  
|KPI(핵심 성과 지표)|[핵심 성과 지표 &#40;Kpi&#41; 다차원 모델의](key-performance-indicators-kpis-in-multidimensional-models.md)|  
|새 명명된 집합|[다차원 모델의 계산](calculations-in-multidimensional-models.md)|  
|Translations|[다차원 모델의 번역](translations-in-multidimensional-models-analysis-services.md)|  
  
## <a name="related-tasks"></a>관련 작업  
  
|항목|Description|  
|-----------|-----------------|  
|[큐브 마법사를 사용하여 큐브 만들기](create-a-cube-using-the-cube-wizard.md)|큐브 마법사를 사용하여 큐브, 차원, 차원 특성 및 사용자 정의 계층을 정의하는 방법에 대해 설명합니다.|  
|[다차원 모델의 측정값 및 측정값 그룹 만들기](create-measures-and-measure-groups-in-multidimensional-models.md)|측정값 그룹을 정의하는 방법에 대해 설명합니다.|  
|[다차원 모델의 계산](calculations-in-multidimensional-models.md)|MDX 스크립트에서 계산을 정의 및 구성하는 방법에 대해 설명합니다.|  
|[다차원 모델의 동작](actions-in-multidimensional-models.md)|동작을 정의 및 구성하는 방법에 대해 설명합니다.|  
|[다차원 모델의 큐브 뷰](perspectives-in-multidimensional-models.md)|큐브 뷰를 정의 및 구성하는 방법에 대해 설명합니다.|  
|[저장 프로시저 정의](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)|저장 프로시저 작업 방법에 대해 설명합니다.|  
  
  
