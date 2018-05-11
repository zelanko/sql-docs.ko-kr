---
title: Source 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ef825b947a767aab3b2efb0a6e7bbc6493271c3e
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="source-element-xmla"></a>Source 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  동안 병합할 원본 파티션을 나타냅니다는 [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md) 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Sources>  
   <Source>  
      <DatabaseID>...</DatabaseID>  
      <CubeID>...</CubeID>  
      <MeasureGroupID>...</MeasureGroupID>  
      <PartitionID>...</PartitionID>  
   </Source>  
</Sources>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-n: 두 번 이상 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[원본](../../../analysis-services/xmla/xml-elements-properties/sources-element-xmla.md)|  
|자식 요소|[CubeID](../../../analysis-services/xmla/xml-elements-properties/cubeid-element-xmla.md), [DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md), [MeasureGroupID](../../../analysis-services/xmla/xml-elements-properties/measuregroupid-element-xmla.md), [PartitionID](../../../analysis-services/xmla/xml-elements-properties/partitionid-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **소스** 요소에서 지정한 대상 파티션으로 병합할 단일 파티션에 대 한 개체 참조는는 **대상** 부모 **MergePartitions** 요소입니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 `Internet Sales` 측정값 그룹의 4개 파티션을 모두 `Internet_Sales_2004` 대상 파티션으로 결합합니다. 예제 참조 하는 **Adventure Works** 의 큐브는 [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)] 샘플 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스입니다.  
  
```  
<MergePartitions xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Sources>  
     <Source>        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>        <CubeID>Adventure Works</CubeID>        <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>        <PartitionID>Internet_Sales_2001</PartitionID>     </Source>     <Source>        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>        <CubeID>Adventure Works</CubeID>      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>      <PartitionID>Internet_Sales_2002</PartitionID>    </Source>    <Source>      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>      <PartitionID>Internet_Sales_2003</PartitionID>    </Source>  
  </Sources>  
  <Target>  
    <DatabaseID Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2004</PartitionID>  
  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>참고 항목  
 [Target 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)   
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
