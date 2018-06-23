---
title: 내 구독 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- subscriptions [Reporting Services], My Subscriptions page
- My Subscriptions page [Reporting Services]
ms.assetid: e96623ba-677e-4748-8787-f32bed3b5c12
caps.latest.revision: 36
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: c1125792543e3a926ddb98e3d33e0f600328d232
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187329"
---
# <a name="use-my-subscriptions"></a>내 구독 사용
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서 관리자에 포함 되어는 **내 구독** 구독을 한 곳에서 모든 구성 하는 페이지입니다. 내 구독을 사용하여 기존 구독을 보고, 수정하고, 삭제할 수 있습니다. 하지만 내 구독을 사용하여 구독을 만들 수는 없습니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 기본 모드|  
  
 내 구독에서 폴더, 보고서, 설명, 트리거, 마지막 실행 또는 상태를 기준으로 구독을 정렬할 수 있습니다. 시간순으로 정렬되는 마지막 실행을 제외하고 모든 값은 사전순으로 정렬됩니다.  
  
 내 구독에는 사용자가 만든 구독만 표시됩니다. 다른 사용자의 구독에 구독자로 추가되더라도 다른 사용자 소유의 구독은 나열되지 않으며 데이터 기반 구독도 표시되지 않습니다.  
  
 구독을 이름별로 검색할 수 없으며 트리거 정보, 상태 정보 등을 기준으로 구독을 검색할 수도 없습니다. 자세한 내용은 참조 [Create, Modify, and 표준 구독 삭제 &#40;Reporting Services 기본 모드에서&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md)합니다.  
  
## <a name="how-to-use-my-subscriptions"></a>내 구독 사용 방법  
 내 구독은 보고서 관리자에서 사용할 수 있습니다. 내 구독에 액세스하려면 보고서 관리자 일반 도구 모음에서 **내 구독** 을 클릭합니다.  
  
## <a name="use-windows-powershell-to-list-mysubscriptions"></a>Windows PowerShell을 사용하여 MySubscriptions 나열  
 ![PowerShell 관련 콘텐츠](../media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠")  
  
 다음 PowerShell 스크립트는 현재 사용자의 구독 목록 및 구독 속성을 반환합니다. 자세한 내용은 [ReportingService2010.ListMySubscriptions 메서드](http://technet.microsoft.com/library/reportservice2010.reportingservice2010.listmysubscriptions.aspx)를 참조하십시오.  
  
```  
#server -  all subscriptions of the current user at the given server or site  
$server="[server name]/reportserver"  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
  
$subscriptions=ListMySubscriptions(ItemPathOrSiteURL)  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status  
#uncomment the following to list all the subscription properties  
#$subscriptions  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터 기반 구독](data-driven-subscriptions.md)   
 [구독 및 배달 &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [기본 모드 보고서 서버 구독 만들기 및 관리](../create-manage-subscriptions-native-mode-report-servers.md)  
  
  