---
title: "큐브 계층 속성 정의 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], cubes
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 69781dd1476cd0396e748be0ddf91fd4dd0bb0dc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="define-cube-hierarchy-properties"></a>큐브 계층 속성 정의
  큐브 계층 속성을 통해 동일한 데이터베이스 차원에 기반을 두는 큐브 차원의 사용자 정의 계층에 대해 고유한 설정을 지정할 수 있습니다. 다음 표에서는 큐브 계층의 속성을 설명합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**설정**|큐브 차원에 대해 계층이 설정되는지 여부를 결정합니다.|  
|**HierarchyID**|계층의 고유 ID를 포함합니다.|  
|**OptimizedState**|계층에 적용되는 최적화 수준을 결정합니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **FullyOptimized**:<br />                    인스턴스에서 계층에 대해 인덱스를 작성하여 쿼리 성능을 향상시킵니다. 이 값은 기본값입니다.<br /><br /> **NotOptimized**:<br />                    인스턴스에서 추가 인덱스를 작성하지 않습니다.|  
|**Visible**|큐브 계층의 표시 유형을 결정합니다. 기본값은 **True**입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [사용자 계층](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  

