---
title: CustomRollupProperties 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CustomRollupProperties Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.customrollupproperties
- urn:schemas-microsoft-com:xml-analysis#CustomRollupProperties
- http://schemas.microsoft.com/analysisservices/2003/engine#CustomRollupProperties
helpviewer_keywords:
- CustomRollupProperties element
ms.assetid: 4abf0129-e529-4355-b8d5-6f4e6a88e796
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c9a107f793b0cbfe057d2ce7c683fad2320ce2c0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083023"
---
# <a name="customrollupproperties-element-xmla"></a>CustomRollupProperties 요소(XMLA)
  부모를 나타내는 특성 멤버에 대 한 사용자 지정 롤업 속성을 포함 [특성](attribute-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Attribute>  
   ...  
   <CustomRollupProperties>...</CustomRollupProperties>  
   ...  
</Attribute>  
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
|부모 요소|[Attribute](attribute-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `CustomRollupProperties` 요소는 부모 `Attribute` 요소에 지정된 특성 멤버의 사용자 지정 롤업 속성을 정의하는 MDX(Multidimensional Expressions) 식을 포함합니다.  
  
 MDX 식에 대 한 자세한 내용은 참조 하십시오 [식 &#40;MDX&#41;](/sql/mdx/expressions-mdx)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소를 삽입 &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Update 요소 &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
