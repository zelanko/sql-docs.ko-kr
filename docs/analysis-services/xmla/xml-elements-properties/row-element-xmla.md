---
title: "row 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
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
apiname: row Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#row
- microsoft.xml.analysis.row
- http://schemas.microsoft.com/analysisservices/2003/engine#row
helpviewer_keywords: row element
ms.assetid: 4d9977a0-c396-44c7-9fd4-97f4c3d643aa
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2b38517cea700ac5fab6cdccbef77aaeea0dc969
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="row-element-xmla"></a>row 요소(XMLA)
  에 대 한 데이터의 단일 행을 포함 한 [루트](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) 요소에서 반환 된 테이블 형식 데이터를 포함 하는 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 또는 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드를 호출 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <row>  
      <!-- One or more column elements -->  
   </row>  
</root>  
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
|부모 요소|[루트](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) (사용 하 여 [행 집합](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md) 데이터 형식)|  
|자식 요소|하나 이상의 열 요소|  
  
## <a name="remarks"></a>주의  
 테이블 형식 데이터를 포함하는 **root** 요소에서 반환한 각 행에는 이에 해당하는 **row** 요소가 있습니다. **root** 요소의 각 열은 개별 XML 요소로 표시됩니다. **row** 요소의 열 값은 XML 요소에 포함된 데이터이고 열 이름은 XML 요소 이름과 일치합니다.  
  
 행에서 열에 Null 값을 표현하는 방법은 두 가지가 있습니다.  
  
-   누락된 열 요소는 열이 Null임을 의미합니다.  
  
-   열 요소는 `xsi:nil='true'` 특성을 사용하여 해당 열에 Null 값이 있음을 나타낼 수 있습니다.  
  
 예를 들어 행의 한 열이 Store_Name이고 해당 값이 NULL인 경우 다음 중 하나로 표시될 있습니다.  
  
```  
<row>  
</row>  
```  
  
 또는  
  
```  
<row>  
   <Store_name xsi:nil='true'/>  
</row>  
```  
  
 열 요소에 오류가 있으면 **Error** 요소에서 다음 예제와 같이 오류에 대한 정보를 제공합니다.  
  
```  
<row>   <Store_name>  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception">  
         <ErrorCode>3238658054</ErrorCode>  
         <Description>The object [X] was not found in the cube when [X] was parsed.</Description>  
      </Error>  
   </Store_name>  
</row>  
```  
  
 자세한 열 이름을 지정 하는 방법에 대 한 정보 및 테이블 형식 데이터에 대 한 스키마 정보를 참조 하십시오. [Rowset 데이터 형식 &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md).  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
