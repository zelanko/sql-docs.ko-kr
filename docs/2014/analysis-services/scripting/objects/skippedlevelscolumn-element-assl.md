---
title: SkippedLevelsColumn 요소 (ASSL) | Microsoft Docs
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
- SkippedLevelsColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SkippedLevelsColumn
helpviewer_keywords:
- SkippedLevelsColumn element
ms.assetid: 6b00a288-99c1-4735-9e6b-cd13ed4fa346
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3ae469982f39e1274759eaaea992fe456330d8fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089161"
---
# <a name="skippedlevelscolumn-element-assl"></a>SkippedLevelsColumn 요소(ASSL)
    
> [!NOTE]  
>  이 기능은 이 버전의 Microsoft SQL Server에서 지원되지 않습니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.  
  
 각 멤버와 해당 부모 간의 건너뛴(빈) 수준 수를 저장하는 열의 세부 정보를 제공합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <SkippedLevelsColumn xsi:type="DataItem">...</SkippedLevelsColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `SkippedLevelsColumn` 요소는 부모 특성에만 적용할 수 (즉, 값은 [사용](../properties/usage-element-dimensionattribute-assl.md) 요소에 대 한는 `DimensionAttribute` 로 설정 됩니다 *부모*). `SkippedLevelsColumn` 요소는 각 멤버와 해당 부모 멤버 간의 건너뛴 수준 수를 저장하는 부모 특성에 대한 열 또는 특성을 포함합니다. 따라서 부모 특성을 기반으로 하는 부모-자식 계층이 멤버 간 수준을 건너뛸 수 있습니다. 이 열 또는 특성에 포함된 값은 음수가 아닌 정수여야 하며 그렇지 않으면 처리 오류가 발생합니다. `SkippedLevelsColumn` 요소를 지정하지 않거나 이 요소에 값을 포함하지 않으면 현재 멤버가 해당 부모 멤버보다 한 수준 아래에 있게 됩니다.  
  
 에 대 한 자세한 내용은 `DataItem` 테이블의 Analysis Services Scripting Language (ASSL) 개체 및 속성을 포함 하 여는 `DataItem` 테이블에서 참조 [DataItem 데이터 형식 &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md)합니다.  
  
 부모에 해당 하는 요소 `SkippedLevelsColumn` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DimensionAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소 특성 &#40;ASSL&#41;](../collections/attributes-element-assl.md)   
 [요소를 차원 &#40;ASSL&#41;](dimension-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  