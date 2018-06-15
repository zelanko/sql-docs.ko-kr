---
title: DefaultScript 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e21b89833edf744a6e47474e9c438be74530479c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34034194"
---
# <a name="defaultscript-element-assl"></a>DefaultScript 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  기본값을 식별 [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) 요소에는 [MdxScripts](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md) 컬렉션입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MdxScript>  
   ...  
   <DefaultScript>...</DefaultScript>  
   ...  
</MdxScript>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|**True**|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 한 스크립트에 대해 **DefaultScript** 의 값을 **True** 로 설정하면 **DefaultScript** 컬렉션의 다른 모든 **False** 요소에 대해 **MdxScript** 의 값이 **MdxScripts** 로 설정됩니다.  
  
 부모에 해당 하는 요소 **DefaultScript** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MdxScript>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
