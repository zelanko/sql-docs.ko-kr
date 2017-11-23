---
title: "DbSchemaName 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DbSchemaName Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#DbSchemaName
- microsoft.xml.analysis.dbschemaname
- http://schemas.microsoft.com/analysisservices/2003/engine#DbSchemaName
helpviewer_keywords: DbSchemaName element
ms.assetid: 40ca10c9-7597-48fe-a9d9-ee2c7b84d4d1
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bfa0ae41571fcd04361801e13571f758afbc44cd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="dbschemaname-element-xmla"></a>DbSchemaName 요소(XMLA)
  [DbTableName](../../../analysis-services/xmla/xml-elements-properties/tablenotification-element-xmla.md) 요소로 식별된 테이블의 부모 [TableNotification](../../../analysis-services/xmla/xml-elements-properties/dbtablename-element-xmla.md) 요소에서 사용하는 스키마 이름을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<TableNotification>  
   ...  
   <DbSchemaName>...</DbSchemaName>  
   ...  
</TableNotification>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[TableNotification](../../../analysis-services/xmla/xml-elements-properties/tablenotification-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
