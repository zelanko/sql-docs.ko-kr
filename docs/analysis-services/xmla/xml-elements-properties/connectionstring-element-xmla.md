---
title: ConnectionString 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c286aa928195181d5d1b344f71b648510ccceda1
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34575845"
---
# <a name="connectionstring-element-xmla"></a>ConnectionString 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모에서 사용 하는 연결 문자열이 들어 [위치](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) 또는 [소스](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Location> <!-- or Source -->  
   ...  
   <ConnectionString>...</ConnectionString>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|아래 표를 참조하세요.|  
  
|상위 항목 또는 부모|카디널리티|  
|------------------------|-----------------|  
|[위치](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)|1-1: 한 번만 나타나는 필수 요소입니다.|  
|[원본](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[위치](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md), [소스](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 **위치** 요소는 **ConnectionString** 에서 사용 하는 연결 문자열을 포함 하는 요소는 **복원** 또는 **동기화** 로컬 데이터 원본을 업데이트 하거나 원격 인스턴스에 연결 하는 명령입니다.  
  
 에 대 한 **소스** 요소는 **ConnectionString** 요소에서 사용 하는 연결 문자열을 포함는 **동기화** 명령이 원본 인스턴스에 연결할 수 있습니다.  
  
 백업 및 개체를 복원 하는 방법에 대 한 자세한 내용은 참조 [Backing Up, Restoring, and Synchronizing &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>참고자료
 [Restore 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [Synchronize 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
