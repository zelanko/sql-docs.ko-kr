---
title: "Members 요소 (XMLA) | Microsoft Docs"
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
apiname: Members Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Members
- urn:schemas-microsoft-com:xml-analysis#Members
- microsoft.xml.analysis.members
helpviewer_keywords: Members element
ms.assetid: 55f9ec3a-5a41-4b3a-acd6-c07598868c46
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2d2b4f8a9c466fa85bdd1131a58c2c11fc232967
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="members-element-xmla"></a>Members 요소(XMLA)
  컬렉션을 포함 [멤버](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) 부모에 포함 된 요소 [CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md) 요소입니다.  
  
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md)|  
|자식 요소|[멤버](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|Attribute|설명|  
|---------------|-----------------|  
|계층|필수 **String** 특성입니다. 에 포함 된 멤버를 계층의 이름에서 **멤버** 요소 속해야 합니다.|  
  
## <a name="remarks"></a>주의  
 클라이언트 응용 프로그램 설정 하는 경우는 **a x** 속성을 *ClusterFormat*, 각 축의 멤버가 각 클러스터의 정렬 된 집합 간의 교차곱을 나타냅니다 하는 클러스터로 나누어집니다. 각 계층의 멤버입니다. 각 **축** 요소는 하나 이상의 구성 됩니다. **CrossProduct** 요소입니다. 모든 **CrossProduct** 요소를 포함 한 **멤버** 축의 각 계층에 대 한 요소입니다. **멤버** 요소를 포함 하나 **멤버** 요소는 교차곱에 포함 된 지정 된 계층의 각 멤버에 대 한 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는의 구조는 **멤버** 요소는 클라이언트를 지정 하는 경우 *ClusterFormat* 에 대 한는 **a x** 제공 되는 XMLA 속성인은 축에 대 한 다음과 같은 멤버:  
  
||||||  
|-|-|-|-|-|  
|**시간** 계층|1999|1999|2000|2001|  
|**범주** 계층|Actual|Budget|Budget|Budget|  
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
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
