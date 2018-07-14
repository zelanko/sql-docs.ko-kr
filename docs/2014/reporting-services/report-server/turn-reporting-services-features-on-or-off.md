---
title: Reporting Services 기능 설정 또는 해제 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, configuration
- security [Reporting Services], strategies
ms.assetid: b69db02a-43a7-4fdc-ad9b-438d817a7f83
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6521a2bcdf080eb4a22c9540d965d0b5829d74fe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37282599"
---
# <a name="turn-reporting-services-features-on-or-off"></a>Reporting Services 기능 설정 또는 해제
  프로덕션 보고서 서버의 공격 노출 영역을 줄이기 위한 잠금 전략의 일환으로 사용하지 않는 보고서 서버 기능을 해제할 수 있습니다. 대부분의 경우에는 여러 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능을 동시에 실행하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 제공하는 모든 기능을 사용해야 합니다. 그러나 배포 모델에 따라서는 필요하지 않은 기능을 비활성화할 수 있습니다. 예를 들어 모든 보고서 처리가 예약된 작업으로 구성된 경우 백그라운드 처리만 활성화할 수 있습니다. 마찬가지로 요청 시 실행되는 대화형 보고서만 원하는 경우에는 보고서 서버 웹 서비스만 실행할 수 있습니다.  
  
 이 항목의 절차에서는 기본 모드 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능을 해제하는 방법을 보여 줍니다. `RsReportServer.config` 파일을 직접 편집하거나 **에서 정책 기반 관리의** Reporting Services에 대한 노출 영역 구성 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]패싯을 사용하는 등의 다양한 방법으로 기능을 구성할 수 있습니다. 해당 링크를 사용하여 기능을 설정하거나 해제하는 방법을 설명하는 절차를 찾을 수 있습니다.  
  
