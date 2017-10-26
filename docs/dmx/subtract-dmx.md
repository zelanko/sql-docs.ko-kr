---
title: "- (빼기) (DMX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
ms.assetid: 9602e908-e80c-442a-a412-073e10d0abd4
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6385e939f6dcf1881b86d9aa20d7f8e6c04aceb4
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="--subtract-dmx"></a>-(빼기)(DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  한 수에서 다른 수를 빼는 산술 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Numeric_Expression - Numeric_Expression  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Numeric_Expression*  
 숫자 값을 반환하는 유효한 DMX(Data Mining Extensions) 식입니다.  
  
## <a name="return-value"></a>반환 값  
 우선 순위가 더 높은 매개 변수의 데이터 형식을 갖는 값입니다.  
  
## <a name="remarks"></a>주의  
 두 식이 모두 동일한 데이터 형식으로 되어 있거나 식 하나가 암시적으로 다른 식의 데이터 형식으로 변환될 수 있어야 합니다. 한 식이 Null 값으로 계산되는 경우 이 연산자는 다른 식의 결과를 반환합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [산술 연산자 &#40; DMX &#41;](../dmx/operators-arithmetic.md)   
 [Data Mining Extensions &#40; DMX &#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [연산자 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

