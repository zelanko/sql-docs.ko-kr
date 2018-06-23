---
title: Tuples 요소 (XMLA) | Microsoft Docs
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
- Tuples Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Tuples
- microsoft.xml.analysis.tuples
- urn:schemas-microsoft-com:xml-analysis#Tuples
helpviewer_keywords:
- Tuples element
ms.assetid: 5494bbaa-c1aa-43fa-b3e0-83befb2bccdd
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: da9614fb01620a3dec5bdff9f63d044652a4749b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182643"
---
# <a name="tuples-element-xmla"></a>Tuples 요소(XMLA)
  집합이 포함 되어 [튜플](tuple-element-xmla.md) 에 대 한 개체는 [축](axis-element-xmla.md) 요소를 사용 하는 [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) 가 반환 되는 데이터 형식이 [Execute](../xml-elements-methods-execute.md) 메서드.  
  
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Axis](axis-element-xmla.md)|  
|자식 요소|[튜플](tuple-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 클라이언트 응용 프로그램 설정 하는 경우는 `AxisFormat` 속성을 *TupleFormat*, 축이 튜플 집합을로 표시 됩니다. 각 `Axis` 요소는 해당 축의 튜플 집합을 나타내는 `Tuples` 요소를 포함합니다. 사용 하 여 각 튜플에 표시 됩니다는 `Tuple` 포함 된 요소 [멤버](member-element-xmla.md) 축의 모든 계층에서 요소입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는의 구조는 `Tuples` 요소는 클라이언트를 지정 하는 경우 *TupleFormat* 또는 *CustomFormat* 에 대 한는 `AxisFormat` XML for Analysis (XMLA) 속성 축에 대 한 다음과 같은 멤버를 가정합니다.  
  
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
  
  