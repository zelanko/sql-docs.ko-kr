---
title: Reporting Services SharePoint 모드 및 기본 모드의 명령 프롬프트 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 048169b3-512c-41e4-895a-0416eff41268
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fc1e5ae5d17d45b937a5dd44ab3ea6fe5f8620eb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108776"
---
# <a name="command-prompt-installation-of-reporting-services-sharepoint-mode-and-native-mode"></a>Reporting Services SharePoint 모드 및 기본 모드의 명령 프롬프트 설치
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 SQL Server 설치 프로그램에서 명령줄 설치를 지원합니다. 이 항목에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]와 관련된 몇 가지 명령줄 설치 예가 포함됩니다. 모든 SQL Server 구성 요소에 사용할 수 있는 명령줄 옵션에 대 한 자세한 설명은 [명령 프롬프트에서 SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)를 참조 하세요. 이 항목에서는 SharePoint 제품용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능에 대한 명령줄 옵션은 다루지 않습니다. 추가 기능 명령 설치에 자세한 내용은 [rsSharePoint.msi 설치 파일을 사용하여 추가 기능 설치](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md#bkmk_install_rssharepoint)를 참조하세요.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 모드 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드  
  
## <a name="rsinstallmode-native-mode"></a>RSINSTALLMODE(기본 모드)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 위한 기본 입력 설정은 **/RSINSTALLMODE** 입력 설정입니다. 설정에는 **DefaultNativeMode** 와 **FilesOnlyMode**의 두 가지 옵션이 있습니다.  
  
 설치에 SQL Server 데이터베이스 엔진이 있는 경우 RSINSTALLMODE 기본값은 DefaultNativeMode입니다. 설치에 SQL Server 데이터베이스 엔진이 없는 경우 RSINSTALLMODE 기본값은 FilesOnlyMode입니다. DefaultNativeMode를 선택했지만 설치에 SQL Server 데이터베이스 엔진이 없는 경우 설치가 RSINSTALLMODE를 FilesOnlyMode로 자동으로 변경합니다. 입력 설정에 대 한 자세한 내용은 [명령 프롬프트에서 SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)를 참조 하세요.  
  
## <a name="rsshpinstallmode-sharepoint-mode"></a>RSSHPINSTALLMODE(SharePoint 모드)  
 SharePoint 모드로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 설치하기 위한 입력 설정은 **/RSSHPINSTALLMODE**입니다. 입력 설정에는 SharePointFilesOnlyMode라는 한 옵션만 있습니다. 이 옵션은 SharePoint 모드에 필요한 모든 파일을 설치하지만 설치 후 구성이 필요합니다. SharePoint 중앙 관리를 사용하여 이 추가 구성 단계가 완료됩니다. 자세한 내용은 [sharepoint 2010에 대 한 Sharepoint 모드 설치 Reporting Services](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)를 참조 하세요.  
  
## <a name="examples-of-sharepoint-mode-installation"></a>SharePoint 모드 설치 예  
 다음 예에서는 SharePoint 모드로 SQL Server 데이터베이스 엔진 서비스 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 와 SharePoint용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능(RS_SHPWFE)을 설치합니다.  
  
```  
setup /q /ACTION=install /FEATURES=SQL, RS_SHP, RS_SHPWFE,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE"  
```  
  
 다음 예에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드만 설치합니다.  
  
```  
Setup.exe /q /ACTION="Install" /IACCEPTSQLSERVERLICENSETERMS /FEATURES="RS_SHP" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SECURITYMODE="SQL" /SAPWD="*****" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Name]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="[Account Name]" /UPDATEENABLED="False"  
  
```  
  
 다음 예에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 및 SharePoint 모드 둘 다를 포함하여 모든 SQL Server 기능을 설치합니다.  
  
```  
Setup.exe /q /ACTION="Install" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Replication,SNAC,SNAC_SDK,Browser,Writer,AS,IS,MDS,Adv_SSMS,BC,BOL,Conn,SDK,DReplay_CTLR,DReplay_CLT, RS_SHP,RS_SHPWFE,DQC,BIDS,FullText, RS,DQ,SSMS" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SQLSVCACCOUNT="[Account Name]" /SQLSVCPASSWORD="********" /AGTSVCACCOUNT="[Account Nam]" /AGTSVCPASSWORD="********" /CTLRSVCACCOUNT="[Account Nam]" /CTLRSVCPASSWORD="********" /CLTSVCACCOUNT="[Account Nam]" /CLTSVCPASSWORD="********" /ASSVCACCOUNT="[Account Nam]" /ASSVCPASSWORD="********" /RSSVCACCOUNT="[Account Nam]" /RSSVCPASSWORD="********" /FTSVCACCOUNT="[Account Nam]" /FTSVCPASSWORD="********" /SECURITYMODE="SQL" /SAPWD="********" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Nam]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSSHPINSTALLMODE="SharePointFilesOnlyMode" /RSINSTALLMODE="DefaultNativeMode"  
```  
  
## <a name="examples-of-sharepoint-mode-upgrade"></a>SharePoint 모드 업그레이드 예  
 다음 예에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드를 업그레이드합니다. **RSUPGRADEPASSWORD** 는 기존 Report Server 서비스 계정의 암호입니다. RSUPGRADEPASSWORD는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 계정이 기본 제공 계정이 아닌 한 업그레이드 시나리오에서 필수 필드입니다.  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[PID value]" /FTSVCACCOUNT="[DOMAIN\ACCOUNT]" /FTSVCPASSWORD="[ACCOUNTPASSSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSUPGRADEPASSWORD="******"  
```  
  
 다음 예를 사용하면 SharePoint 공유 서비스 아키텍처를 기반으로 하는 SharePoint 모드 설치를 업그레이드할 수 있습니다. 이 예에는 ALLOWUPGRADEFORSSRSSHAREPOINTMODE 스위치가 사용됩니다. 공유 서비스 아키텍처를 기반으로 하지 않는 이전 버전을 업그레이드할 때는 이 스위치가 필요 없습니다.  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[Your PID Value]" /FTSVCACCOUNT="[ACCOUNT Name]" /FTSVCPASSWORD="****" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /ALLOWUPGRADEFORSSRSSHAREPOINTMODE="True"  
```  
  
## <a name="examples-of-native-mode-installation"></a>기본 모드 설치 예  
  
```  
Setup.exe /q /ACTION="Install" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Replication,SNAC,SNAC_SDK,Browser,Writer,AS,IS,MDS,Adv_SSMS,BC,BOL,Conn,SDK,DReplay_CTLR,DReplay_CLT,DQC,BIDS,FullText, RS,DQ,SSMS" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SQLSVCACCOUNT="[Account Name]" /SQLSVCPASSWORD="********" /AGTSVCACCOUNT="[Account Nam]" /AGTSVCPASSWORD="********" /CTLRSVCACCOUNT="[Account Nam]" /CTLRSVCPASSWORD="********" /CLTSVCACCOUNT="[Account Nam]" /CLTSVCPASSWORD="********" /ASSVCACCOUNT="[Account Nam]" /ASSVCPASSWORD="********" /RSSVCACCOUNT="[Account Nam]" /RSSVCPASSWORD="********" /FTSVCACCOUNT="[Account Nam]" /FTSVCPASSWORD="********" /SECURITYMODE="SQL" /SAPWD="********" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Nam]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSINSTALLMODE="DefaultNativeMode"  
```  
  
## <a name="see-also"></a>참고 항목  
 [명령 프롬프트에서 SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [SysPrep 매개 변수](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#SysPrep)   
 [명령 프롬프트에서 PowerPivot 설치](../../sql-server/install/install-powerpivot-from-the-command-prompt.md)  
  
  
