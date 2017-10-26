---
title: "새 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- New Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#New
- microsoft.xml.analysis.new
- urn:schemas-microsoft-com:xml-analysis#New
helpviewer_keywords:
- New element
ms.assetid: 1321adcb-67f7-40f0-8f20-b17c1d3e3f17
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5eade126deeecbe8b224077d506c8231587f739d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="new-element-xmla"></a>New 요소(XMLA)
  사용 하는 새 파일 시스템 저장소 위치를 포함 한 [폴더](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Folder>  
   ...  
   <New>...</New>  
   ...  
</Folder>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Folder](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **새로** 의 값을 바꾸는 UNC 경로 포함 하는 요소는 **원래** 부모에 포함 된 요소의 **폴더** 복원 또는 동기화 하는 모든 개체에 대 한 요소 각각 중는 **복원** 또는 **동기화** 명령입니다. 값은 **원래** 요소의 값과 비교 되는 **StorageLocation** 각 큐브, 측정값 그룹 또는 파티션에 대 한 요소와 일치 하는 항목이 없는 경우이 요소의 값은 업데이트 하는 데는 **StorageLocation** 복원 또는 동기화 중 개체의 합니다.  
  
 백업 및 개체를 복원 하는 방법에 대 한 자세한 내용은 참조 [백업 및 복원 Objects (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [원래 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/original-element-xmla.md)   
 [요소 &#40; 복원 XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [StorageLocation 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)   
 [요소 &#40; 동기화 XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

