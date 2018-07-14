---
title: 집계 (Analysis Services-다차원) 디자인 | Microsoft Docs
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
- aggregations [Analysis Services], partitions
- partitions [Analysis Services], aggregations
ms.assetid: 3072b7e0-6961-42ad-a287-16f391f2cec4
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aae25fb906eed7f31578070e2327a9caf4c7b66c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37224723"
---
# <a name="designing-aggregations-analysis-services---multidimensional"></a>집계 디자인(Analysis Services - 다차원)
  집계는 큐브 데이터의 미리 계산된 요약으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 신속한 쿼리 응답을 제공할 수 있도록 도와 줍니다.  
  
 집계 디자인 마법사를 사용하여 파티션에 대한 저장소 옵션을 설정하고 집계를 디자인할 수 있습니다. 이 마법사는 한 번에 개별 측정값 그룹의 단일 파티션에 대해 실행되므로 각 파티션마다 다른 옵션과 디자인을 선택할 수 있습니다. 저장소 디자인 마법사는 파티션에 대한 저장소를 구성하고 집계를 디자인하는 단계로 이루어져 있습니다. 저장소를 구성하는 방법에 대한 자세한 내용은 다음을 참조하십시오.  
  
 마법사가 디자인할 집계 수의 제어 방법을 선택한 다음 마법사가 집계를 디자인하게 둡니다.  
  
 여기서 목표는 최적의 집계 수를 디자인하는 것입니다. 최적의 집계 수란 응답 시간을 빠르게 할 뿐만 아니라 파티션 크기가 필요 이상으로 커지는 것도 막을 수 있어야 합니다. 집계 수가 커질수록 응답 속도는 빨라지지만 그에 따라 저장소 공간도 많이 필요하고 계산하는 데 시간이 오래 걸릴 수 있습니다. 뿐만 아니라 마법사가 점점 더 많은 집계를 디자인함에 따라 후반 집계보다 초반 집계에서 훨씬 많은 성능 향상이 이루어집니다. 자주 사용하지 않는 집계를 줄이면 성능이 향상됩니다. 마법사에서 사용할 수 있는 다음과 같은 방법 중 하나를 사용하면 마법사가 디자인하는 집계 수를 제어할 수 있습니다.  
  
-   집계에 대한 저장소 공간 제한을 지정합니다.  
  
-   성능 향상 제한을 지정합니다.  
  
-   표시된 성능 대 크기 곡선이 적정 성능 향상 수준에서 평행을 이루기 시작하면 마법사를 수동으로 중지합니다.  
  
-   집계를 디자인하지 않도록 선택합니다.  
  
 저장소를 디자인하려면 마법사가 대상 서버의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 연결할 수 있어야 합니다. 대상 서버에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 실행하고 있지 않거나 저장소 디자인 프로세스에서 대상 서버에 연결할 수 없는 경우 오류 메시지가 표시됩니다.  
  
 마법사의 마지막 단계에서는 처리를 시작하거나 지연할 수 있습니다. 처리하는 경우에는 마법사로 디자인한 집계가 생성되며, 연기하는 경우에는 디자인된 집계를 나중에 처리할 수 있도록 저장하여 처리 과정 없이 디자인 동작을 계속할 수 있습니다. 파티션 크기에 따라 처리 시간이 오래 걸릴 수도 있습니다. 필요한 경우 파티션 처리를 중단할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [집계 및 집계 디자인](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
