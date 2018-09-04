---
title: 응용 프로그램에 Reporting Services 통합 | Microsoft Docs
ms.date: 10/19/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.suite: pro-bi
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
author: markingmyname
ms.author: maghan
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ac677d269f25b8cc6d9c4587e729fd3e57063259
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43266550"
---
# <a name="integrating-reporting-services-into-applications"></a>응용 프로그램에 Reporting Services 통합

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 개발자에게 솔루션 개발을 위한 포괄적인 API 집합을 제공하도록 디자인된 개방형의 확장 가능한 보고 플랫폼입니다.

> [!NOTE]
> SQL Server 2017 Reporting Services부터 솔루션을 개발하는 데 REST API 액세스를 사용할 수 있습니다. SOAP API 액세스는 더 이상 사용되지 않습니다. 자세한 내용은 [Reporting Services에 대한 REST API를 사용하여 개발](../developer/rest-api.md)을 참조하세요.
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 사용자 지정 응용 프로그램에 통합하는 데는 보고서 서버 웹 서비스([!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SOAP API라고도 함), [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]용 ReportViewer 컨트롤, URL 액세스의 세 가지 옵션이 있습니다. 각 옵션에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 응용 프로그램에 통합하기 위한 서로 다른 방법을 제공합니다.
  
## <a name="report-server-web-service"></a>보고서 서버 웹 서비스

 보고서 서버 웹 서비스는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 대해 개발하기 위한 기본 인터페이스입니다. 보고서 카탈로그를 관리할 코드를 개발하든 아니면 보고서를 지원되는 형식으로 렌더링하는 코드를 개발하는 경우이든 웹 서비스는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 응용 프로그램에 통합하는 데 필요한 모든 방법을 제공합니다. 이러한 응용 프로그램의 예는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 포함되어 있는 보고서 관리자로서 여기서는 웹 서비스를 사용하여 보고서 서버 데이터베이스를 관리합니다.  
  
## <a name="reportviewer-controls-for-visual-studio"></a>Visual Studio용 ReportViewer 컨트롤

 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에 사용 가능한 ReportViewer 컨트롤은 보고서 보기를 응용 프로그램에 통합하는 데 사용합니다. 컨트롤에는 Windows Forms 기반 응용 프로그램용과 Web Forms 응용 프로그램용 두 가지가 있습니다. 각 컨트롤은 보고서 서버에 배포된 보고서를 보기 위한 기능뿐만 아니라 보고서 서버가 설치되지 않은 환경에 있는 보고서를 렌더링하는 기능도 제공합니다.  
  
## <a name="url-access"></a>URL 액세스  
 URL 액세스는 ReportViewer 컨트롤을 사용하지 않을 경우 보고서 보기를 응용 프로그램에 통합하기 위한 또 다른 옵션입니다. 그 외에도 URL 액세스는 전자 메일을 통해 사용자에게 보고서에 대한 링크를 보내는 데도 유용합니다.  
  
## <a name="in-this-section"></a>섹션 내용

 [SOAP를 사용하여 Reporting Services 통합](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)  
 보고서 서버 웹 서비스를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 탐색 및 관리를 기존 비즈니스 응용 프로그램에 통합하는 방법을 설명합니다.  
  
 [ReportViewer 컨트롤을 사용하여 Reporting Services 통합](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 ReportViewer 컨트롤을 사용하여 보고서 보기를 기존 응용 프로그램에 통합하는 방법을 설명합니다.  
  
 [URL 액세스를 사용하여 Reporting Services 통합](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)  
 URL 액세스를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 탐색을 기존 비즈니스 응용 프로그램에 통합하는 방법을 설명합니다.  
  
## <a name="next-steps"></a>다음 단계

URL 액세스 또는 SOAP API를 사용할지 결정하려면 [Reporting Services에서 URL 액세스와 SOAP 중 선택](choosing-between-url-access-and-soap.md)을 참조하세요.

SQL Server 2017 Reporting Services REST API에 대한 자세한 내용은 [Reporting Services에 대한 REST API를 사용하여 개발](../developer/rest-api.md)을 참조하세요.

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
