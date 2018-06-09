---
title: '&gt; (보다 큼) (DMX) | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 17c48c5321a0eef25a7fdf3ad0fba5aa643398d4
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842866"
---
# <a name="gt-greater-than-dmx"></a>&gt; (보다 큼) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  DMX(Data Mining Extensions) 식의 값이 다른 DMX 식의 값보다 큰지 확인하는 비교 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DMX_Expression > DMX_Expression  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DMX_Expression*  
 유효한 DMX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 두 매개 변수가 Null이 아니고 첫 번째 매개 변수 값이 두 번째 매개 변수 값보다 크면 부울 값에 TRUE가 포함됩니다. 두 매개 변수가 Null이 아니고 첫 번째 매개 변수 값이 두 번째 매개 변수 값보다 작거나 같으면 부울 값에 FALSE가 포함됩니다. 매개 변수 중 하나 또는 둘 모두가 Null 값으로 계산되면 부울 값에 Null 값이 포함됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [비교 연산자 &#40;DMX&#41;](../dmx/operators-comparison.md)   
 [Data Mining Extensions &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [연산자 &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
