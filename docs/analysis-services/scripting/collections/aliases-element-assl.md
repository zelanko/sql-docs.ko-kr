---
title: Aliases 요소 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2ecac1cba39971411af3fe18a6ead9fd4e8a3ea8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="aliases-element-assl"></a>Aliases 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  컬렉션을 포함 [별칭](../../../analysis-services/scripting/properties/alias-element-assl.md) 와 관련 된 요소는 [계정](../../../analysis-services/scripting/objects/account-element-assl.md) 요소  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Account>  
      ...  
   <Aliases>  
      <Alias>...</Alias>  
      </Aliases>  
      ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음(컬렉션)|  
|기본값|없음(컬렉션)|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[계정](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|자식 요소|[별칭](../../../analysis-services/scripting/properties/alias-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **별칭** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Account>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [요소 계정 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [Database 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [컬렉션 & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
