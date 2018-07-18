---
title: 소스 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5466ee4ed04b7890718e5d613cbade3f37cd6929
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38019801"
---
# <a name="sources-element-xmla"></a>Sources 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)|  
|자식 요소|[원본](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
  
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
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
