---
title: Original 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0ddf701f236e66680f562fa0721bcc8a2eb179f8
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38050391"
---
# <a name="original-element-xmla"></a>Original 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  사용 하는 원래 파일 시스템 저장소 위치를 포함 한 [폴더](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Folder>  
   ...  
   <Original>...</Original>  
   ...  
</Folder>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Folder](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 합니다 **원래** 요소 값으로 바꿀 UNC 경로 포함 합니다 [새로 만들기](../../../analysis-services/xmla/xml-elements-properties/new-element-xmla.md) 요소는 부모에서 포함할 **폴더** 복원 하는 모든 개체에 대 한 요소 또는 동기화 중 각각을 [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) 또는 [Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) 명령입니다. 이 요소 값의 값과 비교 되는 [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md) 각 큐브, 측정값 그룹 또는 파티션에 대 한 요소 및 있으면 일치 하는 값을 **새로 만들기** 요소는 업데이트 하는 데는  **StorageLocation** 복원 또는 동기화 중에 개체입니다.  
  
 백업 및 복원 하는 개체에 대 한 자세한 내용은 참조 하세요. [Backing Up, Restoring, and 데이터베이스 동기화 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
