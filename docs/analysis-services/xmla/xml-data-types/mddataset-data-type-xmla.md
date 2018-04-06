---
title: MDDataSet 데이터 형식 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MDDataSet Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#MDDataSet
- MDDataSet
- urn:schemas-microsoft-com:xml-analysis#MDDataSet
helpviewer_keywords:
- MDDataSet data type
ms.assetid: 1a7e0092-f9f0-4ae5-ba27-ad1d8ebe8cb9
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 382c3badf6b31e99c707c9adce011c278df82280
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="mddataset-data-type-xmla"></a>MDDataSet 데이터 형식(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]반환 된 다차원 데이터를 나타내는 파생된 데이터 형식을 정의 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드.  
  
 **Namespace** :-microsoft-com:xml-분석: mddataset  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <!-- The following elements extend Resultset -->  
   <!-- Optional schema elements -->  
   <OlapInfo>...</OlapInfo>  
   <Axes>...</Axes>  
   <CellData>...</CellData>  
</root>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[결과 집합](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[축](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md), [CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md), [OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|파생 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 **MDDataSet** 는 OLAP 기반 행 집합 (또는 데이터 집합) OLAP 데이터를 XML 나타내는 데 필요한 데이터 형식은 제공 합니다. 이 행 집합의 콘텐츠 값에 따라 달라질 수 있습니다는 **콘텐츠** 및 **형식** 속성에는 [속성](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md) 의 컬렉션은  **실행** 메서드. 에 대 한 자세한 내용은 **콘텐츠** 및 **형식** 속성 참조 [지원 XMLA 속성 &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
 OLAP용 OLE DB 데이터 집합 구조에 대한 기본 내용은 XML for Analysis 1.1 사양의 "OLE DB에 MDDataSet 데이터 형식 매핑"을 참조하십시오. 전체 XML 스키마 정의 언어 (XSD) 예제에 대 한는 **MDDataSet** 데이터 형식 "부록 d:: mddataset Example" XML for Analysis 1.1 사양의를 참조 하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 데이터 형식 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  
