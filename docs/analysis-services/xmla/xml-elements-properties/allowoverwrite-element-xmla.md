---
title: AllowOverwrite 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 76ba7c6b3046e5298a346cb84472de3ba090e2bc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37972999"
---
# <a name="allowoverwrite-element-xmla"></a>AllowOverwrite 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  확인 여부를 부모 [백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) 또는 [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) 명령은 대상 파일 또는 데이터베이스를 덮어쓸지 하려고 시도 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <AllowOverwrite>...</AllowOverwrite>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|False|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **Backup** 명령의 경우 **AllowOverwrite** 요소는 명령으로 **File** 요소에 지정된 백업 파일을 덮어쓸 수 있는지 여부를 결정합니다.  
  
 에 대 한 **복원** 요소를 **AllowOverwrite** 요소는 명령에 지정 된 Analysis Services 데이터베이스를 덮어쓸 수 있는지 여부를 결정 합니다 **DatabaseName** 요소입니다.  
  
## <a name="see-also"></a>참고자료
 [DatabaseName 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/databasename-element-xmla.md)   
 [파일 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)   
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
