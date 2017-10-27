---
title: "Reporting Services의 예외 처리 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- SOAP [Reporting Services], exceptions
- .NET Framework [Reporting Services]
- exceptions [Reporting Services], about exception handling
- SoapException object
ms.assetid: 1a443432-2db5-48c5-bc29-433b4688082f
caps.latest.revision: 31
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 7e1472c11575ba8bed99992ec9630e408c347291
ms.contentlocale: ko-kr
ms.lasthandoff: 08/12/2017

---
# <a name="handling-exceptions-in-reporting-services"></a>Reporting Services의 예외 처리
  Reporting Services SOAP API 클라이언트 요청을 완료할 수 없는 경우 보고서 서버에서는 호출에 대해 예상된 결과가 아니라 오류를 반환합니다. 보고서 서버 웹 서비스에 대 한 오류가 SOAP로 반환 됩니다 호출 완료할 수 없는 경우 **오류** XML 요소입니다. 오류의 주요 설명 요소는는 **세부** 모든 추가 웹 서비스 오류 정보 뿐만 아니라 보고서 서버에서 제공 하는 오류 정보를 포함 하는 요소입니다. 주요 정보는 **세부** 요소는 보고서 서버 오류 코드입니다. 메시지 및 오류 코드를 기준으로 응용 프로그램에서 수행할 적절한 다음 동작을 결정할 수 있습니다. SOAP 오류에 대한 자세한 내용은 W3C(World Wide Web 컨소시엄) 웹 사이트 http://www.w3.org/TR/SOAP을 참조하십시오.  
  
## <a name="soap-faults-and-the-net-framework"></a>SOAP 오류 및 .NET Framework  
 에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], 웹 서비스에 클라이언트 요청에 오류가 발생 하는 경우 보고서 서버가 통신 하는 오류를 throw 하 여 웹 서비스를 호출 하는 클라이언트 코드에는 **SoapException** 개체입니다. **SoapException** SOAP 오류에 포함 된 정보를 래핑합니다. **세부** 의 속성은 **SoapException** 매핑되는 **세부** 요소는 SOAP 오류에 합니다. 응용 프로그램 catch 해야 합니다는 **SoapException** try/catch 블록으로 개체를 사용 하 여는 **세부** 의 속성에서 **SoapException** 적절 한 조치를 합니다. 에 대 한 자세한 내용은 **SoapException** 클래스 및 **세부** 속성 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], 참조 [Reporting Services SoapException 클래스](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)합니다. 에 대 한 자세한 내용은 **SoapException** 클래스를 참조 하십시오.는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 설명서입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Detail 속성](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Reporting Services의 예외 처리 소개](../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 클래스](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  

