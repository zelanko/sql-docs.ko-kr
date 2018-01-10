---
title: "Reporting Services 보고서 문제 해결 | Microsoft Docs"
ms.custom: 
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: troubleshooting
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a705d103-85b1-49b5-b27f-332b1040d029
caps.latest.revision: "9"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9546aaea0b177552fa83095c342a24a2e0f954e9
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="troubleshoot--reporting-services-report-issues"></a>Reporting Services 보고서 문제 해결
이 항목에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] 보고서 디자인, 보고서 미리 보기, 기본 모드 또는 SharePoint 모드에서 보고서 서버에 보고서 게시, 보고서 서버에서 보고서 보기 또는 다른 파일 형식으로 보고서 내보내기 등의 작업과 관련된 문제를 해결하는 데 필요한 정보를 제공합니다.  
## <a name="monitor-report-servers"></a>보고서 서버 모니터링  
시스템 및 데이터베이스 도구를 사용하여 보고서 서버 작업을 모니터링할 수 있습니다. 또한 보고서 서버 추적 로그 파일을 보거나 보고서 서버 실행 로그를 쿼리하여 특정 보고서에 대한 세부 정보를 확인할 수 있습니다. 성능 모니터를 사용하는 경우 보고서 서버 웹 서비스 및 Windows 서비스에 대한 성능 카운터를 추가하여 요청 시 처리 또는 예약된 처리의 병목 상태를 식별할 수 있습니다.  
자세한 내용은 [보고서 서버 성능을 모니터링](../../reporting-services/report-server/monitoring-report-server-performance.md)을 참조하세요.  
  
  
## <a name="view-the-report-server-logs"></a>보고서 서버 로그 보기  
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] 특정 보고서, 디버깅 정보, HTTP 요청 및 응답, 보고서 서버 이벤트 등에 대한 데이터를 기록하는 로그 파일에 여러 내부 및 외부 이벤트를 기록합니다. 또한 성능 로그를 만들고 수집할 데이터를 지정하는 성능 카운터를 선택할 수 있습니다. 기본 설치의 경우 로그 파일의 기본 디렉터리는 `<drive>\Program Files\Microsoft SQL Server\MSRS130.MSSQLSERVER\Reporting Services\LogFiles`입니다.   
  
자세한 내용은 [Reporting Services 로그 파일 및 소스](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)을 참조하세요.  
  
데이터 검색, 보고서 처리 또는 보고서 렌더링 중 보고서 대기 시간이 발생하는 원인이 무엇인지 자세히 확인하려면 실행 로그를 사용합니다. 자세한 내용은 [보고서 서버 ExecutionLog 및 ExecutionLog3 뷰]를 참조하세요.   
  
## <a name="view-the-call-stack-for-report-processing-error-messages-on-the-report-server"></a>보고서 서버에서 호출 스택을 확인하여 보고서 처리 오류 메시지 보기  
보고서 관리자에서 게시된 보고서를 볼 때는 일반 처리 또는 렌더링 오류를 나타내는 오류 메시지가 표시될 수 있습니다. 자세한 내용은 호출 스택에서 확인할 수 있습니다.   
  
호출 스택을 보려면 로컬 관리자 자격 증명을 사용하여 보고서 서버에 로그온하고 보고서 관리자 페이지를 마우스 오른쪽 단추로 클릭한 다음 **소스 보기**를 선택합니다. 호출 스택은 오류 메시지에 대한 자세한 컨텍스트를 제공합니다.  
  
## <a name="use-includessmanstudiofullincludesssmanstudiofullmd-to-verify-queries-and-credentials"></a>[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull.md)] 를 사용하여 쿼리 및 자격 증명 확인  
보고서에 복잡한 쿼리를 포함하기 전에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull.md)] 를 사용하여 이러한 쿼리의 유효성을 검사할 수 있습니다.   
  
자세한 내용은 [데이터베이스 엔진 쿼리 편집기](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md) 및 [개체 탐색기를 사용하여 개체 관리](~/ssms/object/manage-objects-by-using-object-explorer.md)를 참조하세요.  
  
## <a name="analyze-problem-reports-with-report-data-cached-on-the-client"></a>클라이언트에 캐시된 보고서 데이터를 사용하여 문제 보고서 분석  
보고서 작성자가 Business Intelligence Development Studio에서 보고서를 만들 때 제작 클라이언트는 데이터를 .rdl 데이터 파일로 캐시합니다. 이 캐시 데이터는 보고서를 미리 볼 때 사용됩니다. 이 캐시는 쿼리가 변경될 때마다 업데이트됩니다. 보고서 문제를 디버깅할 때는 디버깅 중에 데이터가 변경되지 않도록 보고서 데이터의 새로 고침을 방지하는 것이 유용할 수 있습니다.   
  
[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull.md)] 에서 캐시된 데이터만 사용할지 여부를 제어하려면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio.md)]의 devenv.exe.config에 다음 섹션을 추가합니다. 기본 디렉터리의 위치는 `<drive>:Program Files\Microsoft Visual Studio 10.0\Common7\IDE`입니다.   
  
```  
<system.diagnostics>  
      <switches>  
         <add name="Microsoft.ReportDesigner.ReportPreviewStore.ForceCache" value="1" />  
      </switches>  
   </system.diagnostics>  
```  
값이 1로 설정되어 있으면 캐시된 보고서 데이터만 사용됩니다. 보고서 디버깅을 마친 후에는 이 섹션을 제거해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
[오류 및 이벤트(Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]


