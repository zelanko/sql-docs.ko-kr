---
title: "데이터 수정 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
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
- modifying data [MDX]
- Multidimensional Expressions [Analysis Services], data modifications
- MDX [Analysis Services], data modifications
- data modifications [MDX]
ms.assetid: 363b662c-b839-4971-bbd7-1842f73ce141
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 63268d2f905d91833ad1ec542d0db78ab7b921cf
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-data-modification---modifying-data"></a>MDX 데이터 수정-데이터 수정
  MDX를 사용하여 차원과 큐브의 데이터를 검색하고 처리하는 방법 외에도, MDX를 사용하여 차원과 큐브 데이터를 업데이트하거나 *쓰기 저장* 할 수 있습니다. 이 업데이트는 이론적 분석이나 "가정(what if)" 분석에서와 같이 임시적이거나 데이터 분석을 기반으로 변화가 발생해야 하는 때와 같이 영구적일 수 있습니다.  
  
 데이터에 대한 업데이트는 차원 또는 큐브 수준에서 발생할 수 있습니다.  
  
 **차원 쓰기 저장**  
 쓰기 가능한 차원의 데이터를 변경하려면 [ALTER CUBE 문(MDX)](../../../mdx/mdx-data-definition-alter-cube.md) 을 사용하고, 특성 값의 삭제, 생성 및 업데이트를 반영하려면 [REFRESH CUBE 문(MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) 을 사용합니다. ALTER CUBE 문을 사용하여 계층의 전체 하위 트리를 삭제하고 삭제된 멤버의 자식을 승격시키는 것과 같은 복잡한 연산을 수행할 수도 있습니다.  
  
 **큐브 쓰기 저장**  
 쓰기 가능한 큐브를 업데이트하려면 [UPDATE CUBE](../../../mdx/mdx-data-manipulation-update-cube.md) 문을 사용합니다. UPDATE CUBE 문을 사용하여 특정 값을 가진 튜플을 업데이트할 수 있습니다. 서버의 업데이트된 데이터로 클라이언트 세션의 데이터를 새로 고치려면 [REFRESH CUBE 문(MDX)](../../../mdx/mdx-data-definition-refresh-cube.md)을 사용합니다.  
  
 자세한 내용은 [큐브 쓰기 저장 사용&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-using-cube-writebacks.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 쿼리 기본 사항&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
