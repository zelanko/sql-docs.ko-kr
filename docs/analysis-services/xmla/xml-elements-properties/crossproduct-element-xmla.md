---
title: CrossProduct 요소 (XMLA) | Microsoft Docs
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
- CrossProduct Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CrossProduct
- microsoft.xml.analysis.crossproduct
- urn:schemas-microsoft-com:xml-analysis#CrossProduct
helpviewer_keywords:
- CrossProduct element
ms.assetid: a9a1584e-d2dd-45db-a918-d694c20d8189
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 60c8eb9a40408471fdd29ebfa5bb89fcc3fbd755
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="crossproduct-element-xmla"></a>CrossProduct 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  에 대 한 각 계층의 멤버를에서 정렬 된 집합 간의 교차곱을 포함 한 [축](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md) 요소를 사용 하는 [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) 가 반환 되는 데이터 형식이 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드.  
  
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[축](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
|자식 요소|[멤버](../../../analysis-services/xmla/xml-elements-properties/members-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|Attribute|Description|  
|---------------|-----------------|  
|크기|필요한 **정수** 특성입니다. 가 나타내는 교차곱에 포함 된 튜플 수를 나타내는 **CrossProduct** 요소입니다.|  
  
## <a name="remarks"></a>주의  
 클라이언트 응용 프로그램 설정 하는 경우는 **a x** 속성을 *ClusterFormat*, 각 축의 멤버가 각 클러스터의 정렬 된 집합 간의 교차곱을 나타냅니다 하는 클러스터로 나누어집니다. 각 계층의 멤버입니다. 각 클러스터로 표시 됩니다는 **CrossProduct** 요소입니다. 모든 **CrossProduct** 요소를 포함 한 **멤버** 축의 각 계층에 대 한 요소입니다. A **CrossProduct** 요소는 단일 계층 구조의 멤버를 포함할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는의 구조는 **CrossProduct** 요소는 클라이언트를 지정 하는 경우 *ClusterFormat* 에 대 한는 **a x** 제공 되는 XMLA 속성인은 축에 대 한 다음과 같은 멤버:  
  
||||||  
|-|-|-|-|-|  
|**시간** 계층|1999|1999|2000|2001|  
|**범주** 계층|Actual|Budget|Budget|Budget|  
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
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
