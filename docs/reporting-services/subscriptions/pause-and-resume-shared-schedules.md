---
title: "공유 일정 일시 중지 및 다시 시작 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pausing schedules
- report-specific schedules [Reporting Services]
- shared schedules [Reporting Services], resuming
- resuming schedules
- continuing schedules
- schedules [Reporting Services], resuming
- schedules [Reporting Services], pausing
ms.assetid: e416be75-5234-4aa6-a3de-77f60f25169a
caps.latest.revision: "36"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 71dcd66394cf96bd6994e40de76b10a519f32a74
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="pause-and-resume-shared-schedules"></a>공유 일정 일시 중지 및 다시 시작
  사용 중인 공유 일정을 일시 중지하고 다시 시작할 수 있습니다. 공유 일정을 일시 중지하여 보고서 처리 및 구독을 트리거하는 데 사용되는 일정을 일시적으로 중지할 수 있습니다. 공유 일정만 일시 중지하고 다시 시작할 수 있습니다. 보고서별 일정은 일시 중지할 수 없습니다.  
  
 진행 중인 보고서의 처리는 일시 중지하고 다시 시작할 수 없습니다. SQL Server 에이전트 서비스의 일정 큐에 있는 일정만 일시 중지하고 다시 시작할 수 있습니다. 처리 중인 작업은 일정 예약 엔진 범위 밖에 있습니다. 자세한 내용은 [실행 중인 프로세스 관리](../../reporting-services/subscriptions/manage-a-running-process.md)를 참조하세요.  
  
 공유 일정이 일시 중지된 동안 수행되었어야 하는 모든 작업은 건너뛸 수 있습니다. 공유 일정을 다시 시작하면 서버의 현지 시간을 사용하여 다음 예약된 시간에 보고서 및 구독 처리가 수행됩니다. 기본 모드 보고서 서버 또는 SharePoint 서비스 응용 프로그램은 일정을 일시 중지하지 않았으면 수행되었을 예약된 작업을 만회하려고 하지 않습니다.  
  
 항목 내용  
  
-   [공유 일정 일시 중지 및 다시 시작(기본 모드)](#bkmk_native)  
  
-   [공유 일정 일시 중지 및 다시 시작(SharePoint 모드)](#bkmk_sharepoint)  
  
##  <a name="bkmk_native"></a> 공유 일정 일시 중지 및 다시 시작(기본 모드)  
 공유 일정을 일시 중지하고 다시 시작하려면 보고서 관리자에서 일정 페이지를 사용합니다. 여기에는 일정을 일시 중지하고 다시 시작하는 옵션이 없으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 사용할 수 없습니다. 자세한 내용은 [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)을 참조하세요.  
  
#### <a name="to-pause-or-resume-a-shared-schedule"></a>공유 일정을 일시 중지 또는 다시 시작하려면  
  
1.  보고서 관리자에서 **사이트 설정**을 클릭합니다.  
  
2.  **일정**을 클릭합니다.  
  
3.  일정을 선택하고 리본에서 **일시 중지** 를 클릭하거나 **재개** 를 클릭합니다. 일정이 현재 일시 중지된 경우 **상태** 열에 **일시 중지됨**이 포함됩니다.  
  
##  <a name="bkmk_sharepoint"></a> 공유 일정 일시 중지 및 다시 시작(SharePoint 모드)  
 공유 일정을 일시 중지하고 재개하려면 사이트 설정 페이지 또는 PowerShell을 사용합니다. 일정은 SharePoint 사이트에 따라 관리됩니다.  
  
#### <a name="to-pause-or-resume-a-shared-schedule"></a>공유 일정을 일시 중지 또는 다시 시작하려면  
  
1.  **사이트 작업**을 클릭합니다.  
  
2.  **사이트 설정**을 클릭합니다.  
  
3.  Reporting Services 섹션에서 **공유 일정 관리**를 클릭합니다.  
  
4.  일정을 선택하고 **선택한 일정 일시 중지** 또는 **선택한 일정 실행**을 클릭합니다. 일정이 현재 일시 중지된 경우 **상태** 열에 **일시 중지됨**이 포함됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [일정](../../reporting-services/subscriptions/schedules.md)   
 [일정 만들기, 수정 및 삭제](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [보고서 서버에서 표준 시간대 및 시계 설정 변경](../../reporting-services/subscriptions/change-time-zones-and-clock-settings-on-a-report-server.md)   
 [실행 중인 프로세스 관리](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
  
