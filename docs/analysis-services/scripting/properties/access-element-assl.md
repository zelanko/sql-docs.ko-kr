---
title: 요소 (ASSL)에 액세스 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 92ee80ebd8428c4d32d1788423c85e9afedd78e6
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="access-element-assl"></a>Access 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  에 지정 된 액세스 수준을 나타냅니다는 [CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CellPermission>  
   ...  
   <Access>...</Access>  
   ...  
</CellPermission>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|Value|Description|  
|-----------|-----------------|  
|*읽기*|읽기 전용 액세스 권한이 허용됩니다.|  
|*불확정 읽기*|불확정 읽기 권한이 허용됩니다.|  
|*ReadWrite*|읽기/쓰기 권한이 허용됩니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **액세스** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CellPermissionAccess>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Role 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
