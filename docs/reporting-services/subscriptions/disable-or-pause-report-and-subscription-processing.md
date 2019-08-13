---
title: 보고서 및 구독 처리 해제 또는 일시 중지 | Microsoft Docs
ms.date: 06/19/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- subscriptions [Reporting Services], pausing
- report processing [Reporting Services], pausing
- shared data sources [Reporting Services]
- pausing subscription processing
- pausing report processing
- temporarily stopping report processing
- disabling shared data sources
- roles [Reporting Services], modifying
- shared schedules [Reporting Services], pausing
ms.assetid: 3cf9a240-24cc-46d4-bec6-976f82d8f830
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 228cb40e1c0f40d9525ca83129878d30b722b910
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893420"
---
# <a name="disable-or-pause-report-and-subscription-processing"></a>보고서 및 구독 처리 해제 또는 일시 중지  
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 및 구독 처리를 해제하거나 일시 중지하는 데 사용할 수 있는 몇 가지 방법이 있습니다. 이 문서에는 구독을 해제하는 방법에서부터 데이터 원본 연결을 중단하는 방법이 포함되어 있습니다. 두 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서버 모드에서 모든 방법을 사용할 수 있는 것은 아닙니다. 다음 표에서는 메서드 및 지원 되 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 서버 모드를 요약 합니다.  
  
##  <a name="bkmk_top"></a> 문서 내용  
  
