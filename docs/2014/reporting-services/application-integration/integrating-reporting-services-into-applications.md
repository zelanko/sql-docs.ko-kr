---
title: 애플리케이션에 Reporting Services 통합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- integrating reports [Reporting Services]
- custom applications [SSRS]
- Reporting Services, application integration
- application integration [Reporting Services]
- reports [Reporting Services], integrating
ms.assetid: 49eb539c-d89b-4291-839a-0ec1a65cd270
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9ad6d24495bb44a7bd1013dbc822eefe346f02d3
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60156661"
---
# <a name="integrating-reporting-services-into-applications"></a>애플리케이션에 Reporting Services 통합
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 개발자에게 솔루션 개발을 위한 포괄적인 API 집합을 제공하도록 디자인된 개방형의 확장 가능한 보고 플랫폼입니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 사용자 지정 응용 프로그램에 통합하는 데는 보고서 서버 웹 서비스([!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SOAP API라고도 함), [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]용 ReportViewer 컨트롤, URL 액세스의 세 가지 옵션이 있습니다. 각 옵션에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 응용 프로그램에 통합하기 위한 서로 다른 방법을 제공합니다.  
  
## <a name="report-server-web-service"></a>보고서 서버 웹 서비스  
 보고서 서버 웹 서비스는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 대해 개발하기 위한 기본 인터페이스입니다. 보고서 카탈로그를 관리할 코드를 개발하든 아니면 보고서를 지원되는 형식으로 렌더링하는 코드를 개발하는 경우이든 웹 서비스는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 응용 프로그램에 통합하는 데 필요한 모든 방법을 제공합니다. 이러한 애플리케이션의 예는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 포함되어 있는 보고서 관리자로서 여기서는 웹 서비스를 사용하여 보고서 서버 데이터베이스를 관리합니다.  
  
## <a name="reportviewer-controls-for-visual-studio"></a>Visual Studio용 ReportViewer 컨트롤  
 [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]에 포함된 ReportViewer 컨트롤은 보고서 보기를 응용 프로그램에 통합하는 데 사용합니다. 컨트롤에는 Windows Forms 기반 응용 프로그램용과 Web Forms 응용 프로그램용 두 가지가 있습니다. 각 컨트롤은 보고서 서버에 배포된 보고서를 보기 위한 기능뿐만 아니라 보고서 서버가 설치되지 않은 환경에 있는 보고서를 렌더링하는 기능도 제공합니다.  
  
## <a name="url-access"></a>URL 액세스  
 URL 액세스는 ReportViewer 컨트롤을 사용하지 않을 경우 보고서 보기를 응용 프로그램에 통합하기 위한 또 다른 옵션입니다. 그 외에도 URL 액세스는 전자 메일을 통해 사용자에게 보고서에 대한 링크를 보내는 데도 유용합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [SOAP를 사용하여 Reporting Services 통합](../application-integration/integrating-reporting-services-using-soap.md)  
 보고서 서버 웹 서비스를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 탐색 및 관리를 기존 비즈니스 응용 프로그램에 통합하는 방법을 설명합니다.  
  
 [ReportViewer 컨트롤을 사용하여 Reporting Services 통합](../application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 ReportViewer 컨트롤을 사용하여 보고서 보기를 기존 응용 프로그램에 통합하는 방법을 설명합니다.  
  
 [URL 액세스를 사용하여 Reporting Services 통합](../application-integration/integrating-reporting-services-using-url-access.md)  
 URL 액세스를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 탐색을 기존 비즈니스 응용 프로그램에 통합하는 방법을 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [URL 액세스와 SOAP 중 선택](../../../2014/reporting-services/application-integration/choosing-between-url-access-and-soap.md)   
 [기술 참조&#40;SSRS&#41;](../../../2014/reporting-services/technical-reference-ssrs.md)   
 [보고서 서버 웹 서비스](../report-server-web-service/report-server-web-service.md)  
  
  
