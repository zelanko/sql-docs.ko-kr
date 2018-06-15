---
title: 일정 | Microsoft Docs
ms.custom: ''
ms.date: 07/01/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: subscriptions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- schedules [Reporting Services]
- schedules [Reporting Services], about schedules
- published reports [Reporting Services], schedules
- reports [Reporting Services], scheduling
- subscriptions [Reporting Services], scheduling
- automatic report processing
ms.assetid: ecccd16b-eba9-4e95-b55d-f15c621e003f
caps.latest.revision: 51
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ff16cd9d2794ded1d6b841a14d4ee01f45a9f9d6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33035520"
---
# <a name="schedules"></a>일정
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 보고서의 처리와 배포를 쉽게 제어할 수 있도록 **공유 일정** 과 **보고서별 일정** 을 제공합니다. 이 두 일정 유형의 차이점은 일정의 정의, 저장 및 관리 방법에 있습니다. 두 일정 유형의 내부 구조는 동일합니다. 모든 일정은 되풀이 유형을 월별, 주별 또는 일별로 지정할 수 있습니다. 되풀이 유형 내에서 이벤트 발생 빈도에 대한 간격과 범위를 설정하세요. 되풀이 패턴의 유형과 되풀이 패턴이 지정되는 방식은 공유 일정을 만드는지 아니면 보고서별 일정을 만드는지 여부에 관계없이 동일합니다.
  
  -   공유 일정은 별도의 항목으로 생성됩니다. 구독이나 예약된 다른 작업을 정의할 때 이렇게 생성된 공유 일정을 참조합니다.  
  
-   보고서별 일정은 구독을 정의하거나 보고서 실행 속성을 설정할 때 생성됩니다. 일정 정보를 작성하는 것은 구독 정의 또는 속성 설정의 일부입니다. 보고서별 일정을 정의하려면 일정을 사용하는 보고서나 구독을 엽니다.  
  
 공유 일정에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버에서 실행되는 게시된 여러 보고서 및 구독에 사용할 수 있는 일정 및 되풀이 정보가 포함됩니다. 동시에 실행되는 보고서와 구독이 여러 개 있을 경우 이러한 작업에 대한 공유 일정을 만들 수 있습니다. 이후에 되풀이 패턴 또는 종료 날짜를 변경하려는 경우 단일 위치에서 변경할 수 있습니다.  
  
 공유 일정은 관리하기가 더 쉬우므로 예약된 작업을 보다 유연하게 관리할 수 있습니다. 예를 들어 공유 일정을 일시 중지하고 재개할 수 있습니다. 또한 예약된 작업이 동시에 너무 많이 실행되는 경우에는 서로 다른 시간에 실행되는 공유 일정을 여러 개 만든 다음 처리 부하가 보고서 서버에서 균등하게 분포될 때까지 일정 정보를 조정할 수 있습니다.  
  
  
##  <a name="bkmk_whatyoucando"></a> 예약으로 수행할 수 있는 작업  
 기본 모드의 경우 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 웹 포털 및 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] , SharePoint 모드의 경우 SharePoint 사이트 관리 페이지를 사용하여 예약을 만들고 관리할 수 있습니다. 다음 작업을 수행할 수 있습니다.  
  
-   표준 또는 데이터 기반 구독에서 보고서 배달 예약  
  
-   새 스냅숏이 정기적으로 보고서 기록에 추가되도록 보고서 기록 일정을 예약합니다.  
  
-   보고서 스냅숏의 데이터 새로 고침 시기 예약  
  
-   공유 데이터 집합의 데이터 새로 고침 시기 예약  
  
-   이후에 새로 고칠 수 있도록 미리 정의된 시간에 캐시된 보고서 또는 공유 데이터 집합 만료 예약  
  
 여러 보고서 또는 구독에 대해 동일한 일정 정보를 사용하려는 경우 공유 일정을 만들 수 있습니다. 공유 일정은 별도로 정의한 다음 일정 정보를 필요로 하는 보고서, 공유 데이터 집합 및 구독에서 정의된 공유 일정을 참조합니다.  
  
 일정을 만들면 보고서는 보고서 서버 데이터베이스 또는 서비스 응용 프로그램 데이터베이스(SharePoint 모드의 경우)에 일정 정보를 저장합니다. 또한 보고서 서버는 해당 일정을 트리거하는 데 사용되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 만듭니다. 일정 처리는 일정을 포함하는 보고서 서버의 현지 시간을 기준으로 합니다. 시간 형식은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 운영 체제 표준을 따릅니다.  
  
 예약을 만들고 관리하는 방법은 [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)를 참조하세요.  
  
