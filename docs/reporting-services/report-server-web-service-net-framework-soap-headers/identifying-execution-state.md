---
title: 실행 상태 식별 | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-soap-headers
ms.topic: reference
helpviewer_keywords:
- session states [Reporting Services]
- lifetimes [Reporting Services]
- sessions [Reporting Services]
- SessionHeader SOAP header
ms.assetid: d8143a4b-08a1-4c38-9d00-8e50818ee380
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8b9e33f7c4d1b3ed953882175cd430df2b1e6ce1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "62991576"
---
# <a name="identifying-execution-state"></a>실행 상태 식별
  HTTP(Hypertext Transfer Protocol)는 연결 없는 상태 비저장 프로토콜이므로 다양한 요청이 동일한 클라이언트에서 나온 것인지 여부 또는 단일 브라우저 인스턴스에서 페이지나 사이트를 계속 사용 중인지 여부를 자동으로 나타내지 않습니다. 다수의 세션에서 논리적 연결이 만들어져 서버와 클라이언트 간의 상태가 HTTP를 통해 유지됩니다. 특정 세션과 관련된 사용자별 정보를 세션 상태라고 합니다.  
  
 세션 관리에는 HTTP 요청과 동일 세션에서 생성된 다른 이전 요청과의 상관 관계를 지정하는 작업이 포함됩니다. 세션 관리가 없으면 HTTP 프로토콜의 연결 없는 상태 비저장 특성으로 인해 이러한 요청은 보고서 서버 웹 서비스와 관련이 없는 것으로 나타납니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]에서 표시하는 것과 같이 세션 상태의 전체적 개념을 표시하지 않습니다. 하지만 보고서를 실행할 때 보고서 서버에서는 **실행**의 형태로 메서드 호출 간의 상태를 유지 관리합니다. 실행을 통해 사용자는 보고서 서버에서 보고서 로드, 보고서에 대한 자격 증명 및 매개 변수 설정, 보고서 렌더링 등을 포함하여 보고서에 여러 작업을 수행할 수 있습니다.  
  
 보고서 서버와 통신하는 동안 클라이언트에서는 실행을 사용하여 보고서 보기, 보고서의 다른 페이지로 사용자 이동 등을 관리하며 보고서의 섹션을 표시하거나 숨깁니다. 클라이언트 애플리케이션에서 실행 중인 각 보고서별로 고유한 실행이 존재합니다.  
  
 일반적으로 실행의 수명은 사용자가 브라우저나 클라이언트 애플리케이션으로 이동하여 보려는 보고서를 선택할 때 시작됩니다. 마지막 실행 요청이 수신된 후 짧은 제한 시간이 지나면 실행은 폐기됩니다(기본 제한 시간은 20분).  
  
 웹 서비스 측면에서 수명은 보고서 서버 웹 서비스 <xref:ReportExecution2005.ReportExecutionService.LoadReport%2A>, <xref:ReportExecution2005.ReportExecutionService.LoadReportDefinition%2A> 또는 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 메서드가 호출될 때 시작됩니다. 애플리케이션에서는 다른 메서드를 사용하여 활성 실행을 조작할 수 있습니다(예: 매개 변수 설정 및 데이터 원본 설정). 마지막 실행 요청이 수신된 후 짧은 제한 시간이 지나면 실행은 폐기됩니다(기본 제한 시간은 20분).  
  
 애플리케이션에서는 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 및 <xref:ReportExecution2005.ReportExecutionService.RenderStream%2A> 메서드에서 SOAP 헤더로 반환되는 <xref:ReportExecution2005.ExecutionHeader.ExecutionID%2A>를 저장하여 웹 서비스 <xref:ReportExecution2005.ReportExecutionService.LoadReport%2A> 및 <xref:ReportExecution2005.ReportExecutionService.LoadReportDefinition%2A> 메서드 호출 간의 여러 활성 실행을 추적합니다.  
  
 다음 다이어그램은 보고서에 대한 처리 및 렌더링 경로를 보여 줍니다.  
  
 ![보고서 처리/렌더링 경로](../../reporting-services/report-server-web-service-net-framework-soap-headers/media/rs-render-process-diagram.gif "보고서 처리/렌더링 경로")  
  
 위에 나타난 함수를 지원하기 위해 현재 SOAP Render 메서드는 실행 초기화, 처리 및 렌더링 단계를 포함한 여러 메서드로 분할되었습니다.  
  
 보고서를 프로그래밍 방식으로 렌더링하려면 다음 작업을 수행해야 합니다.  
  
-   <xref:ReportExecution2005.ReportExecutionService.LoadReport%2A> 또는 <xref:ReportExecution2005.ReportExecutionService.LoadReportDefinition%2A>을 사용하여 보고서 또는 보고서 정의를 로드합니다.  
  
-   <xref:ReportExecution2005.ExecutionInfo.CredentialsRequired%2A> 또는 <xref:ReportExecution2005.ExecutionInfo.ParametersRequired%2A>에 의해 반환된 <xref:ReportExecution2005.ExecutionInfo> 개체의 <xref:ReportExecution2005.ReportExecutionService.LoadReport%2A> 및 <xref:ReportExecution2005.ReportExecutionService.LoadReportDefinition%2A> 속성 값을 검토하여 보고서에 자격 증명 또는 매개 변수가 필요한지 여부를 확인합니다.  
  
-   필요한 경우 <xref:ReportExecution2005.ReportExecutionService.SetExecutionCredentials%2A> 및 <xref:ReportExecution2005.ReportExecutionService.SetExecutionParameters%2A> 메서드를 사용하여 자격 증명 및/또는 매개 변수를 설정합니다.  
  
-   <xref:ReportExecution2005.ReportExecutionService.Render%2A> 메서드를 호출하여 보고서를 렌더링합니다.  
  
 보고서가 세션에 있는 동안 보고서 서버 데이터베이스에 저장된 원본 보고서가 변경될 수 있습니다. 예를 들어 보고서 정의가 변경되거나, 보고서가 삭제 또는 이동되거나, 사용자 권한이 바뀔 수 있습니다. 보고서가 활성 세션에 있는 경우에는 원본 보고서, 즉 보고서 서버 데이터베이스에 저장된 보고서의 변경으로 인한 영향을 받지 않습니다.  
  
 URL 액세스 명령을 사용하여 보고서 세션을 관리할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [기술 참조&#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)   
 [Reporting Services SOAP 헤더 사용](../../reporting-services/report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)  
  
  
