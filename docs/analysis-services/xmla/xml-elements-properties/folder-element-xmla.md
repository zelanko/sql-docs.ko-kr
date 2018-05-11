---
title: Folder 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0a13ac1689c58519a6e8d1ac06cacc8357570b75
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="folder-element-xmla"></a>Folder 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  에 대해 업데이트할 파일 시스템 저장소 위치를 포함 한 [위치](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) 동안은 [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) 또는 [동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) 명령입니다.  
  
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[폴더](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
|자식 요소|[새](../../../analysis-services/xmla/xml-elements-properties/new-element-xmla.md), [원래](../../../analysis-services/xmla/xml-elements-properties/original-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 지정된 경우 **Folder** 요소는 **Restore** 요소의 값과 일치하는 원본 인스턴스의 데이터베이스( **Synchronize** 명령의 경우)나 백업 파일( **Original** 명령의 경우)에 포함된 개체의 저장소 위치를 **New** 요소의 값으로 변경합니다.  
  
 백업 및 개체를 복원 하는 방법에 대 한 자세한 내용은 참조 [Backing Up, Restoring, 및 데이터베이스 동기화 & #40; XMLA & #41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>관련 항목:  
 [StorageLocation 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)   
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