-   [보고서 서버 웹 서비스](#RSWebSvc)  
  
-   [예약된 이벤트 및 처리](#Sched)  
  
-   [보고서 관리자](#ReportManager)  
  
-   [보고서 작성기](#ReportBuilder)  
  
-   [보고서 데이터 원본에 Windows 통합 보안](#WinIntSec)  
  
##  <a name="RSWebSvc"></a> Report Server Web Service  
  
#### <a name="to-turn-on-or-off-the-report-server-web-service-by-editing-configuration"></a>구성을 편집하여 보고서 서버 웹 서비스를 설정하거나 해제하려면  
  
1.  텍스트 편집기에서 `RsReportServer.config` 파일을 엽니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)를 참조하세요.  
  
2.  보고서 서버 웹 서비스를 설정 `IsWebServiceEnabled` 에 `true`:  
  
    ```  
    <IsWebServiceEnabled>true</IsWebServiceEnabled>  
    ```  
  
3.  보고서 서버 웹 서비스를 해제하려면 `IsWebServiceEnabled`를 `false`로 설정합니다.  
  
    ```  
    <IsWebServiceEnabled>false</IsWebServiceEnabled>  
    ```  
  
4.  변경 내용을 저장한 다음 파일을 닫습니다.  
  
#### <a name="to-turn-on-or-off-the-report-server-web-service-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 보고서 서버 웹 서비스를 설정하거나 해제하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 열고 구성할 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 노드를 마우스 오른쪽 단추로 클릭하고 **정책**을 가리킨 다음 **패싯**을 클릭합니다.  
  
3.  **패싯** 목록에서 **Reporting Services에 대한 노출 영역**을 선택합니다.  
  
4.  **패싯 속성**아래에서 다음을 수행합니다.  
  
    -   보고서 서버 웹 서비스를 설정 **WebServiceAndHTTPAccessEnabled** 에 `True`입니다.  
  
    -   보고서 서버 웹 서비스를 해제 하려면 **WebServiceAndHTTPAccessEnabled** 에 `False`입니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="Sched"></a> 예약된 이벤트 및 배달  
  
#### <a name="to-turn-on-or-off-scheduled-events-and-delivery-by-editing-configuration"></a>구성을 편집하여 예약된 이벤트 및 배달을 설정하거나 해제하려면  
  
1.  텍스트 편집기에서 RsReportServer.config 파일을 엽니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)를 참조하세요.  
  
2.  예약된 보고서 처리 및 배달을 활성화하려면 `IsSchedulingService`, `IsNotificationService` 및 `IsEventService`를 `true`로 설정합니다.  
  
    ```  
    <IsSchedulingService>true</IsSchedulingService>  
    <IsNotificationService>true</IsNotificationService>  
    <IsEventService>true</IsEventService>  
    ```  
  
3.  예약된 보고서 처리 및 배달을 해제하려면 `IsSchedulingService`, `IsNotificationService` 및 `IsEventService`를 `false`로 설정합니다.  
  
    ```  
    <IsSchedulingService>false</IsSchedulingService>  
    <IsNotificationService>false</IsNotificationService>  
    <IsEventService>false</IsEventService>  
    ```  
  
4.  변경 내용을 저장한 다음 파일을 닫습니다.  
  
> [!NOTE]  
>  백그라운드 처리는 서버 작업에 필요한 유지 관리 기능을 제공하므로 완전히 해제할 수는 없습니다.  
  
#### <a name="to-turn-on-or-off-scheduled-events-and-delivery-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 예약된 이벤트 및 배달을 설정하거나 해제하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 열고 구성할 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 노드를 마우스 오른쪽 단추로 클릭하고 **정책**을 가리킨 다음 **패싯**을 클릭합니다.  
  
3.  **패싯** 목록에서 **Reporting Services에 대한 노출 영역**을 선택합니다.  
  
4.  **패싯 속성**아래에서 다음을 수행합니다.  
  
    -   예약 된 이벤트 및 배달을 활성화를 설정 **ScheduleEventsAndReportDeliveryEnabled** 에 `True`입니다.  
  
    -   예약 된 이벤트 및 배달을 해제 하려면 설정 **ScheduleEventsAndReportDeliveryEnabled** 에 `False`입니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  백그라운드 처리는 서버 작업에 필요한 유지 관리 기능을 제공하므로 완전히 해제할 수는 없습니다.  
  
##  <a name="ReportManager"></a> 보고서 관리자  
  
#### <a name="to-turn-on-or-off-report-manager-by-editing-configuration"></a>구성을 편집하여 보고서 관리자를 설정하거나 해제하려면  
  
1.  텍스트 편집기에서 RsReportServer.config 파일을 엽니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)을 참조하세요.  
  
2.  보고서 관리자를 설정 `IsReportManagerEnabled` 에 `true`:  
  
    ```  
    <IsReportManagerEnabled>true</IsReportManagerEnabled>  
    ```  
  
3.  보고서 관리자 해제를 설정 `IsReportManagerEnabled` 에 `false`:  
  
    ```  
    <IsReportManagerEnabled>false</IsReportManagerEnabled>  
    ```  
  
4.  변경 내용을 저장한 다음 파일을 닫습니다.  
  
#### <a name="to-turn-on-or-off-report-manager-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 보고서 관리자를 설정하거나 해제하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 열고 구성할 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  **개체 탐색기**에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 노드를 마우스 오른쪽 단추로 클릭하고 **정책**을 가리킨 다음 **패싯**을 클릭합니다.  
  
3.  **패싯** 목록에서 **Reporting Services에 대한 노출 영역**을 선택합니다.  
  
4.  **패싯 속성**아래에서 다음을 수행합니다.  
  
    -   보고서 관리자를 설정 **ReportManagerEnabled** 에 `True`입니다.  
  
    -   보고서 관리자 해제를 설정 **ReportManagerEnabled** 에 `False`입니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ReportBuilder"></a> 보고서 작성기  
  
#### <a name="to-turn-on-or-off-report-builder-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 보고서 작성기를 설정하거나 해제하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 열고 구성할 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 노드를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
3.  **서버 속성** 대화 상자의 **페이지 선택**아래에서 **보안**을 클릭합니다.  
  
    -   보고서 작성기를 활성화하려면 **임시 보고서 실행 사용** 옵션을 선택합니다.  
  
    -   보고서 작성기를 해제하려면 **임시 보고서 실행 사용** 옵션의 선택을 취소합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="WinIntSec"></a> Windows 통합 보안  
  
#### <a name="to-turn-on-or-off-windows-integrated-security-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 Windows 통합 보안을 설정하거나 해제하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 열고 구성할 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 노드를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
3.  **서버 속성** 대화 상자의 **페이지 선택**아래에서 **보안**을 클릭합니다.  
  
    -   Windows 통합 보안을 활성화하려면 **보고서 데이터 원본에 대한 Windows 통합 보안 사용** 옵션을 선택합니다.  
  
    -   Windows 통합 보안을 해제하려면 **보고서 데이터 원본에 대한 Windows 통합 보안 사용** 옵션의 선택을 취소합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
