---
title: MDDataSet 데이터 형식 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDDataSet Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#MDDataSet
- MDDataSet
- urn:schemas-microsoft-com:xml-analysis#MDDataSet
helpviewer_keywords:
- MDDataSet data type
ms.assetid: 1a7e0092-f9f0-4ae5-ba27-ad1d8ebe8cb9
caps.latest.revision: 27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c1580365cc6c7949c552333728b5083b96f7ef9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165324"
---
# <a name="mddataset-data-type-xmla"></a>MDDataSet 데이터 형식(XMLA)
  반환 된 다차원 데이터를 나타내는 파생된 데이터 형식을 정의 합니다 [Execute](../xml-elements-methods-execute.md) 메서드.  
  
 **Namespace** urn: 스키마-microsoft-com:xml-분석: mddataset  
  
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
|기본 데이터 형식|[결과 집합](resultset-data-type-xmla.md)|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[축](../xml-elements-properties/axes-element-xmla.md)하십시오 [CellData](../xml-elements-properties/celldata-element-xmla.md), [OlapInfo](../xml-elements-properties/olapinfo-element-xmla.md)|  
|파생 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `MDDataSet` 데이터 형식은 OLAP 데이터를 XML로 표시하는 데 필요한 OLAP 기반 행 집합 또는 데이터 집합을 제공합니다. 이 행 집합의 콘텐츠는 값에 따라 달라질 수 있습니다는 `Content` 및 `Format` 에서 제공 하는 속성을 [속성](../xml-elements-properties/properties-element-xmla.md) 의 컬렉션을 `Execute` 메서드. 에 대 한 자세한 내용은 합니다 `Content` 하 고 `Format` 속성을 참조 하세요 [지원 되는 XMLA 속성 &#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
 OLAP용 OLE DB 데이터 집합 구조에 대한 기본 내용은 XML for Analysis 1.1 사양의 "OLE DB에 MDDataSet 데이터 형식 매핑"을 참조하십시오. 전체 XML 스키마 정의 언어 (XSD) 예제는 `MDDataSet` XML for Analysis 1.1 사양의 "부록 d: MDDataSet Example" 참조 데이터 형식입니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 데이터 형식 &#40;XMLA&#41;](xml-data-types-xmla.md)  
  
  
