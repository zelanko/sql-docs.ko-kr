---
title: CubeInfo 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CubeInfo Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CubeInfo
- microsoft.xml.analysis.cubeinfo
- urn:schemas-microsoft-com:xml-analysis#CubeInfo
helpviewer_keywords:
- CubeInfo element
ms.assetid: a504bac5-4bf2-4f78-a288-e74a34eaa97e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f58bcd7cbd15c767196e9efc2654e24aeacf94d4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48214643"
---
# <a name="cubeinfo-element-xmla"></a>CubeInfo 요소(XMLA)
  부모에 의해 포함 된 큐브 메타 데이터를 포함 [OlapInfo](olapinfo-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<OlapInfo>  
   ...  
   <CubeInfo>  
      <Cube>...</Cube>  
   </CubeInfo>  
   ...  
</OlapInfo>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[OlapInfo](olapinfo-element-xmla.md)|  
|자식 요소|[Cube](cube-element-olapinfo-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `CubeInfo` 요소는 다차원 데이터 집합에서 참조하는 각 큐브당 하나의 `Cube` 요소를 포함합니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 단일 반환 `Cube` 이 컬렉션의 요소 때문에 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] MDX (Multidimensional Expressions) 언어의 FROM 절에서 여러 큐브를 참조 하는 문을 지원 하지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
