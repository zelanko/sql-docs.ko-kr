---
title: "실행 중인 프로세스 관리 | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report processing [Reporting Services], status information
- jobs [Reporting Services]
- viewing jobs
- canceling jobs
- user jobs [Reporting Services]
- system jobs [Reporting Services]
- report processing [Reporting Services], managing running processes
- processes [Reporting Services]
- scanning processes [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services]
- canceling subscriptions
- report servers [Reporting Services], jobs
- data-driven subscriptions
- displaying jobs
- subscriptions [Reporting Services], running processes
ms.assetid: 473e574e-f1ff-4ef9-bda6-7028b357ac42
caps.latest.revision: 53
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 103472f5003235e0e08c65c40999545ff4d864ee
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="manage-a-running-process"></a>실행 중인 프로세스 관리
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 보고서 서버에서 실행 중인 작업의 상태를 모니터링합니다. 보고서 서버는 진행 중인 작업을 정기적으로 검색하고 SharePoint 모드용 서비스 응용 프로그램 데이터베이스 또는 보고서 서버 데이터베이스에 상태 정보를 씁니다. 원격 또는 로컬 데이터베이스 서버에서 쿼리가 실행되거나 보고서가 처리되거나 보고서가 렌더링되는 경우 작업이 진행 중인 것입니다.  
  
 *사용자 작업* 과 *시스템 작업*을 모두 관리할 수 있습니다.  
  
-   사용자 작업은 개별 사용자나 구독에 의해 시작됩니다. 여기에는 요청 시 보고서 실행, 보고서 기록 스냅숏 요청, 보고서 스냅숏의 수동 생성 및 표준 구독 처리 작업이 포함됩니다.  
  
-   시스템 작업은 보고서 서버에 의해 시작됩니다. 시스템 작업에는 예약된 보고서 실행 스냅숏, 예약된 보고서 기록 스냅숏 및 데이터 기반 구독이 포함됩니다.  
  
 보고서 처리 시간과 리소스 사용량은 보고서, 쿼리 복잡성, 데이터의 양 및 보고서에 대해 지정된 렌더링 형식에 따라 크게 달라집니다. 로컬 데이터 원본에 대한 단순 쿼리를 포함하는 보고서는 밀리초 단위로 완료되며 관리나 튜닝이 필요하지 않습니다. 이와는 반대로 PDF나 Excel에서 렌더링한 큰 보고서는 하드웨어 리소스, 배달 옵션 및 다른 프로세스의 동시 실행 여부에 따라 처리하는 데 시간이 상당히 오래 걸릴 수 있습니다. 보고서 서버에서 장기간 실행되는 대부분의 프로세스는 쿼리 처리가 끝나기를 기다리는 보고서 렌더링 작업 및 프로세스입니다. 경우에 따라 컴퓨터를 오프라인으로 전환한 경우 보고서 프로세스를 취소하거나 완료되는 데 시간이 많이 걸리는 실행 중인 작업을 중지해야 할 수 있습니다.  
  
 다음 프로세스를 취소할 수 있습니다.  
  
-   요청 시 실행 보고서 처리  
  
-   예약된 보고서 처리  
  
