---
title: Parameters 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Parameters Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Parameters
- urn:schemas-microsoft-com:xml-analysis#Parameters
- microsoft.xml.analysis.parameters
helpviewer_keywords:
- Parameters element
ms.assetid: d46454a1-a1d1-4aa8-95ea-54be22a53e83
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3b9c3d0d642ad7248d87e7cc17aaa17953bf6aec
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134053"
---
# <a name="parameters-element-xmla"></a>Parameters 요소(XMLA)
  [Execute](parameter-element-xmla.md) 메서드에서 사용하는 [Parameter](../xml-elements-methods-execute.md) 요소의 컬렉션을 포함합니다.  
  
 **Namespace:** `urn:schemas-microsoft-com:xml-analysis`  
  
## <a name="syntax"></a>구문  
  
```  
  
<Execute>  
...  
   <Parameters>  
      <Parameter>...</Parameter>  
   </Parameters>  
...  
</Execute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[실행](../xml-elements-methods-execute.md)|  
|자식 요소|[매개 변수](parameter-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 일부 XMLA(XML for Analysis) 명령(예: [Process](../xml-elements-commands/process-element-xmla.md) 명령)은 추가 정보를 요청할 수도 있습니다. `Parameters` 요소는 XMLA 명령에 대한 청크 정보를 포함한 추가 정보를 제공하는 메커니즘을 제공합니다.  
  
 XMLA 명령이 `Parameters` 요소를 사용하지 않는 경우 `Execute` 메서드를 호출할 때 이 요소를 생략할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
