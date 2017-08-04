---
title: "&gt;(보다 큼) (DMX) | Microsoft Docs"
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
- greater than operator (>)
- '> (greater than operator)'
ms.assetid: a1485c02-8d10-4722-b8cd-b747c472741b
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 515b8b3dfe8f08b57adaadb6e945baa0a685e38a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="gt-greater-than-dmx"></a>&gt;(보다 큼) (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>관련 항목:  
 [비교 연산자 &#40; DMX &#41;](../dmx/operators-comparison.md)   
 [Data Mining Extensions &#40; DMX &#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [연산자 &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

