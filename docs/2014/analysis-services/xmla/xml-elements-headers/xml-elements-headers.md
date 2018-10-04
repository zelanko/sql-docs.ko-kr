---
title: 헤더 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- XMLA, headers
- SOAP headers [XML for Analysis]
- XML for Analysis, headers
- headers [XML for Analysis]
ms.assetid: 36407b5c-d98d-47e4-8d36-d8896e15a748
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fdc6c9ebfef18b108c31870c5703cac3841cfc29
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48155702"
---
# <a name="headers-xmla"></a>헤더(XMLA)
  XMLA(XML for Analysis) 프로토콜은 SOAP 헤더 내의 XML 요소를 사용하여 프로토콜 수준의 기능(예: 세션 지원, 지원 기능 협상)을 관리합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 항목에서 구현 되는 XMLA 헤더 요소를 설명 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
|메서드|Description|  
|------------|-----------------|  
|[BeginSession 요소 &#40;XMLA&#41;](session-element-xmla.md)|SOAP 요청 메시지의 SOAP 헤더를 사용하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 인스턴스에서 새 세션을 시작합니다.|  
|[EndSession 요소 &#40;XMLA&#41;](endsession-element-xmla.md)|SOAP 요청 메시지의 SOAP 헤더를 사용하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 인스턴스에서 기존 세션을 종료합니다.|  
|[Session 요소 &#40;XMLA&#41;](session-element-xmla.md)|SOAP 요청 메시지의 SOAP 헤더를 사용하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 인스턴스에서 기존의 명시적 세션을 식별합니다.|  
|[ProtocolCapabilities 요소 &#40;XMLA&#41;](protocolcapabilities-element-xmla.md)|SOAP 요청 메시지의 SOAP 헤더를 사용하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 인스턴스와 클라이언트 응용 프로그램 간의 프로토콜 기능을 식별합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [XML 요소 &#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)   
 [XML 데이터 형식 &#40;XMLA&#41;](../xml-data-types/xml-data-types-xmla.md)   
 [XML 요소 &#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)  
  
  
