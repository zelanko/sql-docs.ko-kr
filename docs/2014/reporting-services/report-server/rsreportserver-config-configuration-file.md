---
title: RSReportServer 구성 파일 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 60e0a0b2-8a47-4eda-a5df-3e5e403dbdbc
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 79df68ef047fc879e40ec14fb3754b783dba1ba6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093495"
---
# <a name="rsreportserver-configuration-file"></a>RSReportServer Configuration File
  **RsReportServer.config** 파일은 보고서 관리자, 보고서 서버 웹 서비스 및 백그라운드 처리에 사용되는 설정을 저장합니다. 모든 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 응용 프로그램은 RSReportServer.config 파일에 저장된 구성 설정을 읽는 단일 프로세스 내에서 실행됩니다. 기본 모드 및 SharePoint 모드 보고서 서버에는 모두 RSReportServer.config가 사용되지만 두 모드가 구성 파일에서 모두 동일한 설정을 사용하지는 않습니다. 이 파일의 SharePoint 모드 버전은 SharePoint 모드의 설정 대부분이 파일이 아니라 SharePoint 구성 데이터베이스에 저장되기 때문에 더 작습니다. 이 항목에서는 기본 모드 및 SharePoint 모드에서 설치되는 기본 구성 파일과 구성 파일을 통해 제어되는 일부 중요한 설정 및 동작에 대해 설명합니다.  
  
 SharePoint 모드의 구성 파일에는 해당 컴퓨터에서 실행되는 모든 서비스 응용 프로그램 인스턴스에 적용되는 설정이 포함됩니다. SharePoint 구성 데이터베이스에는 특정 서비스 응용 프로그램에 적용되는 구성 설정이 포함됩니다. 구성 데이터베이스에 저장되고 SharePoint 관리 페이지를 통해 관리되는 설정은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램별로 다를 수 있습니다.  
  
 설정은 기본값에 따라 설치된 구성 파일에 표시되는 순서대로 다음 콘텐츠에 표시됩니다. 이 파일을 편집하는 방법에 대한 지침은 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)을 참조하세요.  
  
 **항목 내용**  
  
