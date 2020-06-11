---
title: '&lt;(보다 작음) (DMX) | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e5cc8429a2fb61b6f7f94b45874ee89968c8be4e
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670356"
---
# <a name="lt-less-than-dmx"></a>&lt;(보다 작음) DMX
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  하나의 DMX(Data Mining Extensions) 식의 값이 다른 DMX 식의 값보다 작은지 확인하는 비교 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DMX_Expression < DMX_Expression  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DMX_Expression*  
 유효한 DMX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 두 매개 변수가 모두 Null이 아니고 첫 번째 매개 변수 값이 두 번째 매개 변수 값보다 작을 경우 부울 값에 TRUE가 포함됩니다. 두 매개 변수가 모두 Null이 아니고 첫 번째 매개 변수 값이 두 번째 매개 변수 값보다 크거나 같을 경우 부울 값에 FALSE가 포함됩니다. 매개 변수 중 하나 또는 둘 모두가 Null 값으로 계산되면 부울 값에 Null 값이 포함됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [DMX&#41;&#40;비교 연산자](../dmx/operators-comparison.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