> [!NOTE]  
>  일정 작업은 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](http://msdn.microsoft.com/library/22ad82d7-860c-43d3-b77a-77fb9eec5454)을 참조하세요.  
  
##  <a name="bkmk_compare"></a> 공유 일정과 보고서별 일정 비교  
 두 가지 유형의 일정 모두 출력 내용이 같습니다.  
  
-   **공유 일정** 은 미리 만들어 놓은 일정 정보가 들어 있는 이식 가능한 다목적 항목입니다. 공유 일정은 시스템 수준 항목이므로 공유 일정을 만들려면 시스템 수준의 사용 권한이 있어야 합니다. 따라서 일반적으로 보고서 서버 관리자나 내용 관리자는 보고서 서버에서 사용할 수 있는 공유 일정을 만듭니다. 공유 일정은 웹 포털 또는 SharePoint 사이트 설정을 사용하여 보고서 서버에서 저장되고 관리됩니다.  
  
     보고서, 공유 데이터 집합 또는 구독 속성을 통해 정의하는 특정 일정과 달리 공유 일정은 다음과 같은 이유로 인해 더 쉽게 관리 및 유지할 수 있습니다.  
  
    -   공유 일정은 중앙 위치에서 관리할 수 있으므로 예약된 여러 작업이 서로 너무 가까이 함께 실행되거나 서버의 다른 프로세스와 충돌하는 경우 보다 쉽게 일정 속성을 비교하고 빈도 및 되풀이 패턴을 조정할 수 있습니다.  
  
    -   컴퓨팅 환경에서 빠르게 변경 내용을 적용할 수 있습니다. 예를 들어 데이터 웨어하우스를 새로 고친 후 오전 4시에 실행되는 보고서 집합이 있는 경우 데이터 새로 고침 작업이 다시 예약되거나 지연되면 단일 공유 일정에서 해당 일정 정보를 업데이트하여 변경 내용을 쉽게 적용할 수 있습니다.  
  
    -   공유 일정만 사용하는 경우 예약된 작업이 발생하는 시기를 정확하게 알 수 있습니다. 이에 따라 성능 문제가 발생하기 전에 보다 쉽게 서버의 부하를 예상하고 이에 맞는 조정 작업을 수행할 수 있습니다. 예를 들어 특정 시간에 컴퓨터 백업을 예약하기로 결정한 경우 공유 일정이 다른 시간에 실행되도록 조정할 수 있습니다.  
  
-   **보고서별 일정** 은 개별 보고서, 구독 또는 보고서 실행 작업 컨텍스트에서 정의되어 캐시 만료나 스냅숏 업데이트를 결정합니다. 구독을 정의하거나 보고서 실행 속성을 설정할 때 보고서별 일정이 인라인으로 생성됩니다. 공유 일정에서 원하는 빈도나 반복 패턴을 제공하지 않으면 보고서별 일정을 만들 수 있습니다. 보고서 실행을 중지하려면 보고서별 일정을 수동으로 편집해야 합니다. 보고서별 일정은 개별 사용자가 만들 수 있습니다.  
  
##  <a name="bkmk_configuredatasources"></a> 데이터 원본 구성  
 보고서에 대해 데이터 또는 구독 처리를 예약하려면 먼저 저장된 자격 증명이나 무인 모드로 실행되는 보고서 처리 계정을 사용하도록 보고서 데이터 원본을 구성해야 합니다. 저장된 자격 증명을 사용하는 경우 하나의 자격 증명 집합만 저장할 수 있으며 이 자격 증명 집합은 보고서를 실행하는 모든 사용자가 사용합니다. 자격 증명은 Windows 사용자 계정이거나 데이터베이스 사용자 계정일 수 있습니다.  
  
 무인 모드로 실행되는 보고서 처리 계정은 보고서 서버에서 구성되는 특수한 용도의 계정입니다. 이 계정은 예약된 작업에 외부 파일 검색이나 처리가 필요한 경우 보고서 서버가 원격 컴퓨터에 연결하는 데 사용됩니다. 구성할 경우 이 계정을 통해 보고서에 데이터를 제공하는 외부 데이터 원본에 연결할 수 있습니다.  
  
 저장된 자격 증명이나 무인 모드로 실행되는 보고서 처리 계정을 지정하려면 보고서의 데이터 원본 속성을 편집합니다. 보고서에서 공유 데이터 원본을 사용하는 경우에는 대신 공유 데이터 원본을 편집합니다.  
  
##  <a name="bkmk_credentials"></a> 자격 증명 및 처리 계정 저장  
 일정 작업 방법은 역할 할당에 속하는 태스크에 따라 다릅니다. 미리 정의된 역할을 사용하는 경우 내용 관리자 및 시스템 관리자인 사용자가 일정을 만들고 관리할 수 있습니다. 사용자 지정 역할 할당을 사용하는 경우 예약된 작업을 지원하는 태스크가 역할 할당에 포함되어 있어야 합니다.  
  
|수행 작업|포함되는 태스크|기본 모드의 미리 정의된 역할|SharePoint 모드 그룹|  
|----------------|-----------------------|----------------------------------|----------------------------|  
|공유 일정 만들기, 수정 또는 삭제|공유 일정 관리|시스템 관리자|소유자|  
|공유 일정 선택|공유 일정 보기|시스템 사용자|멤버|  
|사용자 정의 구독에서 보고서별 일정 만들기, 수정 또는 삭제|개별 구독 관리|브라우저, 보고서 작성기, 내 보고서, 내용 관리자|방문자, 멤버|  
|예약된 다른 모든 작업의 보고서별 일정 만들기, 수정 또는 삭제|보고서 기록 관리, 모든 구독 관리, 보고서 관리|내용 관리자|소유자|  
  
 기본 모드 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 보안에 대한 자세한 내용은 [미리 정의된 역할](../../reporting-services/security/role-definitions-predefined-roles.md), [기본 모드 보고서 서버에 권한 부여](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md) 및 [태스크 및 권한](../../reporting-services/security/tasks-and-permissions.md)을 참조하세요. SharePoint 모드의 경우 [Reporting Services의 역할 및 태스크와 SharePoint 그룹 및 사용 권한 비교](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)를 참조하세요.  
  
##  <a name="bkmk_how_scheduling_works"></a> 일정 예약 및 배달 프로세스 작동 방식  
 일정 예약 및 배달 프로세서는 다음 기능을 제공합니다.  
  
-   보고서 서버 데이터베이스의 이벤트 및 알림 큐를 유지 관리합니다. 스케일 아웃 배포에서는 배포의 모든 보고서 서버에서 큐가 공유됩니다.  
  
-   보고서 프로세서를 호출하여 보고서를 실행하거나 구독을 처리하거나 캐시된 보고서를 지웁니다. 일정 이벤트의 결과로 발생하는 모든 보고서 처리는 백그라운드 프로세스로 수행됩니다. SharePoint 모드는 타이머 작업을 사용합니다.  
  
-   보고서를 배달할 수 있도록 구독에서 지정되어 있는 배달 확장 프로그램을 호출합니다.  
  
 일정 예약 및 배달 작업의 다른 측면은 일정 예약 및 배달 프로세서와 함께 작동하는 다른 구성 요소 및 서비스에 의해 처리됩니다. 특히 일정 예약 및 배달 프로세서는 보고서 서버 서비스에서 실행되며 SQL Server 에이전트를 타이머로 사용하여 예약된 이벤트를 생성합니다. 다음 단계는 Reporting Services 배포에서 예약된 작업이 작동하는 방식을 설명합니다.  
  
1.  예약된 작업은 사용자가 일정을 만들 때 정의됩니다. 일정에는 보고서 배달을 위한 구독 트리거, 스냅숏 새로 고침 또는 캐시 만료에 사용되는 날짜 및 시간이 정의되어 있습니다.  
  
2.  보고서 서버는 보고서 서버 데이터베이스에 일정 정보를 저장합니다.  
  
3.  보고서 서버가 SQL Server 에이전트에서 제공된 일정 정보가 포함된 해당 작업을 만듭니다. 작업은 보고서 서버 데이터베이스에 대해 열린 기존 연결을 사용하여 저장 프로시저를 통해 생성됩니다.  
  
4.  SQL Server 에이전트는 일정에 지정된 날짜 및 시간에 작업을 실행합니다. 작업이 만드는 이벤트는 Reporting Services가 유지 관리하는 큐에 추가됩니다.  
  
5.  이러한 이벤트로 인해 보고서 또는 구독 처리가 발생합니다. 이벤트는 큐에서 감지될 때 처리되며 보고서는 이에 따라 처리 또는 배달됩니다.  
  
     이벤트가 처리되기 전에 일정 예약 및 배달 프로세서는 인증 단계를 수행하여 보고서를 볼 수 있는 권한이 구독 소유자에게 있는지 확인합니다.  
  
 Reporting Services는 모든 예약된 작업에 대해 이벤트 큐를 관리합니다. 또한 새 이벤트를 확인하기 위해 정기적으로 큐를 폴링합니다. 기본적으로 큐는 10초 간격으로 검색됩니다. RSReportServer.config 파일에서 **PollingInterval**, **IsNotificationService**및 **IsEventService** 구성 설정을 수정하여 간격을 변경할 수 있습니다. SharePoint 모드에서도 이러한 설정에 대해 Rsreporserver.config를 사용하며 모든 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램에 값이 적용됩니다. 자세한 내용은 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)을 참조하세요.  
  
