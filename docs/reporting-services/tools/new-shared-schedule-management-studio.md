---
title: "새 공유 일정(Management Studio) | Microsoft Docs"
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
f1_keywords: sql13.swb.reportserver.newschedule.f1
ms.assetid: b2c69586-d98e-4933-827d-f5e6c15c5203
caps.latest.revision: "32"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 37e0b1a6b2e64de4d63456050b094113e288c434
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="new-shared-schedule-management-studio"></a>새 공유 일정(Management Studio)
  이 페이지를 사용하여 게시된 보고서 및 구독의 공유 일정을 만들 수 있습니다. 보고서별 일정 또는 구독별 일정 대신 공유 일정을 사용할 수 있습니다. 공유 일정이 항목별 일정과 구분되는 두 가지 주요 기능은 중앙화된 일정 정보, 그리고 예약된 작업을 일시 중지했다가 재개하는 기능입니다.  
  
 일부 빈도 조합은 단일 일정으로 지원되지 않습니다. 예를 들어 매주 금요일 오후 12시와 4시에 보고서를 실행하려면 실행 날짜가 금요일, 시작 시간이 오후 12시와 4시로 지정된 두 개의 일별 일정을 만들어야 합니다.  
  
 일정 처리는 일정을 호스팅하고 처리하는 보고서 서버의 현지 시간을 기준으로 합니다.  
  
 이 페이지를 열려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 시작하고 보고서 서버에 연결한 다음 **공유 일정**을 마우스 오른쪽 단추로 클릭하고 **새 일정**을 선택합니다. 일정을 저장하려면 SQL Server 에이전트 서비스가 실행 중이어야 합니다.  
  
> [!NOTE]  
>  이 기능은 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서는 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원하는 기능 목록은 [SQL Server 2012 버전에서 지원하는 기능](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **이름**  
 공유 일정의 이름을 입력합니다. 이 이름은 사용자가 보고서 및 구독에 대한 공유 일정을 선택할 때 드롭다운 목록에 나타납니다. 공유 일정의 이름은 목록에 넣기에 적합한 길이로, 알아보기 쉽고 서로 구분이 잘 되도록 지정하십시오. 이름은 하나 이상의 영숫자 문자를 포함해야 합니다. 공백과 특정 기호도 포함할 수 있습니다. 이름 지정 시에는 다음 문자를 사용하지 마십시오.  
  
 ; ? : @ & = + , $ / * < >  
  
 " /  
  
 **일정 시작 날짜**  
 이 일정의 시작 날짜를 지정합니다.  
  
 **일정 종료 날짜**  
 이 일정의 만료 날짜를 지정합니다.  
  
 **형식**  
 되풀이 패턴의 기준을 시간, 일, 주 또는 월로 지정합니다.  
  
 **시(되풀이 패턴)**  
 시간 간격으로 예약된 작업을 실행하려면(예: 6시간마다 보고서 실행) 이 옵션을 선택합니다. 시간 및 분 단위로 간격을 지정할 수 있습니다.  
  
 **일(되풀이 패턴)**  
 일 간격으로 예약된 작업을 실행하려면(예: 이틀마다 보고서 실행) 이 옵션을 선택합니다. 일, 시간 및 분 단위로 간격을 지정하여 일정을 실행시킬 수 있습니다.  
  
 **주(되풀이 패턴)**  
 주 간격으로 예약된 작업을 실행하려는 경우 또는 반복할 패턴이 주를 기반으로 하는 경우(예: 격주로 보고서 실행) 이 옵션을 선택합니다. 주별 일정을 일, 시간 및 분 단위로 지정하여 실행시킬 수 있습니다.  
  
 **월(되풀이 패턴)**  
 월 간격으로 예약된 작업을 실행하려는 경우 또는 반복할 패턴이 월을 기반으로 하는 경우 이 옵션을 선택합니다. 월별 일정을 일, 시간 및 분 단위로 지정하여 실행시킬 수 있습니다. 일정에서 특정 월을 생략할 수 있습니다.  
  
 **한 번**  
 특정 날짜 및 시간에 한 번만 실행되는 일정을 만들려면 이 옵션을 선택합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Management Studio의 보고서 서버 F1 도움말](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Management Studio에서 보고서 서버에 연결](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [일정 만들기, 수정 및 삭제](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [일정](../../reporting-services/subscriptions/schedules.md)   
 [Management Studio의 보고서 서버 F1 도움말](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
