---
title: "Original 요소 (XMLA) | Microsoft Docs"
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
- Original Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.original
- http://schemas.microsoft.com/analysisservices/2003/engine#Original
- urn:schemas-microsoft-com:xml-analysis#Original
helpviewer_keywords:
- Original element
ms.assetid: c98a3700-ac19-4341-85d9-5afedf662601
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 75a0345459be5e065a7a737b8036e505f799d549
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="original-element-xmla"></a>Original 요소(XMLA)
  사용 하는 원래 파일 시스템 저장소 위치를 포함 한 [폴더](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Folder>  
   ...  
   <Original>...</Original>  
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
 **원래** 값으로 바꿀 UNC 경로 포함 하는 요소는 [새로](../../../analysis-services/xmla/xml-elements-properties/new-element-xmla.md) 부모에 포함 된 요소의 **폴더** 복원 하는 모든 개체에 대 한 요소 또는 동기화 중에 각각는 [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) 또는 [동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) 명령입니다. 이 요소의 값의 값과 비교 되는 [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md) 각 큐브, 측정값 그룹 또는 파티션에 대 한 요소 및 값 일치 하는 항목이 **새로** 요소는 업데이트를사용 **StorageLocation** 복원 또는 동기화 중 개체의 합니다.  
  
 백업 및 개체를 복원 하는 방법에 대 한 자세한 내용은 참조 [Backing Up, Restoring, 및 데이터베이스 동기화 &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
