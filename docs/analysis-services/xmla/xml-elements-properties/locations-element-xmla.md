---
title: Locations 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Locations Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Locations
- urn:schemas-microsoft-com:xml-analysis#Locations
- microsoft.xml.analysis.locations
helpviewer_keywords:
- Locations element
ms.assetid: 630929cb-f0dc-472a-86bc-28b67e907c3d
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 644c813d9ddc11db1d43ac51b616806c9fc1f141
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="locations-element-xmla"></a>Locations 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모 [Backup](../../../analysis-services/xmla/xml-elements-properties/query-element-xmla.md) , [Restore](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)또는 [Synchronize](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) 명령에서 사용하는 [Location](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) 요소의 컬렉션을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
< Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Locations>  
      <Location>...</Location>  
   </Locations>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [Restore](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) 또는 [Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|  
|자식 요소|[위치](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>참고 항목  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