-   [파일 위치](#bkmk_file_location)  
  
-   [일반 구성 설정 (rsreportserver.config)](#bkmk_generalconfiguration)  
  
-   [URLReservations (RSReportServer.config 파일)](#bkmk_URLReservations)  
  
-   [Authentication (RSReportServer.config 파일)](#bkmk_Authentication)  
  
-   [Service (RSReportServer.config 파일)](#bkmk_service)  
  
-   [배달 UI 확장 프로그램 일반 구성](#bkmk_ui)  
  
-   [확장 프로그램 (RSReportServer.config 파일) 기본 모드](#bkmk_extensions)  
  
    -   [배달 확장 프로그램 일반 구성](#bkmk_extensionsgeneral)  
  
        -   [파일 공유 배달 확장 프로그램 구성 설정](#bkmk_fileshare_extension)  
  
        -   [보고서 서버 전자 메일 확장 프로그램 구성 설정](#bkmk_email_extension)  
  
        -   [보고서 서버 SharePoint 문서 라이브러리 확장 구성](#bkmk_documentlibrary_extension)  
  
        -   [NULL 배달 확장 프로그램 구성](#bkmk_null_extension)  
  
    -   [배달 UI 확장 프로그램 일반 구성](#bkmk_ui)  
  
    -   [렌더링 확장 프로그램 일반 구성](#bkmk_rendering)  
  
    -   [데이터 확장 프로그램 일반 구성](#bkmk_data)  
  
    -   [의미 체계 쿼리 확장 프로그램 일반 구성](#bkmk_semantic)  
  
    -   [모델 생성 구성](#bkmk_model)  
  
    -   [보안 확장 프로그램 구성](#bkmk_security)  
  
    -   [인증 확장 프로그램 구성](#bkmk_authentication)  
  
    -   [이벤트 처리](#bkmk_eventprocessing)  
  
    -   [보고서 정의 사용자 지정](#bkmk_reportdefinition)  
  
    -   [RDLSandboxing](#bkmk_rdlsandboxing)  
  
-   [MapTileServerConfiguration (RSReportServer.config 파일)](#bkmk_MapTileServer)  
  
-   [기본 모드 보고서 서버에 대 한 기본 구성 파일](#bkmk_nativedefaultfile)  
  
-   [SharePoint 모드 보고서 서버에 대 한 기본 구성 파일](#bkmk_sharepointdefaultfile)  
  
##  <a name="bkmk_file_location"></a> 파일 위치  
  
-   RSReportServer.config는 보고서 서버 모드에 따라 다음 폴더에 있습니다.  
  
     **기본 모드 보고서 서버:**  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
-   **SharePoint 모드 보고서 서버:**  
  
    ```  
    C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
    ```  
  
 파일 편집에 대한 자세한 내용은 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)을 참조하세요.  
  
##  <a name="bkmk_generalconfiguration"></a> 일반 구성 설정(rsreportserver.config)  
 다음 표에서는 파일의 첫 부분에 나타나는 일반 구성 설정에 대한 정보를 제공합니다. 설정은 구성 파일에 나타나는 순서로 표시됩니다. 표의 마지막 열은 해당 설정이 기본 모드 보고서 서버에 적용되는지 **(N)** , SharePoint 모드 보고서 서버에 적용되는지 **(S)** 또는 두 가지 서버 모두에 적용되는지를 나타냅니다.  
  
> [!NOTE]  
>  이 항목에서 "최대 정수"는 INT_MAX 값, 2147483647을 의미합니다.  자세한 내용은 [정수 제한](http://msdn.microsoft.com/library/296az74e\(v=vs.110\).aspx)(http://msdn.microsoft.com/library/296az74e(v=vs.110).aspx)을 참조하세요.  
  
|설정|Description|모드|  
|-------------|-----------------|----------|  
|**Dsn**|보고서 서버 데이터베이스를 호스팅하는 데이터베이스 서버에 대한 연결 문자열을 지정합니다. 이 값은 보고서 서버 데이터베이스를 만들 때 암호화되어 구성 파일에 추가됩니다. Sharepoint에 대한 데이터베이스 연결 정보는 SharePoint 구성 데이터베이스에서 가져옵니다.|N,S|  
|**ConnectionType**|보고서 서버에서 보고서 서버 데이터베이스 연결에 사용하는 자격 증명 유형을 지정합니다. 유효한 값은 `Default` 및 `Impersonate`합니다. 보고서 서버가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 서비스 계정을 사용하여 보고서 서버 데이터베이스에 연결하도록 구성된 경우 `Default`가 지정됩니다. 보고서 서버가 Windows 계정을 사용하여 보고서 서버 데이터베이스에 연결하는 경우에는 `Impersonate`가 지정됩니다.|N|  
|**LogonUser, LogonDomain, LogonCred**|보고서 서버가 보고서 서버 데이터베이스에 연결하는 데 사용하는 도메인 계정의 도메인, 사용자 이름 및 암호를 저장합니다. 에 대 한 값 `LogonUser`, `LogonDomain`, 및 `LogonCred` 도메인 계정을 사용 하도록 보고서 서버 연결 구성 될 때 생성 됩니다. 보고서 서버 데이터베이스 연결에 대한 자세한 내용은 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)를 참조하세요.|N|  
|**InstanceID**|보고서 서버 인스턴스의 식별자입니다. 보고서 서버 인스턴스 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 기반으로 합니다. 이 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 지정합니다. 기본적으로이 값은 `MSRS12`  *\<인스턴스 이름 >* 합니다. 이 설정은 수정하지 마세요. 다음은 전체 값을 보여주는 예입니다. `<InstanceId>MSRS12.MSSQLSERVER</InstanceId>`<br /><br /> 다음은 SharePoint 모드의 예입니다.<br /><br /> `<InstanceId>MSRS12.@Sharepoint</InstanceId>`|N,S|  
|**InstallationID**|설치 프로그램에서 만드는 보고서 서버 설치의 ID입니다. 이 값은 GUID로 설정됩니다. 이 설정은 수정하지 마세요.|N|  
|**SecureConnectionLevel**|웹 서비스 호출에 SSL(Secure Sockets Layer)을 반드시 사용해야 하는 수준을 지정합니다. 이 설정은 보고서 서버 웹 서비스와 보고서 관리자에 모두 사용됩니다. 이 값은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구에서 사용할 URL(HTTP 또는 HTTPS)을 구성할 때 설정됩니다. 유효한 값은 0에서 3 사이이며 0은 보안 수준이 가장 낮습니다. 자세한 내용은 [보안 웹 서비스 메서드 사용](../report-server-web-service/net-framework/using-secure-web-service-methods.md) 및 [기본 모드 보고서 서버에서 SSL 연결 구성](../security/configure-ssl-connections-on-a-native-mode-report-server.md)을 참조하세요.|N,S|  
|**DisableSecureFormsAuthenticationCookie**|기본값은 False입니다.<br /><br /> 보안되도록 표시할 폼 및 사용자 지정 인증에 사용된 쿠키를 강제로 적용하지 않도록 설정할지 여부를 지정합니다. SQL Server 2012부터 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 사용자 지정 인증 확장 프로그램에 사용된 폼 인증 쿠키를 클라이언트에 전송할 때 보안 쿠키로 표시합니다. 보고서 서버 관리자 및 사용자 지정 보안 확장 프로그램 작성자는 이 속성을 변경하여, 사용자 지정 보안 확장 프로그램 작성자가 쿠키를 보안 쿠키로 표시할지 여부를 결정할 수 있도록 한 이전 동작으로 되돌릴 수 있습니다. 네트워크 스니핑과 재생 공격을 방지하도록 폼 인증에 보안 쿠키를 사용하는 것이 좋습니다.|N|  
|**CleanupCycleMinutes**|보고서 서버 데이터베이스에서 기존 세션 및 만료된 스냅숏을 제거할 시간 주기(분)를 지정합니다. 유효한 값은 0에서 최대 정수 사이입니다. 기본값은 10입니다. 이 값을 0으로 설정하면 데이터베이스 정리 프로세스가 해제됩니다.|N,S|  
|**MaxActiveReqForOneUser**|사용자 한 명이 동시에 처리할 수 있는 보고서의 최대 수를 지정합니다. 최대 수에 도달한 후에는 추가적인 보고서 처리 요청이 모두 거부됩니다. 유효한 값은 1에서 최대 정수 사이입니다. 기본값은 20입니다.<br /><br /> 대부분의 요청은 대단히 빠르게 처리되므로 단일 사용자가 지정된 시간에 연결이 20개 이상 열린 상태에서 작업할 가능성은 없습니다. 사용자가 많은 프로세스가 진행되는 보고서를 15개 이상 열 경우 이 값을 늘려야 할 수 있습니다.<br /><br /> SharePoint 통합 모드에서 실행되는 보고서 서버의 경우에는 이 설정이 무시됩니다.|N,S|  
|**DatabaseQueryTimeout**|보고서 서버 데이터베이스에 대한 연결이 종료되는 시간(초)을 지정합니다. 이 값은 System.Data.SQLClient.SQLCommand.CommandTimeout 속성으로 전달됩니다. 유효한 값은 0에서 2147483647 사이입니다. 기본값은 120입니다. 값 0은 무제한 대기 시간을 지정하므로 사용하지 않는 것이 좋습니다.|N|  
|**AlertingCleanupCycleMinutes**|기본값은 20입니다.<br /><br /> 경고 데이터베이스에 저장된 임시 데이터의 정리 빈도를 결정합니다.|S|  
|**AlertingDataCleanupMinutes**|기본값은 360입니다.<br /><br /> 경고 정의에 대한 만들기 또는 편집에 사용된 세션 데이터를 경고 데이터베이스 내에서 유지할 기간을 결정합니다. 기본값은 6시간입니다.|S|  
|**AlertingExecutionLogCleanup**Minutes|기본값은 10080입니다.<br /><br /> 경고 실행 로그 값을 유지할 기간을 결정합니다. 기본값은 7일입니다.|S|  
|**AlertingMaxDataRetentionDays**|기본값은 180입니다.<br /><br /> 경고 데이터가 변경되지 않은 경우 중복 경고 메시지를 방지하는 데 필요한 경고 데이터를 유지할 기간을 결정합니다.|S|  
|**RunningRequestsScavengerCycle**|분리 및 만료 요청 취소 간격을 지정합니다. 이 값은 초 단위로 지정됩니다. 유효한 값은 0에서 최대 정수 사이입니다. 기본값은 60입니다.|N,S|  
|**RunningRequestsDbCycle**|보고서 실행 제한 시간이 초과되었는지 여부를 확인하고 보고서 관리자의 작업 관리 페이지에 실행 중인 작업 정보를 표시하기 위해 보고서 서버에서 실행 중인 작업을 평가하는 간격을 지정합니다. 이 값은 초 단위로 지정됩니다. 유효한 값은 0에서 2147483647 사이입니다. 기본값은 60입니다.|N,S|  
|**RunningRequestsAge**|실행 중인 작업의 상태를 "신규"에서 "실행 중"으로 변경할 시간 간격(초)을 지정합니다. 유효한 값은 0에서 2147483647 사이입니다. 기본값은 30입니다.|N,S|  
|**MaxScheduleWait**|**다음 실행 시간**이 요청되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 일정을 업데이트하는 동안 보고서 서버 Windows 서비스가 대기하는 시간(초)을 지정합니다. 유효한 값은 1에서 60 사이입니다.<br /><br /> 기본 구성 파일에서는 MaxScheduleWait가 **5**로 설정되어 있습니다.<br /><br /> 보고서 서버에서 구성 파일을 찾지 못하거나 읽을 수 없는 경우 서버 기본값 MaxScheduleWait를 1로 설정합니다.|N,S|  
|**DisplayErrorLink**|오류 발생 시 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 도움말 및 지원 사이트에 대한 링크를 표시할지 여부를 나타냅니다. 이 링크는 오류 메시지에 나타납니다. 사용자는 링크를 클릭하여 해당 사이트에 대한 업데이트된 오류 메시지 내용을 열 수 있습니다. 유효한 값은 `True` (기본값) 및 `False`합니다.|N,S|  
|**WebServiceuseFileShareStorage**|사용자 세션 동안 보고서 서버 웹 서비스에서 만든 캐시된 보고서와 임시 스냅숏을 파일 시스템에 저장할지 여부를 지정합니다. 유효한 값은 `True` 및 `False` (기본값). 이 값을 false로 설정하면 임시 데이터가 reportservertempdb 데이터베이스에 저장됩니다.|N,S|  
|**WatsonFlags**|[!INCLUDE[msCoName](../../includes/msconame-md.md)]에 보고되는 오류 조건에 대해 기록되는 정보의 양을 지정합니다.<br /><br /> 0x0430 = 전체 덤프<br /><br /> 0x0428 = 미니 덤프<br /><br /> 0x0002 = 덤프 없음|N,S|  
|**WatsonDumpOnExceptions**|오류 로그에 보고할 예외 목록을 지정합니다. 이 설정은 반복적으로 발생하는 문제가 있고 분석을 위해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에 보낼 정보가 포함된 덤프를 만드는 경우에 유용합니다. 덤프를 만들면 성능에 영향을 주므로 문제를 진단하는 경우에만 이 설정을 변경하세요.|N,S|  
|**WatsonDumpExcludeIfContainsExceptions**|오류 로그에 보고하지 않을 예외 목록을 지정합니다. 이 설정은 문제를 진단할 때 서버에서 특정 예외에 대한 덤프를 만들지 않도록 할 경우에 유용합니다.|N,S|  
  
##  <a name="bkmk_URLReservations"></a> URLReservations(RSReportServer.config 파일)  
 `URLReservations` 보고서 서버 웹 서비스와 현재 인스턴스에 대 한 보고서 관리자에 대 한 HTTP 액세스를 정의합니다. URL은 보고서 서버를 구성할 때 예약되고 HTTP.SYS에 저장됩니다.  
  
> [!WARNING]  
>  SharePoint 모드의 경우 URL 예약은 SharePoint 중앙 관리에서 구성됩니다. 자세한 내용은 [대체 액세스 매핑 구성(http://technet.microsoft.com/library/cc263208(office.12).aspx)](http://technet.microsoft.com/library/cc263208\(office.12\).aspx)을 참조하세요.  
  
 구성 파일에서 URL 예약을 직접 수정하지 마세요. 항상 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자 또는 보고서 서버 WMI 공급자를 사용하여 기본 모드 보고서 서버에 대한 URL 예약을 만들거나 수정해야 합니다. 구성 파일에서 값을 수정하는 경우 예약이 손상되어 런타임에 서버 오류가 발생하거나 소프트웨어를 제거해도 제거되지 않는 분리된 예약이 HTTP.SYS에 남게 됩니다. 자세한 내용은 [보고서 서버 URL 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md) 및 [구성 파일의 URL&#40;SSRS 구성 관리자&#41;](../install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)를 참조하세요.  
  
 `URLReservations` 선택적 요소가입니다. 이 요소가 RSReportServer.config 파일에 없는 경우 서버가 구성되지 않은 것일 수 있습니다. 이 요소가 지정된 경우에는 `AccountName`을 제외한 모든 자식 요소가 필요합니다.  
  
 표의 마지막 열은 해당 설정이 기본 모드 보고서 서버에 적용되는지(N) 또는 SharePoint 모드 보고서 서버에 적용되는지(S) 또는 두 가지 서버 모두에 적용되는지를 나타냅니다.  
  
|설정|Description|모드|  
|-------------|-----------------|----------|  
|**응용 프로그램**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 응용 프로그램에 대한 설정을 포함합니다.|N|  
|**이름**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 응용 프로그램을 지정합니다. 유효한 값은 ReportServerWebService나 ReportManager입니다.|N|  
|**VirtualDirectory**|응용 프로그램의 가상 디렉터리 이름을 지정합니다.|N|  
|**URL**|응용 프로그램에 대한 하나 이상의 URL 예약을 포함합니다.|N|  
|**UrlString**|HTTP.SYS에 유효한 URL 구문을 지정합니다. 구문에 대한 자세한 내용은 [URL 예약 구문&#40;SSRS 구성 관리자&#41;](../install-windows/url-reservation-syntax-ssrs-configuration-manager.md)를 참조하세요.|N|  
|`AccountSid`|URL 예약을 만들 대상 계정의 SID(보안 식별자)를 지정합니다. 이 계정은 보고서 서버 서비스가 실행되는 계정이어야 합니다. SID가 서비스 계정과 일치하지 않으면 보고서 서버가 해당 URL에서 요청을 수신하지 못할 수 있습니다.|N|  
|`AccountName`|`AccountSid`에 해당하는 읽을 수 있는 계정 이름을 지정합니다. 이 이름은 사용되지 않지만 URL 예약에 사용된 계정의 서비스 계정을 쉽게 확인할 수 있도록 파일에 나타납니다.|N|  
  
##  <a name="bkmk_Authentication"></a> Authentication(RSReportServer.config 파일)  
 `Authentication`은 보고서 서버에서 허용되는 하나 이상의 인증 유형을 지정합니다. 기본 설정 및 값은 이 섹션에 사용할 수 있는 설정 및 값의 하위 집합입니다. 기본 설정만 자동으로 추가됩니다. 다른 설정을 추가하려면 텍스트 편집기를 사용하여 RSReportServer.config 파일에 요소 구조를 추가하고 값을 설정해야 합니다.  
  
 기본값은 `RSWindowsNegotiate`가 `RSWindowsNTLM`로 설정된 `EnableAuthPersistance` 및 `True`입니다.  
  
```  
   <Authentication>  
      <AuthenticationTypes>  
         <RSWindowsNegotiate/>  
         <RSWindowsNTLM/>  
      </AuthenticationTypes>  
      <EnableAuthPersistence>true</EnableAuthPersistence>  
   </Authentication>  
```  
  
 다른 모든 값은 수동으로 추가해야 합니다. 자세한 내용 및 예제는 [보고서 서버 인증](../security/authentication-with-the-report-server.md)을 참조하세요.  
  
 다음 표의 마지막 열은 해당 설정이 기본 모드 보고서 서버에 적용되는지(N) 또는 SharePoint 모드 보고서 서버에 적용되는지(S) 또는 두 가지 서버 모두에 적용되는지를 나타냅니다.  
  
|설정|Description|모드|  
|-------------|-----------------|----------|  
|**AuthenticationTypes**|하나 이상의 인증 유형을 지정합니다. 유효한 값은 `RSWindowsNegotiate`, `RSWindowsKerberos`, `RSWindowsNTLM`, `RSWindowsBasic` 및 `Custom`입니다.<br /><br /> `RSWindows` 유형 및 `Custom`은 함께 사용할 수 없습니다.<br /><br /> `RSWindowsNegotiate`, `RSWindowsKerberos`, `RSWindowsNTLM` 및 `RSWindowsBasic`은 누적되며 이 섹션의 앞부분에 나오는 기본값 예에서처럼 함께 사용할 수 있습니다.<br /><br /> 다양한 유형의 인증을 사용하는 여러 클라이언트 응용 프로그램 또는 브라우저에서 요청을 받는 경우 여러 인증 유형을 지정해야 합니다.<br /><br /> 지원되는 브라우저 종류 중 일부로 브라우저 지원이 제한되므로 `RSWindowsNTLM`을 제거하지 마십시오. 자세한 내용은 참조 [Reporting Services 및 Power View 브라우저 지원 계획 &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)합니다.|N|  
|`RSWindowsNegotiate`|보고서 서버가 Kerberos 또는 NTLM 보안 토큰을 수락합니다. 이 설정은 보고서 서버를 기본 모드에서 실행할 경우의 기본값이며 서비스 계정은 네트워크 서비스입니다. 보고서 서버를 기본 모드에서 실행하고 서비스 계정이 도메인 사용자 계정으로 구성된 경우에는 이 설정이 무시됩니다.<br /><br /> 보고서 서버 서비스 계정에 대해 도메인 계정이 구성되고 보고서 서버에 대해 SPN(서비스 사용자 이름)이 구성되지 않은 경우 이 설정을 사용하면 사용자가 서버에 로그온하지 못할 수 있습니다.|N|  
|`RSWindowsNTLM`|서버가 NTLM 보안 토큰을 수락합니다.<br /><br /> 이 설정을 제거하면 지원되는 일부 브라우저 유형에 대한 브라우저 지원이 제한될 수 있습니다. 자세한 내용은 참조 [Reporting Services 및 Power View 브라우저 지원 계획 &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)합니다.|N, S|  
|`RSWindowsKerberos`|서버가 Kerberos 보안 토큰을 수락합니다.<br /><br /> 제한된 위임 인증 체계에서 Kerberos 인증을 사용할 경우에는 이 설정이나 RSWindowsNegotiate를 사용합니다.|N|  
|`RSWindowsBasic`|서버가 기본 자격 증명을 수락하고, 자격 증명 없이 연결할 경우 시도/응답을 실행합니다.<br /><br /> 기본 인증을 사용하면 HTTP 요청 시 자격 증명이 일반 텍스트로 전달됩니다. 기본 인증을 사용할 경우 SSL을 사용하여 보고서 서버와의 네트워크 트래픽을 암호화해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 기본 인증에 대한 구성 구문 예를 보려면 [보고서 서버 인증](../security/authentication-with-the-report-server.md)을 참조하세요.|N|  
|`Custom`|보고서 서버 컴퓨터에 사용자 지정 보안 확장 프로그램을 배포한 경우 이 값을 지정합니다. 자세한 내용은 [Implementing a Security Extension](../extensions/security-extension/implementing-a-security-extension.md)을 참조하세요.|N|  
|**LogonMethod**|이 값에 대 한 로그온 유형을 지정 `RSWindowsBasic`합니다. 지정 하는 경우 `RSWindowsBasic`,이 값이 필요 합니다. 유효한 값은 2 또는 3입니다. 각 값에 대한 설명은 다음과 같습니다.<br /><br /> `2` = 일반 텍스트 암호를 인증 하는 로그온 고성능 서버 네트워크<br /><br /> `3` = 일반 텍스트 로그온 각 HTTP 요청과 함께 전송 되는 인증 패키지에 로그온 자격 증명, 보존 하는 서버를 네트워크에 있는 다른 서버에 연결할 때 사용자를 가장할 수 있습니다.<br /><br /> 참고: 값 0(대화형 로그온) 및 1(일괄 처리 로그온)은 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]에서 지원되지 않습니다.|N|  
|**Realm**|에 대 한이 값은 사용 `RSWindowsBasic`합니다. Realm은 조직의 보호된 리소스에 대한 액세스를 제어하는 데 사용되는 권한 부여 및 인증 기능이 포함된 리소스 파티션을 지정합니다.|N|  
|**DefaultDomain**|에 대 한이 값은 사용 `RSWindowsBasic`합니다. DefaultDomain은 사용자를 인증할 때 서버가 사용하는 도메인을 결정하는 데 사용됩니다. 이 값은 선택 사항이지만 생략하면 보고서 서버가 컴퓨터 이름을 도메인으로 사용합니다. 도메인 컨트롤러에 보고서 서버를 설치한 경우에는 컴퓨터에서 제어되는 도메인이 사용됩니다.|N|  
|**RSWindowsExtendedProtectionLevel**|기본값은 **해제**입니다. 자세한 내용은 [Extended Protection for Authentication with Reporting Services](../security/extended-protection-for-authentication-with-reporting-services.md)를 참조하세요.|N|  
|**RSWindowsExtendedProtectionScenario**|기본값은 **프록시**입니다.|N|  
|**EnableAuthPersistence**|인증을 연결 시 수행할지, 아니면 요청마다 수행할지를 결정합니다.<br /><br /> 유효한 값은 `True`(기본값)나 `False`입니다. `True`로 설정하면 같은 연결의 이후 요청이 첫 번째 요청의 가장 컨텍스트를 가정합니다.<br /><br /> ISA 서버와 같은 프록시 서버 소프트웨어를 사용하여 보고서 서버에 액세스하는 경우에는 이 값을 `False`로 설정해야 합니다. 프록시 서버를 사용하면 여러 사용자가 프록시 서버의 단일 연결을 사용할 수 있습니다. 이 시나리오에서는 각 사용자 요청이 별도로 인증되도록 인증 지속성을 사용하지 않아야 합니다. 설정 하지 않으면 **EnableAuthPersistence** 를 `False`, 모든 사용자가 첫 번째 요청의 가장 컨텍스트를 사용 하 여 연결 합니다.|N,S|  
  
##  <a name="bkmk_service"></a> Service(RSReportServer.config 파일)  
 `Service` 전체 서비스에 적용 되는 응용 프로그램 설정을 지정 합니다.  
  
 다음 표의 마지막 열은 해당 설정이 기본 모드 보고서 서버에 적용되는지(N) 또는 SharePoint 모드 보고서 서버에 적용되는지(S) 또는 두 가지 서버 모두에 적용되는지를 나타냅니다.  
  
|설정|Description|모드|  
|-------------|-----------------|----------|  
|**IsSchedulingService**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자가 만든 일정 및 구독에 해당하는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에이전트 작업 집합을 보고서 서버가 유지 관리하는지 여부를 지정합니다. 유효한 값은 `True` (기본값) 및 `False`합니다.<br /><br /> 정책 기반 관리의 Reporting Services 패싯에 대한 노출 영역 구성을 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능을 설정하거나 해제하면 이 설정이 영향을 받습니다. 자세한 내용은 [보고서 서버 서비스 시작 및 중지](start-and-stop-the-report-server-service.md)를 참조하세요.|N,S|  
|**IsNotificationService**|보고서 서버가 알림 및 배달을 처리하는지 여부를 지정합니다. 유효한 값은 `True` (기본값) 및 `False`합니다. 값이 `False`이면 구독이 배달되지 않습니다.<br /><br /> 정책 기반 관리의 Reporting Services 패싯에 대한 노출 영역 구성을 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능을 설정하거나 해제하면 이 설정이 영향을 받습니다. 자세한 내용은 [보고서 서버 서비스 시작 및 중지](start-and-stop-the-report-server-service.md)를 참조하세요.|N,S|  
|**IsEventService**|서비스가 이벤트 큐의 이벤트를 처리하는 지 여부를 지정합니다. 유효한 값은 `True` (기본값) 및 `False`합니다. 값이 `False`, 보고서 서버가 일정 또는 구독에 대 한 작업을 수행 하지 않습니다.<br /><br /> 정책 기반 관리의 Reporting Services 패싯에 대한 노출 영역 구성을 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능을 설정하거나 해제하면 이 설정이 영향을 받습니다. 자세한 내용은 [보고서 서버 서비스 시작 및 중지](start-and-stop-the-report-server-service.md)를 참조하세요.|N,S|  
|**IsAlertingService**|기본값은 `True`|S|  
|**PollingInterval**|보고서 서버가 이벤트 테이블을 폴링하는 간격(초)을 지정합니다. 유효한 값은 0에서 최대 정수 사이입니다. 기본값은 10입니다.|N,S|  
|**WindowsServiceUseFileShareStorage**|사용자 세션 동안 보고서 서버 서비스가 만든 캐시된 보고서와 임시 스냅숏을 파일 시스템에 저장할지 여부를 지정합니다. 유효한 값은 `True` 및 `False` (기본값).|N,S|  
|`MemorySafetyMargin`|보통 및 낮음 가중 시나리오 간 경계를 정의하는 `WorkingSetMaximum`의 비율을 지정합니다. 기본값은 80입니다. 에 대 한 자세한 내용은 `WorkingSetMaximum` 참조 사용 가능한 메모리를 구성 하 고 [보고서 서버 응용 프로그램에 대 한 사용 가능한 메모리 구성](../report-server/configure-available-memory-for-report-server-applications.md)합니다.|N,S|  
|**MemoryThreshold**|비율을 지정 `WorkingSetMaximum` 높음 및 보통가 중 시나리오 간 경계를 정의 하는 합니다. 기본값은 **90**입니다. 이 값에 대해 설정 된 값 보다 커야 `MemorySafetyMargin`합니다. 자세한 내용은 [보고서 서버 응용 프로그램을 위한 사용 가능한 메모리 구성](../report-server/configure-available-memory-for-report-server-applications.md)을 참조하세요.|N,S|  
|**RecycleTime**|응용 프로그램 도메인에 대한 재활용 시간(분)을 지정합니다. 유효한 값은 0에서 최대 정수 사이입니다. 기본값은 720입니다.|N,S|  
|**MaxAppDomainUnloadTime**|재활용 작업 중 응용 프로그램 도메인 언로드 작업이 허용되는 간격을 지정합니다. 이 기간 동안 재활용이 완료되지 않으면 응용 프로그램 도메인의 모든 처리가 중지됩니다. 자세한 내용은 [Application Domains for Report Server Applications](application-domains-for-report-server-applications.md)을 참조하세요.<br /><br /> 이 값은 분 단위로 지정됩니다. 유효한 값은 0에서 최대 정수 사이입니다. 기본값은 **30**입니다.|N,S|  
|**MaxQueueThreads**|보고서 서버 Windows 서비스에서 구독 및 알림을 동시에 처리하기 위해 사용하는 스레드 수를 지정합니다. 유효한 값은 0에서 최대 정수 사이입니다. 기본값은 0입니다. 0을 선택하면 보고서 서버가 최대 스레드 수를 결정합니다. 정수를 지정하면 사용자가 지정한 값이 한 번에 만들 수 있는 스레드 개수 상한값으로 설정됩니다. 보고서 서버 Windows 서비스의 프로세스 실행을 위한 메모리 관리 방법에 대한 자세한 내용은 [보고서 서버 응용 프로그램을 위한 사용 가능한 메모리 구성](../report-server/configure-available-memory-for-report-server-applications.md)을 참조하세요.|N,S|  
|**UrlRoot**|전자 메일 및 파일 공유 구독에 배달되는 보고서에 사용할 URL을 구성하기 위해 보고서 서버 배달 확장 프로그램에서 사용합니다. 이 값은 게시된 보고서를 액세스하는 보고서 서버에 대해 유효한 URL 주소여야 합니다. 보고서 서버가 오프라인 또는 무인 액세스를 위한 URL을 생성하는 데 사용합니다. 이러한 URL은 내보낸 보고서 및 배달 확장 프로그램에서 전자 메일의 링크와 같이 배달 메시지에 포함된 URL을 작성할 때 사용합니다. 보고서 서버는 다음과 같은 동작을 기반으로 보고서의 URL을 결정합니다.<br /><br /> **UrlRoot** 가 비어 있고(기본값) 예약된 URL이 있으면 보고서 서버는 ListReportServerUrls 메서드에 대해 URL이 생성되는 방식과 동일하게 URL을 자동으로 결정합니다. ListReportServerUrls 메서드에서 반환하는 첫 번째 URL이 사용되거나, SecureConnectionLevel이 0보다 큰 경우 첫 번째 SSL URL이 사용됩니다.<br /><br /> **UrlRoot** 에 특정 값을 설정하면 해당 값이 사용됩니다.<br /><br /> **UrlRoot** 가 비어 있고 URL 예약도 구성되어 있지 않으면 렌더링된 보고서 및 전자 메일 링크에 잘못된 URL이 사용됩니다.|N,S|  
|**UnattendedExecutionAccount**|보고서 서버에서 보고서를 실행하는 데 사용하는 사용자 이름, 암호 및 도메인을 지정합니다. 이러한 값은 암호화되어 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구 또는 **rsconfig** 유틸리티를 사용하여 이러한 값을 설정합니다. 자세한 내용은 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)을 참조하세요.<br /><br /> SharePoint 모드의 경우 SharePoint 중앙 관리를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램에 대한 실행 계정을 설정합니다. 자세한 내용은 [Reporting Services SharePoint 서비스 응용 프로그램 관리](../manage-a-reporting-services-sharepoint-service-application.md)를 참조하세요.|N|  
|**PolicyLevel**|보안 정책 구성 파일을 지정합니다. 유효한 값은 Rssrvrpolicy.config입니다. 자세한 내용은 [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md)을 참조하세요.|N,S|  
|**IsWebServiceEnabled**|보고서 서버 웹 서비스가 SOAP 및 URL 액세스 요청에 응답할지 여부를 지정합니다. 정책 기반 관리의 Reporting Services에 대한 노출 영역 구성 패싯을 사용하여 서비스를 설정하거나 해제하면 이 값이 설정됩니다.|N,S|  
|**IsReportManagerEnabled**|보고서 서버에서 보고서 관리자 응용 프로그램을 사용할 수 있는지 여부를 지정합니다. 유효한 값은 `True` (기본값) 및 `False`합니다. 값은로 설정 하는 경우 `True`, 보고서 관리자를 사용할 수 있습니다. 보고서 관리자에 대한 URL 예약을 사용하려면 먼저 구성해야 합니다.|N|  
|**FileShareStorageLocation**|파일 시스템에 임시 스냅숏을 저장할 단일 폴더를 지정합니다. 폴더 경로를 UNC 경로로 지정할 수 있지만 이 방법은 사용하지 않는 것이 좋습니다. 기본값은 비어 있습니다.<br /><br /> `<FileShareStorageLocation>`<br /><br /> `<Path>`<br /><br /> `</Path>`<br /><br /> `</FileShareStorageLocation>`|N,S|  
|**IsRdceEnabled**|RDCE(Report Definition Customization Extension) 설정 여부를 지정합니다. 유효한 값은 `True` 및 `False`합니다.|N,S|  
  
##  <a name="bkmk_UI"></a> UI(RSReportServer.config 파일)  
 `UI`는 보고서 관리자 응용 프로그램에 적용되는 구성 설정을 지정합니다.  
  
 다음 표의 마지막 열은 해당 설정이 기본 모드 보고서 서버에 적용되는지(N) 또는 SharePoint 모드 보고서 서버에 적용되는지(S) 또는 두 가지 서버 모두에 적용되는지를 나타냅니다.  
  
|설정|Description|모드|  
|-------------|-----------------|----------|  
|**ReportServerUrl**|보고서 관리자가 연결하는 보고서 서버의 URL을 지정합니다. 다른 인스턴스 또는 원격 컴퓨터의 보고서 서버에 연결하도록 보고서 관리자를 구성하는 경우에만 이 값을 수정합니다. 자세한 내용은 [보고서 관리자 구성&#40;기본 모드&#41;](configure-web-portal.md)을 참조하세요.|N,S|  
|**ReportBuilderTrustLevel**|이 값을 수정하지 마세요. 이 값은 구성할 수 없습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 이후 버전에서는 보고서 작성기 실행에 `FullTrust`합니다. 자세한 내용은 [보고서 작성기 액세스 구성](configure-report-builder-access.md) 을 참조하세요. 부분 신뢰 모드를 중단 하는 방법에 대 한 자세한 내용은 참조 [SQL Server 2014에서 SQL Server Reporting Services에 지원 되지 않는 기능](../discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)합니다.|N,S|  
|`PageCountMode`|보고서 관리자에게만 해당되는 이 설정은 보고서가 렌더링되기 전에 보고서 서버가 페이지 수 값을 계산하는지, 아니면 보고서를 볼 때 보고서 서버가 페이지 수 값을 계산하는지를 지정합니다. 유효한 값은 `Estimate` (기본값) 및 `Actual`합니다. 사용 하 여 `Estimate` 에 사용자가 보고서를 볼 때 페이지 수 정보를 계산 합니다. 처음에 페이지 수는 2(현재 페이지와 추가 한 페이지)로 설정되지만 사용자가 보고서 페이지를 이동할 때 상향 조정됩니다. 사용 하 여 `Actual` 보고서가 표시 되기 전에 미리 페이지 수를 계산 하려는 경우. `Actual`은 이전 버전과의 호환성을 위해 제공됩니다. 설정한 경우 `PageCountMode` 를 `Actual`, 보고서가 표시 되기 전에 대기 시간이 증가 하는 올바른 페이지 수를 가져오기 위해 전체 보고서를 처리 해야 합니다.|N,S|  
  
##  <a name="bkmk_extensions"></a> 확장 프로그램(RSReportServer.config 파일) 기본 모드  
 확장 프로그램 섹션은 **기본 모드** 보고서 서버의 경우에만 rsreportserver.config 파일에 표시됩니다. SharePoint 모드 보고서 서버의 확장 정보는 SharePoint 구성 데이터베이스에 저장되며 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램에 따라 구성됩니다.  
  
 `Extensions` 다음 확장 가능 모듈에 대 한 구성 설정을 지정는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치:  
  
-   배달 확장 프로그램  
  
-   DeliveryUI 확장 프로그램  
  
-   렌더링 확장 프로그램  
  
-   데이터 처리 확장 프로그램  
  
-   의미 체계 쿼리 확장 프로그램(내부 전용)  
  
-   모델 생성 확장 프로그램(내부 전용)  
  
-   보안 확장 프로그램  
  
-   인증 확장 프로그램  
  
-   이벤트 처리 확장 프로그램(내부 전용)  
  
-   보고서 정의 사용자 지정 확장 프로그램  
  
 이러한 확장 프로그램 중 일부는 보고서 서버에서 내부 전용으로 사용됩니다. 내부 전용 확장 프로그램에 대한 구성 설정은 설명되지 않습니다. 다음 섹션에서는 기본 확장 프로그램에 대한 구성 설정에 대해 설명합니다. 사용자 지정 확장 프로그램이 있는 보고서 서버를 사용하는 경우 구성 파일에 여기에 설명되지 않은 설정이 포함되어 있을 수 있습니다. 이 섹션에서는 나타나는 순서로 확장 프로그램을 나열합니다. 같은 종류의 확장 프로그램 인스턴스에 대해 반복해서 발생하는 설정은 한 번만 설명합니다.  
  
###  <a name="bkmk_extensionsgeneral"></a> 배달 확장 프로그램 일반 구성  
 구독을 통해 보고서를 배달하는 데 사용되는 기본(또는 사용자 지정) 배달 확장 프로그램을 지정합니다. RSReportServer.config 파일에는 보고서 서버 전자 메일, 파일 공유 배달,  
  
1.  보고서 서버 전자 메일  
  
2.  파일 공유 배달  
  
3.  SharePoint 통합 모드에서 실행되는 보고서 서버에 사용되는 보고서 서버 문서 라이브러리  
  
4.  보고서 캐시를 미리 로드하는 데 사용되는 Null 배달 공급자  
  
 배달 확장 프로그램에 대한 자세한 내용은 [구독 및 배달&#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md)를 참조하세요.  
  
 모든 배달 확장 프로그램에는 **Extension Name**, **MaxRetries**, **SecondsBeforeRetry**및 **Configuration**이 있습니다. 이러한 공유 설정은 먼저 설명됩니다. 확장 프로그램별 설정에 대한 설명은 두 번째 표에 나와 있습니다.  
  
|설정|Description|  
|-------------|-----------------|  
|**Extension Name**|배달 확장 프로그램의 이름 및 어셈블리를 지정합니다. 이 값은 수정하지 마세요.|  
|**MaxRetries**|첫 번째 시도가 성공하지 않을 경우 보고서 서버가 배달을 다시 시도하는 횟수를 지정합니다. 기본값은 3입니다.|  
|**SecondsBeforeRetry**|각 다시 시도 간 간격(초)을 지정합니다. 기본값은 900입니다.|  
|**Configuration**|각 배달 확장 프로그램에 고유한 구성 설정을 포함합니다.|  
  
####  <a name="bkmk_fileshare_extension"></a> 파일 공유 배달 확장 프로그램 구성 설정  
 파일 공유 배달은 네트워크의 공유 폴더에 응용 프로그램 파일 형식으로 내보내진 보고서를 보냅니다. 자세한 내용은 [File Share Delivery in Reporting Services](../subscriptions/file-share-delivery-in-reporting-services.md)을 참조하세요.  
  
|설정|Description|  
|-------------|-----------------|  
|**ExcludedRenderFormats**, **RenderingExtension**|이러한 설정은 파일 공유 배달과 제대로 작동하지 않는 내보내기 형식을 의도적으로 제외하는 데 사용됩니다. 이러한 형식은 일반적으로 대화형 보고/미리 보기에 사용되거나 보고서 캐시를 미리 로드하는 데 사용됩니다. 이러한 형식은 데스크톱 응용 프로그램에서 쉽게 볼 수 있는 응용 프로그램 파일을 생성하지 않습니다. 유효한 값은<br /><br /> **HTMLOWC**<br /><br /> **RGDI**<br /><br /> **Null**|  
  
####  <a name="bkmk_email_extension"></a> 보고서 서버 전자 메일 확장 프로그램 구성 설정  
 보고서 서버 전자 메일은 SMTP 네트워크 장치를 사용하여 보고서를 전자 메일 주소로 보냅니다. 이 배달 확장 프로그램을 사용하려면 먼저 구성해야 합니다. 자세한 내용은 참조 [전자 메일 배달을 위한 보고서 서버 구성 &#40;SSRS 구성 관리자&#41; ](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) 및 [Reporting Services의 전자 메일 배달](../subscriptions/e-mail-delivery-in-reporting-services.md)합니다.  
  
|설정|Description|  
|-------------|-----------------|  
|**SMTPServer**|원격 SMTP 서버 또는 전달자의 주소를 나타내는 문자열 값을 지정합니다. 이 값은 원격 SMTP 서비스에 필요하며 IP 주소, 회사 인트라넷에 있는 컴퓨터의 UNC 이름 또는 정규화된 도메인 이름일 수 있습니다.|  
|**SMTPServerPort**|SMTP 서비스가 보내는 메일 전송에 사용하는 포트를 나타내는 정수 값을 지정합니다. 포트 25는 일반적으로 전자 메일을 보내는 데 사용됩니다.|  
|**SMTPAccountName**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook Express 계정 이름을 할당하는 문자열 값을 포함합니다. SMTP 서버가 이 값을 사용하도록 구성된 경우 이 값을 설정할 수 있지만 그렇지 않은 경우에는 비워 둘 수 있습니다. **보낸 사람** 을 사용하여 보고서를 보낼 때 사용할 전자 메일 계정을 지정합니다.|  
|**SMTPConnectionTimeout**|SMTP 서비스와의 유효한 소켓 연결 시 대기 제한 시간(초)을 나타내는 정수 값을 지정합니다. 기본값은 30초이지만 **SendUsing** 이 2로 설정된 경우 이 값이 무시됩니다.|  
|**SMTPServerPickupDirectory**|로컬 SMTP 서비스의 픽업 디렉터리를 나타내는 문자열 값을 지정합니다. 이 값은 정규화된 로컬 폴더 경로(예: d:\rs-emails)여야 합니다.|  
|**SMTPUseSSL**|네트워크를 통해 SMTP 메시지를 보낼 때 SSL(Secure Sockets Layer)을 사용하도록 설정할 수 있는 부울 값을 지정합니다. 기본값은 0 또는 false입니다. 이 설정은 **SendUsing** 요소가 2로 설정되면 사용할 수 있습니다.|  
|**SendUsing**|메시지를 보낼 때 사용할 방법을 지정합니다. 유효한 값은<br /><br /> 1= 로컬 SMTP 서비스 픽업 디렉터리에서 메시지를 보냅니다.<br /><br /> 2= 네트워크 SMTP 서비스에서 메시지를 보냅니다.|  
|**SMTPAuthenticate**|TCP/IP 연결을 통해 SMTP 서비스에 메시지를 보낼 때 사용할 인증 종류를 나타내는 정수 값을 지정합니다. 유효한 값은<br /><br /> 0= 인증 없음<br /><br /> 1= (지원되지 않음)<br /><br /> 2= NTLM(NT LanMan) 인증. 보고서 서버 Windows 서비스의 보안 컨텍스트는 네트워크 SMTP 서버에 연결하는 데 사용됩니다.|  
|**보낸 사람**|보고서를 *abc@host.xyz*을 참조하세요. 주소는 보내는 전자 메일 메시지의 **보낸 사람** 줄에 나타납니다. 이 값은 원격 SMTP 서버를 사용할 때 필요합니다. 또한 이 값은 메일을 보낼 수 있는 권한이 있는 유효한 전자 메일 계정이어야 합니다.|  
|**EmbeddedRenderFormats, RenderingExtension**|전자 메일 메시지 본문에 보고서를 캡슐화하는 데 사용되는 렌더링 형식을 지정합니다. 보고서 내의 이미지는 보고서 내에 포함됩니다. 유효한 값은 MHTML 및 HTML4.0입니다.|  
|**PrivilegedUserRenderFormats**|"모든 구독 관리" 태스크 통해 구독이 설정되면 사용자가 보고서 구독에 대해 선택할 수 있는 렌더링 형식을 지정합니다. 이 값을 설정하지 않으면 의도적으로 제외하지 않은 모든 렌더링 형식을 사용할 수 있습니다.|  
|**ExcludedRenderFormats, RenderingExtension**|지정된 배달 확장 프로그램에서 제대로 작동하지 않는 형식을 제외합니다. 같은 렌더링 확장 프로그램의 여러 인스턴스를 제외할 수는 없습니다. 여러 인스턴스를 제외하면 보고서 서버에서 구성 파일을 읽을 때 오류가 발생합니다. 기본적으로 다음 확장 프로그램은 전자 메일 배달에서 제외됩니다.<br /><br /> **HTMLOWC**<br /><br /> **Null**<br /><br /> **RGDI**|  
|**SendEmailToUserAlias**|이 값은 **DefaultHostName**과 함께 작동합니다.<br /><br /> 때 **SendEmailToUserAlias** 로 설정 된 `True`, 개별 구독을 정의 하는 사용자가 보고서를 받는 사람으로 자동 지정 됩니다. **받는 사람** 필드는 숨겨집니다. 이 값이 `False`, **를** 필드가 표시 됩니다. 이 값을 설정 `True` 보고서 배포를 최대한 제어 하려는 경우. 유효한 값은 다음과 같습니다.<br /><br /> `True`= 구독을 만든 사용자의 전자 메일 주소 사용 됩니다. 이것은 기본값입니다.<br /><br /> `False`= 임의의 전자 메일 주소를 지정할 수 있습니다.|  
|**DefaultHostName**|이 값은 **SendEmailToUserAlias**와 함께 작동합니다.<br /><br /> **SendEmailToUserAlias** 를 true로 설정하면 사용자 별칭에 추가할 호스트 이름을 나타내는 문자열 값을 지정합니다. 이 값은 DNS(Domain Name System) 이름 또는 IP 주소일 수 있습니다.|  
|**PermittedHosts**|전자 메일 배달을 받을 호스트를 명시적으로 지정하여 보고서 배포를 제한합니다. **PermittedHosts**내에서 각 호스트는 **HostName** 요소로 지정됩니다. 해당 값은 IP 주소 또는 DNS 이름이 됩니다.<br /><br /> 호스트에 정의된 전자 메일 계정만 받는 사람으로 유효합니다. **DefaultHostName**을 지정한 경우 해당 호스트를 **PermittedHosts** 의 **HostName**요소로 포함시켜야 합니다. 이 값은 하나 이상의 DNS 이름이거나 IP 주소입니다. 기본적으로 이 값은 설정되어 있지 않습니다. 이 값이 설정되어 있지 않으면 전자 메일로 보낸 보고서를 받을 수 있는 사용자에 제한이 없습니다.|  
  
####  <a name="bkmk_documentlibrary_extension"></a> 보고서 서버 SharePoint 문서 라이브러리의 확장 구성  
 보고서 서버 문서 라이브러리는 문서 라이브러리에 응용 프로그램 파일 형식으로 내보내진 보고서를 보냅니다. 이 배달 확장 프로그램은 SharePoint 통합 모드에서 실행되도록 구성된 보고서 서버에서만 사용할 수 있습니다. 자세한 내용은 [SharePoint Library Delivery in Reporting Services](../subscriptions/sharepoint-library-delivery-in-reporting-services.md)을 참조하세요.  
  
|설정|Description|  
|-------------|-----------------|  
|**ExcludedRenderFormats, RenderingExtension**|이러한 설정은 문서 라이브러리 배달과 제대로 작동하지 않는 내보내기 형식을 의도적으로 제외하는 데 사용됩니다. HTMLOWC, RGDI 및 Null 배달 확장 프로그램이 제외됩니다. 이러한 형식은 일반적으로 대화형 보고/미리 보기에 사용되거나 보고서 캐시를 미리 로드하는 데 사용됩니다. 이러한 형식은 데스크톱 응용 프로그램에서 쉽게 볼 수 있는 응용 프로그램 파일을 생성하지 않습니다.|  
  
####  <a name="bkmk_null_extension"></a> Null 배달 확장 프로그램 구성  
 NULL 배달 공급자는 개별 사용자를 위해 미리 생성된 보고서와 함께 캐시를 미리 로드하는 데 사용됩니다. 이 배달 확장 프로그램에 대한 구성 설정은 없습니다. 자세한 내용은 [보고서 캐시&#40;SSRS&#41;](caching-reports-ssrs.md)버전에서 캐시를 미리 로드할 수 있는 유일한 방법이었습니다.  
  
###  <a name="bkmk_ui"></a> 배달 UI 확장 프로그램 일반 구성  
 보고서 관리자에서 개별 구독을 정의할 때 사용되는 구독 정의 페이지에 나타나는 사용자 인터페이스 구성 요소가 포함된 배달 확장 프로그램을 지정합니다. 사용자 정의 옵션이 있는 사용자 지정 배달 확장 프로그램을 만들고 배포하는 경우 보고서 관리자를 사용하려면 이 섹션의 배달 확장 프로그램을 등록해야 합니다. 기본적으로 보고서 서버 전자 메일 및 보고서 서버 파일 공유에 대한 구성 설정이 있습니다. 데이터 기반 구독 또는 SharePoint 응용 프로그램 페이지에서만 사용되는 배달 확장 프로그램에는 이 섹션의 설정이 없습니다.  
  
|설정|Description|  
|-------------|-----------------|  
|**DefaultDeliveryExtension**|이 설정은 구독 정의 페이지의 배달 유형 목록에서 맨 위에 표시되는 배달 확장 프로그램을 결정합니다. 이 설정은 배달 확장 프로그램 하나에만 포함될 수 있습니다. 유효한 값은 `True` 또는 `False`합니다. 이 값이 `True`로 설정된 확장 프로그램이 기본으로 선택됩니다.|  
|**Configuration**|배달 확장 프로그램에 대한 구성 옵션을 지정합니다. 각 배달 확장 프로그램에 대한 기본 렌더링 형식을 설정할 수 있습니다. 유효한 값은 rsreportserver.config 파일의 render 섹션에 지정된 렌더링 확장 프로그램 이름입니다.|  
|**DefaultRenderingExtension**|배달 확장 프로그램이 기본값인지 여부를 지정합니다. 보고서 서버 전자 메일이 기본 배달 확장 프로그램입니다. 유효한 값은 `True` 또는 `False`합니다. 둘 이상의 확장 프로그램에 `True` 값이 포함되어 있으면 첫 번째 확장 프로그램을 기본 확장 프로그램으로 간주합니다.|  
  
###  <a name="bkmk_rendering"></a> 렌더링 확장 프로그램 일반 구성  
 보고서 프레젠테이션에 사용되는 (사용자 지정) 렌더링 확장 프로그램 및 기본 확장 프로그램을 지정합니다.  
  
 사용자 지정 렌더링 확장 프로그램을 배포하지 않는 한 이 섹션을 수정하지 마세요. 자세한 내용은 [Implementing a Rendering Extension](../extensions/rendering-extension/implementing-a-rendering-extension.md)을 참조하세요.  
  
 기본 렌더링 확장 프로그램에는 다음이 포함됩니다.  
  
-   XML  
  
-   Null  
  
-   CSV  
  
-   PDF  
  
-   RGDI  
  
-   HTML4.0  
  
-   MHTML  
  
-   EXCEL  
  
-   RPL  
  
-   IMAGE  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 릴리스부터는 MHTML 및 HTML 4.0 렌더링에는 기본적으로 데이터 시각화 크기 조정 동작을 제어하기 위해 다음과 같은 장치 정보 설정이 포함됩니다.  
  
```  
<DeviceInfo><DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing></DeviceInfo>  
```  
  
 DeviceInfo 설정에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [MHTML 장치 정보 설정](../html-device-information-settings.md)  
  
-   [HTML 장치 정보 설정]... /.. / 장치 정보 settings.md html)  
  
-   [렌더링 확장 프로그램에 대한 장치 정보 설정&#40;Reporting Services&#41;](../device-information-settings-for-rendering-extensions-reporting-services.md)  
  
 **\<Render>** 에서 자식 **\<Extension>** 요소의 특성에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수 사용자 지정](../customize-rendering-extension-parameters-in-rsreportserver-config.md)  
  
-   [렌더링 확장 프로그램 배포](../extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
 사용자 지정 렌더링 확장 프로그램을 배포하지 않는 한 이 섹션을 수정하지 마세요. 자세한 내용은 [Implementing a Rendering Extension](../extensions/rendering-extension/implementing-a-rendering-extension.md)을 참조하세요.  
  
###  <a name="bkmk_data"></a> 데이터 확장 프로그램 일반 구성  
 쿼리 처리에 사용되는 (사용자 지정) 데이터 처리 확장 프로그램 및 기본 확장 프로그램을 지정합니다. 기본 데이터 처리 확장 프로그램에는 다음이 포함됩니다.  
  
-   SQL  
  
-   SQLAZURE  
  
-   SQLPDW  
  
-   OLEDB  
  
-   OLEDB-MD  
  
-   ORACLE  
  
-   ODBC  
  
-   XML  
  
-   SHAREPOINTLIST  
  
-   SAPBW  
  
-   ESSBASE  
  
-   TERADATA  
  
 사용자 지정 데이터 처리 확장 프로그램을 추가하지 않는 한 이 섹션을 수정하지 마세요. 자세한 내용은 [Implementing a Data Processing Extension](../extensions/data-processing/implementing-a-data-processing-extension.md)을 참조하세요.  
  
###  <a name="bkmk_semantic"></a> 의미 체계 쿼리 확장 프로그램 일반 구성  
 보고서 모델 처리에 사용되는 의미 체계 쿼리 처리 확장 프로그램을 지정합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에 포함된 의미 체계 쿼리 처리 확장 프로그램은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 데이터, Oracle 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 다차원 데이터에 대한 지원을 제공합니다. 이 섹션은 수정하지 마세요. 쿼리 처리는 확장 가능하지 않습니다.  
  
###  <a name="bkmk_model"></a> 모델 생성 구성  
 보고서 서버에 이미 게시된 공유 데이터 원본에서 보고서 모델을 만드는 데 사용되는 모델 생성 확장 프로그램을 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 데이터, Oracle 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 다차원 데이터 원본에 대한 모델을 생성할 수 있습니다. 이 섹션은 수정하지 마세요. 모델 생성은 확장 가능하지 않습니다.  
  
###  <a name="bkmk_security"></a> 보안 확장 프로그램 구성  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 사용되는 권한 부여 구성 요소를 지정합니다. 이 구성 요소에 등록 된 인증 확장 프로그램 사용 되는 `Authentication` RSReportServer.config 파일의 요소입니다. 사용자 지정 인증 확장 프로그램을 구현하지 않는 한 이 섹션을 수정하지 마십시오. 사용자 지정 보안 기능을 추가하는 방법은 [Implementing a Security Extension](../extensions/security-extension/implementing-a-security-extension.md)을 참조하세요. 권한 부여에 대한 자세한 내용은 [Authorization in Reporting Services](../extensions/security-extension/authorization-in-reporting-services.md)를 참조하세요.  
  
###  <a name="bkmk_authentication"></a> 인증 확장 프로그램 구성  
 보고서 서버에 사용되는 기본 인증 확장 프로그램 및 사용자 지정 인증 확장 프로그램을 지정합니다. 기본 확장 프로그램은 Windows 인증을 기반으로 합니다. 사용자 지정 인증 확장 프로그램을 구현하지 않는 한 이 섹션을 수정하지 마십시오. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 인증에 대한 자세한 내용은 [Reporting Services의 인증](../extensions/security-extension/authentication-in-reporting-services.md) 및 [보고서 서버 인증](../security/authentication-with-the-report-server.md)을 참조하세요. 사용자 지정 보안 기능을 추가하는 방법은 [Implementing a Security Extension](../extensions/security-extension/implementing-a-security-extension.md)을 참조하세요.  
  
###  <a name="bkmk_eventprocessing"></a> 이벤트 처리  
 기본 이벤트 처리기를 지정합니다. 이 섹션은 수정하지 마세요. 이 섹션은 확장할 수 없습니다.  
  
###  <a name="bkmk_reportdefinition"></a> 보고서 정의 사용자 지정  
 보고서 정의를 수정하는 사용자 지정 확장 프로그램의 이름과 유형을 지정합니다.  
  
###  <a name="bkmk_rdlsandboxing"></a> RDLSandboxing  
 보고서 서버의 단일 웹 팜을 여러 명이 공유하는 시나리오에서 개인별로 특정 유형의 보고서 리소스 사용을 검색하고 제한할 수 있는 RDL(Report Definition Language) 모드를 지정합니다. 자세한 내용은 [Enable and Disable RDL Sandboxing](../enable-and-disable-rdl-sandboxing.md)을 참조하세요.  
  
##  <a name="bkmk_MapTileServer"></a> MapTileServerConfiguration(RSReportServer.config 파일)  
 `MapTileServerConfiguration` 에 대 한 구성 설정을 정의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보고서 서버에 게시 된 보고서에서 Bing Maps 웹 서비스는 맵에 대 한 타일 배경을 제공 하는 보고서 항목입니다. 모든 자식 요소가 필요합니다.  
  
|설정|Description|  
|-------------|-----------------|  
|**MaxConnections**|Bing Maps 웹 서비스에 대한 최대 연결 수를 지정합니다.|  
|**Timeout**|Bing Maps 웹 서비스의 응답을 기다리는 제한 시간(초 단위)을 지정합니다.|  
|**AppID**|Bing Maps 웹 서비스에 사용할 응용 프로그램 식별자(AppID)를 지정합니다. `(Default)` 지정 된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 AppID입니다.<br /><br /> 보고서에서 Bing 지도 타일을 사용하는 방법은 [추가 사용 조건(Additional Terms of Use)](http://go.microsoft.com/fwlink/?LinkId=151371) 및 [개인 정보 취급 방침](http://go.microsoft.com/fwlink/?LinkId=151372)을 참조하십시오.<br /><br /> 고유한 Bing Maps 사용권 계약을 위해 사용자 지정 AppID를 지정해야 하는 경우가 아니라면 이 값을 변경하지 마세요. AppID를 변경한 경우 변경 내용을 적용하기 위해 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 다시 시작할 필요는 없습니다.|  
|**CacheLevel**|System.Net.Cache의 HttpRequestCacheLevel 열거형 값을 지정합니다. 기본값은 `Default`입니다. 자세한 내용은 [HttpRequestCacheLevel 열거형](http://go.microsoft.com/fwlink/?LinkId=153353)을 참조하십시오.|  
  
##  <a name="bkmk_nativedefaultfile"></a> 기본 모드 보고서 서버에 대한 기본 구성 파일  
 rsreportserver.config 파일은 기본적으로 다음 위치에 설치됩니다.  
  
 **C:\Program Files\Microsoft SQL Server\MSRS12 합니다. MSSQLSERVER\Reporting Services\ReportServer입니다.**  
  
```  
<Configuration>     <Dsn>AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAoyfT3iJKS0qxG3ibhRCYhAQAAAAiAAAAUgBlAHAAbwByAHQAaQBuAGcAIABTAGUAcgB2AGUAcgAAAANmAADAAAAAEAAAADMnIAaBwxRDy2mu4yg0zKAAAAAABIAAAKAAAAAQAAAAX+0WIyZTGyyEE7R8rtmmZegAAAByz0h1aXSAggJLDnVfd1eyGlLqTln9cCff3DQ25pcNBccP2rsLkwokUrS9kcee4up6UOawgKQuQjqWbLXfpqY9Dp/ueDTcF8h+VlSWNCmcH/OlDo7Pt2S6FestlnrmFrUXImx+XPZoeDYQelDUTgy8cHUAgUlD/wW8beboXXcS04QB0uTy2mwtUl5/xAPOGXFOKkXp6w8wqnxkEdVd60WyyppOu7djRf25OBSZn3I4T5dwaORHqPGVJmVGzcagoG5u0hDqtEf2RD4FnJgcAAIRHcqxj+jqOV+ZCVvmDcdBWCsbg5OdvIBEFAAAABi/yAmdbbA2emMyOAFIQ1k0His4</Dsn>     <ConnectionType>Default</ConnectionType>     <LogonUser></LogonUser>     <LogonDomain></LogonDomain>     <LogonCred></LogonCred>     <InstanceId>MSRS12.MSSQLSERVER</InstanceId>     <InstallationID>{6af9ea4c-2593-4dd8-8e2b-6315014c1a52}</InstallationID>     <Add Key="SecureConnectionLevel" Value="0"/>     <Add Key="DisableSecureFormsAuthenticationCookie" Value="false"/>     <Add Key="CleanupCycleMinutes" Value="10"/>     <Add Key="MaxActiveReqForOneUser" Value="20"/>     <Add Key="DatabaseQueryTimeout" Value="120"/>     <Add Key="RunningRequestsScavengerCycle" Value="60"/>     <Add Key="RunningRequestsDbCycle" Value="60"/>     <Add Key="RunningRequestsAge" Value="30"/>     <Add Key="MaxScheduleWait" Value="5"/>     <Add Key="DisplayErrorLink" Value="true"/>     <Add Key="WebServiceUseFileShareStorage" Value="false"/>     <!--  <Add Key="ProcessTimeout" Value="150" /> -->     <!--  <Add Key="ProcessTimeoutGcExtension" Value="30" /> -->     <!--  <Add Key="WatsonFlags" Value="0x0430" /> full dump-->     <!--  <Add Key="WatsonFlags" Value="0x0428" /> minidump -->     <!--  <Add Key="WatsonFlags" Value="0x0002" /> no dump-->     <Add Key="WatsonFlags" Value="0x0428"/>     <Add Key="WatsonDumpOnExceptions" Value="Microsoft.ReportingServices.Diagnostics.Utilities.InternalCatalogException,Microsoft.ReportingServices.Modeling.InternalModelingException,Microsoft.ReportingServices.ReportProcessing.UnhandledReportRenderingException"/>     <Add Key="WatsonDumpExcludeIfContainsExceptions" Value="System.Threading.ThreadAbortException,System.Web.UI.ViewStateException,System.OutOfMemoryException,System.Web.HttpException,System.IO.IOException,System.IO.FileLoadException,Microsoft.SharePoint.SPException,Microsoft.ReportingServices.WmiProvider.WMIProviderException"/>     <URLReservations>          <Application>               <Name>ReportServerWebService</Name>               <VirtualDirectory>ReportServer</VirtualDirectory>               <URLs>                    <URL>                         <UrlString>http://+:80</UrlString>                         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>                         <AccountName>NT Service\ReportServer</AccountName>                    </URL>               </URLs>          </Application>          <Application>               <Name>ReportManager</Name>               <VirtualDirectory>Reports</VirtualDirectory>               <URLs>                    <URL>                         <UrlString>http://+:80</UrlString>                         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>                         <AccountName>NT Service\ReportServer</AccountName>                    </URL>               </URLs>          </Application>     </URLReservations>     <Authentication>          <AuthenticationTypes>               <RSWindowsNTLM/>          </AuthenticationTypes>          <RSWindowsExtendedProtectionLevel>Off</RSWindowsExtendedProtectionLevel>          <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>          <EnableAuthPersistence>true</EnableAuthPersistence>     </Authentication>     <Service>          <IsSchedulingService>True</IsSchedulingService>          <IsNotificationService>True</IsNotificationService>          <IsEventService>True</IsEventService>          <PollingInterval>10</PollingInterval>          <WindowsServiceUseFileShareStorage>False</WindowsServiceUseFileShareStorage>          <MemorySafetyMargin>80</MemorySafetyMargin>          <MemoryThreshold>90</MemoryThreshold>          <RecycleTime>720</RecycleTime>          <MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>          <MaxQueueThreads>0</MaxQueueThreads>          <UrlRoot>          </UrlRoot>          <UnattendedExecutionAccount>               <UserName></UserName>               <Password></Password>               <Domain></Domain>          </UnattendedExecutionAccount>          <PolicyLevel>rssrvpolicy.config</PolicyLevel>          <IsWebServiceEnabled>True</IsWebServiceEnabled>          <IsReportManagerEnabled>True</IsReportManagerEnabled>          <FileShareStorageLocation>               <Path>               </Path>          </FileShareStorageLocation>     </Service>     <UI>          <ReportServerUrl>          </ReportServerUrl>          <PageCountMode>Estimate</PageCountMode>     </UI>     <Extensions>          <Delivery>               <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider,ReportingServicesFileShareDeliveryProvider">                    <MaxRetries>3</MaxRetries>                    <SecondsBeforeRetry>900</SecondsBeforeRetry>                    <Configuration>                         <FileShareConfiguration>                              <ExcludedRenderFormats>                                   <RenderingExtension>HTMLOWC</RenderingExtension>                                   <RenderingExtension>NULL</RenderingExtension>                                   <RenderingExtension>RGDI</RenderingExtension>                              </ExcludedRenderFormats>                         </FileShareConfiguration>                    </Configuration>               </Extension>               <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailProvider,ReportingServicesEmailDeliveryProvider">                    <MaxRetries>3</MaxRetries>                    <SecondsBeforeRetry>900</SecondsBeforeRetry>                    <Configuration>                         <RSEmailDPConfiguration>                              <SMTPServer></SMTPServer>                              <SMTPServerPort>                              </SMTPServerPort>                              <SMTPAccountName>                              </SMTPAccountName>                              <SMTPConnectionTimeout>                              </SMTPConnectionTimeout>                              <SMTPServerPickupDirectory>                              </SMTPServerPickupDirectory>                              <SMTPUseSSL>                              </SMTPUseSSL>                              <SendUsing>2</SendUsing>                              <SMTPAuthenticate>                              </SMTPAuthenticate>                              <From></From>                              <EmbeddedRenderFormats>                                   <RenderingExtension>MHTML</RenderingExtension>                              </EmbeddedRenderFormats>                              <PrivilegedUserRenderFormats>                              </PrivilegedUserRenderFormats>                              <ExcludedRenderFormats>                                   <RenderingExtension>HTMLOWC</RenderingExtension>                                   <RenderingExtension>NULL</RenderingExtension>                                   <RenderingExtension>RGDI</RenderingExtension>                              </ExcludedRenderFormats>                              <SendEmailToUserAlias>True</SendEmailToUserAlias>                              <DefaultHostName>                              </DefaultHostName>                              <PermittedHosts>                              </PermittedHosts>                         </RSEmailDPConfiguration>                    </Configuration>               </Extension>               <Extension Name="Report Server DocumentLibrary" Type="Microsoft.ReportingServices.SharePoint.SharePointDeliveryExtension.DocumentLibraryProvider,ReportingServicesSharePointDeliveryExtension">                    <MaxRetries>3</MaxRetries>                    <SecondsBeforeRetry>900</SecondsBeforeRetry>                    <Configuration>                         <DocumentLibraryConfiguration>                              <ExcludedRenderFormats>                                   <RenderingExtension>HTMLOWC</RenderingExtension>                                   <RenderingExtension>NULL</RenderingExtension>                                   <RenderingExtension>RGDI</RenderingExtension>                              </ExcludedRenderFormats>                         </DocumentLibraryConfiguration>                    </Configuration>               </Extension>               <Extension Name="NULL" Type="Microsoft.ReportingServices.NullDeliveryProvider.NullProvider,ReportingServicesNullDeliveryProvider"/>          </Delivery>          <DeliveryUI>               <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">                    <DefaultDeliveryExtension>True</DefaultDeliveryExtension>                    <Configuration>                         <RSEmailDPConfiguration>                              <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>                         </RSEmailDPConfiguration>                    </Configuration>               </Extension>               <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider"/>          </DeliveryUI>          <Render>               <Extension Name="XML" Type="Microsoft.ReportingServices.Rendering.DataRenderer.XmlDataReport,Microsoft.ReportingServices.DataRendering"/>               <Extension Name="NULL" Type="Microsoft.ReportingServices.Rendering.NullRenderer.NullReport,Microsoft.ReportingServices.NullRendering" Visible="false"/>               <Extension Name="CSV" Type="Microsoft.ReportingServices.Rendering.DataRenderer.CsvReport,Microsoft.ReportingServices.DataRendering"/>               <Extension Name="ATOM" Type="Microsoft.ReportingServices.Rendering.DataRenderer.AtomDataReport,Microsoft.ReportingServices.DataRendering" Visible="false"/>               <Extension Name="PDF" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.PDFRenderer,Microsoft.ReportingServices.ImageRendering"/>               <Extension Name="RGDI" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.RGDIRenderer,Microsoft.ReportingServices.ImageRendering" Visible="false"/>               <Extension Name="HTML4.0" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.Html40RenderingExtension,Microsoft.ReportingServices.HtmlRendering" Visible="false">                    <Configuration>                         <DeviceInfo>                              <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>                         </DeviceInfo>                    </Configuration>               </Extension>               <Extension Name="MHTML" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.MHtmlRenderingExtension,Microsoft.ReportingServices.HtmlRendering">                    <Configuration>                         <DeviceInfo>                              <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>                         </DeviceInfo>                    </Configuration>               </Extension>               <Extension Name="EXCEL" Type="Microsoft.ReportingServices.Rendering.ExcelRenderer.ExcelRenderer,Microsoft.ReportingServices.ExcelRendering" Visible="false"/>               <Extension Name="EXCELOPENXML" Type="Microsoft.ReportingServices.Rendering.ExcelOpenXmlRenderer.ExcelOpenXmlRenderer,Microsoft.ReportingServices.ExcelRendering"/>               <Extension Name="RPL" Type="Microsoft.ReportingServices.Rendering.RPLRendering.RPLRenderer,Microsoft.ReportingServices.RPLRendering" Visible="false" LogAllExecutionRequests="false"/>               <Extension Name="IMAGE" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering"/>               <Extension Name="WORD" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordDocumentRenderer,Microsoft.ReportingServices.WordRendering" Visible="false"/>               <Extension Name="WORDOPENXML" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordOpenXmlRenderer.WordOpenXmlDocumentRenderer,Microsoft.ReportingServices.WordRendering"/>          </Render>          <Data>               <Extension Name="SQL" Type="Microsoft.ReportingServices.DataExtensions.SqlConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.DataExtensions.SqlAzureConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="SQLPDW" Type="Microsoft.ReportingServices.DataExtensions.SqlDwConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="OLEDB" Type="Microsoft.ReportingServices.DataExtensions.OleDbConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="OLEDB-MD" Type="Microsoft.ReportingServices.DataExtensions.AdoMdConnection,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="ORACLE" Type="Microsoft.ReportingServices.DataExtensions.OracleClientConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="ODBC" Type="Microsoft.ReportingServices.DataExtensions.OdbcConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="XML" Type="Microsoft.ReportingServices.DataExtensions.XmlDPConnection,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="SHAREPOINTLIST" Type="Microsoft.ReportingServices.DataExtensions.SharePointList.SPListConnection,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="SAPBW" Type="Microsoft.ReportingServices.DataExtensions.SapBw.SapBwConnection,Microsoft.ReportingServices.DataExtensions.SapBw"/>               <Extension Name="ESSBASE" Type="Microsoft.ReportingServices.DataExtensions.Essbase.EssbaseConnection,Microsoft.ReportingServices.DataExtensions.Essbase"/>               <Extension Name="TERADATA" Type="Microsoft.ReportingServices.DataExtensions.TeradataConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>          </Data>          <SemanticQuery>               <Extension Name="SQL" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MSSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>False</EnableMathOpCasting>                    </Configuration>               </Extension>               <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MSSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>False</EnableMathOpCasting>                    </Configuration>               </Extension>               <Extension Name="SQLPDW" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQLADW.MSSqlAdwSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>False</EnableMathOpCasting>                    </Configuration>               </Extension>               <Extension Name="ORACLE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Oracle.OraSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>True</EnableMathOpCasting>                         <DisableNO_MERGEInLeftOuters>False</DisableNO_MERGEInLeftOuters>                         <EnableUnistr>False</EnableUnistr>                         <DisableTSTruncation>False</DisableTSTruncation>                    </Configuration>               </Extension>               <Extension Name="TERADATA" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Teradata.TdSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>True</EnableMathOpCasting>                         <ReplaceFunctionName>oREPLACE</ReplaceFunctionName>                    </Configuration>               </Extension>               <Extension Name="OLEDB-MD" Type="Microsoft.AnalysisServices.Modeling.QueryExecution.ASSemanticQueryCommand,Microsoft.AnalysisServices.Modeling"/>          </SemanticQuery>          <ModelGeneration>               <Extension Name="SQL" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MsSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>               <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MsSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>               <Extension Name="ORACLE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Oracle.OraSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>               <Extension Name="TERADATA" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Teradata.TdSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>               <Extension Name="OLEDB-MD" Type="Microsoft.AnalysisServices.Modeling.Generation.ModelGeneratorExtention,Microsoft.AnalysisServices.Modeling"/>          </ModelGeneration>          <Security>               <Extension Name="Windows" Type="Microsoft.ReportingServices.Authorization.WindowsAuthorization, Microsoft.ReportingServices.Authorization"/>          </Security>          <Authentication>               <Extension Name="Windows" Type="Microsoft.ReportingServices.Authentication.WindowsAuthentication, Microsoft.ReportingServices.Authorization"/>          </Authentication>          <EventProcessing>               <Extension Name="SnapShot Extension" Type="Microsoft.ReportingServices.Library.HistorySnapShotCreatedHandler,ReportingServicesLibrary">                    <Event>                         <Type>ReportHistorySnapshotCreated</Type>                    </Event>               </Extension>               <Extension Name="Timed Subscription Extension" Type="Microsoft.ReportingServices.Library.TimedSubscriptionHandler,ReportingServicesLibrary">                    <Event>                         <Type>TimedSubscription</Type>                    </Event>               </Extension>               <Extension Name="Cache Refresh Plan Extension" Type="Microsoft.ReportingServices.Library.CacheRefreshPlanHandler,ReportingServicesLibrary">                    <Event>                         <Type>RefreshCache</Type>                    </Event>               </Extension>               <Extension Name="Cache Update Extension" Type="Microsoft.ReportingServices.Library.ReportExecutionSnapshotUpdateEventHandler,ReportingServicesLibrary">                    <Event>                         <Type>SnapshotUpdated</Type>                    </Event>               </Extension>          </EventProcessing>     </Extensions>     <MapTileServerConfiguration>          <MaxConnections>2</MaxConnections>          <Timeout>10</Timeout>          <AppID>(Default)</AppID>          <CacheLevel>Default</CacheLevel>     </MapTileServerConfiguration></Configuration>  
```  
  
##  <a name="bkmk_sharepointdefaultfile"></a> SharePoint 모드 보고서 서버에 대한 기본 구성 파일  
 rsreportserver.config 파일은 기본적으로 다음 위치에 설치됩니다.  
  
 **C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\WebServices\Reporting**  
  
```  
<Configuration>  
  <Dsn />  
  <ConnectionType>Default</ConnectionType>  
  <LogonUser>  
  </LogonUser>  
  <LogonDomain>  
  </LogonDomain>  
  <LogonCred>  
  </LogonCred>  
  <InstanceId>MSRS12.@Sharepoint</InstanceId>  
  <Add Key="SecureConnectionLevel" Value="0" />  
  <Add Key="CleanupCycleMinutes" Value="10" />  
  <Add Key="MaxActiveReqForOneUser" Value="20" />  
  <Add Key="AlertingCleanupCycleMinutes" Value="20" />  
  <Add Key="AlertingDataCleanupMinutes" Value="360" />  
  <Add Key="AlertingExecutionLogCleanupMinutes" Value="10080" />  
  <Add Key="AlertingMaxDataRetentionDays" Value="180" />  
  <Add Key="RunningRequestsScavengerCycle" Value="60" />  
  <Add Key="RunningRequestsDbCycle" Value="60" />  
  <Add Key="RunningRequestsAge" Value="30" />  
  <Add Key="MaxScheduleWait" Value="5" />  
  <Add Key="DisplayErrorLink" Value="true" />  
  <Add Key="WebServiceUseFileShareStorage" Value="false" />  
  <!--  <Add Key="ProcessTimeout" Value="150" /> -->  
  <!--  <Add Key="ProcessTimeoutGcExtension" Value="30" /> -->  
  <!--  <Add Key="WatsonFlags" Value="0x0430" /> full dump-->  
  <!--  <Add Key="WatsonFlags" Value="0x0428" /> minidump -->  
  <!--  <Add Key="WatsonFlags" Value="0x0002" /> no dump-->  
  <Add Key="WatsonFlags" Value="0x0428" />  
  <Add Key="WatsonDumpOnExceptions" Value="Microsoft.ReportingServices.Diagnostics.Utilities.InternalCatalogException,Microsoft.ReportingServices.Modeling.InternalModelingException,Microsoft.ReportingServices.ReportProcessing.UnhandledReportRenderingException" />  
  <Add Key="WatsonDumpExcludeIfContainsExceptions" Value="System.Threading.ThreadAbortException,System.Web.UI.ViewStateException,System.OutOfMemoryException,System.Web.HttpException,System.IO.IOException,System.IO.FileLoadException,Microsoft.SharePoint.SPException,Microsoft.ReportingServices.WmiProvider.WMIProviderException" />  
  <RStrace>  
    <add name="FileName" value="ReportServerService" />  
    <add name="FileSizeLimitMb" value="32" />  
    <add name="KeepFilesForDays" value="14" />  
    <add name="Prefix" value="tid, time" />  
    <add name="TraceListeners" value="file" />  
    <add name="TraceFileMode" value="unique" />  
    <add name="Components" value="all:3" />  
  </RStrace>  
  <URLReservations>  
    <Application>  
      <Name>ReportServerWebService</Name>  
      <VirtualDirectory>ReportServer</VirtualDirectory>  
      <URLs>  
        <URL>  
          <UrlString>http://+:80</UrlString>  
          <AccountSid>  
          </AccountSid>  
          <AccountName>  
          </AccountName>  
        </URL>  
      </URLs>  
    </Application>  
    <Application>  
      <Name>ReportManager</Name>  
      <VirtualDirectory>Reports</VirtualDirectory>  
      <URLs>  
        <URL>  
          <UrlString>http://+:80</UrlString>  
          <AccountSid>  
          </AccountSid>  
          <AccountName>  
          </AccountName>  
        </URL>  
      </URLs>  
    </Application>  
  </URLReservations>  
  <Authentication>  
    <AuthenticationTypes>  
      <RSWindowsNTLM />  
    </AuthenticationTypes>  
    <EnableAuthPersistence>true</EnableAuthPersistence>  
  </Authentication>  
  <Service>  
    <IsSchedulingService>True</IsSchedulingService>  
    <IsNotificationService>True</IsNotificationService>  
    <IsEventService>True</IsEventService>  
    <IsAlertingService>True</IsAlertingService>  
    <PollingInterval>10</PollingInterval>  
    <WindowsServiceUseFileShareStorage>False</WindowsServiceUseFileShareStorage>  
    <MemorySafetyMargin>80</MemorySafetyMargin>  
    <MemoryThreshold>90</MemoryThreshold>  
    <RecycleTime>720</RecycleTime>  
    <MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>  
    <MaxQueueThreads>0</MaxQueueThreads>  
    <UrlRoot>  
    </UrlRoot>  
    <PolicyLevel>rssrvpolicy.config</PolicyLevel>  
    <IsWebServiceEnabled>True</IsWebServiceEnabled>  
    <IsReportManagerEnabled>True</IsReportManagerEnabled>  
    <FileShareStorageLocation>  
      <Path>  
      </Path>  
    </FileShareStorageLocation>  
  </Service>  
  <UI>  
    <ReportServerUrl>  
    </ReportServerUrl>  
    <PageCountMode>Estimate</PageCountMode>  
  </UI>  
  <MapTileServerConfiguration>  
    <MaxConnections>2</MaxConnections>  
    <Timeout>10</Timeout>  
    <AppID>(Default)</AppID>  
    <CacheLevel>Default</CacheLevel>  
  </MapTileServerConfiguration>  
</Configuration>  
```  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [보고서 서버 응용 프로그램을 위한 사용 가능한 메모리 구성](../report-server/configure-available-memory-for-report-server-applications.md)   
 [HTML 뷰어 및 보고서 관리자 스타일 시트를 사용자 지정](../customize-style-sheets-for-html-viewer-and-report-manager.md)   
 [Reporting Services 구성 파일](reporting-services-configuration-files.md)   
 [보고서 서버 초기화&#40;SSRS 구성 관리자&#41;](../install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [암호화된 보고서 서버 데이터 저장&#40;SSRS 구성 관리자&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  