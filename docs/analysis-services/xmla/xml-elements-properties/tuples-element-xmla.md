---
title: "Tuples 요소 (XMLA) | Microsoft Docs"
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
apiname: Tuples Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Tuples
- microsoft.xml.analysis.tuples
- urn:schemas-microsoft-com:xml-analysis#Tuples
helpviewer_keywords: Tuples element
ms.assetid: 5494bbaa-c1aa-43fa-b3e0-83befb2bccdd
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 96ae916c249be7fddbf3c66e25a7b213740cbd6b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="tuples-element-xmla"></a>Tuples 요소(XMLA)
  집합이 포함 되어 [튜플](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md) 에 대 한 개체는 [축](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md) 요소를 사용 하는 [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) 가 반환 되는 데이터 형식이 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드.  
  
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
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Axis](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
|자식 요소|[튜플](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 클라이언트 응용 프로그램에서 **AxisFormat** 속성을 *TupleFormat*으로 설정하면 축이 튜플 집합으로 표시됩니다. 각 **Axis** 요소는 해당 축의 튜플 집합을 나타내는 **Tuples** 요소를 포함합니다. 각 튜플은 축의 모든 계층에서 [Member](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) 요소를 포함하는 **Tuple** 요소를 사용하여 나타냅니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는의 구조는 **튜플** 요소는 클라이언트를 지정 하는 경우 *TupleFormat* 또는 *CustomFormat* 에 대 한는 **a x**  XML for Analysis (XMLA) 속성을 축에 대 한 다음과 같은 멤버를 제공 합니다.  
  
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
  
  
