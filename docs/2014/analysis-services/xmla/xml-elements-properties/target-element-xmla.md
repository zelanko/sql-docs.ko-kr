---
title: Target 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Target Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.target
- http://schemas.microsoft.com/analysisservices/2003/engine#Target
- urn:schemas-microsoft-com:xml-analysis#Target
helpviewer_keywords:
- Target element
ms.assetid: 9a69a777-5f34-4e94-b470-6bab2a98df8b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97d198e823acb9bf3c8915e18cbf723032f81b58
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079793"
---
# <a name="target-element-xmla"></a>Target 요소(XMLA)
  하는 동안 병합할 대상 파티션을 나타냅니다는 [MergePartitions](../xml-elements-commands/mergepartitions-element-xmla.md) 명령입니다.  
  
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
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-n: 두 번 이상 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MergePartitions](../xml-elements-commands/mergepartitions-element-xmla.md)|  
|자식 요소|[CubeID](id-element-xmla.md)하십시오 [DatabaseID](databaseid-element-xmla.md)합니다 [MeasureGroupID](measuregroupid-element-xmla.md), [PartitionID](partitionid-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Target` 요소는 원본 파티션의 내용을 지정 된는 단일 파티션에 대 한 개체 참조를 [원본](sources-element-xmla.md) 부모 요소의 `MergePartitions` 요소를 병합할 파티션은 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [Source 요소 &#40;XMLA&#41;](source-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
