---
title: "Tuple 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Tuple Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.tuple
- urn:schemas-microsoft-com:xml-analysis#Tuple
- http://schemas.microsoft.com/analysisservices/2003/engine#Tuple
helpviewer_keywords:
- Tuple element
ms.assetid: d65aba10-55e1-49c1-81bc-0756c39c0da2
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 11a9d3b633e680154787615c04ee1f08b65b8139
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="tuple-element-xmla"></a>Tuple 요소(XMLA)
  부모 [Tuples](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md) 요소에 포함된 [Member](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) 요소의 컬렉션을 포함합니다.  
  
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[튜플](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md)|  
|자식 요소|[멤버](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 클라이언트 응용 프로그램에서 **AxisFormat** 속성을 *TupleFormat*으로 설정하면 축이 튜플 집합으로 표시됩니다. 각 **Axis** 요소는 해당 축의 튜플 집합을 나타내는 **Tuples** 요소를 포함합니다. 각 튜플은 축의 모든 계층에서 **Member** 요소를 포함하는 **Tuple** 요소를 사용하여 나타냅니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 축의 멤버가 다음과 같은 경우 클라이언트가 **AxisFormat** XMLA 속성에 대해 *TupleFormat* 또는 *CustomFormat*을 지정할 때 **Tuple** 요소의 구조를 보여 줍니다.  
  
|||||  
|-|-|-|-|  
|**시간** 계층|1999|1999|2000|  
|**범주** 계층|Actual|Budget|Budget|  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

