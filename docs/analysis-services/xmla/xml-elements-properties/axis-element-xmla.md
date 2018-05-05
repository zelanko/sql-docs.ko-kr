---
title: Axis 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Axis Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.axis
- http://schemas.microsoft.com/analysisservices/2003/engine#Axis
helpviewer_keywords:
- Axis element
ms.assetid: 336895e1-4a57-4b43-9a53-e31569866e6c
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 136ce9c4b39d0b9a93abc491850b63783ff4bf1c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="axis-element-xmla"></a>Axis 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  에 포함 된 다차원 데이터 집합의 단일 축을 나타내는 데 사용 되는 튜플 집합을 포함 한 [축](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md) 요소를 사용 하는 [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) 가 반환 되는 데이터 형식이 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드.  
  
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[축](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md)|  
|자식 요소|[CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md) 또는 [튜플](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 콘텐츠는 **축** 요소 값에 따라 달라 집니다.는 **a x** 에서 사용 하는 XMLA 속성의 **Execute** 메서드.  
  
## <a name="tupleformat"></a>TupleFormat  
 클라이언트 응용 프로그램에서 **AxisFormat** 속성을 *TupleFormat*으로 설정하면 축이 튜플 집합으로 표시됩니다. 각 **축** 요소를 포함 한 **튜플** 해당 축의 튜플 집합을 나타내는 요소입니다. 각 튜플은 축의 모든 계층에서 **Member** 요소를 포함하는 **Tuple** 요소를 사용하여 나타냅니다.  
  
## <a name="clusterformat"></a>ClusterFormat  
 클라이언트 응용 프로그램 설정 하는 경우는 **a x** 속성을 *ClusterFormat*, 각 축의 멤버가 각 클러스터의 정렬 된 집합 간의 교차곱을 나타냅니다 하는 클러스터로 나누어집니다. 각 계층의 멤버입니다. 각 **축** 요소는 하나 이상의 구성 됩니다. **CrossProduct** 요소입니다. 모든 **CrossProduct** 요소를 포함 한 **멤버** 축의 각 계층에 대 한 요소입니다.  
  
## <a name="customformat"></a>CustomFormat  
 클라이언트 응용 프로그램 설정 하는 경우는 **a x** 속성을 *CustomFormat*, 고 값이 처리 동일는 *TupleFormat* Analysis Services 인스턴스에서 값입니다.  
  
## <a name="examples"></a>예  
  
### <a name="description"></a>Description  
 다음 예제에서는의 구조는 **축** 클라이언트를 지정 하는 경우 요소 *TupleFormat* 또는 *CustomFormat* 에 대 한는 **a x**  축에 대 한 다음과 같은 멤버를 제공 하는 XMLA 속성:  
  
|||||  
|-|-|-|-|  
|**시간** 계층|1999|1999|2000|  
|**범주** 계층|Actual|Budget|Budget|  
  
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
 다음 예제에서는의 구조는 **축** 클라이언트를 지정 하는 경우 요소 *ClusterFormat* 에 대 한는 **a x** 다음을 지정 하는 XMLA 속성인 축의 멤버:  
  
||||||  
|-|-|-|-|-|  
|**시간** 계층|1999|1999|2000|2001|  
|**범주** 계층|Actual|Budget|Budget|Budget|  
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
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
