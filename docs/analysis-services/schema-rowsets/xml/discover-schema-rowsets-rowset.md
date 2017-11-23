---
title: "DISCOVER_SCHEMA_ROWSETS 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DISCOVER_SCHEMA_ROWSETS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_SCHEMA_ROWSETS rowset
ms.assetid: e5012aa0-6ef8-497f-96c1-2772e2394f62
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d93c0c7f2844ac96fafa60720e945f80dfcc02c9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="discoverschemarowsets-rowset"></a>DISCOVER_SCHEMA_ROWSETS 행 집합
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA(XML for Analysis) 공급자에서 지원하는 모든 열거 값과 추가 공급자별 열거 값에 대한 이름, 제한, 설명 및 기타 정보를 반환합니다.  
  
 호출 하는 경우는 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드는 **DISCOVER_SCHEMA_ROWSETS** 열거 값은 [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) 요소는 **Discover**메서드가 반환 되는 **DISCOVER_SCHEMA_ROWSETS** 행 집합입니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 DISCOVER_SCHEMA_ROWSETS 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**SchemaName**|**DBTYPE_WSTR**||스키마 또는 요청의 이름입니다. 이 요청은 *RequestTypes* 열거형의 값을 반환합니다.|  
|**SchemaGuid**|**DBTYPE_GUID**||스키마의 GUID입니다.|  
|**제한 사항**|**DBTYPE_HCHAPTER**||공급자에서 지원하는 제한의 배열입니다.|  
|**Description**|**DBTYPE_WSTR**||스키마의 지역화 가능한 설명입니다.|  
|**RestrictionsMask**|**DBTYPE_UI8**|||  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
 DBSCHEMA_MEMBERS 스키마 행 집합의 세 가지 제한을 지원하는 공급자의 경우 **Restrictions** 배열이 다음 결과를 반환할 수 있습니다. 결과의 요소는 스키마의 열 이름을 참조합니다.  
  
```  
<Restrictions>  
      <CATALOG_NAME type="string" />   
      <SCHEMA_NAME type="string" />   
      <CUBE_NAME type="string" />   
</Restrictions>  
```  
  
## <a name="restriction-columns"></a>제한 열  
 **DISCOVER_SCHEMA_ROWSETS** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**SchemaName**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
