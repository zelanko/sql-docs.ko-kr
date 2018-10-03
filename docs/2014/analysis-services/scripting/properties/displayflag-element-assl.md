---
title: DisplayFlag 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DisplayFlag Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DisplayFlag
helpviewer_keywords:
- DisplayFlag element
ms.assetid: a6750477-0763-46da-9add-1f4448146a6b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2cd3c42721c2b70be044039e19001cd8ce7fb21b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149263"
---
# <a name="displayflag-element-assl"></a>DisplayFlag 요소(ASSL)
  사용자 인터페이스 구성 요소는 연결 된 표시할 것인지 여부를 나타내는 읽기 전용 힌트를 포함 [ServerProperty](../objects/serverproperty-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ServerProperty>  
   ...  
   <DisplayFlag>...</DisplayFlag>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ServerProperty](../objects/serverproperty-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 부모에 해당 요소가 `DisplayFlag` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ServerProperty>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ServerProperties 요소 &#40;ASSL&#41;](../collections/serverproperties-element-assl.md)   
 [Server 요소 &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
