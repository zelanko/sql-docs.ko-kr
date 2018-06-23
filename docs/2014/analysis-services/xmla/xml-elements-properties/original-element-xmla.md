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
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 63ee76cd3b476b3a8dbf45a50ad0f9d22a55e0fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184115"
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
 `Original` 값으로 바꿀 UNC 경로 포함 하는 요소는 [새로](new-element-xmla.md) 부모에 포함 된 요소의 `Folder` 모든 개체에 대해 복원 또는 동기화 되는 동안 각각는 [복원 ](../xml-elements-commands/restore-element-xmla.md) 또는 [동기화](../xml-elements-commands/synchronize-element-xmla.md) 명령입니다. 이 요소의 값의 값과 비교 되는 [StorageLocation](../../scripting/properties/storagelocation-element-assl.md) 각 큐브, 측정값 그룹 또는 파티션에 대 한 요소 값의 일치 항목이 발견 하는 경우는 `New` 요소는 업데이트 하는 데 사용 되는 `StorageLocation` 의 복원 또는 동기화 중 개체입니다.  
  
 백업 및 개체를 복원 하는 방법에 대 한 자세한 내용은 참조 [Backing Up, Restoring, and Synchronizing &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  