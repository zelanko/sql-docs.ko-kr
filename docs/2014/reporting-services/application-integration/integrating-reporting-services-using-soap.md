---
title: SOAP을 사용하여 Reporting Services 통합 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, application integration
- SOAP [Reporting Services]
- SOAP [Reporting Services], about report integration
- integrating reports [Reporting Services]
- Web service [Reporting Services], application integration
ms.assetid: 6bc17af5-883c-4bfa-87d9-48cd7056d145
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a7deac283e848ec932b266ac77cf4f5575da5d38
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057843"
---
# <a name="integrating-reporting-services-using-soap"></a>SOAP을 사용하여 Reporting Services 통합
  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SOAP API는 사용자 지정 보고 솔루션 개발을 위한 다수의 웹 서비스 엔드포인트를 제공합니다. 엔드포인트는 현재 관리와 실행의 두 범주로 나누어집니다. 관리 기능은 <xref:ReportService2005>, <xref:ReportService2006> 및 <xref:ReportService2010> 엔드포인트를 통해 표시됩니다. <xref:ReportService2005> 엔드포인트는 기본 모드로 구성된 보고서 서버를 관리하는 데 사용되고, <xref:ReportService2006> 엔드포인트는 SharePoint 통합 모드에 대해 구성된 보고서 서버를 관리하는 데 사용됩니다. <xref:ReportService2010>은 <xref:ReportService2005> 및 <xref:ReportService2006>의 기능을 병합하며, 기본 모드 또는 SharePoint 통합 모드용으로 구성된 보고서 서버를 관리할 수 있습니다.  
  
> [!NOTE]  
>  <xref:ReportService2005> 및 <xref:ReportService2006> 엔드포인트는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]에서 더 이상 사용되지 않습니다. <xref:ReportService2010>엔드포인트에는 두 엔드포인트의 기능이 모두 포함되어 있으며 추가 관리 기능도 포함되어 있습니다.  
  
 실행 기능은 <xref:ReportExecution2005> 엔드포인트를 통해 표시되며 보고서 서버가 기본 또는 SharePoint 통합 모드로 구성된 경우에 사용됩니다. 다음 항목에서는 이러한 엔드포인트를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, SharePoint 및 웹 응용 프로그램에서 보고 솔루션을 개발하는 방법을 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [Windows 응용 프로그램에서 SOAP API 사용](integrating-reporting-services-using-soap-windows-application.md)  
 SOAP API를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 Windows 환경에 통합하는 방법을 설명합니다.  
  
 [웹 응용 프로그램에서 SOAP API 사용](integrating-reporting-services-using-soap-web-application.md)  
 SOAP API를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 웹 환경에 통합하는 방법을 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [응용 프로그램에 Reporting Services 통합](../application-integration/integrating-reporting-services-into-applications.md)   
 [보고서 서버 웹 서비스](../report-server-web-service/report-server-web-service.md)   
 [웹 서비스 및 .NET Framework를 사용하여 응용 프로그램 빌드](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
