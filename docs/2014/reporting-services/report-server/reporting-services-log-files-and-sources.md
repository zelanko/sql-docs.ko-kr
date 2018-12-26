---
title: Reporting Services 로그 파일 및 소스 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting [Reporting Services], log files
- logs [Reporting Services]
- logs [Reporting Services], about log files
- report servers [Reporting Services], log files
- report server log files
- files [Reporting Services], logs
ms.assetid: 80ef0acc-cbef-49d0-87e7-844e3ce19604
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 45991def5af8ea0efbb1b9ea9a7bc6246770b3d3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116903"
---
# <a name="reporting-services-log-files-and-sources"></a>Reporting Services 로그 파일 및 소스
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서 서버 및 보고서 서버 환경은 서버 작업 및 상태에 대한 정보를 기록하는 데 여러 가지 로그 대상을 지원합니다. 로깅에는 실행 로깅 및 추적 로깅의 두 가지 기본 범주가 있습니다. 실행 로깅에는 보고서 실행 통계, 감사, 성능 진단 및 최적화에 대한 정보가 포함됩니다. 추적 로깅은 오류 메시지 및 일반 진단에 대한 정보입니다.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint 모드 | [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 기본 모드  
  
 다음 표에는 로그의 내용을 보는 방법과 로그 위치를 포함한 각 로그에 관한 추가 정보의 링크가 제공됩니다.  
  
|Log|Description|  
|---------|-----------------|  
|[보고서 서버 실행 로그 및 ExecutionLog3 뷰](report-server-executionlog-and-the-executionlog3-view.md)|실행 로그는 보고서 서버 데이터베이스에 저장되는 SQL Server 뷰입니다.<br /><br /> 보고서 서버 실행 로그에는 보고서를 실행한 시간과 사람, 보고서가 배달된 위치 및 사용된 렌더링 형식을 포함하여 특정 보고서에 대한 데이터가 들어 있습니다.|  
|SharePoint 추적 로그|SharePoint에서 실행하는 보고서 서버의 경우 SharePoint 추적 로그에 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 정보가 포함됩니다. SharePoint 통합 로깅 서비스의 경우 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 관련 정보를 구성할 수도 있습니다. 자세한 내용은 [SharePoint 추적 로그에 대한 Reporting Services 이벤트 설정&#40;ULS&#41;](turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)을 참조하세요.|  
|[보고서 서버 서비스 추적 로그](report-server-service-trace-log.md)|서비스 추적 로그에는 애플리케이션을 디버깅하거나 문제 또는 이벤트를 조사하는 경우에 유용한 세부 정보가 들어 있습니다.<br /><br /> `C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles`|  
|[보고서 서버 HTTP 로그](report-server-http-log.md)|HTTP 로그 파일에는 보고서 서버 웹 서비스 및 보고서 관리자에서 처리하는 모든 HTTP 요청 및 응답에 대한 기록이 포함되어 있습니다.|  
|[Windows 응용 프로그램 로그](windows-application-log.md)|Microsoft Windows 애플리케이션 로그에는 보고서 서버 이벤트에 대한 정보가 들어 있습니다.|  
|Windows 성능 로그|Windows 성능 로그에는 보고서 서버 성능 데이터가 들어 있습니다. 성능 로그를 만든 다음 수집할 데이터를 결정하는 카운터를 선택할 수 있습니다. 자세한 내용은 [Monitoring Report Server Performance](monitoring-report-server-performance.md)을 참조하세요.|  
|설치 로그 파일|설치 중에도 로그 파일이 만들어집니다. 설치에 실패하거나 성공했지만 경고 또는 기타 메시지가 있을 경우 문제 해결을 위해 로그 파일을 검사할 수 있습니다. 자세한 내용은 [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)을 참조하세요.|  
|IIS 로그|Microsoft IIS(인터넷 정보 서비스)에 의해 생성되는 로그 파일입니다. 자세한 내용은 [IIS(인터넷 정보 서비스)에서 로깅을 사용하도록 설정하는 방법](http://support.microsoft.com/kb/313437)을 참조하십시오.|  
|비디오|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 로그 파일은 Microsoft 파워 쿼리의 사용을 보여 주는 짧은 비디오에서 볼 수 있습니다.<br /><br /> ![파워 쿼리 및 SSRS 로그에 대 한 비디오를 볼](../media/generic-video-thumbnail.png "파워 쿼리 및 SSRS 로그에 대 한 비디오 보기")|  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 보고서 서버&#40;기본 모드&#41;](reporting-services-report-server-native-mode.md)   
 [오류 및 이벤트 참조 &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
