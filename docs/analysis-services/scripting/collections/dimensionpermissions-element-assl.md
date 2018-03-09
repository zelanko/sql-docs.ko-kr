---
title: "DimensionPermissions 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DimensionPermissions Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DimensionPermissions
helpviewer_keywords: DimensionPermissions element
ms.assetid: cb9fdfbf-2118-423b-ba02-fa36813dbea0
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d4621358267f2741b87b739e671a0f00874d3862
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="dimensionpermissions-element-assl"></a>DimensionPermissions 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]에 적용 가능한 권한 컬렉션을 포함 한 [차원](../../../analysis-services/scripting/objects/dimension-element-assl.md) 요소 또는 [CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Dimension> <!-- or CubePermission -->  
   ...  
   <DimensionPermissions>  
            <DimensionPermission>...</DimensionPermission> <!-- parent: Dimension -->  
      <!-- or -->  
      <DimensionPermission xsi:type="CubeDimensionPermission">...</DimensionPermission> <!-- parent: CubePermission -->  
      </DimensionPermissions>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md), [차원](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|자식 요소|[DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 **CubePermission** 요소의 경우 이 컬렉션의 **DimensionPermission** 요소는 명시적으로 참조되는 각 차원의 **DimensionPermissions** 컬렉션에 지정된 권한을 덮어씁니다. 이 컬렉션에서 차원을 참조하지 않은 경우 **CubePermission** 요소는 차원의 **DimensionPermissions** 컬렉션에 지정된 권한을 상속합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.DimensionPermissionCollection>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [컬렉션 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
