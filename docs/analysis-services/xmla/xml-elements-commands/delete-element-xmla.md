---
title: Delete 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d83557d2925ea41844ba10a512652b4f2e939370
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="delete-element-xmla"></a>Delete 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  개체를 삭제 한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Delete IgnoreFailures="boolean">  
      <Object>...</Object>  
   </Delete>  
</Command>  
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
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[개체](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|Attribute|Description|  
|---------------|-----------------|  
|IgnoreFailures|선택적 **Boolean** 특성입니다. 이 값을 True로 설정하면 **Execute** 메서드가 원격 파티션과 관련된 오류 또는 네트워크 오류를 무시합니다.|  
  
## <a name="remarks"></a>주의  
  
## <a name="see-also"></a>관련 항목:  
 [명령 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
