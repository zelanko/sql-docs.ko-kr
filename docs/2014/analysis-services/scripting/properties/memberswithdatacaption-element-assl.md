---
title: MembersWithDataCaption 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MembersWithDataCaption Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MembersWithDataCaption
helpviewer_keywords:
- MembersWithDataCaption element
ms.assetid: a5d59efd-5d67-485b-a360-67d54a1fe394
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 847a355f2517a5a630096e2617a27bdae396e565
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103903"
---
# <a name="memberswithdatacaption-element-assl"></a>MembersWithDataCaption 요소(ASSL)
  시스템 생성 데이터 멤버에 대한 캡션을 만드는 데 사용되는 템플릿 문자열을 제공합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AttributeTranslation> <!-- or DimensionAttribute -->  
   ...  
   <MembersWithDataCaption>...</MembersWithDataCaption>  
   ...  
</AttributeTranslation>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AttributeTranslation](../data-type/translation-data-type-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 값을 `MembersWithDataCaption` 요소는 부모 특성에만 사용 됩니다 (값 즉,를 [사용](usage-element-dimensionattribute-assl.md) 요소의 `DimensionAttribute` 부모 요소가로 설정 되어 *부모*) 결정할를 부모 특성의 데이터 멤버의 캡션입니다. 데이터 멤버에 대한 자세한 내용은 [부모-자식 계층의 특성](../../multidimensional-models/parent-child-dimension-attributes.md)을 참조하세요.  
  
 부모에 해당 하는 요소가 `MembersWithDataCaption` Analysis Management Objects (AMO) 개체 모델 <xref:Microsoft.AnalysisServices.AttributeTranslation> 및 <xref:Microsoft.AnalysisServices.DimensionAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [MembersWithData 요소 &#40;ASSL&#41;](../objects/data-element-assl.md)   
 [AttributeTranslation 데이터 형식 &#40;ASSL&#41;](../data-type/translation-data-type-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