##  <a name="bkmk_serverdependencies"></a> 서버 종속성  
 일정 예약 및 배달 프로세서를 사용하려면 보고서 서버 서비스와 SQL Server 에이전트를 시작해야 합니다. 일정 예약 및 배달 처리 기능은 정책 기반 관리에 있는 **Reporting Services에 대한 노출 영역 구성** 패싯의 **ScheduleEventsAndReportDeliveryEnabled** 속성을 통해 설정해야 합니다. 예약된 작업이 수행되려면 SQL Server 에이전트와 보고서 서버 서비스가 모두 실행 중이어야 합니다.  
  
> [!NOTE]  
>  **Reporting Services에 대한 노출 영역 구성** 패싯을 사용하여 일시적 또는 영구적으로 예약된 작업을 중지할 수 있습니다. 사용자 지정 배달 확장 프로그램을 만들어 배포할 수는 있지만 일정 예약 및 배달 프로세서만 단독으로 확장할 수는 없습니다. 따라서 이벤트 및 알림이 관리되는 방식을 변경할 수 없습니다. 기능 해제에 대한 자세한 내용은 **의 예약된 이벤트 및 배달** [Turn Reporting Services Features On or Off](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md)섹션을 참조하세요.  
  
###  <a name="bkmk_stoppingagent"></a> SQL Server 에이전트를 중지할 때의 결과  
 예약된 보고서 처리는 기본적으로 SQL Server 에이전트를 사용합니다. 이 서비스를 중지하면 <xref:ReportService2010.ReportingService2010.FireEvent%2A> 메서드를 통해 프로그래밍 방식으로 큐에 처리 요청을 추가할 때까지 큐에 새로운 처리 요청이 추가되지 않습니다. 서비스를 다시 시작하면 보고서 처리 요청을 만드는 작업이 다시 시작됩니다. SQL Server 에이전트가 오프라인 상태일 때 보고서 서버는 과거에 발생했을 수 있는 보고서 처리 작업을 다시 만들려고 하지 않습니다. 따라서 1주일 동안 SQL Server 에이전트를 중지하면 해당 주간에 예약된 모든 작업이 손실됩니다.  
  
