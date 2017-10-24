---
title: "TableBinding 데이터 형식 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- TableBinding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TableBinding
helpviewer_keywords:
- TableBinding data type
ms.assetid: 3195dca4-82bf-46b7-a31f-5383586e3573
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 680587b7bd9154cf8f32ecbebe34e68c39e4c04a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="tablebinding-data-type-assl"></a>TableBinding 데이터 형식(ASSL)
  테이블에 대한 바인딩을 나타내는 파생 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<TableBinding>  
   <!-- The following elements extend TabularBinding -->  
   <DataSourceID>...</DataSourceID>  
   <DbTableName>...</DbTableName>  
   <DbSchemaName>...</DbSchemaName>  
</TableBinding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|[TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[DataSourceID](../../../analysis-services/scripting/properties/datasourceid-element-assl.md), [DbSchemaName](../../../analysis-services/scripting/properties/dbschemaname-element-assl.md), [DbTableName](../../../analysis-services/scripting/properties/dbtablename-element-assl.md)|  
|파생 요소|참조 [바인딩](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>주의  
 필터 식에서 하위 SELECT를 사용하여 다른 테이블을 참조하면 일부 데이터 원본 성능에 영향을 줄 수 있습니다. 그러나 디자이너는 데이터 원본 뷰에서 명명된 쿼리를 정의한 후 이를 참조하면 SQL 식을 완벽하게 제어할 수 있습니다.  
  
 파티션에 대한 바인딩을 정의하는 방법은 데이터 원본 뷰에서 분할된 테이블을 사용하는 것과는 관계가 없습니다.  
  
 예를 들어 한 측정값 그룹의 기본 테이블이 "Sales"이고 Date, Product ID, Qty, Price 및 Amount 열(데이터 원본 뷰에서 계산됨)이 있다고 가정해 보겠습니다. 그러면 파티션 "Sales97"은 "Year(Sales.Date) = 97" 필터로 테이블 "Sales97"을 사용할 수 있습니다.  
  
 효과적인 쿼리 방법은 다음과 같습니다.  
  
```  
SELECT Date, Product ID, Qty, Price, Qty * Price AS Amount   
   FROM Sales97 As Sales  
   WHERE Year(Sales.Date) = 97  
```  
  
 식에 정규화된 테이블 이름(예: Sales.Qty)이 사용된 경우에도 계산된 식은 계속 적용됩니다. 테이블이 일부 쿼리 "SELECT..."으로 대체 되었으며 대신 때도 마찬가지 위의 FROM 절 바로 될 "FROM SELECT... As Sales"가 됩니다.  
  
 에 대 한 자세한 내용은 **바인딩** 유형의 Analysis Services Scripting Language (ASSL) 개체 테이블을 포함 하 여 **바인딩** 의 상속 계층 구조 및 **바인딩** 형식 참조 [바인딩 데이터 형식 &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 ASSL의 데이터 바인딩에 대 한 개요를 참조 하십시오. [데이터 원본 및 바인딩 &#40; SSAS 다차원 &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.TableBinding>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Binding 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [데이터 원본 및 바인딩 &#40; SSAS 다차원 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)   
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

