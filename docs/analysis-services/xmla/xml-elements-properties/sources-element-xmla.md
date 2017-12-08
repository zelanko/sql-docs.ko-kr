---
title: "소스 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
apiname: Sources Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.sources
- http://schemas.microsoft.com/analysisservices/2003/engine#Sources
- urn:schemas-microsoft-com:xml-analysis#Sources
helpviewer_keywords: Sources element
ms.assetid: fefe8f01-4c62-4b70-9bf6-f11d2f01623a
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 85d46b8d29799ec52bf3bf97fcc7f21cd6019540
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sources-element-xmla"></a>Sources 요소(XMLA)
  컬렉션을 포함 [소스](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md) 부모 [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MergePartitions>  
...  
   <Sources>  
      <Source>...</Source>  
   </Sources>  
...  
</MergePartitions>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)|  
|자식 요소|[원본](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
  
## <a name="example"></a>예제  
 다음 예에서는 `Internet Sales` 측정값 그룹의 4개 파티션을 모두 `Internet_Sales_2004` 대상 파티션으로 결합합니다. 이 예에서는 [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)] 예제 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스의 Adventure Works DW 큐브를 사용합니다.  
  
```  
<MergePartitions xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Sources>  
    <Source>  
      <DatabaseID>database</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2001</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>database</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2002</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>database</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2003</PartitionID>  
    </Source>  
  </Sources>  
  <Target>  
    <DatabaseID>database</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2004</PartitionID>  
  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
