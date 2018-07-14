---
title: Tuple 요소 (XMLA) | Microsoft Docs
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
- Tuple Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.tuple
- urn:schemas-microsoft-com:xml-analysis#Tuple
- http://schemas.microsoft.com/analysisservices/2003/engine#Tuple
helpviewer_keywords:
- Tuple element
ms.assetid: d65aba10-55e1-49c1-81bc-0756c39c0da2
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5db226260852207fbcfeb4dc0a071d03d0def7c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233693"
---
# <a name="tuple-element-xmla"></a>Tuple 요소(XMLA)
  부모 [Tuples](tuples-element-xmla.md) 요소에 포함된 [Member](member-element-xmla.md) 요소의 컬렉션을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Tuples>  
   <Tuple>  
      <Member>...</Member>  
   </Tuple>  
   ...  
</Tuples>  
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
|부모 요소|[튜플](tuples-element-xmla.md)|  
|자식 요소|[멤버](member-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 클라이언트 응용 프로그램을 설정 하는 경우는 `AxisFormat` 속성을 *TupleFormat*에서 축이 튜플 집합으로 표시 됩니다. 각 `Axis` 요소는 해당 축의 튜플 집합을 나타내는 `Tuples` 요소를 포함합니다. 각 튜플은 축의 모든 계층에서 `Tuple` 요소를 포함하는 `Member` 요소를 사용하여 표시됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는의 구조를 보여 줍니다.는 `Tuple` 클라이언트를 지정 하는 경우 요소 *TupleFormat* 또는 *CustomFormat* 에 대 한는 `AxisFormat` XMLA 속성에 다음 축의 멤버:  
  
|||||  
|-|-|-|-|  
|`Time` 계층|1999|1999|2000|  
|`Category` 계층|Actual|Budget|Budget|  
  
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
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
