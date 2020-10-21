---
description: 파일만 설치(Reporting Services)
title: 파일만 설치(Reporting Services) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- files-only installation [Reporting Services]
- installation options [Reporting Services]
ms.assetid: bdc74a8f-046c-4aa0-bfbd-4f1711dfb9ce
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5480e7b56f1ebaae56d30be0b0027a989d6ff816
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91933489"
---
# <a name="files-only-installation-reporting-services"></a>파일만 설치(Reporting Services)
  *파일만 설치* 는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 프로그램 파일에 대한 폴더 구조 만들기, 디스크로 파일 복사, 로컬 컴퓨터에 보고서 서버 서비스 등록, 서비스 계정 구성, 서비스 계정에 파일 권한 부여 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 공급자 등록 등의 작업을 설치 프로그램에서 수행하는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 의미합니다.  
  
 파일만 설치에는 보고서 서버 서비스(보고서 서버 웹 서비스 및 백그라운드 처리 애플리케이션을 호스트함), 보고서 작성기, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 명령줄 유틸리티(rsconfig.exe, rskeymgmt.exe 및 rs.exe)와 같은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능이 포함됩니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]와 같은 공유 기능에는 적용되지 않습니다. 따라서 공유 기능을 설치하려면 별도의 항목으로 지정해야 합니다.  
  
 다른 설치 모드와는 반대로 파일만 모드에서 설치되는 보고서 서버는 설치 후 작동하지 않습니다. 보고서 서버를 온라인 상태로 전환하려면 [보고서 서버 구성 관리자&#40;기본 모드&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)를 사용한 추가 구성이 필요합니다.  
  
## <a name="when-to-select-files-only-installation-mode"></a>파일만 설치 모드를 선택하는 경우  
 다음과 같은 경우 파일만 설치를 수행해야 합니다.  
  
-   원격 보고서 서버 데이터베이스에 보고서 서버를 연결하려는 경우  
  
-   보고서 서버를 명명된 인스턴스로 설치하려는 경우  
  
-   사용자 지정 설정 또는 기능 사용을 비롯한 배포 요구 사항이 있으며 서버 구성 시기와 방법을 완전히 제어하려는 경우  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 포함하는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]장애 조치(Failover) 클러스터를 설치하려는 경우  
  
## <a name="how-to-perform-a-files-only-installation"></a>파일만 설치를 수행하는 방법  
 파일만 설치는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 기본값입니다.  
  
 파일만 설치는 명령줄 또는 설치 마법사를 통해 지정할 수 있습니다. 다음 항목에서는 단계별 지침을 제공합니다.  
  
-   [설치 마법사에서 SQL Server 설치 &#40;Setup&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
-   [방법: 명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
#### <a name="example-command-line-script"></a>명령줄 스크립트 예  
 의미를 명확하게 전달하기 위해 이 예에는 /RSINSTALLMODE="FilesOnlyMode"가 포함되어 있습니다. 그러나 파일만 모드는 기본값이므로 생략해도 파일만 모드 설치를 사용할 수 있습니다.  
  
```  
setup /q /ACTION=install /FEATURES=RS /InstanceName=MSSQLSERVER /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /RSINSTALLMODE="FilesOnlyMode"  
```  
  
#### <a name="installation-wizard"></a>설치 마법사  
 기능 선택 페이지에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 선택하면 설치 모드를 지정할 수 있는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 페이지가 표시됩니다. 파일만 설치를 지정하려면 **구성 페이지에서** 보고서 서버를 설치하지만 구성하지는 않습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 설치 확인](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
 [보고서 서버 서비스 계정 구성&#40;보고서 서버 구성 관리자&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [보고서 서버 URL 구성&#40;보고서 서버 구성 관리자&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [보고서 서버 데이터베이스 연결 구성&#40;보고서 서버 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

 [Reporting Services SharePoint 모드 설치](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   

::: moniker-end

 [Reporting Services 기본 모드 보고서 서버 설치](~/reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)   
 [Reporting Services 도구](../../reporting-services/tools/reporting-services-tools.md)  
  
  

