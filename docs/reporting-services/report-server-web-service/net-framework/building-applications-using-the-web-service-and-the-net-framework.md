---
title: "웹 서비스와.NET Framework를 사용 하 여 응용 프로그램을 구축 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
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
- Report Server Web service, application building
- .NET Framework [Reporting Services]
- XML Web service [Reporting Services], client creation
- reports [Reporting Services], building
- Web service [Reporting Services], application building
- Report Server Web service, client creation
- client configuration [Reporting Services]
- XML Web service [Reporting Services], application building
- Web service [Reporting Services], client creation
ms.assetid: 92a9678c-bc4f-4d7a-ba44-85989bfe27ca
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: e228d60a4ae01aa345f007be91109b7bccb76f5a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="building-applications-using-the-web-service-and-the-net-framework"></a>웹 서비스 및 .NET Framework를 사용하여 응용 프로그램 작성
  와 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], 기본 형식, 메서드 등 친숙 한 프로그래밍 구문을 사용할 수 있습니다 및 사용자 정의 복합 형식 웹 서비스와 작동 합니다. [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]에는 모든 W3C(World Wide Web 컨소시엄) 표준 호환 웹 서비스를 호출할 수 있는 웹 서비스 클라이언트를 만드는 데 사용할 수 있는 인프라와 도구가 포함되어 있습니다.  
  
 보고서 서버 웹 서비스 클라이언트는 SOAP(Simple Object Access Protocol) 메시지를 사용하여 보고서 서버와 통신하는 구성 요소 또는 응용 프로그램입니다.  
  
 **.NET Framework를 사용 하 여 보고서 서버 웹 서비스 클라이언트를 만들려면 다음 기본 단계를 수행 합니다.**  
  
1.  웹 서비스에 대한 프록시 클래스를 만듭니다.  
  
     이 작업을 수행하려면 프록시 클래스 또는 웹 참조를 개발 프로젝트에 추가하고 클라이언트 코드에서 프록시 클래스를 참조한 다음 해당 프록시의 인스턴스를 만듭니다. 자세한 내용은 참조 [웹 서비스 프록시를 만드는](../../../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md)합니다.  
  
2.  보고서 서버에서 웹 서비스 클라이언트를 인증합니다.  
  
     이 작업을 수행하려면 서비스 개체의 <xref:System.Web.Services.Protocols.WebClientProtocol.Credentials%2A> 속성을 보고서 서버에서 인증된 사용자의 자격 증명과 동일하게 설정합니다. 자세한 내용은 참조 [웹 서비스 인증](../../../reporting-services/report-server-web-service/net-framework/web-service-authentication.md)합니다.  
  
3.  호출하려는 웹 서비스 작업과 일치하는 프록시 클래스의 메서드를 호출합니다.  
  
     이 작업을 수행하려면 웹 서비스 메서드를 호출하고 필요한 인수를 제공합니다. 웹 서비스 메서드에 대 한 자세한 내용은 참조 [보고서 서버 웹 서비스 메서드](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)합니다. 호출에 대 한 자세한 내용은 참조 [웹 서비스 메서드 호출](../../../reporting-services/report-server-web-service/net-framework/calling-web-service-methods.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[웹 서비스 프록시 만들기](../../../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md)|사용 하 여 프로젝트에 프록시 클래스를 추가 하는 방법을 설명 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]합니다.|  
|[웹 서비스 인증](../../../reporting-services/report-server-web-service/net-framework/web-service-authentication.md)|보고서 서버 웹 서비스에 대한 호출의 인증 방법을 설명합니다.|  
|[웹 서비스 메서드 호출](../../../reporting-services/report-server-web-service/net-framework/calling-web-service-methods.md)|웹 서비스 메서드를 호출 하는 SOAP API를 사용 하는 방법에 설명 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]합니다.|  
|[웹 서비스의 Url 속성 설정](../../../reporting-services/report-server-web-service/net-framework/setting-the-url-property-of-the-web-service.md)|웹 참조를 만든 다음 프로그래밍 방식으로 웹 서비스 프록시를 새 서버 URL에 지정하는 방법을 설명합니다.|  
|[웹 서비스 메서드 인수 제공](../../../reporting-services/report-server-web-service/net-framework/supplying-web-service-method-arguments.md)|웹 서비스 메서드를 호출하고 메서드 인수를 제공하는 방법을 설명합니다.|  
|[선택적 웹 서비스 개체에 대한 값 생략](../../../reporting-services/report-server-web-service/net-framework/omitting-values-for-optional-web-service-objects.md)|선택적 웹 서비스 개체에 대한 값을 생략하는 방법을 설명합니다.|  
|[보안 웹 서비스 메서드 사용](../../../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md)|설명의 **SecureConnectionLevel** 설정 및 Reporting Services SOAP API의 사용 중인 적용 하는 방법입니다.|  
|[장치 정보 설정을 렌더링 확장 프로그램에 전달](../../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)|보고서를 다양한 형식으로 렌더링하는 데 사용되는 장치 정보 설정을 설명합니다.|  
|[Reporting Services 배달 확장 프로그램 설정](../../../reporting-services/report-server-web-service/net-framework/reporting-services-delivery-extension-settings.md)|보고서 서버 전자 메일을 사용하여 보고서를 배달하는 데 사용되는 설정을 설명합니다.|  
|[보고를 사용 하 여 Services SOAP 헤더](../../../reporting-services/report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 SOAP 헤더의 사용에 대해 설명합니다.|  
|[Reporting Services의 예외 처리 소개](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 오류를 처리하는 방법에 대해 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 웹 서비스](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [기술 참조 &#40; Ssrs&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  

