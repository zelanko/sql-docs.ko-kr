---
title: Reporting Services에서 SOAP의 역할 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- SOAP [Reporting Services], role in Reporting Services
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: f229c3ef-f2ca-448f-98f1-b8df350b9992
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4e0b418e44436912b5ed1368ad7a316951872266
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62519206"
---
# <a name="the-role-of-soap-in-reporting-services"></a>The Role of SOAP in Reporting Services
  웹 서버 웹 서비스에서는 SOAP(Simple Object Access Protocol) 메시징을 사용하여 네트워크를 통해 텍스트 기반 명령을 보냅니다. 이러한 명령은 HTTP를 사용하여 World Wide Web을 통해 전송되는 XML 텍스트 형식입니다. SOAP을 통신 프로토콜로 사용하면 보고서 서버 웹 서비스에서는 폭넓게 활용되는 개방형 인프라를 사용하여 응용 프로그램 및 구성 요소와 보고서 서버 간에 데이터 교환이 가능합니다. SOAP 표준은 www.w3.org/TR/SOAP에 정의되어 있습니다.  
  
 SOAP을 인식하고 SOAP 요청을 보낼 수 있으면 모든 클라이언트 응용 프로그램이 SOAP 클라이언트가 될 수 있습니다. 보고서 관리자는 이러한 SOAP 클라이언트 중 하나이며 모든 보고서 및 보고서 관련 내용이 저장되는 보고서 서버 데이터베이스에 대한 인터페이스를 제공합니다. 최종 사용자는 이 응용 프로그램을 사용하여 보고서 서버 네임스페이스에서 보고서 및 폴더를 탐색하고 관리할 수 있습니다. 보고서 관리자는 보고서 서버 웹 서비스 인프라를 기반으로 합니다.  
  
 보고서 서버는 SOAP 서버의 역할을 하며, SOAP 클라이언트로부터 요청을 수신하고 적절한 응답을 만들 수 있는 SOAP 인식 서비스입니다. 서버에서는 요청을 처리하고 인코딩된 응답을 다시 클라이언트로 보냅니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 SOAP 메시지의 형태는 클라이언트의 요청 유형에 따라 다양합니다. 다음 예는 보고서 서버 데이터베이스에서 항목을 제거하는 간단한 SOAP 클라이언트 요청을 나타냅니다.  
  
```  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <soap:Body>  
        <DeleteItem xmlns="https://www.microsoft.com/sql/ReportingServer">  
            <item>/Samples/Report1</item>  
        </DeleteItem>  
    </soap:Body>  
</soap:Envelope>  
```  
  
 SOAP 자체의 경우 전체 메시지를 `Envelope` 요소 내에 두며 메시지 중 많은 부분을 `Body` 요소에 포함합니다. 이 예에서 본문에는 삭제할 항목의 경로를 나타내는 문자열 매개 변수를 가지는 <xref:ReportService2010.ReportingService2010.DeleteItem%2A> 메서드 호출이 포함되어 있습니다. 모든 SOAP 작업을 메서드로 캡슐화하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클라이언트 프록시 클래스를 만들 수 있습니다. 다음 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 메서드는 위의 SOAP 예를 나타냅니다.  
  
```  
public void DeleteItem(string item);  
```  
  
 서버의 응답은 다음과 같습니다.  
  
```  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <soap:Body>  
        <DeleteItemResponse xmlns="https://www.microsoft.com/sql/ReportingServer" />  
    </soap:Body>  
</soap:Envelope>  
```  
  
 <xref:ReportService2010.ReportingService2010.DeleteItem%2A> 메서드에는 반환 값이 없으므로 빈 응답이 반환됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [SOAP API 액세스](accessing-the-soap-api.md)   
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md)   
 [Reporting Services 보고서 서버](../reporting-services-report-server.md)   
 [보고서 서버 웹 서비스](report-server-web-service.md)  
  
  
