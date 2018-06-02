---
title: Security 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c4ea0e1f9bfab567c792bdd7b233bea038e87f54
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576246"
---
# <a name="security-element-xmla"></a>Security 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  백업 하거나 하는 동안 역할 및 권한과 같은 보안 정의 복원 하는 방법을 지정는 [백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) 또는 [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <Security>...</Security>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*SkipMembership*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **보안** 요소에는 Analysis Services 데이터베이스 백업 또는 각각 시, 복원 되는지 여부에 정의 된 역할 및 권한과 같은 보안 정의 결정 한 **백업** 또는 **복원** 명령입니다. 또한 이 요소는 보안 정의의 멤버로 정의된 Windows 사용자 계정 및 그룹을 **Backup** 또는 **Restore** 명령의 일부로 포함할지 여부를 결정합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*SkipMembership*|**Backup** 또는 **Restore** 명령 중에 보안 정의가 포함되지만 멤버 정보는 제외됩니다.|  
|*CopyAll*|**Backup** 또는 **Restore** 명령 중에 보안 정의 및 멤버 정보가 포함됩니다.|  
|*IgnoreSecurity*|**Backup** 또는 **Restore** 명령 중에 보안 정의가 제외됩니다.|  
  
## <a name="see-also"></a>참고자료
 [SynchronizeSecurity 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/synchronizesecurity-element-xmla.md)   
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