||지원되는 서버 모드|  
|-|---------------------------|  
|[구독 설정 및 해제](#bkmk_disable_subscription)|기본 모드|  
|[공유 일정 일시 중지](#bkmk_pause_schedule)|기본 및 SharePoint 모드|  
|[공유 데이터 원본 해제](#bkmk_disable_shared_datasource)|기본 및 SharePoint 모드|  
|[역할 할당을 수정하여 보고서에 대한 액세스 금지(기본 모드)](#bkmk_modify_role_assignment)|기본 모드|  
|[역할에서 구독 관리 권한 제거(기본 모드)](#bkmk_remove_manage_subscriptions_permission)|기본 모드|  
|[배달 확장 프로그램 해제](#bkmk_disable_extensions)|기본 및 SharePoint 모드|  
  
##  <a name="bkmk_disable_subscription"></a>구독 설정 및 해제  
  
>[!TIP]  
>SQL 2016 Reporting Services의 새로운 *기능을 사용 하도록 설정 하 고 구독을 사용 하지 않도록*설정 합니다. 새로운 사용자 인터페이스 옵션을 통해 신속하게 구독을 설정하고 해제할 수 있습니다. 해제된 구독에는 일정과 같은 다른 구성 속성이 유지되며 손쉽게 설정이 가능합니다. 프로그래밍 방식으로 구독을 설정하고 해제하거나 어떤 구독이 해제되었는지에 대한 감사를 수행할 수 있습니다.  
  
  ![구독 페이지의 사용 및 사용 안 함 단추 ](../../reporting-services/subscriptions/media/disable-or-pause-report-and-subscription-processing/subscription-enable-and-disable-buttons.png)  
  
웹 포털의 **내 구독** 페이지 또는 개별 구독의 **구독** 페이지에서 구독을 찾습니다. 구독을 하나 이상 선택한 후 리본에서 해제 단추 또는 설정 단추 를 클릭합니다(위쪽 이미지 참조). 상태 열은 각각 "Disabled" 또는 "Enabled"로 변경 됩니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]구독을 사용 하거나 사용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 하지 않도록 설정 하는 경우 로그에 행을 기록 합니다. 예를 들어, 보고서 서버 로그 파일에:  
  
 `C:\Program Files\Microsoft SQL Server Reporting Services\SSRS\LogFiles\RSPortal_2019_06_20_00_49_22.log`  
  
 다음과 유사한 행을 볼 수 있습니다.  
  
 `RSPortal!subscription!RSPortal.exe!93!06/20/2019-01:16:47:: i INFO: Subscription 2b409d66-d4ea-408a-918c-0f9e41ce49ca disabled at 06/20/2019 01:16:47`  
  
 `RSPortal!subscription!RSPortal.exe!93!06/20/2019-01:16:51:: i INFO: Subscription 2b409d66-d4ea-408a-918c-0f9e41ce49ca enabled at 06/20/2019 01:16:51`  
  
![PowerShell 관련 콘텐츠](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠"): **Windows PowerShell을 사용하여 단일 구독 해제:** 다음 PowerShell 스크립트를 사용하여 특정 구독을 해제합니다. 스크립트의 서버 이름 및 구독 ID를 업데이트합니다.  
  
```PS  
#disable specific subscription  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptionID = "subscription guid";  
$rs2010.DisableSubscription($subscriptionID);  
  
```  
  
 다음 스크립트를 사용하여 모든 구독의 ID를 나열할 수 있습니다. 서버 이름을 업데이트합니다.  
  
```  
#list all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME /ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
$subscriptions | select subscriptionid, report, status, path  
  
```  
  
 ![PowerShell 관련 콘텐츠](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠") **Windows PowerShell을 사용하여 해제된 구독 모두 나열:** 다음 PowerShell 스크립트를 사용하여 현재 기본 모드 보고서 서버의 해제된 구독을 모두 나열합니다. 서버 이름을 업데이트합니다.  
  
```  
#list all disabled subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://uetestb03/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
Write-Host "--- Disabled Subscriptions ---";  
Write-Host "----------------------------------- ";  
$subscriptions | Where-Object {$_.Active.DisabledByUserSpecified -and $_.Active.DisabledByUser } | select subscriptionid, report, status, lastexecuted,path | format-table -auto  
```  
  
 ![PowerShell 관련 콘텐츠](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠") **Windows PowerShell을 사용하여 해제된 구독 모두 사용:** 다음 PowerShell 스크립트를 사용하여 현재 해제된 구독을 모두 사용합니다. 서버 이름을 업데이트합니다.  
  
```  
#enable all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") | Where-Object {$_.status -eq "disabled" } ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.EnableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
  
```  
  
 ![PowerShell 관련 콘텐츠](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠") **Windows PowerShell을 사용하여 구독 모두 해제:** 다음 PowerShell 스크립트를 사용하여 해제 구독을 **모두** 나열합니다.  
  
```  
#DISABLE all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.DisableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
```  
  
##  <a name="bkmk_pause_schedule"></a> 공유 일정 일시 중지  
 보고서나 구독을 공유 일정에 따라 실행하는 경우 일정을 일시 중지하여 처리를 중단할 수 있습니다. 일정에 따라 진행되는 모든 보고서와 구독 처리는 일정을 다시 시작할 때까지 중단됩니다.  
  
-   **SharePoint 모드:** ![SharePoint 설정](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 설정") **사이트 설정**에서 **공유 일정 관리**를 선택합니다. 일정을 선택하고 **선택한 일정 일시 중지**를 클릭합니다.  
  
-   **기본 모드:** 웹 포털의 웹 포털 화면 위쪽에 있는 ![메뉴 모음](media/ssrs-portal-settings-gear.png) 에서 **설정** 단추 설정 단추를 선택 하 고 드롭다운 메뉴에서 **사이트 설정** 을 선택 합니다. **일정탭을선택하여일정** 페이지를 표시 합니다. 사용 하거나 사용 하지 않도록 설정할 일정 옆의 확인란을 선택 하 고 **사용** 또는 사용 **안** 함 단추를 각각 선택 하 여 원하는 작업을 수행 합니다. 상태 열이 그에 따라 "사용 안 함" 또는 "사용"으로 업데이트 됩니다.  
  
##  <a name="bkmk_disable_shared_datasource"></a> 공유 데이터 원본 해제  
 공유 데이터 원본 사용 시 이점은 보고서나 데이터 기반 구독이 실행되지 않도록 공유 데이터 원본을 해제할 수 있다는 점입니다. 공유 데이터 원본을 해제하면 보고서와 외부 원본의 연결이 끊어집니다. 해제되어 있는 동안에는 데이터 원본을 사용하는 모든 보고서와 구독에서 해당 데이터 원본을 사용할 수 없습니다.  
  
 데이터 원본을 사용할 수 없는 경우에도 보고서는 로드됩니다. 보고서에는 데이터가 포함되지 않지만 적절한 권한이 있는 사용자는 보고서에 연결된 속성 페이지, 보안 설정, 보고서 기록 및 구독 정보에 액세스할 수 있습니다.  
  
-   **SharePoint 모드:** SharePoint 모드 보고서 서버에서 공유 데이터 원본을 해제하려면 데이터 원본을 포함하는 문서 라이브러리로 이동합니다. ![공유 데이터 원본 아이콘](../../reporting-services/report-data/media/hlp-16datasource.png "공유 데이터 원본 아이콘") 데이터 원본을 클릭한 후 **이 데이터 원본 사용** 확인란 선택을 해제합니다.  
  
-   **기본 모드:** 기본 모드 보고서 서버에서 공유 데이터 원본을 해제하려면 웹 포털에서 데이터 원본을 열고 **이 데이터 원본 사용** 확인란의 선택을 취소합니다.  
  
##  <a name="bkmk_modify_role_assignment"></a> 역할 할당을 수정하여 보고서에 대한 액세스 금지(기본 모드)  
보고서를 사용할 수 없도록 하는 한 가지 방법은 보고서에 액세스할 수 있는 권한을 제공하는 역할 할당을 일시적으로 제거하는 것입니다. 이 방법은 데이터 원본 연결이 생성되는 방법에 관계없이 모든 보고서에 사용될 수 있습니다. 이 방법은 다른 보고서나 항목의 작업에 영향을 주지 않고 해당 보고서에만 영향을 줍니다.  
  
 역할 할당을 제거 하려면 웹 포털에서 보고서의 **보안** 페이지를 엽니다. 보고서가 부모 보고서에서 보안 설정을 상속받은 경우 **항목 보안** 대화 상자의 **보안 사용자 지정**과 **확인**을 선택하여 광범위한 액세스를 제공하는 역할 할당은 포함하지 않는 제한적인 보안 정책을 만들 수 있습니다. 예를 들어 Everyone에게 액세스를 제공하는 역할 할당은 제거하고 Administrators와 같은 일부 사용자에게만 액세스를 제공하는 역할 할당은 유지할 수 있습니다.  
  
##  <a name="bkmk_remove_manage_subscriptions_permission"></a> 역할에서 구독 관리 권한 제거(기본 모드)  
 구독을 만들지 못하게 하려면 역할에서 **개별 구독 관리** 태스크의 선택을 취소합니다. 이 태스크를 제거하면 구독 페이지를 사용할 수 없게 됩니다. 이 경우 웹 포털의 내 구독 페이지가 이전에는 구독을 포함했다고 해도 빈 상태로 나타나며, 이는 삭제되지 않습니다. 구독 관련 태스크를 제거하면 사용자는 구독을 생성 및 수정하지 못하지만 기존 구독은 삭제되지 않습니다. 기존 구독은 사용자가 삭제할 때까지 계속 실행됩니다. 권한을 제거하려면:  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다. 
  
2.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버에 연결합니다.  
  
3.  **보안** 노드를 확장합니다.  
  
4.  **역할** 노드를 확장 하 고 원하는 역할을 선택 합니다.  
  
5.  역할을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
6.  **개별 구독 관리** 및 **모든 구독 관리** 태스크의 선택을 취소 합니다.  
  
7.  **확인**을 클릭하여 변경 내용을 적용합니다.

  
##  <a name="bkmk_disable_extensions"></a> 배달 확장 프로그램 해제  
 지정된 보고서에 대한 구독을 만들 수 있는 권한이 있는 사용자는 누구나 보고서 서버에 설치된 모든 배달 확장 프로그램을 사용할 수 있습니다. 다음 배달 확장 프로그램은 사용할 수 있으며 자동으로 구성됩니다.  
  
-   Windows 파일 공유  
  
-   SharePoint 라이브러리(SharePoint 통합 모드 보고서 서버와 통합된 SharePoint 사이트에서만 사용 가능)  
  
 전자 메일 배달을 사용하려면 먼저 구성해야 합니다. 구성하지 않으면 사용할 수 없습니다. 자세한 내용은 [전자 메일 설정-Reporting Services 기본 모드 (Configuration Manager)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)를 참조 하세요.  
  
 특정 확장 프로그램을 해제하려면 **RSReportServer.config** 파일에서 해당 확장 프로그램 항목을 제거합니다. 자세한 내용은 [Reporting Services 구성 파일](../../reporting-services/report-server/reporting-services-configuration-files.md) 및 [전자 메일 설정-Reporting Services 기본 모드 (Configuration Manager)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)를 참조 하세요.  
  
 배달 확장 프로그램을 제거한 후에는 웹 포털이나 SharePoint 사이트에서 더 이상 사용할 수 없습니다. 배달 확장 프로그램을 제거하면 비활성 구독이 생성될 수 있습니다. 확장 프로그램을 제거하기 전에 구독이 다른 배달 확장 프로그램을 사용하도록 구성하거나 구독을 삭제하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Reporting Services 구성 파일](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [웹 포털 구성](../../reporting-services/report-server/configure-web-portal.md)   
 [Reporting Services 보고서 서버&#40;기본 모드&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [보고서 서버의 웹 포털(SSRS 기본 모드)](../../reporting-services/web-portal-ssrs-native-mode.md)   
 [보안 개체 항목](../../reporting-services/security/securable-items.md) 
  
