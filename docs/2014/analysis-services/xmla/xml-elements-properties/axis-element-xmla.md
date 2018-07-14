---
title: Axis 요소 (XMLA) | Microsoft Docs
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
- Axis Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.axis
- http://schemas.microsoft.com/analysisservices/2003/engine#Axis
helpviewer_keywords:
- Axis element
ms.assetid: 336895e1-4a57-4b43-9a53-e31569866e6c
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e3e68903dc828f4b14ac60892d1b6fc2baed2f30
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263229"
---
# <a name="axis-element-xmla"></a>Axis 요소(XMLA)
  에 포함 된 다차원 데이터 집합의 단일 축을 나타내는 데 사용 되는 튜플의 집합을 포함를 [축](axes-element-xmla.md) 사용 하는 요소는 [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) 가 반환 되는 데이터 형식이 [Execute](../xml-elements-methods-execute.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Axes>  
   ...  
   <Axis> <!-- when AxisFormat XMLA property is set to ClusterFormat -->  
      <CrossProduct>...</CrossProduct>  
   </Axis>  
   <Axis> <!-- when AxisFormat XMLA property is set to TupleFormat or CustomFormat -->  
      <Tuples>...</Tuples>  
   </Axis>  
   ...  
</Axes>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[축](axes-element-xmla.md)|  
|자식 요소|[CrossProduct](crossproduct-element-xmla.md) 또는 [튜플](tuples-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Axis` 요소의 내용은 `AxisFormat` 메서드에 사용되는 `Execute` XMLA 속성의 값에 따라 달라집니다.  
  
## <a name="tupleformat"></a>TupleFormat  
 클라이언트 응용 프로그램을 설정 하는 경우는 `AxisFormat` 속성을 *TupleFormat*에서 축이 튜플 집합으로 표시 됩니다. 각 `Axis` 요소는 해당 축의 튜플 집합을 나타내는 `Tuples` 요소를 포함합니다. 각 튜플은 축의 모든 계층에서 `Tuple` 요소를 포함하는 `Member` 요소를 사용하여 표시됩니다.  
  
## <a name="clusterformat"></a>ClusterFormat  
 클라이언트 응용 프로그램을 설정 하는 경우는 `AxisFormat` 속성을 *ClusterFormat*, 각 축의 멤버가 클러스터로 나누어집니다 각 클러스터는 각 계층의 멤버를에서 정렬 된 집합 간의 교차곱을 나타냅니다. 각 `Axis` 요소는 하나 이상의 `CrossProduct` 요소로 구성됩니다. 모든 `CrossProduct`요소에는 축의 각 계층에 대한 `Members`요소가 포함됩니다.  
  
## <a name="customformat"></a>CustomFormat  
 클라이언트 응용 프로그램을 설정 하는 경우는 `AxisFormat` 속성을 *CustomFormat*, 처리 됩니다 동일 합니다 *TupleFormat* Analysis Services 인스턴스에서 값입니다.  
  
## <a name="examples"></a>예  
  
### <a name="description"></a>Description  
 다음 예제에서는의 구조를 보여 줍니다.는 `Axis` 클라이언트를 지정 하는 경우 요소 *TupleFormat* 하거나 *CustomFormat* 에 대 한를 `AxisFormat` XMLA 속성에 다음 축의 멤버:  
  
|||||  
|-|-|-|-|  
|`Time` 계층|1999|1999|2000|  
|`Category` 계층|Actual|Budget|Budget|  
  
### <a name="code"></a>코드  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <Tuples>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Actual]</UName>  
               ...  
            </Member>  
         </Tuple>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Tuple>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[2000]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Tuple>  
      </Tuples>  
   </Axis>  
   ...  
</Axes>  
```  
  
### <a name="description"></a>Description  
 다음 예제에서는의 구조를 보여 줍니다.는 `Axis` 클라이언트를 지정 하는 경우 요소 *ClusterFormat* 에 대 한는 `AxisFormat` XMLA 속성에는 축의 멤버가 다음과 같은:  
  
||||||  
|-|-|-|-|-|  
|`Time` 계층|1999|1999|2000|2001|  
|`Category` 계층|Actual|Budget|Budget|Budget|  
|Clusters|클러스터 1|클러스터 1|클러스터 1|클러스터 2|  
  
### <a name="code"></a>코드  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <CrossProduct Size = "4">  
         <Members Hierarchy="Time">  
            <Member>  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member>  
               <UName>[Time].[2000]</UName>  
               ...  
            </Member>  
         </Members>  
         <Members Hierarchy="Category">  
            <Member>  
               <UName>[Scenario].[Actual]</UName>  
               ...  
            </Member>  
            <Member>  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Members>  
      </CrossProduct>  
      <CrossProduct Size = "1">  
         <Members Hierarchy="Time">  
            <Member>  
               <UName>[Time].[2001]</UName>  
               ...  
            </Member>  
         </Members>  
         <Members Hierarchy="Category">  
            <Member>  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Members>  
      </CrossProduct>  
   </Axis>  
   ...  
</Axes>  
```  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
