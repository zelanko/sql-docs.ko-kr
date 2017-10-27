---
title: "보고서 서버 웹 서비스 | Microsoft Docs"
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
- SSIS, Web service
- Web service [Reporting Services]
- Reporting Services, extending
- SQL Server Reporting Services, Web service
- Reporting Services, Web service
- XML Web service [Reporting Services]
- Report Server Web service
ms.assetid: 16c21dec-6b46-4497-9a0c-1b0f2b6ab8fc
caps.latest.revision: 47
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5fd4d415e452549e80aa12b9eb1397bf83ce6557
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="report-server-web-service"></a>보고서 서버 웹 서비스
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버 웹 서비스를 통해 보고서 서버의 전체 기능에 대 한 액세스를 제공 합니다. 보고서 서버 웹 서비스는 SOAP API를 사용하는 XML 웹 서비스입니다. HTTP를 통한 SOAP을 사용하고 클라이언트 프로그램과 보고서 서버 간의 통신 인터페이스로 작동합니다. 웹 서비스는 보고서 실행용과 보고서 관리용으로 끝점을 두 개 제공하며, 여기에는 보고서 서버의 기능을 표시하고 보고서 수명 주기 중 임의의 부분에 대해 사용자 지정 도구를 만들 수 있는 메서드가 사용됩니다.  
  
 세 가지 기본 방법으로 개발 하 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 서비스 기반 응용 프로그램입니다. 다음 작업을 수행할 수 있습니다.  
  
-   사용 하 여 응용 프로그램을 개발 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK입니다. 사용 하는 방법에 대 한 자세한 내용은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 웹 서비스 응용 프로그램을 빌드하려면 참조 [웹 서비스와.NET Framework를 사용 하 여 응용 프로그램 빌드](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)합니다.  
  
-   사용 하 여 응용 프로그램을 개발는 **rs** 유틸리티 (RS.exe)는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 스크립트 환경입니다. 와 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 스크립트를 실행할 수 있습니다 모든 보고서 서버 웹 서비스 작업입니다. 스크립팅 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], 참조 [rs.exe 유틸리티 및 웹 서비스 스크립트](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)합니다.  
  
-   SOAP 사용 개발 도구를 사용하여 응용 프로그램을 개발합니다. 자세한 내용은 참조 [The Role of SOAP in Reporting Services](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md)합니다.  
  
## <a name="programming-diagram"></a>프로그래밍 다이어그램  
 ![보고서 서버 웹 서비스 개발 옵션](../../reporting-services/report-server-web-service/media/reportserviceswebserviceprog-01.gif "Report Server Web service development options")  
Reporting Services 사용 가능한 웹 서비스 개발 옵션  
  
## <a name="in-this-section"></a>섹션 내용  
 [보고서 서버 웹 서비스 메서드](../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)  
 각 보고서 서버 웹 서비스의 기능 및 메서드를 설명합니다.  
  
 [Reporting Services에서 SOAP의 역할](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md)  
 SOAP에 대한 개요를 제공하며 SOAP이 보고서 서버 웹 서비스에서 어떻게 사용되는지를 설명합니다.  
  
 [SOAP API 액세스](../../reporting-services/report-server-web-service/accessing-the-soap-api.md)  
 WSDL(Web Service Description Language)에 대해 설명하고 Reporting Services WSDL 파일 액세스를 위한 URL을 제공합니다.  
  
 [웹 서비스와.NET Framework를 사용 하 여 응용 프로그램 빌드](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
 Reporting Services SOAP API를 호출하는 응용 프로그램 및 웹 서비스 개발에 대한 정보를 포함합니다.  
  
 [Rs.exe 유틸리티 및 웹 서비스를 사용한 스크립팅](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 스크립팅 환경에 대해 개략적으로 설명합니다.  
  
 [기술 참조 &#40; Ssrs&#41;](../../reporting-services/technical-reference-ssrs.md)  
 보고서 서버 웹 서비스 메서드 및 해당하는 복합 형식에 대한 특정 참조 자료를 포함합니다.  
  
## <a name="user-requirements-for-web-service-development"></a>웹 서비스 개발을 위한 사용자 요구 사항  
 보고서 서버 웹 서비스를 사용하여 응용 프로그램을 개발하려면 다음이 필요합니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)]Internet Explorer 5.5 이상이 인터넷 연결 하 여 보고서 서버에 대 한 액세스는 컴퓨터에 설치 되어 있습니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 개발 및 배포 하려는 경우 컴퓨터에 설치 된 SDK [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 사용 하 여 응용 프로그램에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]합니다.  
  
-   깊이 있게 이해할 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능 및 특성입니다.  
  
-   SOAP 및 [!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)]를 잘 알고 있어야 합니다.  
  
-   개발 해 본 경험이 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-과 같은 호환 언어 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]사용 하려는 경우는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 개발 플랫폼으로 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 서버 웹 서비스](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  

