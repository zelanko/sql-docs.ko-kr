---
title: 큐브 계층 속성 정의 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 65cd9ae51a89e32c85b46da0c8f14f0c9a593976
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209000"
---
# <a name="define-cube-hierarchy-properties"></a>큐브 계층 속성 정의
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  큐브 계층 속성을 통해 동일한 데이터베이스 차원에 기반을 두는 큐브 차원의 사용자 정의 계층에 대해 고유한 설정을 지정할 수 있습니다. 다음 표에서는 큐브 계층의 속성을 설명합니다.  
  
|속성|설명|  
|--------------|-----------------|  
|**Enabled**|큐브 차원에 대해 계층이 설정되는지 여부를 결정합니다.|  
|**HierarchyID**|계층의 고유 ID를 포함합니다.|  
|**OptimizedState**|계층에 적용되는 최적화 수준을 결정합니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **FullyOptimized**:<br />                    인스턴스에서 계층에 대해 인덱스를 작성하여 쿼리 성능을 향상시킵니다. 이것은 기본값입니다.<br /><br /> **NotOptimized**:<br />                    인스턴스에서 추가 인덱스를 작성하지 않습니다.|  
|**Visible**|큐브 계층의 표시 유형을 결정합니다. 기본값은 **True**입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [사용자 계층](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
