---
title: DbTableName 요소 (XMLA) | Microsoft Docs
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
- DbTableName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#DbTableName
- microsoft.xml.analysis.dbtablename
- urn:schemas-microsoft-com:xml-analysis#DbTableName
helpviewer_keywords:
- DbTableName element
ms.assetid: 0ffda645-2a88-4f42-8929-9d7385c19a74
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d2abdf2486b1d501dbec3a0f84073ffaa896958b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37287929"
---
# <a name="dbtablename-element-xmla"></a>DbTableName 요소(XMLA)
  부모에 의해 사용 되는 테이블의 이름이 [TableNotification](tablenotification-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<TableNotification>  
   ...  
   <DbTableName>...</DbTableName>  
   ...  
</TableNotification>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[TableNotification](tablenotification-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [DbSchemaName 요소 &#40;XMLA&#41;](name-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
