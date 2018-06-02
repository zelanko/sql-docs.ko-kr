---
title: BackupRemotePartitions 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 33e81bd76e7f900a396b1f9bfbae808092a2877e
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575085"
---
# <a name="backupremotepartitions-element-xmla"></a>BackupRemotePartitions 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  결정 여부 부모 [백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) 명령 개체에 연결 된 원격 파티션을 백업할 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Backup>  
   ...  
   <BackupRemotePartitions>...</BackupRemotePartitions>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|False|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **BackupRemotePartitions** 가 **True**로 설정되면 **Locations** 명령에 하나 이상의 **Location** 요소를 포함하는 **Backup** 요소가 포함되어야 합니다. 그렇지 않으면 오류가 발생합니다. 백업 및 원격 파티션을 복원 하는 방법에 대 한 자세한 내용은 참조 [Backing Up, Restoring, and Synchronizing &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>참고자료
 [Locations 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md)   
 [Location 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)   
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
