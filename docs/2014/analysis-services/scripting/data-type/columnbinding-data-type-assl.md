---
title: ColumnBinding 데이터 형식 (ASSL) | Microsoft Docs
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
- ColumnBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ColumnBinding
helpviewer_keywords:
- ColumnBinding data type
ms.assetid: 3ab1bac1-6716-4b17-a107-d5f9c744c5e6
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1ad7cea5041f8d65964b85e36a0b992f9f5afdae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172991"
---
# <a name="columnbinding-data-type-assl"></a>ColumnBinding 데이터 형식(ASSL)
  한 데이터 원본 뷰의 열 바인딩을 나타내는 파생된 데이터 형식을 정의 [DataItem](dataitem-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ColumnBinding>  
   <!-- The following elements extend Binding -->  
   <TableID>...</TableID>  
      <ColumnID>...</ColumnID>  
</ColumnBinding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[바인딩](binding-data-type-assl.md)|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[ColumnID](../properties/columnid-element-eventcolumn-assl.md), [TableID](../properties/id-element-assl.md)|  
|파생 요소|참조 [바인딩](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 올바른 XML 요소 이름을 만들기 위해 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] `DataSet` 개체는 XSD(XML 스키마 정의)로 직렬화될 때 테이블 이름을 인코딩합니다. 예를 들어 "Order Details"라는 이름은 "Order_x0020_Details"가 됩니다. 마찬가지로, `ColumnID` 요소에 포함되고 DSV(데이터 원본 뷰)의 개체를 참조하는 `TableID` 및 `ColumnBinding` 요소도 직렬화 중에 이름을 인코딩하여 해당 이름이 데이터 원본 뷰의 텍스트와 바로 일치하도록 해야 합니다. Analysis Services 인스턴스는 `DataSet` 개체 모델과 같은 방법으로 이러한 이름을 디코딩합니다.  
  
 `TableDefinitions` 데이터 형식을 사용하여 요소에 포함되고 DSV의 테이블을 참조하는 `TableBinding` 요소도 XML 스키마 정의로 직렬화할 때 이름을 인코딩해야 합니다. 그러나 `Partition` 바인딩의 테이블 이름은 데이터베이스에 있는 테이블의 이름일 뿐 DSV에 있을 필요는 없기 때문에 인코딩하지 않습니다. `Partition` 바인딩의 테이블 이름을 인코딩하지 않으면 다음과 같은 결과도 얻게 됩니다.  
  
-   파티션의 DDL(Data Definition Library)이 보다 간소하게 유지됩니다.  
  
-   파티션이 테이블 이름 또는 SELECT 문을 포함할 수 있으므로 일관성이 높아지며 SELECT 문은 인코딩되지 않습니다.  
  
 테이블 및 열 이름에 구분 기호가 포함되지 않습니다(예: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 경우 "[").  
  
 에 대 한 자세한 내용은 `Binding` 유형의 Analysis Services Scripting Language (ASSL) 개체 테이블을 포함 하 여는 `Binding` 유형과의 상속 계층 구조 `Binding` 형식 참조 [바인딩 데이터 형식 &#40;ASSL&#41;](binding-data-type-assl.md)합니다.  
  
 ASSL의 데이터 바인딩에 대 한 개요를 참조 하세요. [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
 AMO 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ColumnBinding>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 스크립팅 언어 XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  