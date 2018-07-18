---
title: Subscribe 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f784cbe3c33eb6b2587b7b535668e793fac3b138
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37973075"
---
# <a name="subscribe-element-xmla"></a>Subscribe 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  구독을 추적 하 고에서 Analysis Services 인스턴스의 추적 이벤트를 포함 하는 행 집합을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Subscribe>  
      <Object>...</Object>  
   </Subscribe>  
</Command>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
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
 **Subscribe** 명령 구독 하 고 스트림이 지정된 된 추적의 행 집합에서 다시는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스. 추적 이외의 개체가 **Object** 요소에 지정된 경우 오류가 발생합니다.  
  
 경우는 **개체** 요소를 지정 하지 않으면 세션 추적 정의 되 고 하는 행 집합을 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스. 세션 추적은 현재 세션의 고정된 추적 이벤트 집합을 반환합니다.  
  
 클라이언트 응용 프로그램에 대 한 연결을 종료 하는 경우이 명령이 반환한 행 집합 스트림이 종료 됩니다는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스 또는 세션을를 **구독** 명령이 실행 되 종료 됩니다.  
  
## <a name="see-also"></a>참고자료
 [명령 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
