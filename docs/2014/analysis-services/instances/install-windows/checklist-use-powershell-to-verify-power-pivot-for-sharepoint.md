---
title: '검사 목록: PowerShell을 사용 하 여 SharePoint용 PowerPivot 확인 Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 73a13f05-3450-411f-95f9-4b6167cc7607
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0dea40f9c4e4c0672db78ca7e841cb7cedca857e
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78174352"
---
# <a name="checklist-use-powershell-to-verify-powerpivot-for-sharepoint"></a>검사 목록: PowerShell을 사용하여 SharePoint용 PowerPivot 확인
  서비스 및 데이터가 작동하는지 확인하는 견고한 확인 테스트에 성공하지 않으면 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 설치 또는 복구 작업이 완료되지 않습니다. 이 문서에서는 Windows PowerShell을 사용하여 이러한 단계를 수행하는 방법을 보여줍니다. 각 단계를 고유한 섹션에 포함하여 특정 태스크로 바로 이동할 수 있습니다. 예를 들어 유지 관리 또는 백업에 서비스 애플리케이션 및 콘텐츠 데이터베이스를 예약하려면 이 항목의 [데이터베이스](#bkmk_databases) 섹션에서 스크립트를 실행하여 이름을 확인합니다.

|||
|-|-|
|![PowerShell 관련 내용](../../../reporting-services/media/rs-powershellicon.jpg "PowerShell 관련 내용")|전체 PowerShell 스크립트가 항목 맨 아래에 포함되어 있습니다. 전체 스크립트를 시작점으로 사용하여 전체 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 배포를 제작하는 데 사용자 지정 스크립트를 만듭니다.|

||
|-|
|**[!INCLUDE[applies](../../../includes/applies-md.md)]** Sharepoint 2013 &#124; SharePoint 2010|

 **이 항목의**내용: 다음 TOC의 문자로 된 항목은 다이어그램 영역에 해당 합니다. 다이어그램에서는 다음을 보여 줍니다.

|||
|-|-|
|[PowerShell 환경 준비](#bkmk_prerequisites)<br /><br /> [증상 및 권장 되는 작업](#bkmk_symptoms)<br /><br /> **(A)** [Analysis Services Windows 서비스](#bkmk_windows_service)<br /><br /> **(B)** [get-powerpivotsystemservice and get-powerpivotengineservice](#bkmk_engine_and_system_service)<br /><br /> **(C)** [PowerPivot 서비스 응용 프로그램 및 프록시](#bkmk_powerpivot_service_application)<br /><br /> **(D)** [데이터베이스](#bkmk_databases)<br /><br /> [SharePoint 기능](#bkmk_features)<br /><br /> [타이머 작업](#bkmk_timer_jobs)<br /><br /> [상태 규칙](#bkmk_health_rules)<br /><br /> **(E)** [Windows 및 ULS 로그](#bkmk_logs)<br /><br /> [MSOLAP 공급자](#bkmk_msolap)<br /><br /> [ADOMD.Net 클라이언트 라이브러리](#bkmk_adomd)<br /><br /> [상태 데이터 수집 규칙](#bkmk_health_collection)<br /><br /> [솔루션](#bkmk_solutions)<br /><br /> [수동 확인 단계](#bkmk_manual)<br /><br /> [기타 참고 자료](#bkmk_more_resources)<br /><br /> [전체 PowerShell 스크립트](#bkmk_full_script)|![PowerPivot의 PowerShell 확인](../../../sql-server/install/media/ssas-powershell-component-verification.png "PowerPivot의 PowerShell 확인")|

##  <a name="bkmk_prerequisites"></a>PowerShell 환경 준비
 이 섹션의 단계에서는 PowerShell 환경을 준비합니다. 현재 스크립트 환경에 구성된 방법에 따라 단계를 수행하지 않아도 될 수 있습니다.

 **PowerShell 사용 권한**

 
  **관리자 권한**으로 Powershell 창 또는 PowerShell ISE(통합 스크립팅 환경)를 엽니다. 명령을 실행할 때 관리자 권한이 없는 경우 다음과 유사한 오류 메시지가 표시됩니다.

 Get-SPLogEvent: 이 cmdlet을 실행하려면 컴퓨터 **관리자 권한** 이 있어야 합니다.

 **SharePoint 및 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] ** 모듈

 SharePoint 관련 cmdlet을 실행할 때 다음과 유사한 오류 메시지가 표시되는 경우 Add-PSSnapin 명령을 실행합니다.

 'Get-PowerPivotSystemService' 용어 **는 cmdlet, 함수, 스크립트 파일 또는 실행 프로그램의 이름으로 인식되지 않습니다**. 이름의 철자를 확인하거나 경로가 포함되어 있으면 경로가 올바른지 확인하고 다시 시도합니다.

```
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0
```

 **Windows PowerShell**

 PowerShell ISE에 대한 자세한 내용은 [Windows PowerShell ISE 소개](https://technet.microsoft.com/library/dd315244.aspx) 및 [Windows PowerShell을 사용하여 SharePoint 2013 관리](https://technet.microsoft.com/library/ee806878\(v=office.15\).aspx)를 참조하세요.

|||
|-|-|
|![SharePoint 일반 응용 프로그램 집합의 PowerPivot](../../../sql-server/install/media/ssas-powerpivot-logo.png "SharePoint 일반 응용 프로그램 집합의 PowerPivot")|
  [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 관리 대시보드를 사용하여 중앙 관리에서 대부분의 구성 요소를 선택적으로 확인할 수 있습니다. 중앙 관리에서 대시보드를 열려면 **일반 애플리케이션 설정**, **PowerPivot** 의 **관리 대시보드**를 차례로 클릭합니다. 대시보드에 대한 자세한 내용은 [PowerPivot Management Dashboard and Usage Data](../../power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)를 참조하십시오.|

##  <a name="bkmk_symptoms"></a>증상 및 권장 되는 작업
 다음 표는 증상 또는 문제 및 문제를 해결하는 데 도움이 되는 이 항목의 제안되는 섹션 목록입니다.

|증상|섹션 참조|
|-------------|-----------------|
|데이터 새로 고침이 실행되지 않음|
  [Timer Jobs](#bkmk_timer_jobs) 섹션을 참조하여 **PowerPivot 데이터 새로 고침 타이머 작업** 이 온라인인지 확인합니다.|
|관리 대시보드 데이터가 오래됨|
  [타이머 작업](#bkmk_timer_jobs) 섹션을 참고하여 **관리 대시보드 처리 타이머 작업** 이 온라인인지 확인합니다.|
|관리 대시보드의 일부|Excel Services 또는 SharePoint용 PowerPivot이 없는 중앙 관리의 토폴로지가 포함된 팜에 SharePoint용 PowerPivot을 설치하는 경우, PowerPivot 관리 대시보드의 모든 기본 제공 보고서에 액세스하려면 Microsoft ADOMD.NET 클라이언트 라이브러리를 다운로드하여 설치해야 합니다. 대시보드의 일부 보고서는 ADOMD.NET을 사용하여 팜의 PowerPivot 쿼리 처리 및 서버 상태에 대한 보고 데이터를 제공하는 내부 데이터에 액세스합니다. 
  [ADOMD.Net 클라이언트 라이브러리](#bkmk_adomd) 섹션 및 [중앙 관리를 실행하는 웹 프런트 엔드 서버에 ADOMD.NET 설치](../../../sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md)항목을 참조하세요.|
|\<이후 콘텐츠>||

##  <a name="bkmk_windows_service"></a>Windows 서비스 Analysis Services
 이 섹션의 스크립트는 SharePoint 모드에서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스를 확인합니다. 서비스가 **실행**중인지 확인 합니다.

```powershell
Get-Service | Select name, displayname, status | Where {$_.Name -eq "msolap`$powerpivot"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name              DisplayName                                Status
----              -----------                                ------
MSOLAP$POWERPIVOT SQL Server Analysis Services (POWERPIVOT) Running
```

##  <a name="bkmk_engine_and_system_service"></a>Get-powerpivotsystemservice 및 Get-powerpivotengineservice
 이 섹션의 스크립트는 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 시스템 서비스 확인합니다. SharePoint 2013 배포를 위한 시스템 서비스 하나와 SharePoint 2010 배포를 위한 서비스 2개가 있습니다.

 **Get-powerpivotsystemservice**

 상태가 **온라인**인지 확인합니다.

```powershell
Get-PowerPivotSystemService | Select typename, status, applications, farm | Format-Table -Property * -AutoSize | Out-Default
```

```Output
TypeName                                  Status Applications                             Farm
--------                                  ------ ------------                             ----
SQL Server PowerPivot Service Application Online {Default PowerPivot Service Application} SPFarm Name=SharePoint_Config_77d8ab0744a34e8aa27c806a2b8c760c
```

 **Get-powerpivotengineservice**

> [!NOTE]
>  SharePoint 2013를 사용 하는 **경우이 스크립트를 건너뜁니다** . PowerPivotEngineService는 SharePoint 2013 배포의 일부입니다. SharePoint 2013에서 Get-PowerPivot**엔진**서비스 cmdlet을 실행 하면 다음과 유사한 오류 메시지가 표시 됩니다. 이 항목의 사전 요구 사항 섹션에 명시된 Add-PSSnapin 명령을 실행한 경우에도 이 오류 메시지가 반환됩니다.
> 
>  'Get-PowerPivotEngineService' 용어는 cmdlet 이름으로 인식되지 않습니다.

 SharePoint 2010 배포에서 상태가 **온라인**인지 확인합니다.

```powershell
Get-PowerPivotEngineService | Select typename, status, name, instances, farm | Format-Table -Property * -AutoSize | Out-Default
```

```Output
TypeName  : SQL Server Analysis Services
Status    : Online
Name      : MSOLAP$POWERPIVOT
Instances : {POWERPIVOT}
Farm      : SPFarm Name=SharePoint_Config
```

##  <a name="bkmk_powerpivot_service_application"></a>PowerPivot 서비스 응용 프로그램 및 프록시
 상태가 **온라인**인지 확인 합니다. Excel Services 애플리케이션에서는 서비스 애플리케이션 데이터베이스를 사용하지 않으므로 cmdlet이 데이터베이스 이름을 반환하지 않습니다. 이 항목의 이후 데이터베이스 섹션에서 데이터베이스가 온라인인지 확인할 수 있도록 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 서비스 애플리케이션에서 데이터베이스를 사용합니다.

 **PowerPivot 및 Excel Service 애플리케이션**

 SharePoint 2010 배포의 경우 상태가 **온라인**인지 확인합니다.

```powershell
Get-PowerPivotServiceApplication | Select typename,name, status, unattendedaccount, applicationpool, farm, database
Get-SPExcelServiceApplication | Select typename, DisplayName, status
```

```Output
TypeName          : PowerPivot Service Application
Name              : PowerPivotServiceApplication1
Status            : Online
UnattendedAccount : PowerPivotUnattendedAccount
ApplicationPool   : SPIisWebServiceApplicationPool Name=sqlbi_serviceapp
Farm              : SPFarm Name=SharePoint_Config
Database          : GeminiServiceDatabase Name=PowerPivotServiceApplication1_19648f3f2c944e27acdc6c20aab8487a

TypeName    : Excel Services Application Web Service Application
DisplayName : Excel Services Application
Status      : Online
```

 **서비스 응용 프로그램 풀**

> [!NOTE]
>  다음 코드 샘플은 먼저 기본 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 서비스 애플리케이션의 applicationpool 속성을 반환합니다. 이름은 문자열에서 구문 처리되고 애플리케이션 풀 개체 상태를 가져오는 데 사용됩니다.
> 
>  상태가 **온라인**인지 확인합니다. 사이트를 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 검색할 때 상태가 온라인이 아니거나 "http 오류"가 표시 되는 경우 IIS 응용 프로그램 풀의 id 자격 증명이 올바른지 확인 합니다. IIS 풀 이름은 Get-SPServiceApplicationPool 명령에서 반환되는 ID 속성 값입니다.

```powershell
$poolname = [string](Get-PowerPivotServiceApplication | Select -Property applicationpool)
$position = $poolname.lastindexof("=")
$poolname = $poolname.substring($position+1)
$poolname = $poolname.substring(0,$poolname.length-1)

Get-SPServiceApplicationPool | Select name, status, processaccountname, id | Where {$_.Name -eq $poolname} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name                           Status ProcessAccountName Id
----                           ------ ------------------ ------- 
SharePoint Web Services System Online DOMAIN\account     89b50ec3-49e3-4de7-881a-2cec4b8b73ea
```

 ![참고](../../../reporting-services/media/rs-fyinote.png "참고") 응용 프로그램 풀은 중앙 관리 페이지 **서비스 응용 프로그램 관리**에서도 확인할 수 있습니다. 서비스 애플리케이션의 이름을 클릭한 다음 리본에서 **속성** 을 클릭합니다.

 **PowerPivot 및 Excel Service 애플리케이션 프록시**

 상태가 **온라인**인지 확인합니다.

```powershell
Get-SPServiceApplicationProxy | Select typename, status, unattendedaccount, displayname | Where {$_.TypeName -Like "*powerpivot*" -Or $_.TypeName -Like "*excel services*"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
TypeName                                                 Status UnattendedAccount           DisplayName
--------                                                 ------ -----------------           -----------
PowerPivot Service Application Proxy                     Online PowerPivotUnattendedAccount PowerPivotServiceApplication1
Excel Services Application Web Service Application Proxy Online                             Excel Services Application
```

##  <a name="bkmk_databases"></a>데이터베이스인
 다음 스크립트는 서비스 애플리케이션 데이터베이스 및 모든 콘텐츠 데이터베이스의 상태를 반환합니다. 상태가 **온라인**인지 확인 합니다.

```powershell
Get-SPDatabase | Select name, status, server, typename | Where {$_.TypeName -eq "content database" -Or $_.TypeName -Like "*Gemini*"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name                                                                       Status Server                  TypeName 
----                                                                       ------ ------                  -------- 
DefaultPowerPivotServiceApplicationDB-38422181-2b68-4ab2-b2bb-9c00c39e5a5e Online SPServer Name=TESTSERVER Microsoft.AnalysisServices.SPAddin.GeminiServiceDatabase
DefaultWebApplicationDB-f0db1a8e-4c22-408c-b9b9-153bd74b0312               Online TESTSERVER\POWERPIVOT    Content Database 
SharePoint_Admin_3cadf0b098bf49e0bb15abd487f5c684                          Online TESTSERVER\POWERPIVOT    Content Database
```

##  <a name="bkmk_features"></a>SharePoint 기능
 사이트, 웹 및 팜 기능이 온라인인지 확인합니다.

```powershell
Get-SPFeature | Select displayname, status, scope, farm | Where {$_.displayName -Like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
DisplayName     Status Scope Farm                         
-----------     ------ ----- ----                         
PowerPivotSite  Online  Site SPFarm Name=SharePoint_Config
PowerPivotAdmin Online   Web SPFarm Name=SharePoint_Config
PowerPivot      Online  Farm SPFarm Name=SharePoint_Config
```

##  <a name="bkmk_timer_jobs"></a>타이머 작업
 타이머 작업이 **온라인**인지 확인합니다. 
  [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] EngineService가 SharePoint 2013에 설치되어 있지 않으므로 스크립트가 SharePoint 2013 배포에서 EngineService 타이머 작업을 목록에 나타내지 않습니다.

```powershell
Get-SPTimerJob | Where {$_.service -Like "*power*" -Or $_.service -Like "*mid*"} | Select status, displayname, LastRunTime, service | Format-Table -Property * -AutoSize | Out-Default
```

```Output
      Status DisplayName                                                                          LastRunTime          Service                             
------ -----------                                                                          -----------          -------                             
Online Health Analysis Job (Daily, SQL Server Analysis Services, All Servers)               4/9/2014 12:00:01 AM EngineService Name=MSOLAP$POWERPIVOT
Online Health Analysis Job (Hourly, SQL Server Analysis Services, All Servers)              4/9/2014 1:00:01 PM  EngineService Name=MSOLAP$POWERPIVOT
Online Health Analysis Job (Weekly, SQL Server Analysis Services, All Servers)              4/6/2014 12:00:10 AM EngineService Name=MSOLAP$POWERPIVOT
Online PowerPivot Management Dashboard Processing Timer Job                                 4/8/2014 3:45:38 AM  MidTierService
Online PowerPivot Health Statistics Collector Timer Job                                     4/9/2014 1:00:12 PM  MidTierService
Online PowerPivot Data Refresh Timer Job                                                    4/9/2014 1:09:36 PM  MidTierService
Online Health Analysis Job (Daily, SQL Server PowerPivot Service Application, All Servers)  4/9/2014 12:00:00 AM MidTierService
Online Health Analysis Job (Daily, SQL Server PowerPivot Service Application, Any Server)   4/9/2014 12:00:00 AM MidTierService
Online Health Analysis Job (Weekly, SQL Server PowerPivot Service Application, All Servers) 4/6/2014 12:00:03 AM MidTierService
Online Health Analysis Job (Weekly, SQL Server PowerPivot Service Application, Any Server)  4/6/2014 12:00:03 AM MidTierService
Online PowerPivot Setup Extension Timer Job                                                 4/1/2014 1:40:31 AM  MidTierService
```

##  <a name="bkmk_health_rules"></a>상태 규칙
 SharePoint 2013 배포에는 규칙이 훨씬 적습니다. 각 SharePoint 환경에 대 한 규칙의 전체 목록과 규칙 사용 방법에 대 한 설명은 [PowerPivot 상태 규칙-구성](../../power-pivot-sharepoint/configure-power-pivot-health-rules.md)을 참조 하세요.

```powershell
Get-SPHealthAnalysisRule | Select name, enabled, summary | Where {$_.summary -Like "*power*"}  | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name                          Enabled Summary
----                          ------- -------         
SecondaryLogonHealthRule         True PowerPivot:  Secondary Logon service (seclogon) is disabled
DataRefreshTimerJobHealthRule    True PowerPivot: The PowerPivot Data Refresh timer job is disabled.
ASUsageLoadHealthRule            True PowerPivot: The ratio of load events to connections is too high.
ASMiniDumpHealthRule             True PowerPivot: One or more minidump files were found in the Logs directory, indicating a program crash
ASUsageCubeRule                  True PowerPivot: Usage data is not getting updated at the expected frequency.
ASADOMDNETHealthRule             True PowerPivot: ADOMD.NET is not installed on a standalone WFE that is configured for central admin
MidTierAcctReadPermissionRule    True PowerPivot: MidTier process account should have 'Full Read' permission on all associated SPWebApplications.
```

##  <a name="bkmk_logs"></a>Windows 및 ULS 로그
 **Windows 이벤트 로그**

 다음 명령은 SharePoint 모드의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스 관련 이벤트의 Windows 이벤트 로그를 검색합니다. 이벤트를 사용 하지 않도록 설정 하거나 이벤트 수준을 변경 하는 방법에 대 한 자세한 내용은 [SharePoint 로그 파일과 진단 로깅 &#40;구성 및 보기 SharePoint용 PowerPivot&#41;](../../power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)를 참조 하세요.

 **서비스 이름:** MSOLAP $ POWERPIVOT

 **Windows 서비스의 표시 이름:** SQL Server Analysis Services (POWERPIVOT)

```powershell
Get-EventLog "application" | Where-Object {$_.source -Like "msolap`$powerpivot*"}  | Select timegenerated, entrytype , source, message | Format-Table -property * -AutoSize | Out-Default
```

```Output
TimeGenerated           EntryType Source            Message
-------------           --------- ------            -------
4/16/2014 1:45:19 PM  Information MSOLAP$POWERPIVOT Software usage metrics are disabled.
4/16/2014 1:45:19 PM  Information MSOLAP$POWERPIVOT Service started. Microsoft SQL Server Analysis Services 64 Bit Evaluation (x64) RTM 12.0.1997.5.
4/16/2014 1:45:18 PM  Information MSOLAP$POWERPIVOT The flight recorder was started.
4/14/2014 6:45:37 PM  Information MSOLAP$POWERPIVOT Software usage metrics are disabled.
```

 **SharePoint ULS 로그, 지난 48 시간**

 다음 명령은 지난 48시간 동안 생성된 ULS 로그에서 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 메시지를 반환합니다. 필요에 따라 addhours 매개 변수를 조정합니다.

```powershell
Get-SPLogEvent -StartTime(Get-Date).AddHours(-48) | Where-Object {$_.Area -eq "powerpivot service" -and $_.level -eq "high"} | Select timestamp, area, category, eventid,level, message | Format-Table -Property * -AutoSize | Out-Default
```

 다음 명령 변형은 **데이터 새로 고침** 범주에 대한 로그 이벤트만 반환합니다.

```powershell
Get-SPLogEvent -starttime(Get-Date).addhours(-48) | Where-Object {$_.category -eq "data refresh" -and $_.level -eq "high"} | Select timestamp, area, category, eventid, level, correlation, message
```

```Output
Timestamp   : 4/14/2014 7:15:01 PM
Area        : PowerPivot Service
Category    : Data Refresh
EventID     : 43
Level       : High
Correlation : 5755879c-7cab-e097-8f80-f27895d44a77
Message     : The following error occurred when working with the service application, Default PowerPivot Service Application. Skipping the service application..

Timestamp   : 4/14/2014 7:15:02 PM
Area        : PowerPivot Service
Category    : Data Refresh
EventID     : 99
Level       : High
Correlation : 5755879c-7cab-e097-8f80-f27895d44a77
Message     : EXCEPTION: System.TimeoutException: The request channel timed out while waiting for a reply after 00:00:47.0625313. Increase the timeout value passed to 
              the call to Request or increase the SendTimeout value on the Binding. The time allotted to this operation may have been a portion of a longer timeout. 
              ---> System.TimeoutException: The HTTP request to 'http://localhost:32843/SecurityTokenServiceApplication/securitytoken.svc/actas' has exceeded the 
              allotted timeout of 00:00:54.5930000. The time allotted to this operation may have been a portion of a longer timeout. ---> System.Net.WebException: The 
              operation has timed out     at System.Net.HttpWebRequest.GetResponse()     at 
              System.ServiceModel.Channels.HttpChannelFactory`1.HttpRequestChannel.HttpChannelRequest.WaitForReply(TimeSpan timeout...
```

##  <a name="bkmk_msolap"></a>MSOLAP 공급자
 MSOLAP 공급자를 확인합니다. [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]및 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 는 MSOLAP. 5를 요구 합니다.

```powershell
$excelApp = Get-SPExcelServiceApplication
Get-SPExcelDataProvider -ExcelServiceApplication $excelApp | Select providerid, providertype, description | Where {$_.providerid -like "msolap*" } | Format-Table -Property * -AutoSize | Out-Default
```

```Output
ProviderId ProviderType Description
---------- ------------ -----------
MSOLAP     Oledb        Microsoft OLE DB Provider for OLAP Services     
MSOLAP.3   Oledb        Microsoft OLE DB Provider for OLAP Services 9.0 
MSOLAP.4   Oledb        Microsoft OLE DB Provider for OLAP Services 10.0
MSOLAP.5   Oledb        Microsoft OLE DB Provider for OLAP Services 11.0
```

 자세한 내용은 [SharePoint 서버에서 Analysis Services OLE DB 공급자 설치](../../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) 및 [MSOLAP.5를 Excel Services에서 신뢰할 수 있는 데이터 공급자로 추가](https://technet.microsoft.com/library/hh758436.aspx)를 참조하세요.

##  <a name="bkmk_adomd"></a>ADOMD.Net 클라이언트 라이브러리

```powershell
Get-WMIObject -Class win32_product | Where-Object {$_.name -Like "*ado*"} | Select name, version, vendor | Format-Table -Property * -AutoSize | out-default
```

```Output
name                                                  version      vendor
----                                                  -------      ------
Microsoft SQL Server 2008 Analysis Services ADOMD.NET 10.1.2531.0  Microsoft Corporation
Microsoft SQL Server 2005 Analysis Services ADOMD.NET 9.00.1399.06 Microsoft Corporation
```

 자세한 내용은 [중앙 관리를 실행하는 웹 프런트 엔드 서버에 ADOMD.NET 설치](../../../sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md)를 참조하세요.

##  <a name="bkmk_health_collection"></a>상태 데이터 수집 규칙
 
  **상태** 가 온라인이고 **설정** 이 True인지 확인합니다.

```powershell
Get-SPUsageDefinition | Select name, status, enabled, tablename, DaysToKeepDetailedData | Where {$_.name -Like "powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default
```

```Output
Name                         Status Enabled TableName                   DaysToKeepDetailedData
----                         ------ ------- ---------                   ----------------------
PowerPivot Connections       OnlineTrue AnalysisServicesConnections  14
PowerPivot Load Data Usage   Online    True AnalysisServicesLoads                           14
PowerPivot Query Usage       Online    True AnalysisServicesRequests                        14
PowerPivot Unload Data Usage Online    True AnalysisServicesUnloads                         14
```

 자세한 내용은 [PowerPivot Usage Data Collection](../../power-pivot-sharepoint/power-pivot-usage-data-collection.md)을 참조하세요.

##  <a name="bkmk_solutions"></a>해결책이
 다른 구성 요소가 온라인인 경우 솔루션을 확인하는 단계를 건너뛸 수 있습니다. 그러나 상태 규칙이 없는 경우 표시되는 두 해결 방법을 확인하고 PowerPivot 솔루션이 **온라인** 이고 **배포됨**인지 확인하십시오.

```powershell
Get-SPSolution | Select name, status, deployed, DeploymentState, DeployedServers | Where {$_.Name -Like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default
```

SharePoint 2013:

```Output
Name                                 Status Deployed        DeploymentState DeployedServers
----                                 ------ --------        --------------- ---------------
powerpivotfarm14solution.wsp         Online     True         GlobalDeployed {UETESTA00}
powerpivotfarmsolution.wsp           Online     True         GlobalDeployed {UETESTA00}
powerpivotwebapplicationsolution.wsp Online     True WebApplicationDeployed {UETESTA00}
```

SharePoint  2010:

```Output
Name                 Status Deployed        DeploymentState DeployedServers 
----                 ------ --------        --------------- --------------- 
powerpivotfarm.wsp   Online     True         GlobalDeployed {uesql11spoint2}
powerpivotwebapp.wsp Online     True WebApplicationDeployed {uesql11spoint2}
```

 SharePoint 솔루션 배포 방법은 [솔루션 패키지 배포(SharePoint Server 2010)](https://technet.microsoft.com/library/cc262995\(v=office.14\).aspx)를 참조하세요.

##  <a name="bkmk_manual"></a>수동 확인 단계
 이 섹션에서는 PowerShell cmdlet으로 완료할 수 없는 확인 단계에 대해 설명합니다.

 **예약 된 데이터 새로 고침:** 새로 고침 일정을 **가능한 한 빨리 새로 고치도록**통합 문서를 구성 합니다.  자세한 내용은 [데이터 새로 고침 예약 및 Windows 인증을 지원 하지 않는 데이터 원본 &#40;SharePoint용 PowerPivot&#41;](../../power-pivot-sharepoint/schedule-data-refresh-and-data-sources-no-windows-authentication.md)의 "데이터 새로 고침 확인" 섹션을 참조 하세요.

##  <a name="bkmk_more_resources"></a>추가 리소스
 [Windows PowerShell의 웹 서버 (IIS) 관리 cmdlet](https://technet.microsoft.com/library/ee790599.aspx).

 [SharePoint에서 서비스, IIS 사이트 및 응용 프로그램 풀 상태를 확인 하기 위한 PowerShell](https://gallery.technet.microsoft.com/office/PowerShell-to-check-a6ed72a0)입니다.

 [SharePoint 용 Windows PowerShell 2013 참조](https://technet.microsoft.com/library/ee890108\(v=office.15\).aspx)

 [SharePoint Foundation 2010 용 Windows PowerShell 참조](https://technet.microsoft.com/library/ee890105\(v=office.14\).aspx)

 [Windows PowerShell을 사용 하 여 Excel Services 관리 (SharePoint Server 2010)](https://technet.microsoft.com/library/ff191201\(v=office.14\).aspx)

 [SQL Server 설치 로그 파일 보기 및 읽기](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)

 [Get-evenlog cmdlet 사용](https://technet.microsoft.com/library/ee176846.aspx)

##  <a name="bkmk_full_script"></a>전체 PowerShell 스크립트
 다음 스크립트에는 이전 섹션의 모든 명령이 포함되어 있습니다. 스크립트는 이 항목에 있는 것과 동일한 순서로 명령을 실행합니다. 스크립트에는 추가 필터링이 필요할 경우 이 항목에 명시된 일부 선택적 명령 변형이 포함되어 있습니다. 변형은 주석 문자(#)로 비활성화할 수 있습니다. 스크립트에는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint 모드를 확인하기 위한 일부 문도 포함되어 있습니다. 
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 문은 주석 문자(#)로 비활성화할 수 있습니다.

```powershell
# This script audits services related to PowerPivot for SharePoint
$starttime = Get-Date
write-host -foregroundcolor DarkGray StartTime $starttime

Write-Host  "Import the SharePoint PowerShell snappin"
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0

Write-Host -ForegroundColor Green "Analysis Services Windows Service"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-Service | Select name, displayname, status | Where {$_.Name -eq "msolap`$powerpivot"} | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "PowerPivotEngineService and PowerPivotSystemService"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"

Get-PowerPivotSystemService | Select typename, status, applications, farm | Format-Table -property * -AutoSize | Out-Default
# If needed, you can run the following to compare job definitions specific to the service against the results of the timer job definition section
#Get-PowerPivotSystemService | select -ExpandProperty jobdefinitions | select displayname, schedule, service | format-table -property * -autosize | out-default

Get-PowerPivotEngineService | Select typename, status, name, instances, farm | Format-Table -property * -AutoSize | Out-Default
# If needed, you can run the following to compare job definitions specific to the service against the results of the timer job definition section
#Get-PowerPivotEngineService | select -ExpandProperty jobdefinitions | select displayname, schedule, service | format-table -property * -autosize | out-default

#Write-Host -ForegroundColor Green "Service Instances - optional if you want to associate services with the server"
#Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
#Get-SPServiceInstance | select typename, status, server, service, instance | where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*excel*" -or $_.TypeName -like "*Analysis Services*"} | format-table -property * -autosize | out-default
#Get-PowerPivotEngineServiceInstance  | select typename, ASServername, status, server, service, instance
#Get-PowerPivotSystemServiceInstance  | select typename, ASSServerName, status, server, service, instance

Write-Host -ForegroundColor Green "PowerPivot And Excel Service Applications"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-PowerPivotServiceApplication | Select typename,name, status, unattendedaccount, applicationpool, farm, database
Get-SPExcelServiceApplication | Select typename,  DisplayName, status

#Write-Host ""
Write-Host -ForegroundColor Green "PowerPivot Service Application pool"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
# the following assumes there is only 1 PowerPivot Service Application, and returns that application's pool name.  if you have more than one, use the 2nd version
$poolname = [string](Get-PowerPivotServiceApplication | Select -Property applicationpool)
$position = $poolname.lastindexof("=")
$poolname = $poolname.substring($position+1)
$poolname = $poolname.substring(0,$poolname.length-1)
Get-SPServiceApplicationPool | Select name, status, processaccountname, id | Where {$_.Name -eq $poolname} | Format-Table -Property * -AutoSize | Out-Default

#Write-Host ""
Write-Host -ForegroundColor Green "PowerPivot and Excel Service Application Proxy"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPServiceApplicationProxy |  Select typename, status, unattendedaccount, displayname | Where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*excel services*"} | Format-Table -Property * -AutoSize | Out-Default
#Get-SPServiceApplicationProxy |  select typename, status, unattendedaccount, displayname | where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*Reporting Services*" -or $_.TypeName -like "*excel services*"} | format-table -property * -autosize | out-default

Write-Host -ForegroundColor Green "DATABASES"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPDatabase | Select name, status, server, typename | Where {$_.TypeName -eq "content database" -or $_.TypeName -like "*Gemini*"} | Format-Table -Property * -AutoSize | Out-Default
#Get-SPDatabase | select name, status, server, typename | where {$_.TypeName -eq "content database" -or $_.TypeName -like "*Gemini*" -or $_.TypeName -like "*ReportingServices*"}

Write-Host -ForegroundColor Green "features"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPFeature | Select displayname, status, scope, farm | Where {$_.displayName -like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default
#Get-SPFeature | select displayname, status, scope, farm | where {$_.displayName -like "*powerpivot*" -or $_.displayName -like "*ReportServer*"}  | format-table -property * -autosize | out-default

Write-Host -ForegroundColor Green "Timer Jobs (Job Definitions) -- list is the same as seen in the 'Review timer job definitions' section of the management dashboard"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPTimerJob | Where {$_.service -like "*power*" -or $_.service -like "*mid*"} | Select status, displayname, LastRunTime, service | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "health rules"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPHealthAnalysisRule | Select name, enabled, summary | Where {$_.summary -Like "*power*"}  | Format-Table -Property * -AutoSize | Out-Default

$time = Get-Date
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time

Write-Host -ForegroundColor Green "Windows Event Log data MSSQL$POWERPIVOT and "
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*"}  | Select timegenerated, entrytype , source, message | Format-Table -Property * -autosize | Out-Default
#The following is the same command but with the Inforamtion events filtered out.
#Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*" -and ($_.entrytype -match "error" -or $_.entrytype -match "critical" -or $_.entrytype -match "warning")}  |select timegenerated, entrytype , source, message | format-table -property * -autosize | out-default

#Write-Host ""
Write-Host -ForegroundColor Green "ULS Log data"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPLogEvent -StartTime(Get-Date).AddHours(-48) | Where-Object {$_.Area -eq "powerpivot service" -and $_.level -eq "high"} | Select timestamp, area, category, eventid, level, correlation, message | Format-Table -Property * -AutoSize | Out-Default
#the following example filters for the category 'data refresh'
#Get-SPLogEvent -starttime(get-date).addhours(-48) | Where-Object {$_.category -eq "data refresh" -and $_.level -eq "high"} | select timestamp, area, category, eventid, level, correlation, message

$time = Get-Date
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time

Write-Host -ForegroundColor Green "MSOLAP data provider for Excel Servivces, service application"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
$excelApp = Get-SPExcelServiceApplication
Get-SPExcelDataProvider -ExcelServiceApplication $excelApp | Select providerid, providertype, description | Where {$_.providerid -like "msolap*" } | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "ADOMD.net client library"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-WMIObject -Class win32_product | Where-Object {$_.name -like "*ado*"} | Select name, version, vendor | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "Usage Data Rules"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPUsageDefinition | Select name, status, enabled, tablename, DaysToKeepDetailedData | Where {$_.name -like "powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default

Write-Host -ForegroundColor Green "Solutions"
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
Get-SPSolution | Select name, status, deployed, DeploymentState, DeployedServers | Where {$_.Name -like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default

$time = Get-Date
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time
