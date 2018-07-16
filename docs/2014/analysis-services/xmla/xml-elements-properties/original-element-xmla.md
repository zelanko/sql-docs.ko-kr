---
title: Original 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Original Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.original
- http://schemas.microsoft.com/analysisservices/2003/engine#Original
- urn:schemas-microsoft-com:xml-analysis#Original
helpviewer_keywords:
- Original element
ms.assetid: c98a3700-ac19-4341-85d9-5afedf662601
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e70d0f29f41a687cb0716fbb857ff1b3b59023e7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249163"
---
# <a name="original-element-xmla"></a>Original 요소(XMLA)
  사용 하는 원래 파일 시스템 저장소 위치를 포함 한 [폴더](folder-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Folder>  
   ...  
   <Original>...</Original>  
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
 합니다 `Original` 요소 값으로 바꿀 UNC 경로 포함 합니다 [새로 만들기](new-element-xmla.md) 요소는 부모에서 포함할 `Folder` 복원 또는 동기화 중 각각의 모든 요소 개체를 [복원 ](../xml-elements-commands/restore-element-xmla.md) 나 [Synchronize](../xml-elements-commands/synchronize-element-xmla.md) 명령입니다. 이 요소 값의 값과 비교 되는 [StorageLocation](../../scripting/properties/storagelocation-element-assl.md) 각 큐브, 측정값 그룹 또는 파티션에 대 한 요소 및 있으면 일치 하는 값을 `New` 요소 업데이트를 사용 하는 `StorageLocation` 의 복원 또는 동기화 중 개체입니다.  
  
 백업 및 복원 하는 개체에 대 한 자세한 내용은 참조 하세요. [Backing Up, Restoring, and 데이터베이스 동기화 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
