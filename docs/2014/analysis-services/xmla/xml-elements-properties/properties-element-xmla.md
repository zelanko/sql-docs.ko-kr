---
title: Properties 요소 (XMLA) | Microsoft Docs
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
- Properties Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Properties
- microsoft.xml.analysis.properties
- urn:schemas-microsoft-com:xml-analysis#Properties
- Properties
helpviewer_keywords:
- Properties element
ms.assetid: 0b5468e5-bf23-4d22-862f-72e27a9fff2f
caps.latest.revision: 30
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 66accb9aab2c970c1fd09b1e14408b5585269d7f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080507"
---
# <a name="properties-element-xmla"></a>Properties 요소(XMLA)
  사용 하는 분석 XMAL () 속성에 대 한 XML이 포함 되어는 [Discover](../xml-elements-methods-discover.md) 및 [Execute](../xml-elements-methods-execute.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Discover> <!-- or Execute -->  
...  
   <Properties>  
      <PropertyList>...</PropertyList>  
   </Properties>  
...  
</Discover>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[검색](../xml-elements-methods-discover.md), [실행](../xml-elements-methods-execute.md)|  
|자식 요소|[PropertyList](propertylist-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Properties` 요소는 데이터 원본에 연결하는 데 필요한 정보를 정의하거나, 결과 집합의 반환 형식을 지정하거나, 데이터의 서식을 지정할 로캘을 지정하는 등 `Discover` 및 `Execute` 메서드의 요소를 제어하는 데 사용되는 XMLA 속성을 나타냅니다.  
  
 DISCOVER_PROPERTIES 요청 유형을 사용 하 여 사용 가능한 속성 및 해당 값을 가져올 수 있습니다는 `Discover` 메서드.  
  
## <a name="example"></a>예제  
  
```  
<Properties>  
   <PropertyList>  
      <DataSourceInfo>  
         Provider=MSOLAP;Data Source=local;  
      </DataSourceInfo>  
      <Catalog>  
         Foodmart 2000  
      </Catalog>  
      <Format>  
         Multidimensional  
      </Format>  
   </PropertyList>  
</Properties>  
```  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  