---
title: 읽을 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5742e7708158bfb703a5e4de8abcffd52dea67f3
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="read-element-assl"></a>Read 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  지정된 [CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md) 또는 [Permission](../../../analysis-services/scripting/data-type/permission-data-type-assl.md) 요소에 대해 데이터 또는 메타데이터를 읽을 수 있는지 여부를 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeDimensionPermission> <!-- or Permission -->  
   ...  
   <Read>...</Read>  
   ...  
</CubeDimensionPermission>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*없음*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubeDimensionPermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md), [Permission](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*없음*|부모 개체의 데이터 또는 메타데이터에 대한 액세스가 허용되지 않습니다.|  
|*허용*|부모 개체의 데이터 및 메타데이터에 대한 읽기 액세스가 허용됩니다.|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **읽기** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CubeDimensionPermission> 및 <xref:Microsoft.AnalysisServices.Permission>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Cube 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Dimension 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [CubePermission 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)   
 [Permission 데이터 형식 & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
