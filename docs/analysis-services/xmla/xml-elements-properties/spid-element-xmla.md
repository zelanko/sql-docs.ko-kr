---
title: SPID 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c2c665e40334710a631d10e236b26360a87277de
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="spid-element-xmla"></a>SPID 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  활성 서버 프로세스 id (SPID)를 실행할 부모 식별 [취소](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cancel>  
   ...  
   <SPID>...</SPID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|정수|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[취소](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **SPID** 요소 나타냅니다 서버 프로세스 ID (SPID)에 해당된 세션의 인스턴스에서 사용 되는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [CancelAssociated 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/cancelassociated-element-xmla.md)   
 [ConnectionID 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md)   
 [SessionID 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md)   
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
