---
title: "구독 소유자를 관리 하 고 구독-PowerShell 실행 | Microsoft Docs"
ms.custom: 
ms.date: 03/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0fa6cb36-68fc-4fb8-b1dc-ae4f12bf6ff0
caps.latest.revision: 21
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 103cb28ac4917370c8f116b8de46a27f159261cc
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="manage-subscription-owners-and-run-subscription---powershell"></a>구독 소유자를 관리 하 고 구독-PowerShell 실행
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 부터 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독 소유권을 프로그래밍 방식으로 한 사용자에서 다른 사용자에게 전송할 수 있습니다. 이 항목에서는 구독 소유권을 변경하거나 단순히 나열할 수 있는 여러 가지 Windows PowerShell 스크립트를 제공합니다. 각 샘플에는 기본 모드 및 SharePoint 모드에 대한 샘플 구문이 포함됩니다. 구독 소유자를 변경한 후 구독은 새 소유자의 보안 컨텍스트에서 실행되고, 보고서의 User!UserID 필드에 새 소유자 값이 표시됩니다. PowerShell 샘플의 개체 모델에 대한 자세한 내용은 <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 ![PowerShell 관련 내용](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 관련 내용")  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드|  
  
##  <a name="bkmk_top"></a> 항목 내용  
  
-   [스크립트 사용 방법](#bkmk_how_to)  
  
-   [스크립트: 모든 구독의 소유권 나열](#bkmk_list_ownership_all)  
  
-   [스크립트: 특정 사용자가 소유하는 모든 구독 나열](#bkmk_list_all_one_user)  
  
-   [스크립트: 특정 소유자가 소유하는 모든 구독의 소유권 변경](#bkmk_change_all)  
  
-   [스크립트: 특정 보고서와 연결된 모든 구독 나열](#bkmk_list_for_1_report)  
  
-   [스크립트: 특정 구독의 소유권 변경](#bkmk_change_all_1_subscription)  
  
-   [스크립트: 단일 구독 실행](#bkmk_run_1_subscription)  
  
##  <a name="bkmk_how_to"></a> 스크립트 사용 방법  
  
### <a name="permissions"></a>Permissions  
 이 섹션에서는 기본 모드와 SharePoint 모드 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 각 메서드를 사용하기 위해 필요한 권한 수준을 요약합니다. 이 항목의 스크립트는 다음 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 메서드를 사용합니다.  
  
-   [ReportingService2010.ListSubscriptions 메서드](http://msdn.microsoft.com/library/reportservice2010.reportingservice2010.listsubscriptions.aspx)  
  
-   [ReportingService2010.ChangeSubscriptionOwner 메서드](http://msdn.microsoft.com/library/reportservice2010.reportingservice2010.changesubscriptionowner.aspx)  
  
-   [ReportingService2010.ListChildren](http://msdn.microsoft.com/library/reportservice2010.reportingservice2010.listchildren.aspx)  
  
-   [ReportingService2010.FireEvent](http://msdn.microsoft.com/library/reportservice2010.reportingservice2010.fireevent.aspx) 메서드는 실행하는 특정 구독을 트리거하기 위해 마지막 스크립트에서만 사용됩니다. 해당 스크립트를 사용하지 않으려면 FireEvent 메서드에 대한 권한 요구 사항을 무시할 수 있습니다.  
  
 **기본 모드:**  
  
-   구독 나열: [보고서의 ReportOperation 열거형](http://msdn.microsoft.com/library/microsoft.reportingservices.interfaces.reportoperation.aspx) 및 사용자는 구독 소유자임) 또는 ReadAnySubscription  
  
-   구독 변경: 사용자는 BUILTIN\Administrators 그룹의 구성원이어야 합니다.  
  
-   자식 나열: 항목의 ReadProperties  
  
-   이벤트 발생: GenerateEvents (System)  
  
 **SharePoint 모드:**  
  
-   구독 나열: ManageAlerts 또는 [보고서의 CreateAlerts](http://msdn.microsoft.com/library/microsoft.sharepoint.spbasepermissions.aspx) 및 사용자는 구독 소유자이며 구독은 정기 구독임)  
  
-   구독 변경: ManageWeb  
  
-   자식 나열: ViewListItems  
  
-   이벤트 발생: ManageWeb  
  
 자세한 내용은 [Reporting Services의 역할 및 작업과 SharePoint 그룹 및 사용 권한 비교](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)를 참조하세요.  
  
### <a name="script-usage"></a>스크립트 사용자  
 **스크립트 파일(.ps1) 만들기**  
  
1.  이름이 **c:\scripts**인 폴더를 만듭니다. 다른 폴더를 선택하는 경우 예제 명령줄 구문에 사용된 폴더 이름을 수정합니다.  
  
2.  각 스크립트의 텍스트 파일을 만들고 c:\scripts 폴더에 파일을 저장합니다. .ps1 파일을 만들 때 각 예제 명령줄 구문의 이름을 사용합니다.  
  
3.  관리 권한으로 명령 프롬프트를 엽니다.  
  
4.  각 예제에 제공된 샘플 명령줄 구문을 사용하여 각 스크립트 파일을 실행합니다.  
  
 **테스트 완료된 환경**  
  
 이 항목의 스크립트는 PowerShell 버전 3 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 다음 버전에서 테스트되었습니다.  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
##  <a name="bkmk_list_ownership_all"></a> 스크립트: 모든 구독의 소유권 나열  
 이 스크립트는 사이트의 모든 구독을 나열합니다. 이 스크립트를 사용하여 연결을 테스트하거나 다른 스크립트에서 사용하는 보고서 경로 및 구독 ID를 확인할 수 있습니다. 또한 어떤 구독이 존재하며 누가 소유하는지 간단하게 감사할 수 있는 유용한 스크립트입니다.  
  
 **기본 모드 구문:**  
  
```  
powershell c:\scripts\ListAll_SSRS_Subscriptions.ps1 "[server]/reportserver" "/"  
```  
  
 **SharePoint 모드 구문:**  
  
```  
powershell c:\scripts\ListAll_SSRS_Subscriptions.ps1 "[server]/_vti_bin/reportserver" "http://[server]"  
```  
  
 **스크립트:**  
  
```  
# Parameters  
#    server   - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
  
Param(  
    [string]$server,  
    [string]$site  
   )  
  
$rs2010 += New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site); # use "/" for default native mode site  
  
Write-Host " "  
Write-Host "----- $server's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted, Status  
```  
  
> [!TIP]  
>  SharePoint 모드에서 사이트 URL을 확인하려면 SharePoint cmdlet **Get-SPSite**를 사용합니다. 자세한 내용은 [Get-SPSite](http://msdn.microsoft.com/library/ff607950&#40;v=office.15&#41;.aspx)를 참조하세요.  
  
##  <a name="bkmk_list_all_one_user"></a> 스크립트: 특정 사용자가 소유하는 모든 구독 나열  
 이 스크립트는 특정 사용자가 소유하는 모든 구독을 나열합니다. 이 스크립트를 사용하여 연결을 테스트하거나 다른 스크립트에서 사용하는 보고서 경로 및 구독 ID를 확인할 수 있습니다. 이 스크립트는 조직의 누군가가 떠나고 이들이 소유하고 있던 구독을 확인하여 소유자를 변경하거나 구독을 삭제하려고 할 때 유용합니다.  
  
 **기본 모드 구문:**  
  
```  
powershell c:\scripts\ListAll_SSRS_Subscriptions4User.ps1 "[Domain]\[user]" "[server]/reportserver" "/"  
```  
  
 **SharePoint 모드 구문:**  
  
```  
powershell c:\scripts\ListAll_SSRS_Subscriptions4User.ps1 "[Domain]\[user]"  "[server]/_vti_bin/reportserver" "http://[server]"  
```  
  
 **스크립트:**  
  
```  
# Parameters:  
#    currentOwner - DOMAIN\USER that owns the subscriptions you wish to change  
#    server        - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site        - use "/" for default native mode site  
Param(  
    [string]$currentOwner,  
    [string]$server,  
    [string]$site  
)  
  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site);  
  
Write-Host " "  
Write-Host " "  
Write-Host "----- $currentOwner's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status | where {$_.owner -eq $currentOwner}  
```  
  
##  <a name="bkmk_change_all"></a> 스크립트: 특정 소유자가 소유하는 모든 구독의 소유권 변경  
 이 스크립트는 특정 소유자가 소유하는 모든 구독의 소유권을 새 소유자 매개 변수로 변경합니다.  
  
 **기본 모드 구문:**  
  
```  
powershell c:\scripts\ChangeALL_SSRS_SubscriptionOwner.ps1 "[Domain]\current owner]" "[Domain]\[new owner]" "[server]/reportserver"  
```  
  
 **SharePoint 모드 구문:**  
  
```  
powershell c:\scripts\ChangeALL_SSRS_SubscriptionOwner.ps1 "[Domain]\{current owner]" "[Domain]\[new owner]" "[server]/_vti_bin/reportserver"  
```  
  
 **스크립트:**  
  
```  
# Parameters:  
#    currentOwner - DOMAIN\USER that owns the subscriptions you wish to change  
#    newOwner      - DOMAIN\USER that will own the subscriptions you wish to change  
#    server        - server and instance name (e.g. myserver/reportserver, myserver/reportserver_db2, myserver/_vti_bin/reportserver)  
  
Param(  
    [string]$currentOwner,  
    [string]$newOwner,  
    [string]$server  
)  
  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$items = $rs2010.ListChildren("/", $true);  
  
$subscriptions = @();  
  
ForEach ($item in $items)  
{  
    if ($item.TypeName -eq "Report")  
    {  
        $curRepSubs = $rs2010.ListSubscriptions($item.Path);  
        ForEach ($curRepSub in $curRepSubs)  
        {  
            if ($curRepSub.Owner -eq $previousOwner)  
            {  
                $subscriptions += $curRepSub;  
            }  
        }  
    }  
}  
  
Write-Host " "  
Write-Host " "  
Write-Host -foregroundcolor "green" "-----  $currentOwner's Subscriptions changing ownership to $newOwner : "  
$subscriptions | select SubscriptionID, Owner, Path, Description,  Status  | format-table -AutoSize  
  
ForEach ($sub in $subscriptions)  
{  
    $rs2010.ChangeSubscriptionOwner($sub.SubscriptionID, $newOwner);  
}  
  
$subs2 = @();  
  
ForEach ($item in $items)  
{  
    if ($item.TypeName -eq "Report")  
    {  
        $subs2 += $rs2010.ListSubscriptions($item.Path);  
    }  
}  
```  
  
##  <a name="bkmk_list_for_1_report"></a> 스크립트: 특정 보고서와 연결된 모든 구독 나열  
 이 스크립트는 특정 보고서와 연결된 모든 구독을 나열합니다. 보고서 경로 구문은 전체 URL이 필요한 다른 SharePoint 모드입니다. 구문 예제에서 사용된 보고서 이름은 “title only”이며 공백을 포함하고 있으므로 보고서 이름을 작은따옴표로 묶어야 합니다.  
  
 **기본 모드 구문:**  
  
```  
powershell c:\scripts\List_SSRS_One_Reports_Subscriptions.ps1 "[server]/reportserver" "'/reports/title only'" "/"  
```  
  
 **SharePoint 모드 구문:**  
  
```  
powershell c:\scripts\List_SSRS_One_Reports_Subscriptions.ps1 "[server]/_vti_bin/reportserver"  "'http://[server]/shared documents/title only.rdl'" "http://[server]"  
```  
  
 **스크립트:**  
  
```  
# Parameters:  
#    server      - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    reportpath  - path to report in the report server, including report name e.g. /reports/test report >> pass in  "'/reports/title only'"  
#    site        - use "/" for default native mode site  
Param  
(  
      [string]$server,  
      [string]$reportpath,  
      [string]$site  
)  
  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site);  
  
Write-Host " "  
Write-Host " "  
Write-Host "----- $reportpath 's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status | where {$_.path -eq $reportpath}  
```  
  
##  <a name="bkmk_change_all_1_subscription"></a> 스크립트: 특정 구독의 소유권 변경  
 이 스크립트는 특정 구독의 소유권을 변경합니다. 구독은 스크립트에 전달하는 SubscriptionID로 식별됩니다. 구독 나열 스크립트 중 하나를 사용하여 올바른 SubscriptionID를 확인할 수 있습니다.  
  
 **기본 모드 구문:**  
  
```  
powershell c:\scripts\Change_SSRS_Owner_One_Subscription.ps1 "[Domain]\[new owner]" "[server]/reportserver" "/" "ac5637a1-9982-4d89-9d69-a72a9c3b3150"  
```  
  
 **SharePoint 모드 구문:**  
  
```  
powershell c:\scripts\Change_SSRS_Owner_One_Subscription.ps1 "[Domain]\[new owner]" "[server]/_vti_bin/reportserver" "http://[server]" "9660674b-f020-453f-b1e3-d9ba37624519"  
```  
  
 **스크립트:**  
  
```  
# Parameters:  
#    newOwner       - DOMAIN\USER that will own the subscriptions you wish to change  
#    server         - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site        - use "/" for default native mode site  
#    subscriptionID - guid for the single subscription to change  
  
Param(  
    [string]$newOwner,  
    [string]$server,  
    [string]$site,  
    [string]$subscriptionid  
   )  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
  
$subscription += $rs2010.ListSubscriptions($site) | where {$_.SubscriptionID -eq $subscriptionid};  
  
Write-Host " "  
Write-Host "----- $subscriptionid's Subscription properties: "  
$subscription | select Path, report, Description, SubscriptionID, Owner, Status  
  
$rs2010.ChangeSubscriptionOwner($subscription.SubscriptionID, $newOwner)  
  
#refresh the list  
$subscription = $rs2010.ListSubscriptions($site) | where {$_.SubscriptionID -eq $subscriptionid}; # use "/" for default native mode site  
Write-Host "----- $subscriptionid's Subscription properties: "  
$subscription | select Path, report, Description, SubscriptionID, Owner, Status  
```  
  
##  <a name="bkmk_run_1_subscription"></a> 스크립트: 단일 구독 실행  
 이 스크립트는 FireEvent 메서드를 사용하여 특정 구독을 실행합니다. 이 스크립트는 구독에 구성된 일정에 상관없이 구독을 즉시 실행합니다. EventType은 보고서 서버 구성 파일 **rsreportserver.config** 에 정의된 알려진 이벤트 집합과 일치합니다. 이 스크립트는 표준 구독에 대해 다음 이벤트 유형을 사용합니다.  
  
 `<Event>`  
  
 `<Type>TimedSubscription</Type>`  
  
 `</Event>`  
  
 구성 파일에 대한 자세한 내용은 [RsReportServer.config Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)을 참조하세요.  
  
 스크립트에는 지연 논리 “`Start-Sleep -s 6`”이 포함되어 있으므로, 업데이트된 상태가 ListSubscription 메서드를 통해 사용 가능할 수 있도록 이벤트 발생 후 시간이 있습니다.  
  
 **기본 모드 구문:**  
  
```  
powershell c:\scripts\FireSubscription.ps1 "[server]/reportserver" $null "70366e82-2d3c-4edd-a216-b97e51e26de9"  
```  
  
 **SharePoint 모드 구문:**  
  
```  
powershell c:\scripts\FireSubscription.ps1 "[server]/_vti_bin/reportserver" "http://[server]" "c3425c72-580d-423e-805a-41cf9799fd25"  
```  
  
 **스크립트:**  
  
```  
  
# Parameters  
#    server         - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site           - use $null for a native mode server  
#    subscriptionid - subscription guid  
  
Param(  
  [string]$server,  
  [string]$site,  
  [string]$subscriptionid  
  )  
  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
#event type is case sensative to what is in the rsreportserver.config  
$rs2010.FireEvent("TimedSubscription",$subscriptionid,$site)  
  
Write-Host " "  
Write-Host "----- Subscription ($subscriptionid) status: "  
#get list of subscriptions and filter to the specific ID to see the Status and LastExecuted  
Start-Sleep -s 6 # slight delay in processing so ListSubscription returns the updated Status and LastExecuted  
$subscriptions = $rs2010.ListSubscriptions($site);   
$subscriptions | select Status, Path, report, Description, Owner, SubscriptionID, EventType, lastexecuted | where {$_.SubscriptionID -eq $subscriptionid}  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 
[ReportingService2010.ListSubscriptions 메서드](http://msdn.microsoft.com/library/reportservice2010.reportingservice2010.listsubscriptions.aspx)  

[ReportingService2010.ChangeSubscriptionOwner 메서드](http://msdn.microsoft.com/library/reportservice2010.reportingservice2010.changesubscriptionowner.aspx)   

[ReportingService2010.ListChildren](http://msdn.microsoft.com/library/reportservice2010.reportingservice2010.listchildren.aspx)  

[ReportingService2010.FireEvent](http://msdn.microsoft.com/library/reportservice2010.reportingservice2010.fireevent.aspx)
  
  
