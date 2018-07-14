---
title: DataSourceID 요소 (XMLA) | Microsoft Docs
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
- DataSourceID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.datasourceid
- urn:schemas-microsoft-com:xml-analysis#DataSourceID
- http://schemas.microsoft.com/analysisservices/2003/engine#DataSourceID
helpviewer_keywords:
- DataSourceID element
ms.assetid: 695522c7-acca-420a-a5fb-f01f3fd9a96b
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e96d9386319fa9d850a755519fad7360da8ec3b0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231823"
---
# <a name="datasourceid-element-xmla"></a>DataSourceID 요소(XMLA)
  사용 하는 데이터 소스를 식별을 [위치](location-element-xmla.md) 하는 동안 요소를 [백업](../xml-elements-commands/backup-element-xmla.md), [복원](../xml-elements-commands/restore-element-xmla.md), 또는 [동기화](../xml-elements-commands/synchronize-element-xmla.md) 명령.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Location>  
   ...  
   <DataSourceID>...</DataSourceID>  
   ...  
</Location>  
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
|부모 요소|[위치](location-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `DataSourceID` 요소는 원격 파티션 정보가 백업, 복원 및 동기화될 원격 인스턴스를 식별하는 원본 인스턴스에 있는 데이터 원본의 이름을 포함합니다.  
  
 백업 및 원격 파티션을 복원 하는 방법에 대 한 자세한 내용은 참조 하세요. [Backing Up, Restoring, and 데이터베이스 동기화 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ConnectionString 요소 &#40;XMLA&#41;](connectionstring-element-xmla.md)   
 [DataSourceType 요소 &#40;XMLA&#41;](type-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
