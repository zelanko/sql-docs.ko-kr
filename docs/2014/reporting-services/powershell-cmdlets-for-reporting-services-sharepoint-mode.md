---
title: Reporting Services SharePoint 모드용 PowerShell cmdlet | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 7835bc97-2827-4215-b0dd-52f692ce5e02
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 56973f01112b670727cc0ffa83ba6372c45a3faa
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59241581"
---
# <a name="powershell-cmdlets-for-reporting-services-sharepoint-mode"></a>Reporting Services SharePoint 모드용 PowerShell cmdlet
   [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드를 설치하는 경우 SharePoint 모드에서 보고서 서버를 지원하기 위해 PowerShell cmdlet이 설치됩니다. cmdlet은 세 가지 범주의 기능을 포함합니다.  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스 및 프록시 설치  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션과 연결된 프록시의 프로비전 및 관리  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능(예: 확장 및 암호화 키) 관리  
  
||  
|-|  
|[!INCLUDE[applies](../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드|  
  
 **이 항목은 다음과 같이 구성되어 있습니다.**  
  
-   [Cmdlet 요약](#bkmk_cmdlet_sum)  
  
-   [공유 서비스 및 프록시 Cmdlet](#bkmk_sharedservice_cmdlets)  
  
-   [서비스 응용 프로그램 및 프록시 Cmdlet](#bkmk_serviceapp_cmdlets)  
  
-   [Reporting Services 사용자 지정 기능 Cmdlet](#bkmk_ssrsfeatures_cmdlets)  
  
-   [기본 샘플](#bkmk_basic_samples)  
  
-   [자세한 샘플](#bkmk_detailedsamples)  
  
    -   [Reporting Services 서비스 응용 프로그램 및 프록시 만들기](#bkmk_example_create_service_application)  
  
    -   [검토 하 고 Reporting Services 배달 확장 프로그램을 업데이트 합니다.](#bkmk_example_delivery_extension)  
  
    -   [예를 들어 데이터베이스 제한 시간 Servicea 보고 응용 프로그램 데이터베이스의 속성 가져오기 및 설정](#bkmk_example_db_properties)  
  
    -   [목록에서 reporting services 데이터 확장-SharePoint 모드](#bkmk_example_list_data_extensions)  
  
    -   [구독 소유자 변경 및 나열](#bkmk_change_subscription_owner)  
  
##  <a name="bkmk_cmdlet_sum"></a> Cmdlet 요약  

 cmdlet을 실행하려면 SharePoint 관리 셸을 열어야 합니다. Microsoft Windows에 포함된 그래픽 사용자 인터페이스 편집기인 **Windows PowerShell ISE(통합 스크립팅 환경)** 를 사용할 수도 있습니다. 자세한 내용은 [Windows Server에서 Windows PowerShell 시작](https://docs.microsoft.com/powershell/scripting/getting-started/starting-windows-powershell)를 사용할 수도 있습니다. 다음 cmdlet 요약에서 서비스 응용 프로그램 '데이터베이스'에 대 한 참조를 만들고 사용 하 여 데이터베이스의 모든 참조는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램입니다. 여기에는 구성, 경고 및 임시 데이터베이스가 포함됩니다.  

  
 PowerShell 예제를 입력할 때 다음과 비슷한 오류 메시지가 표시됩니다.  
  
-   Install-sprsservice: ' Install-sprsservice ' 용어도 인식 되지 않습니다는  
    cmdlet, 함수, 스크립트 파일 또는 실행 프로그램의 이름으로 인식되지 않습니다. 경로가 올바른지 확인한 다음 다시 시도하세요.  
  
 다음 문제 중 하나가 발생합니다.  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드가 설치되어 있지 않으므로 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] cmdlet이 설치되지 않았습니다.  
  
-   SharePoint 관리 셸 대신 Windows PowerShell 또는 Windows PowerShell ISE에서 PowerShell 명령을 실행했습니다. SharePoint 관리 셸을 사용하거나 다음 명령을 사용하여 Windows PowerShell 창에 SharePoint 스냅인을 추가합니다.  
  
    ```  
    Add-PSSnapin Microsoft.SharePoint.PowerShell  
    ```  
  
 자세한 내용은 참조 [SharePoint 2013 관리를 사용 하 여 Windows PowerShell](https://technet.microsoft.com/library/ee806878.aspx) (https://technet.microsoft.com/library/ee806878.aspx)합니다.  
  
#### <a name="to-open-the-sharepoint-management-shell-and-run-cmdlets"></a>SharePoint 관리 셸을 열고 cmdlet을 실행하려면  
  
1.  **시작** 단추를 클릭합니다.  
  
2.  **Microsoft SharePoint 제품** 그룹을 클릭합니다.  
  
3.  **SharePoint 관리 셸**을 클릭합니다.  
  
 cmdlet의 명령줄 도움말을 보려면 PowerShell 명령 프롬프트에서 PowerShell 'Get-Help' 명령을 사용합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
 `Get-Help Get-SPRSServiceApplicationServers`  
  
###  <a name="bkmk_sharedservice_cmdlets"></a> 공유 서비스 및 프록시 Cmdlet  
 다음 표에는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스에 대한 PowerShell cmdlet이 나와 있습니다.  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Install-SPRSService|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 공유 서비스를 설치 및 등록 또는 제거합니다. 이 작업은 SharePoint 모드에서 SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]가 설치된 시스템에서만 수행할 수 있습니다. 설치 시 다음 두 가지 작업이 수행됩니다.<br /><br /> 1) [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스가 팜에 설치 됩니다.<br /><br /> 2) [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 인스턴스가 현재 컴퓨터에 설치 됩니다.<br /><br /> 제거 시 다음 두 가지 작업이 수행됩니다.<br />1) [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스가 현재 시스템에서 제거 됩니다.<br />2) [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스가 팜에서 제거 됩니다.<br /><br /> <br /><br /> 참고: 다른 시스템에 팜에 있는 경우는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스가 설치 되어 지속 되는 경우 또는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램은 팜에서 실행 중인 경고 메시지가 표시 됩니다.|  
|Install-SPRSServiceProxy|SharePoint 팜에 Reporting Services 서비스 프록시를 설치 및 등록 또는 제거합니다.|  
|Get-SPRSProxyUrl|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 액세스를 위한 URL을 가져옵니다.|  
|Get-SPRSServiceApplicationServers|로컬 SharePoint 팜 내 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 공유 서비스가 설치된 모든 서버를 가져옵니다. 이 cmdlet은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 업그레이드 시 공유 서비스를 실행하므로 업그레이드되어야 하는 서버를 확인하는 데 유용합니다.|  
  
###  <a name="bkmk_serviceapp_cmdlets"></a> 서비스 응용 프로그램 및 프록시 Cmdlet  
 다음 표에는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션과 관련 프록시에 대한 PowerShell cmdlet이 나와 있습니다.  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Get-SPRSServiceApplication|하나 이상의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션 개체를 가져옵니다.|  
|New-SPRSServiceApplication|새 Reporting Services 서비스 애플리케이션 및 연결된 데이터베이스를 만듭니다.<br /><br /> LogonType 매개 변수: 보고서 서버를 사용 하 여 SSRS 응용 프로그램 풀 계정 또는 SQL Server 로그인을 보고서 서버 데이터베이스에 액세스를 지정 합니다. 다음 중 하나일 수 있습니다.<br /><br /> 0 Windows 인증<br /><br /> 1 SQL Server<br /><br /> 2 애플리케이션 풀 계정(기본값)|  
|Remove-SPRSServiceApplication|지정된 Reporting Services 서비스 애플리케이션을 삭제합니다. 그러면 연결된 데이터베이스도 제거됩니다.|  
|Set-SPRSServiceApplication|기존 Reporting Services 서비스 애플리케이션의 속성을 편집합니다.|  
|New-SPRSServiceApplicationProxy|새 Reporting Services 서비스 애플리케이션 프록시를 만듭니다.|  
|Get-SPRSServiceApplicationProxy|하나 이상의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션 프록시를 가져옵니다.|  
|Dismount-SPRSDatabase|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램에 대한 서비스 응용 프로그램 데이터베이스를 분리합니다.|  
|Remove-SPRSDatabase|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션에 대한 서비스 애플리케이션 데이터베이스를 제거합니다.|  
|Set-SPRSDatabase|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램에 연결된 데이터베이스의 속성을 설정합니다.|  
|Mount-SPRSDatabase|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션에 대한 데이터베이스를 탑재합니다.|  
|New-SPRSDatabase|지정된 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션에 대해 새 서비스 애플리케이션 데이터베이스를 만듭니다.|  
|Get-SPRSDatabaseCreationScript|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램 데이터베이스 화면에 데이터베이스 생성 스크립트를 출력합니다. 그런 다음 SQL Server Management Studio에서 스크립트를 실행할 수 있습니다.|  
|Get-SPRSDatabase|하나 이상의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션 데이터베이스를 가져옵니다. 이 명령을 사용하여 서비스 애플리케이션 데이터베이스의 ID를 가져오므로, Set-SPRSDatabase comdlet을 사용하여 속성(예: `querytimeout`)을 수정할 수 있습니다. 이 항목의 예제를 참조 하세요 [가져오기 및 Servicea 보고 응용 프로그램 데이터베이스의 속성을 설정, 예를 들어 제한 시간을 데이터베이스](#bkmk_example_db_properties)합니다.|  
|Get-SPRSDatabaseRightsScript|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션 데이터베이스 화면에 데이터베이스 권한 스크립트를 출력합니다. 원하는 사용자에 대한 프롬프트를 표시한 후 데이터베이스에서 사용 권한을 수정하기 위해 실행할 수 있는 Transact-SQL을 반환합니다. 그런 다음 SQL Server Management Studio에서 이 스크립트를 실행할 수 있습니다.|  
|Get-SPRSDatabaseUpgradeScript|화면에 데이터베이스 업그레이드 스크립트를 출력합니다. 이 스크립트는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션 데이터베이스를 현재 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 설치의 데이터베이스 버전으로 업그레이드합니다.|  
  
###  <a name="bkmk_ssrsfeatures_cmdlets"></a> Reporting Services 사용자 지정 기능 Cmdlet  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Update-SPRSEncryptionKey|지정된 Reporting Services 서비스 애플리케이션에 대한 암호화 키를 업데이트하고 데이터를 다시 암호화합니다.|  
|Restore-SPRSEncryptionKey|Reporting Services 서비스 애플리케이션에 대해 이전에 백업된 암호화 키를 복원합니다.|  
|Remove-SPRSEncryptedData|지정된 Reporting Services 서비스 애플리케이션에 대한 암호화된 데이터를 삭제합니다.|  
|Backup-SPRSEncryptionKey|지정된 Reporting Services 서비스 애플리케이션에 대한 암호화 키를 백업합니다.|  
|New-SPRSExtension|Reporting Services 서비스 애플리케이션의 새 확장 프로그램을 등록합니다.|  
|Set-SPRSExtension|기존 Reporting Services 확장 프로그램의 속성을 설정합니다.|  
|Remove-SPRSExtension|Reporting Services 서비스 애플리케이션에서 확장 프로그램을 삭제합니다.|  
|Get-SPRSExtension|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션에 대해 하나 이상의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 확장을 가져옵니다.<br /><br /> 유효한 값은<br /><br /> **배달**<br /><br /> **DeliveryUI**<br /><br /> **Render**<br /><br /> **Data**<br /><br /> **보안**<br /><br /> **인증**<br /><br /> **EventProcessing**<br /><br /> **ReportItems**<br /><br /> **Designer**<br /><br /> **ReportItemDesigner**<br /><br /> **ReportItemConverter**<br /><br /> **ReportDefinitionCustomization**|  
|Get-SPRSSite|"ReportingService" 기능 사용 여부에 따라 SharePoint 사이트를 가져옵니다. 기본적으로 "ReportingService" 기능이 설정되어 있는 사이트가 반환됩니다.|  
  
##  <a name="bkmk_basic_samples"></a> 기본 샘플  
 이름에 'SPRS'가 포함된 cmdlet 목록을 반환합니다. 이 목록은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] cmdlet의 전체 목록입니다.  
  
```  
Get-command -noun *SPRS*  
```  
  
 자세히 말해서 commandlist.txt라는 텍스트 파일로 전달됩니다.  
  
```  
Get-command -noun *SPRS* | Select name, definition | Format-List | Out-File c:\commandlist.txt  
```  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 서비스 및 서비스 프록시를 설치합니다.  
  
```  
Install-SPRSService  
```  
  
```  
Install-SPRSServiceProxy  
```  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 시작  
  
```  
get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
```  
  
 로그 파일에서 필터링된 행 목록을 반환하려면 SharePoint 관리 셸에서 다음 명령을 입력합니다. 이 명령은 "ssrscustomactionerror"가 포함된 행에 대해 필터링합니다. 이 예제에서는 rssharepoint.msi를 설치할 때 만든 로그 파일을 찾습니다.  
  
```  
Get-content -path C:\Users\testuser\AppData\Local\Temp\rs_sp_0.log | select-string "ssrscustomactionerror"  
```  
  
##  <a name="bkmk_detailedsamples"></a> 자세한 샘플  
 다음 샘플 외에도, [Windows PowerShell script for Steps 1–4](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md#bkmk_full_script)항목의 "Windows PowerShell 스크립트" 섹션을 참조하세요.  
  
###  <a name="bkmk_example_create_service_application"></a> Reporting Services 서비스 응용 프로그램 및 프록시 만들기  
 이 예제 스크립트는 다음 태스크를 완료합니다.  
  
1.  Reporting Services 서비스 애플리케이션 및 프록시를 만듭니다. 이 스크립트는 "My App Pool" 애플리케이션 풀이 이미 있는 것으로 가정합니다.  
  
2.  기본 프록시 그룹에 프록시 추가  
  
3.  포트 80 웹앱의 콘텐츠 데이터베이스에 대한 서비스 앱 액세스를 허용합니다. 스크립트 사이트 가정 "http://sitename" 이미 있습니다.  
  
```  
# Create service application and service application proxy  
$appPool = Get-SPServiceApplicationPool "My App Pool"  
$serviceApp = New-SPRSServiceApplication "My RS Service App" -ApplicationPool $appPool  
$serviceAppProxy = New-SPRSServiceApplicationProxy -Name "My RS Service App Proxy" -ServiceApplication $serviceApp  
  
# Add service application proxy to default proxy group.  Any web application that uses the default proxy group will now be able to use this service application.  
Get-SPServiceApplicationProxyGroup -default | Add-SPServiceApplicationProxyGroupMember -Member $serviceAppProxy  
  
# Grant application pool account access to the port 80 web application's content database.  
$webApp = Get-SPWebApplication "http://sitename"  
$appPoolAccountName = $appPool.ProcessAccount.LookupName()  
$webApp.GrantAccessToProcessIdentity($appPoolAccountName)  
  
```  
  
###  <a name="bkmk_example_delivery_extension"></a> 검토 하 고 Reporting Services 배달 확장 프로그램을 업데이트 합니다.  
 다음 PowerShell 스크립트 예제에서 `My RS Service App`서비스 애플리케이션에 대해 보고서 서버 메일 배달 확장 프로그램의 구성을 업데이트합니다. SMTP 서버(`<email server name>`) 및 FROM 메일 별칭(`<your FROM email address>`) 값을 업데이트합니다.  
  
```  
$app=get-sprsserviceapplication -Name "My RS Service App"  
$emailCfg = Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml   
$emailXml = [xml]$emailCfg   
$emailXml.SelectSingleNode("//SMTPServer").InnerText = "<email server name>"  
$emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
$emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
$emailXml.SelectSingleNode("//From").InnerText = '<your FROM email address>'  
Set-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
```  
  
 위의 예에서 서비스 애플리케이션의 정확한 이름을 모를 경우 부분 이름 검색을 기반으로 서비스 애플리케이션을 가져오도록 첫 번째 문을 다시 작성할 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
$app=get-sprsserviceapplication | where {$_.name -like " ssrs_testapp *"}  
```  
  
 다음 스크립트는 "Reporting Services 애플리케이션" 서비스 애플리케이션에 대해 보고서 서버 이메일 배달 확장 프로그램의 현재 구성 값을 반환합니다. 첫 번째 단계에서는 $app 변수 값을 "My RS Service App" 이름을 가진 서비스 애플리케이션의 개체로 설정합니다.  
  
 두 번째 명령문은 $app 변수에서 서비스 애플리케이션 개체에 대한 'Report Server Email' 배달 확장 프로그램을 가져오고 configurationXML을 선택합니다.  
  
```  
$app=get-sprsserviceapplication -Name "Reporting Services Application"  
Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
```  
  
 또한 다음과 같이 위의 두 문을 하나로 다시 쓸 수 있습니다.  
  
```  
get-sprsserviceapplication -Name "Reporting Services Application" | Get-SPRSExtension -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
```  
  
###  <a name="bkmk_example_db_properties"></a> 예를 들어 데이터베이스 제한 시간 Servicea 보고 응용 프로그램 데이터베이스의 속성 가져오기 및 설정  
 다음 예제에서는 데이터베이스 및 속성의 목록을 먼저 반환하므로 set 명령에 제공하는 데이터베이스 GUID(ID)를 결정할 수 없습니다. 속성의 전체 목록은 `Get-SPRSDatabase | format-list`를 참조하세요.  
  
```  
get-SPRSDatabase | select id, querytimeout,connectiontimeout, status, server, ServiceInstance   
```  
  
 다음은 출력의 예제입니다. SET cmdlet에서 수정하고 사용할 데이터베이스의 ID를 확인하세요.  
  
-   `Id                : 56f8d1bc-cb04-44cf-bd41-a873643c5a14`  
  
     `QueryTimeout      : 120`  
  
     `ConnectionTimeout : 15`  
  
     `Status            : Online`  
  
     `Server            : SPServer Name=uetestb01`  
  
     `ServiceInstance   : SPDatabaseServiceInstance`  
  
```  
Set-SPRSDatabase -identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 -QueryTimeout 300  
```  
  
 값이 설정되었는지 확인하려면 GET cmdlet을 다시 실행하세요.  
  
```  
Get-SPRSDatabase -identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 | select id, querytimeout,connectiontimeout, status, server, ServiceInstance  
```  
  
###  <a name="bkmk_example_list_data_extensions"></a> 목록에서 reporting services 데이터 확장-SharePoint 모드  
 다음 예제는 각 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션을 반복하고 각각에 대한 현재 데이터 확장을 나열합니다.  
  
```  
$apps = Get-SPRSServiceApplication  
foreach ($app in $apps)   
{  
Write-host -ForegroundColor "yellow" Service App Name $app.Name  
Get-SPRSExtension -identity $app -ExtensionType "Data" | select name,extensiontype | Format-Table -AutoSize  
}  
```  
  
 **예제 출력:**  
  
-   `Name           ExtensionType`  
  
     `----           -------------`  
  
     `SQL                     Data`  
  
     `SQLAZURE                Data`  
  
     `SQLPDW                  Data`  
  
     `OLEDB                   Data`  
  
     `OLEDB-MD                Data`  
  
     `ORACLE                  Data`  
  
     `ODBC                    Data`  
  
     `XML                     Data`  
  
     `SHAREPOINTLIST          Data`  
  
###  <a name="bkmk_change_subscription_owner"></a> 구독 소유자 변경 및 나열  
 [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [PowerShell을 사용하여 Reporting Services 구독 소유자 변경, 나열 및 구독 실행](subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)   
 [검사 목록: PowerShell를 사용 하 여 SharePoint 용 PowerPivot 확인](../analysis-services/instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md)   
 [CodePlex SharePoint 관리 PowerShell 스크립트](http://sharepointpsscripts.codeplex.com/)   
 [PowerShell을 사용 하 여 SSRS를 관리 하는 방법](https://curatedviews.cloudapp.net/13107/how-to-administer-ssrs-using-powershell)  
  
  
