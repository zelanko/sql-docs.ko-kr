---
title: SynchronizeSecurity 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5f99f4c0ddf212d2fac33abd08c33ccf3dbe7998
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576485"
---
# <a name="synchronizesecurity-element-xmla"></a>SynchronizeSecurity 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  동안 역할 및 권한과 같은 보안 정의 동기화 하는 방법을 지정 하는 [동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Synchronize>  
   ...  
   <SynchronizeSecurity>...</SynchronizeSecurity>  
   ...  
</Synchronize>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*SkipMembership*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **보안** 요소는 역할 및 Analysis Services 데이터베이스에 정의 된 권한과 같은 보안 정의 하는 동안 동기화는 여부를 결정 한 **동기화** 명령입니다. 또한 보안 정의의 멤버로 정의된 Windows 사용자 계정 및 그룹을 **Synchronize** 명령의 일부로 포함할지 여부도 결정합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*SkipMembership*|**Synchronize** 명령을 실행하는 동안 보안 정의는 포함하지만 멤버 등록 정보는 제외합니다.|  
|*CopyAll*|**Synchronize** 명령을 실행하는 동안 보안 정의 및 멤버 등록 정보를 포함합니다.|  
|*IgnoreSecurity*|**Synchronize** 명령을 실행하는 동안 보안 정의를 제외합니다.|  
  
## <a name="see-also"></a>참고자료
 [보안 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md)   
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
