---
title: "Annotation 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Annotation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Annotation
helpviewer_keywords:
- Annotation element
ms.assetid: 7d75291a-47b4-498a-8ba4-3d093b8513b2
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 109386991ba5d632e6c40523241f6d64c4dba05d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="annotation-element-assl"></a>Annotation 요소(ASSL)
  ASSL(Analysis Services Scripting Language) 스키마를 확장하는 데 사용되는 요소를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Annotations>  
   <Annotation>  
      <Name>...</Name>  
      <Visibility>...</Visibility>  
      <Value>...</Value>  
   </Annotation>  
</Annotations >  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[주석](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
|자식 요소|[이름](../../../analysis-services/scripting/properties/name-element-assl.md), [값](../../../analysis-services/scripting/properties/value-element-assl.md), [표시 유형](../../../analysis-services/scripting/properties/visibility-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 **주석** 요소는 복합 데이터 형식을 정의 하는 데에 사용 되는 것을 제외한 모든 개체에 ASSL 스키마 확장성을 제공 합니다. **값** 의 요소는 **주석** 요소에는 다음 규칙에 따라 ASSL 이외의 모든 XML 네임 스페이스에서 유효한 XML을 포함할 수 있습니다.  
  
-   XML은 요소만 포함할 수 있습니다.  
  
-   각 요소 이름은 고유해야 합니다. 것이 좋습니다의 값은 **이름** 의 요소는 **주석** 요소는 대상 네임 스페이스를 참조 합니다.  
  
 이러한 규칙의 내용이 적용 되는 **주석** 의사 결정 지원 개체 (DSO)와 같은 다른 인터페이스를 통해 이름/값 집합으로 노출 해야 하는 요소 쌍입니다.  
  
 주석 및 공백은 내에서 **주석** 자식 요소로 묶이지 않은 요소는 그대로 유지 되지 않습니다. 또한 모든 요소는 읽기/쓰기 전용이어야 하며 읽기 전용 요소는 무시됩니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Annotation>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
