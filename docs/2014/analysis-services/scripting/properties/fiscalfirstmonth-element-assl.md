---
title: FiscalFirstMonth 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- FiscalFirstMonth Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- FiscalFirstMonth
helpviewer_keywords:
- FiscalFirstMonth element
ms.assetid: 30766baa-ebec-4425-93de-7defe4d6e571
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c5c54a8d4b93b380c4289a03266c6d27bd4d2b40
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197781"
---
# <a name="fiscalfirstmonth-element-assl"></a>FiscalFirstMonth 요소(ASSL)
  에 대 한 회계 기간의 첫 번째 월을 정의 [TimeBinding](../data-type/binding-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<TimeBinding>  
   ...  
   <FiscalFirstMonth>...</FiscalFirstMonth>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Integer(1부터 12까지, 여기서 1은 1월이고 12는 12월)|  
|기본값|`1`|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[TimeBinding](../data-type/binding-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 하는 요소가 `FiscalFirstMonth` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.TimeBinding>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
