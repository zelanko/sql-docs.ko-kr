---
title: CellPermission 요소 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9c4b6c9420be8eec3ba6d856f7c6312bfeb9b7f9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="cellpermission-element-assl"></a>CellPermission 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  멤버는 사용 권한을 설명는 [역할](../../../analysis-services/scripting/objects/role-element-assl.md) 요소 내의 개별 셀에 있는 한 [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CellPermissions>  
   <CellPermission>  
      <Access>...</Access>  
            <Description>...</Description>  
      <Expression>...</Expression>  
      <Annotations>...</Annotations>  
   </CellPermission>  
</CellPermissions>  
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
|부모 요소|[CellPermissions](../../../analysis-services/scripting/collections/cellpermissions-element-assl.md)|  
|자식 요소|[액세스](../../../analysis-services/scripting/properties/access-element-assl.md), [주석](../../../analysis-services/scripting/collections/annotations-element-assl.md), [설명](../../../analysis-services/scripting/properties/description-element-assl.md), [식](../../../analysis-services/scripting/properties/expression-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.CellPermission>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
