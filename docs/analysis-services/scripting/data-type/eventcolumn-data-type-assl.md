---
title: EventColumn 데이터 형식 (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fe9daba9906a3bc65bfd33e87f07ef55615734cb
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="eventcolumn-data-type-assl"></a>EventColumn 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [Event](../../../analysis-services/scripting/objects/event-element-assl.md) 요소에 대해 [Trace](../../../analysis-services/scripting/objects/trace-element-assl.md) 요소의 일부로 캡처할 정보 열을 나타내는 기본 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|없음|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[ColumnID](../../../analysis-services/scripting/properties/columnid-element-eventcolumn-assl.md)|  
|파생 요소|[열](../../../analysis-services/scripting/objects/column-element-assl.md) ([열](../../../analysis-services/scripting/collections/columns-element-assl.md) 컬렉션 [추적](../../../analysis-services/scripting/objects/trace-element-assl.md))|  
  
## <a name="see-also"></a>관련 항목:  
 [Events 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [스크립팅 언어 XML 데이터 형식 & #40; analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
