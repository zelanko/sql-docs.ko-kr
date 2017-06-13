---
title: "Reporting Services 로그 파일 및 소스 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- troubleshooting [Reporting Services], log files
- logs [Reporting Services]
- logs [Reporting Services], about log files
- report servers [Reporting Services], log files
- report server log files
- files [Reporting Services], logs
ms.assetid: 80ef0acc-cbef-49d0-87e7-844e3ce19604
caps.latest.revision: 49
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 08686f83b78c783e1d82c144e4a06f9ecd52bde0
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="reporting-services-log-files-and-sources"></a>Reporting Services 로그 파일 및 소스
  보고서 서버 및 보고서 서버 환경은 서버 작업 및 상태에 대한 정보를 기록하는 데 여러 가지 로그 대상을 사용합니다. 로깅에는 실행 로깅 및 추적 로깅의 두 가지 기본 범주가 있습니다. 실행 로깅에는 보고서 실행 통계, 감사, 성능 진단 및 최적화에 대한 정보가 포함됩니다. 추적 로깅은 오류 메시지 및 일반 진단에 대한 정보입니다.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint mode | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Native mode  
  
 다음 표에는 로그의 내용을 보는 방법과 로그 위치를 포함한 각 로그에 관한 추가 정보의 링크가 제공됩니다.  
  
|Log|Description|  
|---------|-----------------|  
|[보고서 서버 ExecutionLog 및 ExecutionLog3 뷰](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)|실행 로그는 보고서 서버 데이터베이스에 저장되는 SQL Server 뷰입니다.<br /><br /> 보고서 서버 실행 로그에는 보고서를 실행한 시간과 사람, 보고서가 배달된 위치 및 사용된 렌더링 형식을 포함하여 특정 보고서에 대한 데이터가 들어 있습니다.|  
|SharePoint 추적 로그|SharePoint에서 실행하는 보고서 서버의 경우 SharePoint 추적 로그에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 정보가 포함됩니다. SharePoint 통합 로깅 서비스의 경우 [!INCLUDE[ssRS](../../includes/ssrs-md.md)] 관련 정보를 구성할 수도 있습니다. 자세한 내용은 [SharePoint 추적 로그에 대한 Reporting Services 이벤트 설정&#40;ULS&#41;](../../reporting-services/report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)|  
|[보고서 서버 서비스 추적 로그](../../reporting-services/report-server/report-server-service-trace-log.md)|서비스 추적 로그에는 응용 프로그램을 디버깅하거나 문제 또는 이벤트를 조사하는 경우에 유용한 세부 정보가 들어 있습니다. 추적 로그 파일은 ReportServerService_\<타임 스탬프 > 되 고.log은 다음 폴더에 있어야 합니다.<br /><br /> `C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`|  
|[보고서 서버 HTTP 로그](../../reporting-services/report-server/report-server-http-log.md)|HTTP 로그 파일에는 보고서 서버 웹 서비스 및 보고서 관리자에서 처리하는 모든 HTTP 요청 및 응답에 대한 기록이 포함되어 있습니다.|  
|[Windows 응용 프로그램 로그](../../reporting-services/report-server/windows-application-log.md)|Microsoft Windows 응용 프로그램 로그에는 보고서 서버 이벤트에 대한 정보가 들어 있습니다.|  
|Windows 성능 로그|Windows 성능 로그에는 보고서 서버 성능 데이터가 들어 있습니다. 성능 로그를 만든 다음 수집할 데이터를 결정하는 카운터를 선택할 수 있습니다. 자세한 내용은 [Monitoring Report Server Performance](../../reporting-services/report-server/monitoring-report-server-performance.md)을 참조하세요.|  
|SQL Server 설치 로그 파일|설치 중에도 로그 파일이 만들어집니다. 설치에 실패하거나 성공했지만 경고 또는 기타 메시지가 있을 경우 문제 해결을 위해 로그 파일을 검사할 수 있습니다. 자세한 내용은 [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)을 참조하세요.|  
|IIS 로그|Microsoft IIS(인터넷 정보 서비스)에 의해 생성되는 로그 파일입니다. 자세한 내용은 [IIS(인터넷 정보 서비스)에서 로깅을 사용 가능하게 설정하는 방법](http://support.microsoft.com/kb/313437) (http://support.microsoft.com/kb/313437)을 참조하세요.|  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services 보고서 서버&#40;기본 모드&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [오류 및 이벤트 참조&#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
