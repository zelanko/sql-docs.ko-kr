---
title: 형식 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 344730d6f46a3772252a91d6672f44b7f54e1123
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="format-element-assl"></a>Format 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  필수 형식을 포함 된 [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataItem>  
   ...  
   <Format>...</Format>  
      ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **Format** 요소에 대해 허용되는 값은 Microsoft Office Excel 형식과 문자열 *TrimRight*, *TrimLeft*, *TrimAll*및 *TrimNone*입니다. 잘라내기의 경우 *TrimRight* 가 기본값입니다.  
  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|모든 Excel 형식 문자열|지정한 명명된 형식 문자열 또는 사용자 지정 형식 문자열에 따라 데이터의 형식이 지정됩니다. Excel에서 지원되는 모든 형식 문자열을 제공할 수 있습니다.|  
|*TrimAll*|데이터가 왼쪽과 오른쪽에서 잘립니다.|  
|*TrimLeft*|데이터가 왼쪽에서 잘립니다.|  
|*TrimNone*|데이터가 잘리지 않습니다.|  
|*TrimRight*|데이터가 오른쪽에서 잘립니다.|  
  
 부모에 해당 하는 요소 **형식** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DataItem>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
