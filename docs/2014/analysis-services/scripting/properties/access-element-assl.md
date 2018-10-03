---
title: 요소 (ASSL)에 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Access Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Access
helpviewer_keywords:
- Access element
ms.assetid: 6ad99010-fac5-48e9-a099-ecbca380e127
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 60fbf476e1d884cce28dd674ab16d3bda001a3a0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051843"
---
# <a name="access-element-assl"></a>Access 요소(ASSL)
  에 지정 된 액세스 수준을 나타냅니다는 [CellPermission](../objects/cellpermission-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CellPermission>  
   ...  
   <Access>...</Access>  
   ...  
</CellPermission>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CellPermission](../objects/cellpermission-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*읽기*|읽기 전용 액세스 권한이 허용됩니다.|  
|*불확정 읽기*|불확정 읽기 권한이 허용됩니다.|  
|*ReadWrite*|읽기/쓰기 권한이 허용됩니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `Access`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.CellPermissionAccess>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [역할 요소 &#40;ASSL&#41;](../objects/role-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
