---
title: Tuples 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c0578c541c39bdaceede6bff8afdea3d642abcef
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38062547"
---
# <a name="tuples-element-xmla"></a>Tuples 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  집합을 포함 [튜플](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md) 개체에 대 한는 [축](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md) 사용 하는 요소는 [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) 가 반환 되는 데이터 형식이 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Axis>  
   ...  
   <Tuples>  
      <Tuple>...</Tuple>  
   </Tuples>  
   ...  
</Axis>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Axis](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
|자식 요소|[튜플](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 클라이언트 응용 프로그램에서 **AxisFormat** 속성을 *TupleFormat*으로 설정하면 축이 튜플 집합으로 표시됩니다. 각 **Axis** 요소는 해당 축의 튜플 집합을 나타내는 **Tuples** 요소를 포함합니다. 각 튜플은 축의 모든 계층에서 [Member](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) 요소를 포함하는 **Tuple** 요소를 사용하여 나타냅니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는의 구조를 보여 줍니다.는 **튜플** 클라이언트를 지정 하는 경우 요소 *TupleFormat* 또는 *CustomFormat* 에 대 한는 **AxisFormat**  XML for Analysis (XMLA) 속성, 축에 대 한 다음과 같은 멤버를 지정 합니다.  
  
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
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
