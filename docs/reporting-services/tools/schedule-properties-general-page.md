---
title: 일정 속성(일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/11/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: tools
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.scheduleproperties.general.f1
ms.assetid: 20e43966-6caf-4972-a2e2-0d9131ac8f51
caps.latest.revision: 36
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 66857465ab7e083c1f5a67f1ab6b27f6175f3c37
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="schedule-properties-general-page"></a>일정 속성(일반 페이지)
  [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 의 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 페이지를 사용하여 공유 일정을 보거나 수정할 수 있습니다. 보고서별 일정 또는 구독별 일정 대신 공유 일정을 사용할 수 있습니다. 일정에 대한 변경 내용은 일정을 저장한 후에 적용됩니다. 일정을 편집해도 현재 진행 중인 작업은 영향을 받지 않습니다. 사용 중인 일정을 편집할 경우 해당 일정에서 트리거된 현재 처리 중인 모든 보고서 및 구독을 완료할 수 있습니다.  
  
 일부 빈도 조합은 단일 일정으로 지원되지 않습니다. 예를 들어 매주 금요일 오후 12시와 4시에 보고서를 실행하려면 실행 날짜가 금요일, 시작 시간이 오후 12시와 4시로 지정된 두 개의 일별 일정을 만들어야 합니다.  
  
 일정 처리는 일정을 호스팅하고 처리하는 보고서 서버의 현지 시간을 기준으로 합니다.  
  
 이 페이지를 열려면
 1) [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 시작합니다.
 2) 보고서 서버에 연결합니다.
 3) **공유 일정** 폴더를 확장합니다.
 4) 공유 일정을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
> [!NOTE]  
>이 기능은 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서는 사용할 수 없으며 이 페이지는 이 기능이 포함되지 않은 버전을 실행할 경우 표시되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **이름**  
 공유 일정의 이름을 지정합니다.  
  
 **일정 시작 날짜**  
 이 일정의 시작 날짜를 지정합니다.  
  
 **일정 종료 날짜**  
 이 일정의 만료 날짜를 지정합니다.  
  
 **형식**  
 되풀이 패턴의 기준을 시간, 일, 주 또는 월로 지정하거나 한 번만 실행되도록 지정합니다.  
  
 **시(되풀이 패턴)**  
 시간 간격으로 예약된 작업을 실행하려면(예: 6시간마다 보고서 실행) 이 옵션을 지정합니다. 시간 및 분 단위로 간격을 지정할 수 있습니다.  
  
 **일(되풀이 패턴)**  
 일 간격으로 예약된 작업을 실행하려면(예: 이틀마다 보고서 실행) 이 옵션을 지정합니다. 일, 시간 및 분 단위로 간격을 지정하여 일정을 실행시킬 수 있습니다.  
  
 **주(되풀이 패턴)**  
 주 간격으로 예약된 작업을 실행하려는 경우 또는 반복할 패턴이 주를 기반으로 하는 경우(예: 격주로 보고서 실행) 이 옵션을 지정합니다. 주별 일정을 일, 시간 및 분 단위로 지정하여 실행시킬 수 있습니다.  
  
 **월(되풀이 패턴)**  
 월 간격으로 예약된 작업을 실행하려는 경우 또는 반복할 패턴이 월을 기반으로 하는 경우 이 옵션을 지정합니다. 월별 일정을 일, 시간 및 분 단위로 지정하여 실행시킬 수 있습니다. 일정에서 특정 월을 생략할 수 있습니다.  
  
 **한 번**  
 특정 날짜 및 시간에 한 번만 실행되는 일정을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Management Studio의 보고서 서버 F1 도움말](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Management Studio에서 보고서 서버에 연결](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [일정 만들기, 수정 및 삭제](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [일정](../../reporting-services/subscriptions/schedules.md)  
  
  

