---
title: Reporting Services의 예외 처리 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], exceptions
- .NET Framework [Reporting Services]
- exceptions [Reporting Services], about exception handling
- SoapException object
ms.assetid: 1a443432-2db5-48c5-bc29-433b4688082f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1d887853b475f7b4d673d7b04343ae9bc71644d3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046045"
---
# <a name="handling-exceptions-in-reporting-services"></a>Reporting Services의 예외 처리
  Reporting Services SOAP API 클라이언트 요청을 완료할 수 없는 경우 보고서 서버에서는 호출에 대해 예상된 결과가 아니라 오류를 반환합니다. 호출을 완료할 수 없는 경우 보고서 서버 웹 서비스에 대한 오류가 SOAP **Fault** XML 요소로 반환됩니다. 오류의 주요 설명 요소는 보고서 서버에서 제공하는 모든 오류 정보와 추가 웹 서비스 오류 정보를 포함하는 **detail** 요소입니다. 
  **detail** 요소의 주요 정보는 보고서 서버 오류 코드입니다. 메시지 및 오류 코드를 기준으로 애플리케이션에서 수행할 적절한 다음 동작을 결정할 수 있습니다. SOAP 오류에 대한 자세한 내용은 W3C(World Wide Web 컨소시엄) 웹 사이트 http://www.w3.org/TR/SOAP을 참조하십시오.  
  
## <a name="soap-faults-and-the-net-framework"></a>SOAP 오류 및 .NET Framework  
 
  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]에서 웹 서비스에 대한 클라이언트 요청에 오류가 발생할 경우 보고서 서버에서 **SoapException** 개체를 throw하여 웹 서비스를 호출하는 클라이언트 코드에 오류를 전달합니다. 
  **SoapException**은 SOAP 오류에 포함된 정보를 래핑합니다. 
  **SoapException**의 **Detail** 속성은 SOAP 오류의 **detail** 요소에 매핑됩니다. 애플리케이션에서는 try/catch 블록으로 **SoapException** 개체를 catch하고 **SoapException**의 **Detail** 속성을 사용하여 올바른 조치를 취해야 합니다. 
  **SoapException** 클래스 및 **의 **Detail[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 속성에 대한 자세한 내용은 [Reporting Services SoapException 클래스](soapexception-class/reporting-services-soapexception-class.md)를 참조하세요. 
  **SoapException** 클래스에 대한 자세한 내용은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 설명서를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Detail 속성](soapexception-class/detail-property.md)   
 [Reporting Services의 예외 처리 소개](introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 클래스](soapexception-class/reporting-services-soapexception-class.md)  
  
  
