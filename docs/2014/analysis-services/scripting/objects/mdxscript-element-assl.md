---
title: MdxScript 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MdxScript Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MdxScript
helpviewer_keywords:
- MdxScript element
ms.assetid: 0c59a550-dc95-4d50-948a-bb99348bdd86
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f1e138b4112a96bc6cdd5e08af0dbd0941a422d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106533"
---
# <a name="mdxscript-element-assl"></a>MdxScript 요소(ASSL)
  연결 된 MDX (Multidimensional Expressions) 스크립트에 대 한 정보를 포함 한 [큐브](cube-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MdxScripts>  
   <MdxScript>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Annotations>...</Annotations>  
      <Commands>...</Commands>  
      <DefaultScript>...</DefaultScript>  
      <CalculationProperties>...</CalculationProperties>  
   </MdxScript>  
</MdxScripts>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MdxScripts](../collections/mdxscripts-element-assl.md)|  
|자식 요소|[주석을](../collections/annotations-element-assl.md), [CalculationProperties](../collections/calculationproperties-element-assl.md), [명령](../collections/commands-element-assl.md)를 [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)를 [DefaultScript](../properties/defaultscript-element-assl.md)를 [설명](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md)하십시오 [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [이름](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 스크립트의 `DefaultScript` 요소는 기본적으로 `True`로 설정됩니다. 특정 스크립트에 대해 `DefaultScript`를 `True`로 설정하면 다른 모든 스크립트에 대해 `DefaultScript`가 `False`로 설정됩니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.MdxScript>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
