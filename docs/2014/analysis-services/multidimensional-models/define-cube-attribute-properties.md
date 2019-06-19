---
title: 큐브 특성 속성 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], defining
ms.assetid: 579ca818-f33d-4060-906d-c8bfee93bf99
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6a6c5cb8c8ca0492edf9798f972b458054ae5b58
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075734"
---
# <a name="define-cube-attribute-properties"></a>큐브 특성 속성 정의
  큐브 특성 속성을 사용하면 같은 데이터베이스 차원을 기반으로 하는 큐브 차원의 차원 특성에 고유한 설정을 지정할 수 있습니다. 다음 표에서는 큐브 특성의 속성에 대해 설명합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|`AggregationUsage`|집계 디자인 마법사에서 특성의 집계를 디자인하는 방법을 지정합니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> `Default`: 기본. 집계 디자인 마법사에서 특성 유형을 기반으로 기본 규칙을 적용합니다(키의 경우 전체, 기타의 경우 제한 없음).<br /><br /> `None`: 큐브의 집계에 이 특성이 포함되지 않아야 합니다.<br /><br /> `Unrestricted`: 제한이 집계 디자인 마법사에 배치 됩니다.<br /><br /> `Full`: 큐브의 모든 집계에 이 특성이 포함되어야 합니다.|  
|`AttributeHierarchyEnabled`|이 큐브 차원에서 특성 계층을 사용할 수 있는지 여부를 나타냅니다. 이렇게 하면 특정 큐브나 차원 역할에 대해 특성 계층을 비활성화할 수 있습니다. 기본 특성 계층이 비활성화된 경우 이 설정은 적용되지 않습니다. 기본값은 `True`여야 합니다.|  
|`OptimizedState`|이 큐브 차원에서 특성 계층을 최적화할지 여부를 식별합니다. 이렇게 하면 특정 큐브 또는 차원 역할에서 특성 계층을 최적화할 수 있습니다. 기본 특성 계층이 최적화되지 않는 경우 이 설정은 적용되지 않습니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> `FullyOptimized`: 기본. 인스턴스에서 계층에 대해 인덱스를 작성하여 쿼리 성능을 향상시킵니다. 이것은 기본값입니다.<br /><br /> `NotOptimized`: 인스턴스에서 추가 인덱스를 작성하지 않습니다.|  
|`AttributeHierarchyVisible`|이 큐브 차원에서 특성 계층을 표시할지 여부를 식별합니다. 이렇게 하면 특정 큐브 또는 차원 역할에서 특성 계층을 표시할 수 있습니다. 기본 특성 계층이 표시되지 않는 경우 이 설정은 적용되지 않습니다. 기본값은 `True`입니다.|  
|`AttributeID`|특성의 고유 ID를 포함합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [큐브 차원 속성 정의](define-cube-dimension-properties.md)   
 [큐브 계층 속성 정의](define-cube-hierarchy-properties.md)  
  
  
