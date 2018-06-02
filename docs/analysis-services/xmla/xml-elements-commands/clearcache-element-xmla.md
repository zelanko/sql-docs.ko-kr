---
title: ClearCache 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6fecd3b679f69166d8a9946372ba58d95e79c9f3
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575065"
---
# <a name="clearcache-element-xmla"></a>ClearCache 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Analysis Services 인스턴스에서 지정된 된 개체에 대 한 메모리 캐시를 지웁니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <ClearCache>  
      <Object>...</Object>  
   </ClearCache>  
</Command>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[개체](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 **ClearCache** 명령에 지정 된 데이터베이스, 차원, 큐브, 측정값 그룹 또는 파티션에 대 한 캐시를 플러시합니다는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스. **Object** 요소에 데이터베이스, 차원, 큐브, 측정값 그룹 또는 파티션 이외의 개체가 지정되면 오류가 발생합니다.  
  
## <a name="see-also"></a>참고자료
 [명령 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
