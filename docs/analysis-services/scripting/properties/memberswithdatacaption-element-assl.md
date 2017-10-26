---
title: "MembersWithDataCaption 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MembersWithDataCaption Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MembersWithDataCaption
helpviewer_keywords:
- MembersWithDataCaption element
ms.assetid: a5d59efd-5d67-485b-a360-67d54a1fe394
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f254c1fb3c747a64e3e8e5df50bf30d532678d09
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 값은 **MembersWithDataCaption** 요소 부모 특성에만 사용 됩니다 (의 값 즉,는 [사용량](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) 의 요소는 **DimensionAttribute** 부모 로 설정 된 *부모*)를 부모 특성의 데이터 멤버 캡션을 결정 합니다. 데이터 멤버에 대한 자세한 내용은 [부모-자식 계층의 특성](../../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)을 참조하세요.  
  
 부모에 해당 하는 요소 **MembersWithDataCaption** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.AttributeTranslation> 및 <xref:Microsoft.AnalysisServices.DimensionAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MembersWithData 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md)   
 [AttributeTranslation 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

