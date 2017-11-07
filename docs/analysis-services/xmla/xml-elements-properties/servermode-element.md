---
title: "ServerMode 요소 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: c2f8cb39-dad7-433b-b7b7-fb1625f76a84
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8145c7090e1c172fe210202e55078cb4bd404fcb
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="servermode-element"></a>ServerMode 요소
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
  
|값|Description|  
|-----------|-----------------|  
|*다차원*|다차원 및 데이터 마이닝 모드|  
|*테이블 형식*|테이블 형식 모드|  
|*SharePoint*|SharePoint 모드|  
  
## <a name="see-also"></a>관련 항목:  
 [Server](../../../analysis-services/scripting/objects/server-element-assl.md)  
  
  

