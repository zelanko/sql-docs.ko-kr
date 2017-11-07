---
title: "파티션 병합 (XMLA) | Microsoft Docs"
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- merging partitions [XMLA]
- XMLA, partitions
- partitions [Analysis Services], XML for Analysis
- XML for Analysis, partitions
ms.assetid: 657e1d4d-6d50-40f8-a771-7b20c9d865f8
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5528a4392eb5e6554cafc179e0ceedc14b26c0c7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="merging-partitions-xmla"></a>파티션 병합(XMLA)
  사용 하 여 파티션을 병합할 수 파티션이 동일한 집계 디자인 및 구조를 있으면는 [MergePartitions](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md) xml for Analysis (XMLA) 명령입니다. 파티션 병합은 파티션을 관리할 때 수행하는 중요한 동작으로, 특히 날짜별로 파티션된 기록 데이터가 들어 있는 파티션을 관리하는 데 유용합니다.  
  
 예를 들어, 재무 큐브에서 다음과 같은 파티션 2개를 사용할 수 있습니다.  
  
-   한 파티션은 올해의 재무 데이터를 나타내며 성능을 위해 실시간 ROLAP(관계형 OLAP) 저장소 설정을 사용합니다.  
  
-   다른 파티션은 작년의 재무 데이터를 나타내며 저장을 위해 MOLAP(다차원 OLAP) 저장소 설정을 사용합니다.  
  
 두 파티션에 사용된 저장소 설정은 서로 다르지만 집계 디자인은 같습니다. 끝 연도에 기록 데이터를 연도별로 큐브를 처리 하는 대신 대신 사용할 수 있습니다는 **MergePartitions** 을 이전 연도의 파티션을 현재 연도 대 한 파티션을 병합 하려면 명령입니다. 이렇게 하면 많은 시간이 소요될 수 있는 전체 큐브 처리 작업을 수행하지 않고도 집계 데이터를 유지할 수 있습니다.  
  
## <a name="specifying-partitions-to-merge"></a>병합할 파티션 지정  
 경우는 **MergePartitions** 명령 실행에 지정 된 원본 파티션에 저장 된 집계 데이터는 [소스](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md) 속성에 지정 된 대상 파티션에 추가 [대상 ](../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md) 속성입니다.  
  
> [!NOTE]  
>  **소스** 속성 둘 이상의 파티션 개체 참조를 포함할 수 있습니다. 그러나는 **대상** 속성 수 없습니다.  
  
 성공적으로 병합 하려면, 둘 다에 지정 된 파티션에 **소스** 및 **대상** 동일한 집계 디자인을 사용 하는 같은 측정값 그룹에 포함 되어야 합니다. 그렇지 않으면 오류가 발생합니다.  
  
 에 지정 된 파티션에 **소스** 이후에 삭제 됩니다.는 **MergePartitions** 명령이 성공적으로 완료 되어야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="description"></a>Description  
 다음 예에서는 병합의 모든 파티션에 **Customer Counts** 의 측정값 그룹은 **Adventure Works** 큐브에 **Adventure Works DW** 샘플 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스는 **Customers_2004** 파티션 합니다.  
  
### <a name="code"></a>코드  
  
```  
<MergePartitions xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Sources>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2001</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2002</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2003</PartitionID>  
    </Source>  
  </Sources>  
  <Target>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2004</PartitionID>  
  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services에서 XMLA를 사용 하 여 개발](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

