---
title: 기본 모드 보고서 서버 구독 만들기 및 관리 | Microsoft Docs
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
- subscriptions [Reporting Services], managing
ms.assetid: 7f46cbdb-5102-4941-bca2-5e0ff9012c6b
caps.latest.revision: 37
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 56fb4e61fe7e442247fb9977afc440f13e5276e6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37186180"
---
# <a name="create-and-manage-subscriptions-for-native-mode-report-servers"></a>기본 모드 보고서 서버 구독 만들기 및 관리
  이 섹션에는 구독 처리, 감독 및 제어 항목이 포함되어 있습니다. 표준 구독인지 데이터 기반 구독인지에 따라 구독 관리가 달라집니다. 표준 구독은 일반적으로 사용자가 소유하고 관리합니다. 반대로 데이터 기반 구독은 보고서 서버 관리자가 만들어 유지 관리합니다.  
  
 구독 및 배달 기능은 기본적으로 사용할 수 있습니다. 전자 메일 배달을 사용하려면 먼저 구성해야 합니다. 기본 배달 확장 프로그램에는 보고서 서버 전자 메일 및 파일 공유 배달이 포함되어 있습니다. 사용자 지정 배달 확장 프로그램을 만들거나 설치하지 않는 한 기본 모드 보고서 서버에서 구독에 사용할 수 있는 배포 방법은 이러한 기본 배달 확장 프로그램뿐입니다.  
  
## <a name="permissions-for-subscribing-to-reports-on-a-native-mode-report-server"></a>기본 모드 보고서 서버의 보고서 구독 권한  
 역할을 사용하는 방법에 따라 역할별로 구독 태스크를 설정 또는 해제하여 선택한 사용자 그룹에 구독 기능을 제공할 수 있습니다. 사용자는 다음 두 태스크를 통해 구독 기능을 사용할 수 있습니다.  
  
-   "개별 구독 관리" 태스크를 사용하면 특정 보고서에 대한 구독을 생성, 수정 및 삭제할 수 있습니다. 미리 정의된 역할에서 이 태스크는 브라우저 및 보고서 작성기 역할의 일부입니다. 사용자는 이 태스크를 포함하는 역할 할당을 사용하여 자신이 만든 구독만 관리할 수 있습니다.  
  
-   "모든 구독 관리" 태스크를 사용하면 모든 구독을 액세스 및 수정할 수 있습니다. 이 태스크는 데이터 기반 구독을 만드는 데 필요합니다. 미리 정의된 역할에서 내용 관리자 역할에만 이 태스크가 포함됩니다.  
  
## <a name="disabling-subscriptions"></a>구독 해제  
 구독을 만들지 못하게 하려면 역할에서 "개별 구독 관리" 태스크의 선택을 취소합니다. 이 태스크를 제거하면 구독 페이지를 사용할 수 없게 됩니다. 이 경우 보고서 관리자의 내 구독 페이지가 이전에는 구독을 포함했다고 해도 빈 상태로 나타나며, 이는 삭제되지 않습니다. 구독 관련 태스크를 제거하면 사용자는 구독을 생성 및 수정하지 못하지만 기존 구독은 삭제되지 않습니다. 기존 구독은 사용자가 삭제할 때까지 계속 실행됩니다. 구독을 삭제 하는 방법에 대 한 자세한 내용은 참조 하세요. [Create, Modify, and 표준 구독 삭제 &#40;기본 모드의 Reporting Services&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)합니다.  
  
 보고서 서버에서 처리 중인 구독을 사용 하지 않으려면 설정할 수 있습니다 합니다 `ScheduleEventsAndReportDeliveryEnabled` 속성을 `False` 에 **Reporting Services에 대 한 노출 영역 구성** 패싯 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 정책 기반 관리 합니다. 이렇게 하면 예약된 모든 작업이 실행되지 않습니다. 보고서 서버에서 처리 중인 구독만 해제할 수는 없습니다.  
  
 보고서 서버에서 처리 중인 구독을 취소 하는 방법에 지침은 [실행 중인 프로세스 관리](subscriptions/manage-a-running-process.md)합니다.  
  
## <a name="disabling-delivery-extensions"></a>배달 확장 프로그램 해제  
 지정된 보고서에 대한 구독을 만들 수 있는 권한이 있는 사용자는 누구나 보고서 서버에 설치된 모든 배달 확장 프로그램을 사용할 수 있습니다. 다음 배달 확장 프로그램은 사용할 수 있으며 자동으로 구성됩니다.  
  
-   Windows 파일 공유  
  
-   SharePoint 라이브러리(SharePoint 통합 모드 보고서 서버와 통합된 SharePoint 사이트에서만 사용 가능)  
  
 전자 메일 배달을 사용하려면 먼저 구성해야 합니다. 구성하지 않으면 사용할 수 없습니다. 자세한 내용은 [전자 메일 배달을 위한 보고서 서버 구성 &#40;SSRS 구성 관리자&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)합니다.  
  
 특정 확장 프로그램을 해제하려면 RSReportServer.config 파일에서 해당 확장 프로그램 항목을 제거합니다. 자세한 내용은 [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md) 하 고 [전자 메일 배달을 위한 보고서 서버를 구성 &#40;&AMP;#40;SSRS 구성 관리자&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 배달 확장 프로그램을 제거한 후에는 보고서 관리자나 SharePoint 사이트에서 더 이상 사용할 수 없습니다. 배달 확장 프로그램을 제거하면 비활성 구독이 생성될 수 있습니다. 확장 프로그램을 제거하기 전에 구독이 다른 배달 확장 프로그램을 사용하도록 구성하거나 구독을 삭제하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
 [내 구독 사용](subscriptions/use-my-subscriptions-native-mode-report-server.md)  
 내 구독 페이지를 사용하여 자신이 소유한 구독을 관리하는 방법을 설명합니다.  
  
 [보고서 및 구독 처리 일시 중지](subscriptions/disable-or-pause-report-and-subscription-processing.md)  
 역할 할당 사용 또는 보고서 서버 리소스 비활성화와 같은 보고서 처리를 일시 중지하기 위한 여러 가지 방법을 설명합니다.  
  
 [보고서 배포 제어](../../2014/reporting-services/control-report-distribution.md)  
 보고서 배포를 제어하는 데 사용할 수 있는 구성 설정 및 배달 옵션을 설명합니다.  
  
 [Reporting Services 구독 모니터링](subscriptions/monitor-reporting-services-subscriptions.md)  
 구독의 성공 여부를 확인하는 방법과 보고서 변경이 기존 구독에 미치는 영향을 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [만들기, 수정 및 표준 구독을 삭제 &#40;기본 모드의 Reporting Services&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
  
