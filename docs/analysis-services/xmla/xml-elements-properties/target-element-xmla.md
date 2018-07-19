---
title: Target 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 53cf0589cff69dab21c07979ba89e84e35f30d11
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38064140"
---
# <a name="target-element-xmla"></a>Target 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  하는 동안 병합할 대상 파티션을 나타냅니다는 [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md) 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MergePartitions>  
   <Target>  
      <DatabaseID>...</DatabaseID>  
      <CubeID>...</CubeID>  
      <MeasureGroupID>...</MeasureGroupID>  
      <PartitionID>...</PartitionID>  
   </Target>  
</MergePartitions>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-n: 두 번 이상 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)|  
|자식 요소|[CubeID](../../../analysis-services/xmla/xml-elements-properties/cubeid-element-xmla.md)하십시오 [DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md)합니다 [MeasureGroupID](../../../analysis-services/xmla/xml-elements-properties/measuregroupid-element-xmla.md), [PartitionID](../../../analysis-services/xmla/xml-elements-properties/partitionid-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 합니다 **대상** 요소는 원본 파티션의 내용을 지정 된는 단일 파티션에 대 한 개체 참조는 [원본](../../../analysis-services/xmla/xml-elements-properties/sources-element-xmla.md) 부모 요소의 **MergePartitions** 요소를 병합할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Internet Sales 측정값 그룹의 4개 파티션을 모두 `Internet_Sales_2004` 대상 파티션에 결합합니다. 이 예에서는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]의 예제 데이터베이스인 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 큐브를 참조합니다.  
  
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
  <Target>    <DatabaseID>database</DatabaseID>    <CubeID>Adventure Works DW</CubeID>    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>    <PartitionID>Internet_Sales_2004</PartitionID>  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>참고자료
 [Source 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)   
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
