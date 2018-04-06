---
title: Alias 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Alias Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Alias
helpviewer_keywords:
- Alias element
ms.assetid: 674fdb06-e33c-4f35-bd6a-d9bbb13ececa
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ead0aae5b918d3803eeefcfd92005f0354a45bd8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="alias-element-assl"></a>Alias 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]에 대 한 별칭을 정의 [계정](../../../analysis-services/scripting/objects/account-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Aliases>  
      <Alias>...</Alias>  
</Aliases>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[별칭](../../../analysis-services/scripting/collections/aliases-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 **Alias** 요소의 값은 **Account** 부모 요소에 의해 정의되는 계정의 대체 이름으로 사용되며 사용자 인터페이스에서 계정 유형과 집계 함수의 조합을 식별하는 데 도움이 됩니다.  
  
 부모에 해당 하는 요소는 **별칭** Analysis Management Objects (AMO) 개체 모델에서 컬렉션은 <xref:Microsoft.AnalysisServices.Account>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