> [!NOTE]  
>  SQL Server 에이전트가 Reporting Services에 제공하는 기능은 <xref:ReportService2010.ReportingService2010.FireEvent%2A> 메서드를 사용하여 큐에 일정 이벤트를 추가하는 사용자 지정 코드로 대체될 수 있습니다.  
  
###  <a name="bkmk_stoppingservice"></a> 보고서 서버 서비스를 중지할 때의 결과  
 보고서 서버 서비스가 중지되더라도 SQL Server 에이전트는 보고서 처리 요청을 큐에 계속 추가합니다. SQL Server 에이전트의 상태 정보는 작업이 성공적으로 수행되었음을 나타냅니다. 그러나 보고서 서버 서비스가 중지되었으므로 실제로 보고서 처리는 발생하지 않습니다. 요청은 보고서 서버 서비스를 다시 시작할 때까지 큐에 계속 누적됩니다. 보고서 서버 서비스를 다시 시작하면 큐에 있는 모든 보고서 처리 요청이 순서대로 처리됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 기록에서 스냅숏 만들기, 수정 및 삭제](../../reporting-services/report-server/create-modify-and-delete-snapshots-in-report-history.md)   
 [구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [데이터 기반 구독](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [보고서 캐시&#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)   
 [보고서 서버 콘텐츠 관리&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [공유 데이터 집합 캐시&#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)  
  
  
