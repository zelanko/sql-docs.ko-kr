---
title: "AxisInfo 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AxisInfo Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#AxisInfo
- microsoft.xml.analysis.axisinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#AxisInfo
helpviewer_keywords: AxisInfo element
ms.assetid: 060741db-b2ec-4174-9277-58d996440a88
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ad12131fe961f279bf0d670d91ab03900a8a6ad1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="axisinfo-element-xmla"></a>AxisInfo 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]부모에 의해 포함 된 단일 축의 메타 데이터를 나타내는 [AxesInfo](../../../analysis-services/xmla/xml-elements-properties/axesinfo-element-xmla.md) 요소입니다.  
  
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
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-n: 두 번 이상 나타날 수 있는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[AxesInfo](../../../analysis-services/xmla/xml-elements-properties/axesinfo-element-xmla.md)|  
|자식 요소|[HierarchyInfo](../../../analysis-services/xmla/xml-elements-properties/hierarchyinfo-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|속성|필수 **String** 특성입니다. 축의 이름입니다.|  
  
## <a name="remarks"></a>주의  
 에 **루트** 요소를 사용 하는 **MDDataSet** 개체는 **AxisInfo** 의 컬렉션을 포함 하는 요소 **HierarchyInfo** 요소는 의 값과 함께 사용 된 **이름** 특성에는 다차원 데이터 집합에 반환 된 단일 축의 정의 나타냅니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
