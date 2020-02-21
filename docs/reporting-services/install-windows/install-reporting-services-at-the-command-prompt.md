---
title: 명령 프롬프트에 Reporting Services 2016 설치 - SSRS | Microsoft Docs
ms.date: 01/09/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- command line
ms.assetid: 048169b3-512c-41e4-895a-0416eff41268
author: maggiesMSFT
ms.author: maggies
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7c4597a19b3fbcde0a5b4f6a82cb2398b6776128
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "62513688"
---
# <a name="install-reporting-services-2016-at-the-command-prompt"></a>명령 프롬프트에 Reporting Services 2016 설치

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 SQL Server 설치 프로그램에서 명령줄 설치를 지원합니다. 이 항목에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]와 관련된 몇 가지 명령줄 설치 예가 포함됩니다. 모든 SQL Server 구성 요소에 대해 사용 가능한 명령줄 옵션에 대한 자세한 설명은 [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)를 참조하세요. 이 항목에서는 SharePoint 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능에 대한 명령줄 옵션은 다루지 않습니다. 추가 기능 명령 설치에 자세한 내용은 [rsSharePoint.msi 설치 파일을 사용하여 추가 기능 설치](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md#bkmk_install_rssharepoint)를 참조하세요.

##  <a name="bkmk_native_mode"></a> 기본 모드 Reporting Services

### <a name="rsinstallmode-native-mode"></a>RSINSTALLMODE(기본 모드)
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 위한 기본 입력 설정은 **/RSINSTALLMODE** 입력 설정입니다. 설정에는 **DefaultNativeMode**와 **FilesOnlyMode**의 두 가지 옵션이 있습니다.  
  
 설치에 SQL Server 데이터베이스 엔진이 있는 경우 RSINSTALLMODE 기본값은 DefaultNativeMode입니다. 설치에 SQL Server 데이터베이스 엔진이 없는 경우 RSINSTALLMODE 기본값은 FilesOnlyMode입니다. DefaultNativeMode를 선택했지만 설치에 SQL Server 데이터베이스 엔진이 없는 경우 설치가 RSINSTALLMODE를 FilesOnlyMode로 자동으로 변경합니다. 입력 설정에 대한 자세한 내용은 [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)를 참조하세요.

### <a name="examples-of-native-mode-installation"></a>기본 모드 설치 예

 다음 예제는 다음을 설치하고 다음에 대한 계정을 구성합니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]입니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독 기능에 필요한 SQL Server 에이전트입니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]입니다.  
  
```  
Setup.exe /q /IACCEPTSQLSERVERLICENSETERMS /ACTION="install" /ERRORREPORTING=1 /UPDATEENABLED="False" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Adv_SSMS,RS" /RSINSTALLMODE="DefaultNativeMode" /SQLSVCACCOUNT="[DOMAIN\ACCOUNT]" /SQLSVCPASSWORD="[PASSWORD]" /AGTSVCACCOUNT="[DOMAIN\ACCOUNT]" /AGTSVCPASSWORD="[PASSWORD]" /SQLSYSADMINACCOUNTS="[DOMAIN\ACCOUNT]"  
```  
  
##  <a name="bkmk_sharepoint_mode"></a> SharePoint 모드 Reporting Services  
  
### <a name="rsshpinstallmode-sharepoint-mode"></a>RSSHPINSTALLMODE(SharePoint 모드)  
 SharePoint 모드로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 설치하기 위한 입력 설정은 **/RSSHPINSTALLMODE**입니다. 입력 설정에는 SharePointFilesOnlyMode라는 한 옵션만 있습니다. 이 옵션은 SharePoint 모드에 필요한 모든 파일을 설치하지만 설치 후 구성이 필요합니다. SharePoint 중앙 관리를 사용하여 이 추가 구성 단계가 완료됩니다. 자세한 내용은 [SharePoint 모드에서 첫 번째 보고서 서버 설치](install-the-first-report-server-in-sharepoint-mode.md)를 참조하세요.  
  
### <a name="examples-of-sharepoint-mode-installation"></a>SharePoint 모드 설치 예  
 다음 예에서는 SharePoint 모드로 SQL Server 데이터베이스 엔진 서비스 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 와 SharePoint용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능(RS_SHPWFE)을 설치합니다.  
  
```  
setup /q /ACTION=install /FEATURES=SQL, RS_SHP, RS_SHPWFE,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE"  
```  
  
 다음 예에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드만 설치합니다.  
  
```  
Setup.exe /q /ACTION="Install" /IACCEPTSQLSERVERLICENSETERMS /FEATURES="RS_SHP" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SECURITYMODE="SQL" /SAPWD="[PASSWORD]" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Name]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="[Account Name]" /UPDATEENABLED="False"  
  
```  
  
### <a name="examples-of-sharepoint-mode-upgrade"></a>SharePoint 모드 업그레이드 예  
 다음 예에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드를 업그레이드합니다. **RSUPGRADEPASSWORD** 는 기존 Report Server 서비스 계정의 암호입니다. RSUPGRADEPASSWORD는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 계정이 기본 제공 계정이 아닌 한 업그레이드 시나리오에서 필수 필드입니다.  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[PID value]" /FTSVCACCOUNT="[DOMAIN\ACCOUNT]" /FTSVCPASSWORD="[PASSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSUPGRADEPASSWORD="[PASSWORD]"  
```  
  
 다음 예를 사용하면 SharePoint 공유 서비스 아키텍처를 기반으로 하는 SharePoint 모드 설치를 업그레이드할 수 있습니다. 이 예에는 ALLOWUPGRADEFORSSRSSHAREPOINTMODE 스위치가 사용됩니다. 공유 서비스 아키텍처를 기반으로 하지 않는 이전 버전을 업그레이드할 때는 이 스위치가 필요 없습니다.  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[Your PID Value]" /FTSVCACCOUNT="[ACCOUNT Name]" /FTSVCPASSWORD="[PASSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /ALLOWUPGRADEFORSSRSSHAREPOINTMODE="True"  
```

## <a name="next-steps"></a>다음 단계

[명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
[SysPrep 매개 변수](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#SysPrep)   
[명령 프롬프트에서 파워 피벗 설치](https://msdn.microsoft.com/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
