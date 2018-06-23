---
title: 새 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- New Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#New
- microsoft.xml.analysis.new
- urn:schemas-microsoft-com:xml-analysis#New
helpviewer_keywords:
- New element
ms.assetid: 1321adcb-67f7-40f0-8f20-b17c1d3e3f17
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 983c32cc19ebbc876d53d46865f81b0d37e10d59
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172732"
---
# <a name="new-element-xmla"></a>New 요소(XMLA)
  사용 하는 새 파일 시스템 저장소 위치를 포함 한 [폴더](folder-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Folder>  
   ...  
   <New>...</New>  
   ...  
</Folder>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Folder](folder-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `New` 요소는 각각 `Original` 또는 `Folder` 명령 중에 복원 또는 동기화되는 모든 개체에 대해 부모 `Restore` 요소에 포함된 `Synchronize` 요소의 값을 바꾸는 UNC 경로를 포함합니다. `Original` 요소의 값은 각 큐브, 측정값 그룹 또는 파티션에 대한 `StorageLocation` 요소의 값과 비교되며 일치하는 항목이 있을 경우 이 요소의 값이 복원 또는 동기화 중에 개체의 `StorageLocation`을 업데이트하는 데 사용됩니다.  
  
 백업 및 개체를 복원 하는 방법에 대 한 자세한 내용은 참조 [백업 및 복원 Objects (XMLA)](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Original 요소 &#40;XMLA&#41;](original-element-xmla.md)   
 [Restore 요소 &#40;XMLA&#41;](../xml-elements-commands/restore-element-xmla.md)   
 [StorageLocation 요소 &#40;ASSL&#41;](../../scripting/properties/storagelocation-element-assl.md)   
 [Synchronize 요소 &#40;XMLA&#41;](../xml-elements-commands/synchronize-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  