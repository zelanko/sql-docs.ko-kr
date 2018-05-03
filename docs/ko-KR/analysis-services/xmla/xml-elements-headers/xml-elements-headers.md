---
title: 헤더 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XMLA, headers
- SOAP headers [XML for Analysis]
- XML for Analysis, headers
- headers [XML for Analysis]
ms.assetid: 36407b5c-d98d-47e4-8d36-d8896e15a748
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0fd680e1fe5df195752e1618fe23551f4c10f2a2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="xml-elements---headers"></a>XML 요소-헤더
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  XMLA(XML for Analysis) 프로토콜은 SOAP 헤더 내의 XML 요소를 사용하여 프로토콜 수준의 기능(예: 세션 지원, 지원 기능 협상)을 관리합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 항목에서 설명 하 여 구현 되는 XMLA 헤더 요소 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
|메서드|설명|  
|------------|-----------------|  
|[BeginSession 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)|SOAP 요청 메시지의 SOAP 헤더를 사용하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 인스턴스에서 새 세션을 시작합니다.|  
|[EndSession 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)|SOAP 요청 메시지의 SOAP 헤더를 사용하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 인스턴스에서 기존 세션을 종료합니다.|  
|[Session 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)|SOAP 요청 메시지의 SOAP 헤더를 사용하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 인스턴스에서 기존의 명시적 세션을 식별합니다.|  
|[ProtocolCapabilities 요소 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)|SOAP 요청 메시지의 SOAP 헤더를 사용하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 인스턴스와 클라이언트 응용 프로그램 간의 프로토콜 기능을 식별합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [XML 요소 & #40; XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML 데이터 형식 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [XML 요소 & #40; XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
