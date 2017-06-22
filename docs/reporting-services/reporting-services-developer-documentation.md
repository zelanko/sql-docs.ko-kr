---
title: "Reporting Services 개발자 설명서 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
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
- developer's guide [Reporting Services]
- Reporting Services, programming
- programming [Reporting Services]
ms.assetid: d8afa405-1012-4349-a72d-e10d94f8453d
caps.latest.revision: 21
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3704373a08b29a8f36ce843db5f67a860a04a47b
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="reporting-services-developer-documentation"></a>Reporting Services 개발자 설명서
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 응용 프로그램에서 활용할 수 있는 몇 가지 프로그래밍 인터페이스를 제공 합니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 기존 기능을 사용하여 웹 사이트와 Windows 응용 프로그램에 사용자 지정 보고 및 관리 도구를 작성할 수 있으며 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 플랫폼을 확장할 수도 있습니다.  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 플랫폼 확장에는 데이터 액세스, 보고서 배달 등에 사용할 수 있는 새 구성 요소 및 리소스를 만드는 작업이 포함됩니다. 조직에서 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]를 사용하는 회사를 대상으로 이러한 구성 요소 및 리소스를 마케팅할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에는 시작하는 데 도움이 되는 프로그래밍 예제와 자습서가 포함되어 있습니다. 자세한 내용은 참조 [Reporting Services 샘플](https://msdn.microsoft.com/library/ms160954\(v=sql.110\).aspx) 및 [개발자 가이드: 자습서 (Reporting Services)](https://msdn.microsoft.com/library/aa337423\(v=sql.110\).aspx)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [응용 프로그램에 Reporting Services 통합](../reporting-services/application-integration/integrating-reporting-services-into-applications.md)  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]를 사용하여 사용자 지정 응용 프로그램에 보고 기능을 통합하는 방법을 개략적으로 설명합니다. 보고서 서버에 액세스하기 위해 언제 직접 URL 액세스를 사용하고 언제 웹 서비스를 사용하는지를 설명합니다.  
  
 [보고서 서버 웹 서비스](../reporting-services/report-server-web-service/report-server-web-service.md)  
 보고서 서버 웹 서비스는 보고서 서버의 전체 기능에 대한 액세스를 제공합니다. 웹 서비스는 HTTP를 통한 SOAP을 사용하며 클라이언트 프로그램과 보고서 서버 간의 통신 인터페이스 역할을 하도록 디자인되었습니다. 웹 서비스 및 해당 메서드는 보고서 서버의 기능을 표시하며, 작업자는 이를 사용하여 관리부터 실행까지 보고서 수명 주기 중 임의의 부분에 대해 사용자 지정 도구를 만들 수 있습니다.  
  
 [URL 액세스 &#40; Ssrs&#41;](../reporting-services/url-access-ssrs.md)  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]는 보고서 탐색 및 보기를 위한 빠르고 쉬운 액세스 지점으로 사용할 수 있는 전체 URL 기반 요청 집합을 지원합니다. 보고서 서버 웹 서비스와 함께 이 기술을 사용하여 전체 보고 솔루션을 사용자 지정 비즈니스 응용 프로그램에 통합할 수 있습니다. URL 액세스는 보고서를 웹 포털의 일부로 통합하거나 웹 브라우저에서 보고서를 볼 때 특히 유용합니다.  
  
 [Reporting Services 확장 프로그램](../reporting-services/extensions/reporting-services-extensions.md)  
 확장성을 위해 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 모듈식 아키텍처를 디자인했습니다. 다양한 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구성 요소에서 사용되는 확장 프로그램을 쉽게 개발, 설치 및 관리할 수 있도록 관리 코드 API를 사용할 수 있습니다. 사용 하 여 어셈블리를 만들 수는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 새로 추가 하 고 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 개발 중인 비즈니스 요구를 충족 하는 렌더링, 보안, 배달 및 데이터 처리 기능입니다.  
  
 [사용자 지정 보고서 항목](../reporting-services/custom-report-items/custom-report-items.md)  
 사용자 지정 보고서 항목을 만들어 RDL에 기능을 추가하거나 기존 컨트롤의 기능을 확장하는 방법을 설명합니다.  
  
 [보고서에 사용자 지정 어셈블리 사용](../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
 보고서 정의 내에 코드 참조를 포함시켜 보고서에 사용자 지정 어셈블리를 사용하는 방법을 설명합니다.  
  
 [Reporting Services WMI 공급자 액세스](../reporting-services/tools/access-the-reporting-services-wmi-provider.md)  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] WMI 공급자를 사용하여 보고서 서버 배포를 관리하는 방법을 설명합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services&#40;SSRS&#41;](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [보고서 정의 언어 &#40; Ssrs&#41;](../reporting-services/reports/report-definition-language-ssrs.md)   
 [기술 참조&#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)   
 [개발 &#40; 보안 Reporting services&#41;](../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
  
