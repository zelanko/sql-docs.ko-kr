---
title: "MemberUniqueNameStyle 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MemberUniqueNameStyle Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MemberUniqueNameStyle element
ms.assetid: f0771c81-0127-4203-9501-ae4f864730fa
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 94e0ed38f78c485e3c0178ac4dcc02cd318d065b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="memberuniquenamestyle-element-assl"></a>MemberUniqueNameStyle 요소(ASSL)
  얼마나 고유한 이름을 결정에 포함 된 계층의 멤버에 대해 생성 되는 [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeDimension>  
   ...  
   <MemberUniqueNameStyle>...</MemberUniqueNameStyle>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*네이티브*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*네이티브*|인스턴스에서 자동으로 멤버의 고유한 이름을 결정합니다.|  
|*NamePath*|인스턴스에서 각 수준과 멤버의 캡션으로 구성된 복합 이름을 생성합니다.|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **MemberUniqueNameStyle** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CubeDimension>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Cube 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Dimension 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [CubeDimension 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)  
  
  

