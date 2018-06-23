---
title: Folder 요소 (XMLA) | Microsoft Docs
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
- Folder Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.folder
- http://schemas.microsoft.com/analysisservices/2003/engine#Folder
- urn:schemas-microsoft-com:xml-analysis#Folder
helpviewer_keywords:
- Folder element
ms.assetid: 87b305b0-57e3-4ec3-9d80-f1bcf3ce7540
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 64bc73db4cfb1fee4471e474bf498094751edcf5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091360"
---
# <a name="folder-element-xmla"></a>Folder 요소(XMLA)
  에 대해 업데이트할 파일 시스템 저장소 위치를 포함 한 [위치](location-element-xmla.md) 동안은 [복원](../xml-elements-commands/restore-element-xmla.md) 또는 [동기화](../xml-elements-commands/synchronize-element-xmla.md) 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Folders>  
   ...  
   <Folder>  
      <Original>...</Original>  
      <New>...</New>  
   </Folder>  
   ...  
</Folders>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[폴더](folders-element-xmla.md)|  
|자식 요소|[새](new-element-xmla.md), [원래](original-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 지정된 경우 `Folder` 요소는 `Restore` 요소의 값과 일치하는 원본 인스턴스의 데이터베이스(`Synchronize` 명령의 경우)나 백업 파일(`Original` 명령의 경우)에 포함된 개체의 저장소 위치를 `New` 요소의 값으로 변경합니다.  
  
 백업 및 개체를 복원 하는 방법에 대 한 자세한 내용은 참조 [Backing Up, Restoring, and Synchronizing &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [StorageLocation 요소 &#40;ASSL&#41;](../../scripting/properties/storagelocation-element-assl.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  