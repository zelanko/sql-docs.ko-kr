---
title: Exception 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Exception Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Exception
- urn:schemas-microsoft-com:xml-analysis#Exception
- microsoft.xml.analysis.exception
helpviewer_keywords:
- Exception element
ms.assetid: 0be4cc2f-c03e-490a-a6f7-8b1ede5d09ba
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e447bda3d52ac63125f3a96769fcee2c0158494c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178543"
---
# <a name="exception-element-xmla"></a>Exception 요소(XMLA)
  예외가 반환 되었음을 나타냅니다는 [Discover](../xml-elements-methods-discover.md) 또는 [Execute](../xml-elements-methods-execute.md) 메서드를 호출 합니다.  
  
 **Namespace** http://schemas.microsoft.com/analysisservices/2003/exception  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<root>  
   ...  
   <Exception />  
   ...  
</root>  
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
|부모 요소|[root](root-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `Discover` 메서드 호출 또는 `Execute` 메서드 호출의 단일 XMLA 명령을 실행하는 중에 메서드나 명령이 완료되지 못하게 하는 오류가 발생하면 해당 명령 또는 메서드에 대한 `root` 요소에 `Exception` 요소와 `Messages` 요소가 포함됩니다. `Exception` 요소는 메서드 또는 명령이 실행되지 못하게 하는 오류가 발생했음을 나타내며 `Messages` 요소는 오류 목록 또는 해당 오류와 관련된 경고 메시지를 포함합니다.  
  
## <a name="see-also"></a>관련 항목  
 [메시지 요소 &#40;XMLA&#41;](messages-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
