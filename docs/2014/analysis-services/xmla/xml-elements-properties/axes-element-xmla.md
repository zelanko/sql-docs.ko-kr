---
title: 요소 (XMLA) 축 | Microsoft Docs
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
- Axes Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Axes
- http://schemas.microsoft.com/analysisservices/2003/engine#Axes
- microsoft.xml.analysis.axes
- urn:schemas-microsoft-com:xml-analysis#Axes
helpviewer_keywords:
- Axes element
ms.assetid: 2005d06a-f8a2-4b4f-8c0d-2f7f73eb6f5c
caps.latest.revision: 21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b8ac4baded4dd516e12c31ffd701e1c4668d769e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237403"
---
# <a name="axes-element-xmla"></a>Axes 요소(XMLA)
  컬렉션을 포함 [축](axis-element-xmla.md) 에 포함 된 축 데이터를 나타내는 요소를 [루트](root-element-xmla.md) 요소를 사용 하는 [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) 데이터 형식.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">  
   ...  
   <Axes>  
      <Axis>...</Axis>  
   </Axes>  
   ...  
</root>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|전체|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[root](root-element-xmla.md)|  
|자식 요소|[Axis](axis-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Axes` 요소 아래에는  `Axis` 요소가 발생한 순서대로 0부터 시작하여 데이터 집합에 나열됩니다. `AxisFormat` XMLA 속성 설정은 `Axis` 요소의 서식이 지정되는 방식을 결정합니다. 에 대 한 자세한 내용은 합니다 `AxisFormat` 속성을 참조 하세요 [지원 되는 XMLA 속성 &#40;XMLA&#41;](propertylist-element-supported-xmla-properties.md)합니다.  
  
 축은 튜플의 집합을 나타내며 여기서 집합의 모든 튜플은 차원이 동일합니다. 집합은 각기 다른 이점이 있는 다양한 방식으로 나타낼 수 있습니다. 예를 들어 다음 네 튜플의 집합은 2차원 튜플의 컬렉션 또는 1차원 집합 두 개의 카티션 곱으로 나타낼 수 있습니다.  
  
|1999|1999|2000|2000|  
|----------|----------|----------|----------|  
|Actual|Budget|Actual|Budget|  
  
 이 튜플의 집합을 다음과 같이 2차원 튜플의 컬렉션으로 나타낼 수 있습니다.  
  
```  
{ ( 1999, Actual ), ( 1999, Budget ), ( 2000, Actual ), ( 2000, Budget ) }  
```  
  
 또한 다음과 같이 1차원 집합 두 개의 카티션 곱으로 나타낼 수 있습니다.  
  
```  
{ 1999, 2000 } x { Actual, Budget }  
```  
  
 첫 번째 표현인 2차원 튜플은 클라이언트 도구에서 사용하기에 더욱 편리합니다. 두 번째 표현인 1차원 집합의 카티션 곱은 적은 공간을 사용하며 집합의 다차원 특성을 유지합니다.  
  
 다음 표에서는 축의 구조와 멤버를 정의하고 특징을 결정하는 데 사용할 수 있는 작업을 나열합니다.  
  
|연산|Description|  
|---------------|-----------------|  
|멤버|차원 계층의 멤버를 나타내는 축의 가장 작은 단위입니다.|  
|멤버|동일한 차원 계층의 `Member` 개체 컬렉션입니다.|  
|Tuple|다른 차원 계층의 멤버 컬렉션입니다.|  
|튜플|동일한 차원의 `Tuple` 개체 컬렉션입니다.|  
|Union|집합의 합집합입니다.|  
|CrossJoin|집합의 카티션 곱입니다.|  
  
 이러한 작업은 2차원 튜플 및 1차원 집합의 카티션 곱을 다음과 같이 변환합니다.  
  
## <a name="two-dimensional-tuples"></a>2차원 튜플  
  
```  
Tuples (  
   Tuple( Member(1999), Member(Actual) ),  
   Tuple( Member(1999), Member(Budget) ),  
   Tuple( Member(2000), Member(Actual) ),  
   Tuple( Member(2000), Member(Budget) )  
```  
  
## <a name="cartesian-product-of-one-dimensional-sets"></a>1차원 집합의 카티션 곱  
  
```  
CrossProduct (  
   Members( Member(1999), Member(2000) ),  
   Members( Member(Actual), Member(Budget) )  
```  
  
 클라이언트는 `AxisFormat` 속성을 사용하여 특정 표현을 요청할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDDataSet 데이터 형식 &#40;XMLA&#41;](../xml-data-types/mddataset-data-type-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
