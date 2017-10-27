---
title: "URL 액세스와 SOAP in Reporting Services 간의 선택 | Microsoft Docs"
ms.custom: 
ms.date: 10/19/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 1d9b4df388cd1d6bb96d88b64bf319f5fd9866e9
ms.contentlocale: ko-kr
ms.lasthandoff: 10/20/2017

---
# <a name="choosing-between-url-access-and-soap-in-reporting-services"></a>URL 액세스와 SOAP in Reporting Services 간의 선택

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 사용자 지정 응용 프로그램에 통합하는 작업은 까다로울 수 있습니다. 하지만 문제는 프로그래밍 모델이나 API의 복잡성이 아니라 통합에 사용할 수 있는 방법이 다양하다는 점입니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 처음부터 개발자 플랫폼으로 디자인되었기 때문에 프로그래밍 유연성을 염두에 두고 만들어졌습니다. 이러한 유연성으로 인해 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 탐색 및 관리 기능을 기존 비즈니스 응용 프로그램에 통합하는 데 있어서 중요한 결정이 필요합니다.

> [!NOTE]
> SQL Server 2017 Reporting Services부터 REST API 액세스는 솔루션을 개발 하는 데 사용할 수 있습니다. SOAP API 액세스는 더 이상 사용 되지 않습니다. 자세한 내용은 참조 [Reporting Services에 대 한 REST Api로 개발](../developer/rest-api.md)합니다.
  
 통합 하는 방법은 두 가지가 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 을 사용자 지정 응용 프로그램에: URL 액세스와 Reporting Services SOAP API입니다. 어느 방법을 사용할지는 여러 요소에 따라 달라집니다. 경우에 따라 통합 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 사용자 지정 비즈니스 응용 프로그램은 URL 액세스와 SOAP를 사용 해야 합니다. 다음과 같은 질문을 고려해야 합니다.  
  
-   자신 또는 최종 사용자에게 어떤 유형의 엔터프라이즈 보고 기능이 필요합니까? 보고서를 간단하게 시작하고 탐색할 수 있는 방법이 필요합니까 아니면 사용자 지정 비즈니스 솔루션에서 고급 보고서 서버 관리 기능이 필요합니까?  
  
-   사용자들이 일반적으로 어떤 유형의 환경에서 작업합니까? 사용하는 비즈니스 응용 프로그램이 웹 응용 프로그램입니까 아니면 Windows 응용 프로그램입니까? 얼마나 쉽게 최종 사용자에 게 전환할 수 Win32 환경에서 웹 환경? 보고서가 실행되고 관리되는 환경에 대해 어떤 유형의 컨트롤이 필요합니까?  
  
 위의 질문에 대한 대답을 기준으로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 IT 인프라에 통합할 방법을 결정할 수 있습니다. 일반적으로 URL 액세스는 개별 보고서를 보고 탐색하는 데 사용하는 것이 좋습니다. URL 액세스를 통해 웹 서비스 오버헤드 없이 보고서를 쉽고 빠르게 탐색할 수 있습니다. 또한 URL 액세스는 현재 보고서 도구 모음을 포함하여 보고서 탐색을 위해 전체 HTML 뷰어를 사용하는 유일한 프로그래밍 기술입니다. 그리고 URL 액세스는 서버를 상대로 한 SOAP 요청에 대한 마샬링을 거치지 않으므로 SOAP보다 뛰어난 성능을 제공합니다. 보기 및 탐색용 기본 제공 도구를 사용하여 보고서에 쉽고 빠르게 액세스해야 하는 통합 시나리오에서는 URL 액세스를 선택하는 것이 더 좋습니다.  
  
> [!NOTE]  
> 보고서 서버 URL 액세스는 HTML 뷰어 및 보고서 도구 모음의 확장된 기능을 지원합니다. SOAP API는 이러한 종류의 렌더링된 보고서를 지원하지 않습니다. SOAP API를 사용 하 여 보고서를 렌더링 하는 경우 디자인 하 고 고유의 보고서 도구 모음을 개발 합니다.
  
 보고서 도구 모음에 대 한 자세한 내용은 참조 [HTML 뷰어 및 보고서 도구 모음](../../reporting-services/html-viewer-and-the-report-toolbar.md)합니다.  
  
 URL 액세스에 대 한 자세한 내용은 참조 [URL 액세스](../../reporting-services/url-access-ssrs.md)합니다.  
  
 URL 액세스는 보고서를 보는 데 유용하지만 엔터프라이즈 보고 시나리오에 필수적일 수 있는 보고서 및 네임스페이스 관리 기능을 제공하지 않습니다. 이 경우 Reporting Services SOAP API에서 제공되는 다양하고 풍부한 기능을 사용하는 것이 좋습니다. SOAP API를 통해 보고서 관리 및 배포, 일정 만들기, 서버 속성 구성, 보고서 서버 네임스페이스 관리, 구독 만들기 등의 작업을 수행할 수 있습니다. SOAP API는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 전체 관리 기능 집합을 표시합니다. 또한 SOAP API에서는 API의 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 메서드를 통해 보고서 보기 및 탐색이 가능합니다. 그러나 SOAP API를 통해 보고서 보기를 URL 액세스를 제공 하는 보고서 대화형 작업을 자동으로 처리 없으며 보고서 도구 모음에서의 기본 제공 보기 기능을 지원 하지 않습니다.  
  
 Reporting Services SOAP API에 대 한 자세한 내용은 참조 [보고서 서버 웹 서비스](../../reporting-services/report-server-web-service/report-server-web-service.md)합니다.  
  
 대부분의 경우 보고 요구를 충족하기 위해서는 URL 액세스와 SOAP 호출이 모두 필요합니다. SOAP은 처음에 보고서 서버 데이터베이스에 연결하고 사용자 인터페이스에 사용 가능한 보고서 목록을 표시하는 데 사용되며, URL 액세스는 개별 보고서를 실제로 액세스하고 탐색하는 데 사용됩니다.  
  
 URL 액세스와 통합 된 보고서를 제공 하는 웹 서비스를 결합 하 여 예제를 보려면 [SQL Server Reporting Services 제품 샘플](http://go.microsoft.com/fwlink/?LinkId=177889)합니다.

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)

