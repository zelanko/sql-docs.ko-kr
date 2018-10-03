---
title: AxisInfo 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AxisInfo Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#AxisInfo
- microsoft.xml.analysis.axisinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#AxisInfo
helpviewer_keywords:
- AxisInfo element
ms.assetid: 060741db-b2ec-4174-9277-58d996440a88
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 04e1ce189d38a77a09db6ee9649f5743cac8c7d4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48194973"
---
# <a name="axisinfo-element-xmla"></a>AxisInfo 요소(XMLA)
  부모에 의해 포함 된 단일 축의 메타 데이터를 나타냅니다 [AxesInfo](axesinfo-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<AxesInfo>  
   ...  
   <AxisInfo name="string">  
      <HierarchyInfo>...</HierarchyInfo>  
   </AxisInfo>  
   ...  
</AxesInfo>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|1-n: 두 번 이상 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AxesInfo](axesinfo-element-xmla.md)|  
|자식 요소|[HierarchyInfo](hierarchyinfo-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|이름|필요한 `String` 특성입니다. 축의 이름입니다.|  
  
## <a name="remarks"></a>Remarks  
 `root` 개체를 사용하는 `MDDataSet` 요소에서 `AxisInfo` 요소는 `HierarchyInfo` 특성의 값과 결합되어 다차원 데이터 집합에 반환되는 단일 축의 정의를 나타내는 `name` 요소의 컬렉션을 포함합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
