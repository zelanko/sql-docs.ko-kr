---
title: 내 구독 사용(기본 모드 보고서 서버) | Microsoft Docs
description: Reporting Services 웹 포털의 내 구독 페이지를 사용하여 기존 구독을 확인, 수정, 사용하지 않도록 설정 또는 삭제하는 방법을 알아봅니다.
ms.date: 07/01/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], My Subscriptions page
- My Subscriptions page [Reporting Services]
ms.assetid: e96623ba-677e-4748-8787-f32bed3b5c12
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 964e6752dc44477215180e6e61f6440feb8972af
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939418"
---
# <a name="use-my-subscriptions-native-mode-report-server"></a>내 구독 사용(기본 모드 보고서 서버)
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털에는 하나의 위치에서 모든 구독을 구성하는 **내 구독** 페이지가 포함되어 있습니다. *내 구독* 을 사용하여 기존 구독을 보고, 수정하고, 삭제할 수 있습니다. 하지만 내 구독을 사용하여 구독을 만들 수는 없습니다.  내 구독에는 사용자가 만든 구독만 표시됩니다. 다른 사용자의 구독에 구독자로 추가되더라도 다른 사용자 소유의 구독은 나열되지 않으며 데이터 기반 구독도 표시되지 않습니다.
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드|  
  
구독을 이름별로 검색할 수 없으며 트리거 정보, 상태 정보 등을 기준으로 검색할 수도 없으므로 검색 필드에서는 구독 목록을 동적으로 필터링합니다. 자세한 내용은 [기본 모드 보고서 서버 구독 만들기 및 관리](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)를 참조하세요.
  
## <a name="to-open-the-my-subscriptions-page"></a>내 구독 페이지를 열려면  
1. [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 웹 포털을 엽니다.
2. 도구 모음에서 설정 ![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png) 를 클릭합니다.
3. **내 구독**을 클릭합니다.

자세한 내용은 [Web portal (SSRS Native Mode)](../../reporting-services/web-portal-ssrs-native-mode.md)을 참조하세요.

## <a name="use-windows-powershell-to-list-mysubscriptions"></a>Windows PowerShell을 사용하여 MySubscriptions 나열  
 ![PowerShell 관련 콘텐츠](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠")  
  
 다음 PowerShell 스크립트는 현재 사용자의 구독 목록 및 구독 속성을 반환합니다. 자세한 내용은 [ReportingService2010.ListMySubscriptions 메서드](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.listmysubscriptions.aspx)를 참조하십시오.  
  
```  
#server -  all subscriptions of the current user at the given server or site  
$server="[server name]/reportserver"  
$rs2010 = New-WebServiceProxy -Uri "https://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
  
$subscriptions=ListMySubscriptions(ItemPathOrSiteURL)  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status  
#uncomment the following to list all the subscription properties  
#$subscriptions

```  
  
## <a name="see-also"></a>참고 항목  
 [Data-Driven Subscriptions](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [기존_기본 모드 보고서 서버 구독 만들기 및 관리](https://docs.microsoft.com/sql/reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers)  
  
  
