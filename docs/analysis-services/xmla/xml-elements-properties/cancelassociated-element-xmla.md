---
title: "CancelAssociated 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- CancelAssociated Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cancelassociated
- urn:schemas-microsoft-com:xml-analysis#CancelAssociated
- http://schemas.microsoft.com/analysisservices/2003/engine#CancelAssociated
helpviewer_keywords:
- CancelAssociated element
ms.assetid: fd890440-d1a7-4c05-9e81-c81e6b8c274c
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3f1441e6e54a085181bf7afcff8c4961a8a60d9c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="cancelassociated-element-xmla"></a>CancelAssociated 요소(XMLA)
  부모 [Cancel](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md) 요소가 연결된 모든 명령을 취소해야 할지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cancel>  
   ...  
   <ConnectionID>...</ConnectionID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|False|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[취소](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소를 지정하고 **True**로 설정한 경우 부모 **Cancel** 명령에서 식별되는 각 해당 연결, 세션 및 명령이 취소됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ConnectionID 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md)   
 [SessionID 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md)   
 [SPID 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/spid-element-xmla.md)   
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

