---
title: Members 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Members Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Members
- urn:schemas-microsoft-com:xml-analysis#Members
- microsoft.xml.analysis.members
helpviewer_keywords:
- Members element
ms.assetid: 55f9ec3a-5a41-4b3a-acd6-c07598868c46
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fa1a418c0dc131f02c1afc2f2dd67810ebf90ea2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083506"
---
# <a name="members-element-xmla"></a>Members 요소(XMLA)
  컬렉션을 포함 [멤버](member-element-xmla.md) 요소는 부모에서 포함할 [CrossProduct](crossproduct-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CrossProduct>  
   <Members Hierarchy="string">  
      <Member>...</Member>  
   </Members>  
   ...  
</CrossProduct>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CrossProduct](crossproduct-element-xmla.md)|  
|자식 요소|[멤버](member-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|계층|필요한 `String` 특성입니다. `Members` 요소에 포함된 멤버가 속하는 계층의 이름입니다.|  
  
## <a name="remarks"></a>Remarks  
 클라이언트 응용 프로그램을 설정 하는 경우는 `AxisFormat` 속성을 *ClusterFormat*, 각 축의 멤버가 클러스터로 나누어집니다 각 클러스터는 각 계층의 멤버를에서 정렬 된 집합 간의 교차곱을 나타냅니다. 각 `Axis` 요소는 하나 이상의 `CrossProduct` 요소로 구성됩니다. 모든 `CrossProduct`요소에는 축의 각 계층에 대한 `Members`요소가 포함됩니다. `Members` 요소는 교차곱에 포함되어 있는 지정된 계층의 각 멤버에 대해 하나의 `Member` 요소를 포함합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는의 구조를 보여 줍니다.는 `Members` 클라이언트를 지정 하는 경우 요소 *ClusterFormat* 에 대 한는 `AxisFormat` XMLA 속성에는 축의 멤버가 다음과 같은:  
  
||||||  
|-|-|-|-|-|  
|`Time` 계층|1999|1999|2000|2001|  
|`Category` 계층|Actual|Budget|Budget|Budget|  
|Clusters|클러스터 1|클러스터 1|클러스터 1|클러스터 2|  
  
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
  
  
