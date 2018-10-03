---
title: CellPermission 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CellPermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CellPermission
helpviewer_keywords:
- CellPermission element
ms.assetid: 54a6afc0-1fcb-4b24-851a-6d81e1fe0efc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 360d6d1e348971c073613b16607c5992396a920d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172063"
---
# <a name="cellpermission-element-assl"></a>CellPermission 요소(ASSL)
  해당 멤버의 권한을 설명를 [역할](role-element-assl.md) 요소 내의 개별 셀에는 [큐브](cube-element-assl.md) 요소입니다.  
  
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CellPermissions](../collections/cellpermissions-element-assl.md)|  
|자식 요소|[액세스](../properties/access-element-assl.md)하십시오 [주석](../collections/annotations-element-assl.md), [설명](../properties/description-element-assl.md), [식](../properties/expression-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.CellPermission>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
