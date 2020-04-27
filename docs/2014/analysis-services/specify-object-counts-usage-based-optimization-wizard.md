---
title: 개체 수 지정 (사용 빈도 기반 최적화 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.calculatingobjectcounts.f1
ms.assetid: 306c7c25-ae24-4852-ab8c-c82f68a4bc1f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e0503192c3c948110f8301c8eb375e1c8203e42f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66068243"
---
# <a name="specify-object-counts-usage-based-optimization-wizard"></a>개체 수 지정(사용 빈도 기반 최적화 마법사)
  **개체 수 지정** 페이지를 사용하여 큐브의 개체 수를 자동으로 계산하거나 예상 개수를 직접 입력할 수 있습니다. 사용 빈도 기반 최적화 마법사는 개체 수를 사용하여 스토리지 요구 사항을 예상합니다.  
  
## <a name="options"></a>옵션  
 **큐브 개체**  
 큐브의 차원 및 특성을 표시합니다. 마법사의 **집계 사용 검토** 페이지에서 해당 `AggregationUsage` 속성이 None으로 설정 되지 않은 특성만 표시 됩니다 .이 특성은 개수를 지정 해야 하기 때문입니다.  
  
 **예상 개수**  
 측정값 그룹의 예상 행 수와 데이터베이스 차원의 예상 특성 멤버 수를 표시합니다. 예상 개수로 사용할 값을 입력하거나 예상 개수 값을 계산할 수 있습니다. 개수 값을 계산하려면 필드에 0 을 입력한 다음 **개수**를 클릭합니다. 이미 수가 표시된 필드는 업데이트되지 않습니다.  
  
 **파티션 수**  
 (옵션) 측정값 그룹의 예상 행 수와 파티션의 예상 특성 멤버 수를 입력합니다.  
  
 **Count**  
 모든 빈 필드에 대해 **예상 개수** 열의 값을 계산하고 다시 채웁니다. 이미 수가 표시된 필드는 업데이트되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [집계 디자인 마법사 F1 도움말](aggregation-design-wizard-f1-help.md)   
 [다차원 데이터를 &#40;마법사 Analysis Services&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
