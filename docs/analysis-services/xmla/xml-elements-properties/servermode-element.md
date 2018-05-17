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
ms.openlocfilehash: bcbd6e0315fc8a418ccff20fe5c2a69eebe4490b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
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
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|(없음)|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 서버는 다음 모드 중 하나에서 작동합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|*다차원*|다차원 및 데이터 마이닝 모드|  
|*테이블 형식*|테이블 형식 모드|  
|*SharePoint*|SharePoint 모드|  
  
## <a name="see-also"></a>관련 항목:  
 [Server](../../../analysis-services/scripting/objects/server-element-assl.md)  
  
  
