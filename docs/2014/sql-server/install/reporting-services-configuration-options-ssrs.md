---
title: Reporting Services 구성 옵션 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.ins.instwizard.reportserverinstoptions.f1
helpviewer_keywords:
- Report Server Installation Options page [SQL Server Installation Wizard]
- report servers [Reporting Services], installing
- SQL Server Installation Wizard, Report Server Installation Options page
ms.assetid: e4561f6c-bc7f-467e-821a-cde8e5cd7391
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9afc4e179807d6cc10925d4fb4964cea857427d7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185343"
---
# <a name="reporting-services-configuration-options-ssrs"></a>Reporting Services 구성 옵션(SSRS)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사의 **Reporting Services 구성** 페이지를 사용하여 보고서 서버의 설치 및 구성 방법을 지정할 수 있습니다. 사용 가능한 설치 옵션은 이전에 **기능 선택** 페이지에서 선택한 옵션과 보고서 서버 설치 시 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 로컬 인스턴스도 함께 설치하는지 여부에 따라 달라집니다.  
  
 경우에 따라 컴퓨터에 SSL(Secure Sockets Layer) 인증서가 설치되어 강력한 와일드카드에 바인딩되어 있는 경우 설치 프로그램이 HTTPS 접두사를 사용하여 Reporting Services URL을 만듭니다. 인증서 Reporting Services Url에 매핑되는 방법에 대 한 자세한 내용은 참조 하세요. [Secure Sockets Layer (SSL) 연결에 대 한 보고서 서버 구성](http://go.microsoft.com/fwlink/?LinkId=199089) (http://go.microsoft.com/fwlink/?LinkId=199089) SQL Server 온라인 설명서의 합니다.  
  
 최신 정보에 대 한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치 및이 릴리스의 구성 내용과 [추가 설치 정보](http://go.microsoft.com/fwlink/?LinkId=207425) (http://go.microsoft.com/fwlink/?LinkId=207425)합니다.  
  
## <a name="options"></a>변수  
  
### <a name="reporting-services-native-mode"></a>Reporting Services 기본 모드  
 하나 이상의 요구 사항이 충족되지 않아 설치 프로그램이 기본 보고서 서버 구성을 수행할 수 없는 경우 설치 마법사는 최소 설치 옵션만 사용할 수 있습니다. 필요에 따라 파일을 복사할 수 있지만 설치가 완료된 후에는 Reporting Services 구성 관리자를 사용해야 기본 모드 보고서 서버를 구성할 수 있습니다.  
  
> [!NOTE]  
>  기본 설치 옵션 중 하나를 선택할 경우 기존 보고서 서버 데이터베이스 파일로 인해 설치 프로그램이 실패할 수 있습니다. 기본 설치 옵션을 선택하면 설치 프로그램에서 기본 이름을 사용하여 보고서 서버 데이터베이스를 만듭니다. 해당 이름의 데이터베이스가 이미 있는 경우 설치 프로그램이 실패하며 설치를 롤백해야 합니다. 이 문제를 방지하려면 설치 프로그램을 실행하기 전에 기존 데이터베이스의 이름을 바꾸거나 **설치만** 옵션을 선택하여 설치가 완료된 다음 사용자 지정 데이터베이스 설정을 지정할 수 있도록 합니다.  
  
#### <a name="install-and-configure"></a>설치 및 구성  
 기본 모드에서 보고서 서버 데이터베이스, 서비스 계정 및 URL 예약에 대한 기본값을 사용하여 보고서 서버 인스턴스를 설치합니다. 이 옵션을 선택하면 설치 후 보고서 서버 인스턴스를 바로 사용할 수 있습니다. 설치 프로그램은 로컬 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 사용하여 보고서 서버 데이터베이스를 만들고 기본값을 사용하도록 보고서 서버를 구성합니다.  
  
 보고서 서버 설치에 사용되는 기본값이 시스템에 적합한 경우에만 이 옵션을 사용할 수 있습니다. 로컬에서 모든 구성 요소를 설치하는 개발자와 소프트웨어를 평가하는 사용자의 경우 이 옵션을 사용하는 것이 좋습니다.  
  
 설치에 사용하는 기본 설정에 대한 정보를 검토하거나 기본 구성을 설치할 수 없는 이유를 알아 보려면 **자세히**를 클릭합니다. 기본 모드 보고서 서버용 기본 구성에 대 한 자세한 내용은 참조 하세요. [Native Mode Installation (Reporting Services)에 대 한 기본 구성을](http://go.microsoft.com/fwlink/?LinkId=199091) (http://go.microsoft.com/fwlink/?LinkId=199091)합니다.  
  
#### <a name="install-only"></a>설치만  
 보고서 서버 프로그램 파일을 설치하고 보고서 서버 서비스 계정을 만든 다음 보고서 서버 WMI(Windows Management Instrumentation) 공급자를 등록합니다. 이 설치 옵션은 "파일만" 설치라고도 합니다. 기본 구성을 사용하지 않으려면 이 옵션을 선택합니다. 기본 구성을 설치할 수 없거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 포함된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]장애 조치 클러스터를 설치하는 경우에는 이 옵션만 사용할 수 있습니다. 파일만 설치에 대 한 자세한 내용은 참조 하세요. [파일만 설치 (Reporting Services)](http://go.microsoft.com/fwlink/?LinkId=199093) (http://go.microsoft.com/fwlink/?LinkId=199093)합니다.  
  
 설치가 완료된 후 보고서 서버 데이터베이스를 만들고 보고서 서버를 사용할 수 있도록 구성합니다. 보고서 서버를 구성하고 데이터베이스를 만들려면 Reporting Services 구성 관리자를 사용합니다. 자세한 내용은 참조 하세요. [방법: 보고서 서버 데이터베이스 (Reporting Services Configuration)를 만듭니다](http://go.microsoft.com/fwlink/?LinkId=199094) (http://go.microsoft.com/fwlink/?LinkId=199094) 및 [보고서 서버 데이터베이스 연결을 구성할](http://go.microsoft.com/fwlink/?LinkId=199095) (http://go.microsoft.com/fwlink/?LinkId=199095)합니다.  
  
### <a name="reporting-services-sharepoint-mode"></a>Reporting Services SharePoint 모드  
  
#### <a name="install-only"></a>설치만  
 보고서 서버 프로그램 파일과 PowerShell cmdlet을 설치합니다. 설치가 완료된 후에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 서비스를 시작하고 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램을 만들어야 합니다. 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [Reporting Services SharePoint 모드 보고서 서버 설치 Power View 및 데이터 경고에 대 한](http://go.microsoft.com/fwlink/?LinkId=207543) (http://go.microsoft.com/fwlink/?LinkId=207543)합니다.  
  
-   [Reporting Services SharePoint 모드 단일 서버 팜으로 설치](http://go.microsoft.com/fwlink/?LinkId=207544) (http://go.microsoft.com/fwlink/?LinkId=207544)합니다.  
  
-   [Reporting Services 보고서 서버 (SSRS)](http://go.microsoft.com/fwlink/?LinkID=207244) (http://go.microsoft.com/fwlink/?LinkID=207244)합니다.  
  
## <a name="installing-the-reporting-services-add-in-for-sharepoint-technologies"></a>SharePoint 기술용 Reporting Services 추가 기능 설치  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 릴리스부터 이 추가 기능은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사의 기능 선택 페이지에서 SQL Server 설치의 일부로 설치할 수 있습니다.  
  
 그러나 다음 방법 중 하나를 사용하여 SharePoint 2010용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 설치할 수 있습니다.  
  
-   SharePoint 2010 제품 준비 도구인 **PreRequisiteInstaller.exe**를 실행합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어에서 설치합니다. **설치가 끝난 후** 설치 미디어의 Setup 폴더에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rsSharePoint.msi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 파일을 클릭합니다.  
  
-   추가 기능을 다운로드하고 설치합니다. 자세한 내용은 [SharePoint 제품용 Reporting Services 추가 기능 검색 위치](http://go.microsoft.com/fwlink/?LinkID=208634) (http://go.microsoft.com/fwlink/?LinkID=208634)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 관리자 시작](http://go.microsoft.com/fwlink/?LinkId=199096)   
 [Create a Report Server Database (Reporting Services 구성)](http://go.microsoft.com/fwlink/?LinkId=199094)   
 [Reporting Services 업그레이드 및 마이그레이션](http://go.microsoft.com/fwlink/?LinkID=245628)   
 [Reporting Services SharePoint 모드 및 기본 모드의 명령 프롬프트 설치](http://go.microsoft.com/fwlink/?LinkId=217620)  
  
  
