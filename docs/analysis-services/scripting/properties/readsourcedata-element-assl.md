---
title: "ReadSourceData 요소 (ASSL) | Microsoft Docs"
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
- ReadSourceData Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ReadSourceData element
ms.assetid: 7da4665a-fba3-4aae-8dee-678dc14d3b05
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ca4e5be499af359f72a75223054405d2d9993632
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="readsourcedata-element-assl"></a>ReadSourceData 요소(ASSL)
  얼마나 고유한 이름을 결정에 포함 된 계층에 대해 생성 되는 [CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubePermission>  
   ...  
   <ReadSourceData>...</ReadSourceData>  
   ...  
</CubePermission>  
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
|부모 요소|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*없음*|계산 패스 0에서 사용 가능한 데이터에 액세스할 수 없습니다.|  
|*허용*|계산 패스 0에서 사용 가능한 데이터에 액세스할 수 있습니다.|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **ReadSourceData** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CubePermission>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Cube 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Dimension 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

