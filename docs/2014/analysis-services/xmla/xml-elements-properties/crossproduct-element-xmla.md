---
title: CrossProduct 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CrossProduct Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CrossProduct
- microsoft.xml.analysis.crossproduct
- urn:schemas-microsoft-com:xml-analysis#CrossProduct
helpviewer_keywords:
- CrossProduct element
ms.assetid: a9a1584e-d2dd-45db-a918-d694c20d8189
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 1324a3c9449383301242ab6d0e76f94c636d9b5e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081209"
---
# <a name="crossproduct-element-xmla"></a>CrossProduct 요소(XMLA)
  에 대 한 각 계층의 멤버를에서 정렬 된 집합 간의 교차곱을 포함 한 [축](axis-element-xmla.md) 요소를 사용 하는 [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) 가 반환 되는 데이터 형식이 [Execute](../xml-elements-methods-execute.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Axis>  
   ...  
   <CrossProduct Size="integer">  
      <Members>...</Members>  
   </CrossProduct>  
   ...  
</Axis>  
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
|부모 요소|[Axis](axis-element-xmla.md)|  
|자식 요소|[멤버](members-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|크기|필요한 `Integer` 특성입니다. `CrossProduct` 요소에서 나타내는 교차곱에 포함된 튜플 수를 표시합니다.|  
  
## <a name="remarks"></a>Remarks  
 클라이언트 응용 프로그램 설정 하는 경우는 `AxisFormat` 속성을 *ClusterFormat*, 각 축의 멤버가 각 클러스터는 각 계층의 멤버를에서 정렬 된 집합 간의 교차곱을 나타내는 클러스터로 나누어집니다. 각 클러스터는 `CrossProduct` 요소로 표현됩니다. 모든 `CrossProduct`요소에는 축의 각 계층에 대한 `Members`요소가 포함됩니다. `CrossProduct` 요소는 단일 계층의 멤버를 포함할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는의 구조는 `CrossProduct` 요소는 클라이언트를 지정 하는 경우 *ClusterFormat* 에 대 한는 `AxisFormat` 축에 대 한 다음과 같은 멤버를 제공 하는 XMLA 속성:  
  
||||||  
|-|-|-|-|-|  
|`Time` 계층|1999|1999|2000|2001|  
|`Category` 계층|Actual|Budget|Budget|Budget|  
|Clusters|클러스터 1|클러스터 1|클러스터 1|클러스터 2|  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <CrossProduct Size="4">  
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
      <CrossProduct Size="1">  
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
  
  