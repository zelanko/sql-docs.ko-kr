---
title: ServerMode 요소 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 21e9344ef945311b3af07398e6e927482718f5ff
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37968496"
---
# <a name="servermode-element"></a>ServerMode 요소
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  **ServerMode** Server 요소는 서버가 작동하고 있는 모드를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Server>  
...  
   <ddl300:ServerMode>...</ddl300:ServerMode>  
...  
</Server>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|(없음)|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 서버는 다음 모드 중 하나에서 작동합니다.  
  
|값|Description|  
|-----------|-----------------|  
|*다차원*|다차원 및 데이터 마이닝 모드|  
|*테이블 형식*|테이블 형식 모드|  
|*SharePoint*|SharePoint 모드|  
  
## <a name="see-also"></a>참고자료
 [Server](../../../analysis-services/scripting/objects/server-element-assl.md)  
  
  
