---
title: MdxMissingMemberMode 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cad22b3ed0408ae6c916bf39093d540662917196
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="mdxmissingmembermode-element-assl"></a>MdxMissingMemberMode 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  MDX(Multidimensional Expressions) 문에 대해 누락된 멤버가 처리되는 방식을 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Dimension>  
   ...  
   <MdxMissingMemberMode>...</MdxMissingMemberMode>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*Default*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[차원](../../../analysis-services/scripting/data-type/dimension-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*무시*|누락된 멤버가 무시됩니다.|  
|*오류*|누락된 멤버가 발견되면 오류가 발생합니다.|  
|*Default*|누락된 멤버가 무시됩니다.|  
  
 부모에 해당 하는 요소 **MdxMissingMemberMode** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Dimension>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 식 & #40; Mdx& #41; 참조](../../../mdx/multidimensional-expressions-mdx-reference.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
