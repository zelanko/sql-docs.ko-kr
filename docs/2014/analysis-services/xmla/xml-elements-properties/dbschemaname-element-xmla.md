---
title: DbSchemaName 요소 (XMLA) | Microsoft Docs
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
- DbSchemaName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#DbSchemaName
- microsoft.xml.analysis.dbschemaname
- http://schemas.microsoft.com/analysisservices/2003/engine#DbSchemaName
helpviewer_keywords:
- DbSchemaName element
ms.assetid: 40ca10c9-7597-48fe-a9d9-ee2c7b84d4d1
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 7fde4fe223ae667d1fdc90c51b3df9be7ce37207
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186625"
---
# <a name="dbschemaname-element-xmla"></a>DbSchemaName 요소(XMLA)
  [DbTableName](tablenotification-element-xmla.md) 요소로 식별된 테이블의 부모 [TableNotification](name-element-xmla.md) 요소에서 사용하는 스키마 이름을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<TableNotification>  
   ...  
   <DbSchemaName>...</DbSchemaName>  
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
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  