-   개별 사용자가 소유한 표준 구독  
  
 작업을 취소하면 보고서 서버에서 실행 중인 프로세스만 취소됩니다. 보고서 서버는 다른 컴퓨터에서 발생하는 데이터 처리를 관리하지 않으므로 이후에 다른 시스템에서 분리되는 쿼리 프로세스는 수동으로 취소해야 합니다. 실행하는 데 시간이 너무 오래 걸리는 쿼리는 자동으로 종료되도록 쿼리 제한 시간 값을 지정하세요. 자세한 내용은 [보고서 및 공유 데이터 집합 처리에 대한 제한 시간 값 설정&#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)을 참조하세요. 보고서를 일시적으로 중지하는 방법에 대한 자세한 내용은 [보고서 및 구독 처리 해제 또는 일시 중지](../../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md)를 참조하세요.  
  
> [!NOTE]  
>  간혹 프로세스를 취소하기 위해 서버를 다시 시작해야 할 수도 있습니다. SharePoint 모드의 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램을 호스팅하는 응용 프로그램 풀을 다시 시작해야 할 수 있습니다. 자세한 내용은 [보고서 서버 서비스 시작 및 중지](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)를 참조하세요.  
  
 항목 내용  
  
-   [작업 보기 및 취소(기본 모드)](#bkmk_native)  
  
-   [작업 보기 및 취소(SharePoint 모드)](#bkmk_sharepoint)  
  
-   [프로그래밍 방식으로 작업 관리](#bkmk_programmatically)  
  
##  <a name="bkmk_native"></a> 작업 보기 및 취소(기본 모드)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용하여 보고서 서버에서 실행 중인 작업을 보거나 취소할 수 있습니다. 현재 실행 중인 작업 목록을 검색하거나 보고서 서버 데이터베이스에서 최신 작업 상태를 가져오려면 페이지를 새로 고쳐야 합니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 보고서 서버에 연결하면 작업 폴더를 열어 보고서 서버 컴퓨터에서 현재 처리 중인 보고서 목록을 볼 수 있습니다. 각 작업에 대한 상태 정보는 작업 속성 페이지에 표시됩니다. 보고서 서버 작업 취소 대화 상자를 열어 모든 작업에 대한 상태 정보를 볼 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용하여 보고서 서버에서 실행 중인 작업을 보거나 취소할 수 있습니다. 현재 실행 중인 작업 목록을 검색하거나 보고서 서버 데이터베이스에서 최신 작업 상태를 가져오려면 페이지를 새로 고쳐야 합니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 보고서 서버에 연결하면 작업 폴더를 열어 보고서 서버 컴퓨터에서 현재 처리 중인 보고서 목록을 볼 수 있습니다. 각 작업에 대한 상태 정보는 작업 속성 페이지에 표시됩니다. 보고서 서버 작업 취소 대화 상자를 열어 모든 작업에 대한 상태 정보를 볼 수 있습니다.  
  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용하여 모델 생성, 모델 처리 또는 데이터 기반 구독을 나열하거나 취소할 수 없습니다. Reporting Services는 모델 생성 또는 처리를 취소하는 방법을 제공하지 않습니다. 그러나 이 항목에 제공된 지침에 따라 데이터 기반 구독을 취소할 수 있습니다.  
  
### <a name="how-to-cancel-report-processing-or-subscription"></a>보고서 처리 또는 구독을 취소하는 방법  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 보고서 서버에 연결합니다. 자세한 내용은 [Management Studio에서 보고서 서버에 연결](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)을 참조하세요.  
  
2.  **작업** 폴더를 엽니다.  
  
3.  보고서를 마우스 오른쪽 단추로 클릭한 다음 **작업 취소**를 클릭합니다.  
  
### <a name="how-to-cancel-a-data-driven-subscription"></a>데이터 기반 구독을 취소하는 방법  
  
1.  텍스트 편집기에서 RSReportServer.config 파일을 엽니다.  
  
2.  **IsNotificationService**을 찾습니다.  
  
3.  **False**로 설정합니다.  
  
4.  파일을 저장합니다.  
  
5.  보고서 관리자에서 보고서의 구독 탭 또는 **내 구독**에서 데이터 기반 구독을 삭제합니다.  
  
6.  구독을 삭제한 후 RSReportServer.config 파일에서 **IsNotificationService** 를 찾아 **True**로 설정합니다.  
  
7.  파일을 저장합니다.  
  
### <a name="configuring-frequency-settings-for-retrieving-job-status"></a>작업 상태 검색을 위한 빈도 설정 구성  
 실행 중인 작업은 보고서 서버 임시 데이터베이스에 저장됩니다. RSReportServer.config 파일에서 구성 설정을 수정하여 보고서 서버가 진행 중인 작업을 검색하는 빈도 및 실행 작업의 상태가 새 작업에서 실행 중인 작업으로 변경되는 간격을 제어할 수 있습니다. **RunningRequestsDbCycle** 설정은 보고서 서버가 실행 중인 프로세스를 검색하는 빈도를 지정합니다. 기본적으로 상태 정보는 60초마다 기록됩니다. **RunningRequestsAge** 설정은 작업이 새 작업에서 실행 중인 작업으로 전환되는 간격을 지정합니다.  
  
##  <a name="bkmk_sharepoint"></a> 작업 보기 및 취소(SharePoint 모드)  
 SharePoint 모드 배포에서 작업 관리는 각 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램에 대해 SharePoint 중앙 관리를 사용하여 완료됩니다.  
  
#### <a name="to-manage-jobs-in-sharepoint-mode"></a>SharePoint 모드에서 작업을 관리하려면  
  
1.  SharePoint 중앙 관리에서 **서비스 응용 프로그램 관리**를 클릭합니다.  
  
2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램의 이름을 찾아서 클릭하여 응용 프로그램 관리 페이지를 엽니다.  
  
3.  **작업 관리**를 클릭합니다.  
  
4.  작업 세부 정보를 보려면 **작업 ID** 를 클릭합니다.  
  
5.  또는 작업에 대한 상자를 클릭하고 **삭제** 를 클릭하여 작업을 취소합니다. 작업을 삭제해도 구독은 삭제되지 않습니다.  
  
##  <a name="bkmk_programmatically"></a> 프로그래밍 방식으로 작업 관리  
 프로그래밍 방식으로 또는 스크립트를 사용하여 작업을 관리할 수 있습니다. 자세한 내용은 <xref:ReportService2010.ReportingService2010.ListJobs%2A> 및 <xref:ReportService2010.ReportingService2010.CancelJob%2A>를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 작업 취소&#40;Management Studio&#41;](../../reporting-services/tools/cancel-report-server-jobs-management-studio.md)   
 [작업 속성&#40;Management Studio&#41;](../../reporting-services/tools/job-properties-management-studio.md)   
 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [보고서 관리자&#40;SSRS 기본 모드&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [보고서 서버 성능 모니터링](../../reporting-services/report-server/monitoring-report-server-performance.md)  
  
  
