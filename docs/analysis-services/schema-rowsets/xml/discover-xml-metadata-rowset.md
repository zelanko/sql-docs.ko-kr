---
title: "DISCOVER_XML_METADATA 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DISCOVER_XML_METADATA
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_XML_METADATA rowset
ms.assetid: 0befd026-db1b-43ac-b0e6-734abb56a4b1
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d0f2a0a63ff4d08a3a273f303a956b49f4932a21
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="discoverxmlmetadata-rowset"></a>DISCOVER_XML_METADATA 행 집합
  요청된 개체를 설명하는 XML 문서를 반환합니다. 반환되는 행 집합은 항상 하나의 행과 하나의 열로 구성됩니다.  
  
 호출 하는 경우는 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드는 **DISCOVER_XML_METATDATA** 열거 값은 [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) 요소는 **Discover**메서드가 반환 되는 **DISCOVER_XML_METATDATA** 행 집합입니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_XML_METADATA** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**메타 데이터**|**DBTYPE_WSTR**||제한에 의해 요청된 개체를 설명하는 XML 문서입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
> [!IMPORTANT]  
>  SELECT 명령 구문을 사용하여 **DISCOVER_XML_METADATA** 행 집합을 쿼리할 수 없습니다. 그러나는 **DISCOVER_XML_METADATA** 를 사용 하 여 행 집합을 쿼리할 수 있는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>합니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DISCOVER_XML_METADATA** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**DatabaseID**|**DBTYPE_WSTR**|(선택 사항)|  
|**DimensionID**|**DBTYPE_WSTR**|(선택 사항)|  
|**CubeID**|**DBTYPE_WSTR**|(선택 사항)|  
|**MeasureGroupID**|**DBTYPE_WSTR**|(선택 사항)|  
|**PartitionID**|**DBTYPE_WSTR**|(선택 사항)|  
|**PerspectiveID**|**DBTYPE_WSTR**|(선택 사항)|  
|**DimensionPermissionID**|**DBTYPE_WSTR**|(선택 사항)|  
|**RoleID**|**DBTYPE_WSTR**|(선택 사항)|  
|**DatabasePermissionID**|**DBTYPE_WSTR**|(선택 사항)|  
|**MiningModelID**|**DBTYPE_WSTR**|(선택 사항)|  
|**MiningModelPermissionID**|**DBTYPE_WSTR**|(선택 사항)|  
|**DataSourceID**|**DBTYPE_WSTR**|(선택 사항)|  
|**MiningStructureID**|**DBTYPE_WSTR**|(선택 사항)|  
|**AggregationDesignID**|**DBTYPE_WSTR**|(선택 사항)|  
|**Traceid가**|**DBTYPE_WSTR**|(선택 사항)|  
|**MiningStructurePermissionID**|**DBTYPE_WSTR**|(선택 사항)|  
|**CubePermissionID**|**DBTYPE_WSTR**|(선택 사항)|  
|**AssemblyID**|**DBTYPE_WSTR**|(선택 사항)|  
|**MdxScriptID**|**DBTYPE_WSTR**|(선택 사항)|  
|**DataSourceViewID**|**DBTYPE_WSTR**|(선택 사항)|  
|**DataSourcePermissionID**|**DBTYPE_WSTR**|(선택 사항)|  
|**ObjectExpansion**|**DBTYPE_WSTR**|(선택 사항)|  
  
 제한은 **ObjectExpansion**의 모든 주요 개체에 사용할 수 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다. 일반적으로 클라이언트는 제한을 사용하여 DDL이 반환되는 OLAP 개체를 설명하며, **ObjectExpansion** 제한을 사용하여 반환된 DDL의 확장 수준을 정의합니다. 다음 표는 열거형 값에 대 한 허용 되는지 여부를 나타냅니다. [Alter 요소 &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) 명령입니다.  
  
|열거 값|Description|  
|-----------------------|-----------------|  
|**ReferenceOnly**|요청된 개체 및 모든 하위 주요 개체에 대해 요청된 이름/ID/타임스탬프/상태만 재귀적으로 반환합니다.|  
|**ObjectProperties**|포함된 개체에 대한 참조가 없는 요청된 개체를 확장합니다(확장되고 포함된 보조 개체 포함).|  
|**ExpandObject**|*ObjectProperties*와 같지만 포함된 주요 개체에 대한 이름, ID 및 타임스탬프도 반환합니다.|  
|**ExpandFull**|요청된 개체를 포함된 모든 개체의 맨 아래까지 재귀적으로 완전히 확장합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

