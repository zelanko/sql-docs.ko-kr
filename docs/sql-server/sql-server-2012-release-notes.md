---
title: "SQL Server 2012 릴리스 정보 | Microsoft 문서"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Release Notes, SQL Server
ms.assetid: 9ccb390a-67a9-4593-85ea-2b4c41c4620f
caps.latest.revision: "21"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e7adc5d4b4fdcf8886b2c8d08bce8de90d9b3eb1
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-2012-release-notes"></a>SQL Server 2012 릴리스 정보
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)] 이 릴리스 정보 문서에서는 Microsoft SQL Server 2012([다운로드하려면 여기를 클릭](http://go.microsoft.com/fwlink/?LinkId=238647))를 설치하거나 문제를 해결하기 전에 읽어야 할 알려진 문제에 대해 설명합니다. 이 릴리스 정보 문서는 정기적으로 업데이트되며 온라인으로만 사용할 수 있고 설치 미디어에는 포함되지 않습니다.  
  
SQL Server 2012를 시작하고 설치하는 방법은 SQL Server 2012 추가 정보를 참조하십시오. 추가 정보 문서는 설치 미디어에 포함되어 있거나 [추가 정보](http://download.microsoft.com/download/3/B/D/3BD9DD65-D3E3-43C3-BB50-0ED850A82AD5/ENU/Readme.htm) 다운로드 페이지에서 다운로드할 수 있습니다. 또한 [SQL Server 온라인 설명서](http://go.microsoft.com/fwlink/?LinkId=190948) 및 [SQL Server 포럼](http://go.microsoft.com/fwlink/?LinkId=213599)에서 자세한 내용을 볼 수 있습니다.  
  
## <a name="Install"></a>1.0 시작하기 전  
[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]를 설치하기 전에 다음 정보를 고려하십시오.  
  
### <a name="11-rules-documentation-for-sql-server-2012-setup"></a>1.1 SQL Server 2012 설치 프로그램에 대한 규칙 설명서  
**문제:** SQL Server 설치 프로그램은 설치 작업이 완료되기 전에 컴퓨터 구성의 유효성을 검사합니다. SQL Server 설치 작업 중에 실행되는 다양한 규칙은 SCC(시스템 구성 검사기) 보고서를 사용하여 캡처됩니다. 이러한 설치 규칙에 대한 설명서는 MSDN 라이브러리에서 더 이상 제공되지 않습니다.  
  
**해결 방법:** 이러한 설치 규칙에 대한 자세한 내용은 시스템 구성 검사 보고서를 참조할 수 있습니다. 시스템 구성 검사에서는 각 실행 규칙에 대한 간단한 설명과 실행 상태를 포함하는 보고서를 생성합니다. 시스템 구성 검사 보고서는 %programfiles%\Microsoft SQL Server\110\Setup Bootstrap\Log\\\<YYYYMMDD_HHMM>\\에 있습니다.  
  
### <a name="12-adding-a-local-user-account-for-the-distributed-replay-controller-service-might-terminate-setup-unexpectedly"></a>1.2 Distributed Replay Controller 서비스의 로컬 사용자 계정을 추가하면 설치가 갑자기 종료될 수 있음  
**문제:** SQL Server 설치 프로그램의 **Distributed Replay Controller** 페이지에서 Distributed Replay Controller 서비스의 로컬 사용자 계정을 추가하려고 하면 “SQL Server 설치 오류” 오류 메시지와 함께 설치 프로그램이 갑자기 종료됩니다.  
  
**해결 방법:** SQL 설치 중에 “현재 사용자 추가” 또는 “추가…”를 통해 로컬 사용자 계정을 추가하지 마세요. 설치가 끝나면 다음 단계를 사용하여 로컬 사용자 계정을 수동으로 추가합니다.  
  
1.  SQL Server Distributed Replay Controller 서비스를 중지합니다.  
  
2.  Controller 서비스가 설치된 컨트롤러 컴퓨터에서 명령 프롬프트에 dcomcnfg를 입력합니다.  
  
3.  구성 요소 서비스 창에서 **콘솔 루트** -> **구성 요소 서비스** -> **컴퓨터** -> **내 컴퓨터** -> **Dconfig** ->**DReplayController**로 이동합니다.  
  
4.  **DReplayController**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
5.  **DReplayController 속성** 창의 **보안** 탭에 있는 **시작 및 활성화 권한** 섹션에서 **편집** 을 클릭합니다.  
  
6.  로컬 사용자 계정에 **로컬 및 원격 활성화** 권한을 부여한 다음 **확인**을 클릭합니다.  
  
7.  액세스 권한 섹션에서 **편집** 을 클릭하고 로컬 사용자 계정에 **로컬 및 원격 액세스** 권한을 부여한 다음 **확인**을 클릭합니다.  
  
8.  **확인** 을 클릭하여 **DReplayController 속성** 창을 닫습니다.  
  
9. 컨트롤러 컴퓨터에서 로컬 사용자 계정을 **Distributed COM Users** 그룹에 추가합니다.  
  
10. SQL Server Distributed Replay Controller 서비스를 시작합니다.  
  
### <a name="13-sql-server-setup-might-fail-while-trying-to-start-the-sql-server-browser-service"></a>1.3 SQL Server 설치 프로그램이 SQL Server Browser 서비스를 시작하려는 동안 실패할 수 있음  
**문제:** SQL Server 설치 프로그램이 SQL Server Browser 서비스를 시작하려는 동안 다음과 유사한 오류로 인해 실패할 수 있습니다.  
  
<pre>The following error has occurred:  
Service 'SQLBrowser' start request failed. Click 'Retry' to retry the failed action, or click 'Cancel' to cancel this action and continue setup.</pre>  
  
또는  
  
<pre>The following error has occurred:  
SQL Server Browser configuration for feature 'SQL_Browser_Redist_SqlBrowser_Cpu32' was cancelled by user after a previous installation failure. The last attempted step: Starting the SQL Server Browser service 'SQLBrowser', and waiting for up to '900' seconds for the process to complete.</pre>  
  
**해결 방법:** 이 문제는 SQL Server 엔진 또는 Analysis Services가 설치되지 못할 때 발생할 수 있습니다. 이 문제를 해결하려면 SQL Server 설치 로그를 참조하고 SQL Server 엔진 및 Analysis Services 실패를 해결합니다. 자세한 내용은 SQL Server 설치 로그 파일 보기 및 읽기를 참조하십시오. 자세한 내용은 [View and Read SQL Server Setup Log Files](http://msdn.microsoft.com/library/ms143702(SQL.110).aspx)을 참조하세요.  
  
### <a name="14-sql-server-2008-2008-r2-analysis-services-failover-cluster-upgrade-to-sql-server-2012-might-fail-after-renaming-the-network-name"></a>1.4 네트워크 이름을 바꾼 후 SQL Server 2008, 2008 R2 Analysis Services 장애 조치(Failover) 클러스터가 SQL Server 2012로 업그레이드되지 않을 수 있음  
**문제:** Windows 클러스터 관리 도구를 사용하여 Microsoft SQL Server 2008 또는 Microsoft SQL Server 2008 R2 Analysis Services 장애 조치(Failover) 클러스터의 네트워크 이름을 변경하고 나면 업그레이드 작업에 실패할 수도 있습니다.  
  
**해결 방법:** 이 문제를 해결하려면 [기술 자료 문서](http://support.microsoft.com/kb/955784)의 해결 방법 섹션에 있는 지침에 따라 ClusterName 레지스트리 항목을 업데이트하세요.  
  
### <a name="15-installing-sql-server-2012-on-windows-server-2008-r2-server-core-service-pack-1"></a>1.5 Windows Server 2008 R2 Server Core 서비스 팩 1에서 SQL Server 2012 설치  
Windows Server 2008 R2 Server Core SP1에 SQL Server를 설치할 수 있습니다. 단, 다음과 같은 제한 사항이 있습니다.  
  
-   Microsoft SQL Server 2012는 Server Core 운영 체제의 설치 마법사를 사용하는 설치를 지원하지 않습니다. Server Core에서 설치할 때 SQL Server 설치는 /Q 매개 변수를 사용하는 완전 자동 모드 또는 /QS 매개 변수를 사용하는 단순 자동 모드를 지원합니다.  
  
-   Windows Server 2008 R2 Server Core SP1을 실행하는 컴퓨터에서 이전 버전의 SQL Server를 Microsoft SQL Server 2012로 업그레이드하는 것은 지원되지 않습니다.  
  
-   Windows Server 2008 R2 Server Core SP1을 실행하는 컴퓨터에서 Microsoft SQL Server 2012의 32비트 버전을 설치하는 것은 지원되지 않습니다.  
  
-   Microsoft SQL Server 2012는 Windows Server 2008 R2 Server Core SP1을 실행하는 컴퓨터에서 이전 버전의 SQL Server와 함께 설치할 수 없습니다.  
  
-   SQL Server 2012의 일부 기능은 Server Core 운영 체제에서 지원되지 않습니다. 지원되는 기능 및 Server Core에 SQL Server 2012 설치에 대한 자세한 내용은 [Server Core에 SQL Server 2012 설치](http://msdn.microsoft.com/library/hh231669(SQL.110).aspx)를 참조하세요.  
  
### <a name="16-semantic-search-requires-you-to-install-an-additional-dependency"></a>1.6 의미 체계 검색을 위한 추가 종속성 설치  
**문제:** 통계 의미 체계 검색에는 의미 체계 언어 통계 데이터베이스라고 하는 추가적인 필수 구성 요소가 있으며, 이는 SQL Server 설치 프로그램으로 설치되지 않습니다.  
  
**해결 방법:** 의미 체계 언어 통계 데이터베이스를 의미 체계 인덱싱을 위한 필수 구성 요소로 설정하려면 다음 태스크를 수행합니다.  
  
1.  SQL Server 설치 미디어에서 SemanticLanguageDatabase.msi라는 Windows Installer 패키지를 찾아 실행하여 데이터베이스를 추출합니다. SQL Server 2012 Express의 경우 의미 체계 언어 통계 데이터베이스를 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=35582) (http://go.microsoft.com/fwlink/?LinkId=221787)에서 다운로드하고 Windows Installer 패키지를 실행하세요.  
  
2.  데이터베이스를 적절한 데이터 폴더로 이동합니다. 데이터베이스를 기본 위치에 두는 경우 연결하기 전에 권한을 변경해야 합니다.  
  
3.  추출한 데이터베이스를 연결합니다.  
  
4.  저장 프로시저 **sp_fulltext_semantic_register_language_statistics_db** 를 호출하고 연결 시 데이터베이스에 지정한 이름을 제공하여 데이터베이스를 등록합니다.  
  
이러한 작업을 완료하지 않으면 의미 체계 인덱스를 만들려고 할 때 다음과 같은 오류 메시지가 표시됩니다.  
  
<pre>Msg 41209, Level 16, State 3, Line 1  
A semantic language statistics database is not registered. Full-text indexes using 'STATISTICAL_SEMANTICS' cannot be created or populated.</pre>  
  
### <a name="17-installation-prerequisite-handling-during-sql-server-2012-setup"></a>1.7 SQL Server 2012 설치 중 설치 필수 구성 요소 처리  
다음 항목은 SQL Server 2012 설치 중 필수 구성 요소 설치 동작에 대해 설명합니다.  
  
-   SQL Server 2012 설치는 Windows 7 SP1 또는 Windows Server 2008 R2 SP1에서만 지원됩니다. 그러나 설치 프로그램은 Windows 7 또는 Windows Server 2008 R2에서 SQL Server 2012 설치를 차단하지 않습니다.  
  
-   .NET Framework 3.5 SP1은 데이터베이스 엔진, 복제, MDS(Master Data Services), Reporting Services, DQS(Data Quality Services) 또는 SQL Server Management Studio 선택 시 SQL Server 2012에 대한 요구 사항이며 프레임워크는 더 이상 SQL Server 설치 프로그램에 의해 설치되지 않습니다.  
  
    -   Windows Vista SP2 또는 Windows Server 2008 SP2 운영 체제가 설치된 컴퓨터에서 설치 프로그램을 실행하고 .NET Framework 3.5 SP1이 설치되어 있지 않은 경우 SQL Server 설치 프로그램을 실행하려면 SQL Server 설치를 계속하기 전에 .NET Framework 3.5 SP1을 다운로드하여 설치해야 합니다. Windows 업데이트에서나 [여기](https://www.microsoft.com/download/details.aspx?id=25150)에서 직접 .NET Framework 3.5 SP1을 다운로드할 수 있습니다. SQL Server 설치 동안 중단을 방지하기 위해 SQL Server 설치를 실행하기 전에 .NET Framework 3.5 SP1을 다운로드하여 설치할 수 있습니다.  
  
    -   Windows 7 SP1 또는 Windows Server 2008 R2 SP1 운영 체제가 설치된 컴퓨터에서 설치 프로그램을 실행하는 경우 SQL Server 2012를 설치하기 전에 .NET Framework 3.5 SP1을 활성화해야 합니다.  
  
        **다음 방법 중 하나를 사용하여 Windows Server 2008 R2 SP1에 .NET Framework 3.5 SP1을 활성화할 수 있습니다.**  
  
        방법 1: 서버 관리자 사용  
  
        1.  서버 관리자에서 **기능 추가** 를 클릭하여 가능한 기능의 목록을 표시합니다.  
  
        2.  **기능 선택** 인터페이스에서 **.NET Framework 3.5.1 기능** 항목을 확장합니다.  
  
        3.  **.NET Framework 3.5.1 기능**을 확장한 후 확인란이 두 개 표시됩니다. 한 확인란은 .NET Framework 3.5.1용이고 다른 확인란은 WCF 활성화용입니다. **.NET Framework 3.5.1**을 선택하고 **다음**을 클릭합니다. 필요한 역할 서비스와 기능을 설치하지 않은 경우에는 .NET Framework 3.5.1 기능을 설치할 수 없습니다.  
  
        4.  **설치 선택 확인**에서 선택 내용을 검토한 다음 설치를 클릭합니다.  
  
        5.  설치 과정이 완료되면 **닫기**를 클릭합니다.  
  
        방법 2: Windows PowerShell 사용  
  
        1.  **시작** | **모든 프로그램** | **보조프로그램**을 클릭합니다.  
  
        2.  **Windows PowerShell**을 확장하고 **Windows PowerShell**을 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다. **사용자 계정 컨트롤** 상자에서 **예** 를 클릭합니다.  
  
        3.  PowerShell 명령 프롬프트에서 다음 명령을 입력하고 각 명령 다음에 Enter 키를 누릅니다.  
  
            ```  
            Import-Module ServerManager  
            Add-WindowsFeature as-net-framework  
            ```  
  
        **다음 방법을 사용하여 Windows 7 SP1에서 .NET Framework 3.5 SP1을 활성화할 수 있습니다.**  
  
        1.  **시작** | **제어판** | **프로그램**을 차례로 클릭한 다음 **Windows 기능 사용/사용 안 함**을 클릭합니다. 관리자 암호를 묻거나 암호를 확인하는 메시지가 표시되면 암호를 입력하거나 확인합니다.  
  
        2.  **Microsoft .NET Framework 3.5.1**을 사용하도록 설정하려면 기능 옆의 확인란을 선택합니다. Windows 기능을 끄려면 해당 확인란의 선택을 취소합니다.  
  
        3.  **확인**을 클릭합니다.  
  
        **배포 이미지 서비스 및 관리(DISM.exe)를 사용하여 .NET Framework 3.5 SP1을 활성화할 수 있습니다.**  
  
        배포 이미지 서비스 및 관리(DISM.exe)를 사용하여 .NET Framework 3.5 SP1을 활성화할 수도 있습니다. Windows 기능을 온라인으로 사용하도록 설정하는 방법은 [Windows 기능을 온라인으로 사용하거나 사용하지 않도록 설정](http://technet.microsoft.com/library/dd744582(WS.10).aspx)을 참조하세요. 다음은 .NET Framework 3.5 SP1 활성화 지침입니다.  
  
        1.  명령 프롬프트에 다음 명령을 입력하여 운영 체제에서 사용할 수 있는 모든 기능을 나열합니다.  
  
            ```  
            sm /online /Get-Features  
            ```  
  
        2.  옵션: 명령 프롬프트에 다음 명령을 입력하여 관심 있는 특정 기능에 대한 정보를 나열합니다.  
  
            ```  
            Dism /online /Get-FeatureInfo /FeatureName:NetFx3  
            ```  
  
        3.  다음 명령을 입력하여 Microsoft .NET Framework 3.5.1을 활성화합니다.  
  
            ```  
            Dism /online /Enable-Feature /FeatureName:NetFx3  
            ```  
  
-   .NET Framework 4는 SQL Server 2012의 요구 사항입니다. SQL Server 설치 프로그램은 기능 설치 단계에서 .NET Framework 4를 설치합니다.  
  
    Windows Server 2008 R2 SP1 Server Core 운영 체제에 설치하는 경우 SQL Server 2012 Express는 .NET Framework 4를 설치하지 않습니다. SQL Server 2012 Express(데이터베이스만)를 설치하는 경우 .NET Framework 3.5 SP1이 있으면 .NET Framework 4가 필요하지 않습니다. .NET Framework 3.5 SP1이 없거나 SQL Server 2012 Management Studio Express, SQL Server 2012 Express with Tools 또는 SQL Server 2012 Express with Advanced Services를 설치할 때 Windows Server 2008 R2 SP1 Server Core 운영 체제에 SQL Server2012 Express를 설치하기 전에 .NET Framework 4를 설치해야 합니다.  
  
-   Visual Studio 구성 요소가 올바르게 설치될 수 있도록 하려면 SQL Server에서 업데이트를 설치해야 합니다. SQL Server 설치 프로그램에서 이 업데이트가 있는지 확인한 다음 SQL Server 설치를 계속하기 전에 업데이트를 다운로드하고 설치해야 합니다. SQL Server를 설치하는 동안 작업이 중단되는 것을 방지하려면 아래에 설명된 대로 SQL Server 설치 프로그램을 실행하기 전에 업데이트를 다운로드하고 설치할 수 있습니다(또는 Windows Update에 사용 가능한 .NET Framework 3.5 SP1의 모든 업데이트를 설치할 수 있습니다).  
  
    -   Windows Vista SP2 또는 Windows Server 2008 SP2 운영 체제가 설치된 컴퓨터에 SQL Server 2012를 설치하는 경우 필요한 업데이트를 [여기](http://support.microsoft.com/?kbid=956250)에서 얻을 수 있습니다.  
  
    -   Windows 7 SP1 또는 Windows Server 2008 R2 SP1 운영 체제가 설치된 컴퓨터에 SQL Server 2012를 설치하는 경우 컴퓨터에 이 업데이트가 이미 설치되어 있습니다.  
  
-   Windows PowerShell 2.0은 SQL Server 2012 데이터베이스 엔진 구성 요소 및 SQL Server Management Studio를 설치하기 위한 필수 구성 요소이지만 Windows PowerShell은 더 이상 SQL Server 설치 프로그램으로 설치되지 않습니다. PowerShell 2.0이 컴퓨터에 설치되어 있지 않은 경우 [Windows 관리 프레임워크](http://support.microsoft.com/kb/968929) 페이지에 나오는 지침에 따라 PowerShell 2.0을 사용하도록 설정할 수 있습니다. Windows PowerShell 2.0을 얻는 방법은 실행 중인 운영 체제에 따라 달라집니다.  
  
    -   Windows Server 2008 – Windows PowerShell 1.0은 기능이며 추가할 수 있습니다. Windows PowerShell 2.0 버전은 다운로드하여 설치합니다(OS 패치로 유효함).  
  
    -   Windows 7/Windows Server 2008 R2 – Windows PowerShell 2.0은 기본적으로 설치됩니다.  
  
-   SharePoint 환경에서 SQL Server 2012의 기능을 사용하려는 경우 SharePoint Server 2010 SP1(서비스 팩 1) 및 SharePoint 8월 누적 업데이트가 필요합니다. SQL Server 2012 기능을 팜에 추가하기 전에 SP1 및 SharePoint [8월 누적 업데이트](http://blogs.technet.com/b/stefan_gossner/archive/2010/09/02/august-2010-cumulative-update-for-sharepoint-has-been-released.aspx)를 설치하고 서버 팜을 완전히 패치해야 합니다. 이러한 요구 사항은 다음의 SQL Server 2012 기능에 적용됩니다. 팜의 데이터베이스 서버로 데이터베이스 엔진의 인스턴스 사용, SharePoint용 PowerPivot 구성 또는 SharePoint 모드에서 Reporting Services 배포에 적용됩니다.  
  
### <a name="18-supported-operating-systems-for-sql-server-2012"></a>1.8 SQL Server 2012에서 지원되는 운영 체제  
SQL Server 2012는 Windows Vista SP2, Windows Server 2008 SP2, Windows 2008 R2 SP1 및 Windows 7 SP1 운영 체제에서 지원됩니다.  
  
### <a name="19-sync-framework-is-not-included-in-the-installation-package"></a>1.9 Sync Framework가 설치 패키지에 포함되지 않음  
**문제:** Sync Framework가 SQL Server 2012 설치 패키지에 포함되어 있지 않습니다.  
  
**해결 방법:** [Microsoft 다운로드 센터 페이지](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=23217)에서 적합한 Sync Framework 버전을 다운로드할 수 있습니다.  
  
### <a name="110-if-visual-studio-2010-service-pack-1-is-uninstalled-the-sql-server-2012-instance-must-be-repaired-to-restore-certain-components"></a>1.10 Visual Studio 2010 서비스 팩 1이 제거된 경우 SQL Server 2012 인스턴스를 복구하여 특정 구성 요소를 복원해야 함  
**문제:**[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 설치는 Visual Studio 2010 서비스 팩 1의 일부 구성 요소에 종속되어 있습니다. 서비스 팩 1을 제거하면 공유 구성 요소 중 일부가 원래 버전으로 다운그레이드되고 몇몇 다른 구성 요소가 컴퓨터에서 완전히 제거됩니다.  
  
**해결 방법:** 원래 원본 미디어 또는 네트워크 설치 위치에서 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 인스턴스를 복구합니다.  
  
1.  SQL Server 설치 미디어에서 SQL Server 설치 프로그램(setup.exe)을 실행합니다.  
  
2.  필수 구성 요소 및 시스템 확인이 끝나면 설치 프로그램에 **SQL Server 설치 센터** 페이지가 표시됩니다.  
  
3.  왼쪽의 탐색 영역에서 **유지 관리** 를 클릭한 다음 **복구** 를 클릭하여 복구 작업을 시작합니다. **시작** 메뉴를 사용하여 설치 센터를 시작한 경우 지금은 설치 미디어의 위치를 제공해야 합니다.  
  
4.  시스템에 필수 구성 요소가 설치되어 있고 컴퓨터가 설치 유효성 검사 규칙을 통과하는지 확인하기 위해 설치 지원 규칙 및 파일 루틴이 실행됩니다. 계속하려면 **확인** 또는 **설치** 를 클릭합니다.  
  
5.  **인스턴스 선택** 페이지에서 복구할 인스턴스를 선택한 후 **다음** 을 클릭하여 계속합니다.  
  
6.  작업이 유효한지 검사하는 복구 규칙이 실행됩니다. 계속하려면 **다음**을 클릭합니다.  
  
7.  **복구 준비** 페이지에서 작업을 진행할 준비가 되었음을 알려 줍니다. 계속하려면 **복구**를 클릭합니다.  
  
8.  **복구 진행률** 페이지에 복구 작업 상태가 표시됩니다. **완료** 페이지에서 작업이 완료되었음을 알려 줍니다.  
  
SQL Server 인스턴스를 복구하는 방법에 대한 자세한 내용은 [실패한 SQL Server 2012 설치 복구](http://msdn.microsoft.com/library/cc646006(SQL.110).aspx)를 참조하세요.  
  
### <a name="111-an-instance-of-sql-server-2012-might-fail-after-an-os-upgrade"></a>1.11 OS 업그레이드 후 SQL Server 2012 인스턴스가 실패할 수 있음  
**문제:** 운영 체제를 Windows 7 SP1에서 Windows Vista로 업그레이드한 후 다음 오류로 인해 SQL Server 2012 인스턴스가 실패할 수 있습니다.  
  
`Setup has detected that the .NET Framework version 4 needs to be repaired. Do not restart your computer until Setup is complete.`  
  
**해결 방법**: 운영 체제를 업그레이드한 후 .NET Framework 4 설치를 복구합니다. 자세한 내용은 [.NET Framework의 기존 설치를 복구하는 방법](http://support.microsoft.com/kb/306160)을 참조하세요.  
  
### <a name="112-sql-server-edition-upgrade-requires-a-restart"></a>1.12 SQL Server 버전을 업그레이드하려면 다시 시작해야 함  
**문제**: SQL Server 2012 인스턴스 버전을 업그레이드하는 경우 새 버전과 관련된 일부 기능이 즉시 활성화되지 않을 수 있습니다.  
  
**해결 방법**: SQL Server 2012 인스턴스의 버전 업그레이드를 수행한 후 컴퓨터를 다시 시작합니다. SQL Server 2012에서 지원되는 업그레이드에 대한 자세한 내용은 [지원되는 버전 및 버전 업그레이드](http://msdn.microsoft.com/library/ms143393.aspx)를 참조하세요.  
  
### <a name="113-database-with-read-only-filegroup-or-files-cannot-be-upgraded"></a>1.13 읽기 전용 파일 그룹 또는 파일이 포함된 데이터베이스를 업그레이드할 수 없음  
**문제**: 파일/파일 그룹이 읽기 전용으로 설정된 경우 데이터베이스를 연결하거나 백업에서 데이터베이스를 복구하는 방식으로 데이터베이스를 업그레이드할 수 없습니다.  오류 3415가 반환됩니다.  이 문제는 SQL Server 인스턴스의 전체 업그레이드를 실행하는 경우에도 적용됩니다. 즉, SQL Server 2012를 설치하여 기존 SQL Server 인스턴스를 대체하려고 하는데 하나 이상의 기존 데이터베이스가 읽기 전용으로 설정되어 있습니다.  
  
**해결 방법:** 업그레이드하기 전에 데이터베이스 및 해당 파일/파일 그룹이 읽기/쓰기로 설정되어 있는지 확인합니다.  
  
### <a name="114-reinstalling-an-instance-of-sql-server-failover-custer-fails-if-you-use-the-same-ip-address"></a>1.14 동일한 IP 주소를 사용하는 경우 SQL Server 장애 조치(Failover) 클러스터 인스턴스의 다시 설치가 실패함  
**문제:** SQL Server 장애 조치(Failover) 클러스터 인스턴스를 설치하는 동안 잘못된 IP 주소를 지정하는 경우 설치에 실패합니다. 실패한 인스턴스를 제거한 후 올바른 IP 주소와 동일한 인스턴스 이름을 사용하여 SQL Server 장애 조치(Failover) 클러스터 인스턴스를 다시 설치하려고 하면 설치에 실패합니다. 이 오류는 이전 설치로 인해 중복된 리소스 그룹이 남겨졌기 때문에 발생합니다.  
  
**해결 방법:** 이 문제를 해결하려면 설치하는 동안 다른 인스턴스 이름을 사용하거나 다시 설치하기 전에 리소스 그룹을 수동으로 삭제합니다. 자세한 내용은 [SQL  Server  장애 조치(failover)  클러스터에서 노드 추가 또는 제거](http://msdn.microsoft.com/library/ms191545)를 참조하십시오.  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="AS"></a>2.0 Analysis Services  
  
### <a name="21-sql-editor-and-as-editor-cannot-connect-to-their-respective-server-instances-in-the-same-ssms-instance"></a>2.1 SQL 편집기 및 AS 편집기는 동일한 SSMS 인스턴스의 해당 서버 인스턴스에 연결할 수 없음  
**문제:** SQL 편집기가 이미 연결된 경우 MDX/DMX 편집기를 사용하여 Analysis Services 서버에 연결할 수 없습니다.  
  
SQL Server Management Studio 2012(SSMS)를 사용할 때 편집기에 .sql 파일이 열려 있고 SQL Server 인스턴스에 연결된 경우 동일한 SSMS 인스턴스에서 열린 MDX/ DMX 파일을 AS 서버 인스턴스에 연결할 수 없습니다. 마찬가지로 MDX 또는 DMX 파일이 SSMS의 편집기에서 열려 있고 AS 서버 인스턴스에 연결된 경우 동일한 SSMS 인스턴스에서 열린 .sql 파일은 SQL Server 인스턴스에 연결할 수 없습니다.  
  
**해결 방법**: 이 문제를 해결하려면 다음 옵션 중 하나를 사용하세요.  
  
-   SSMS의 다른 인스턴스를 시작하여 MDX / DMX 파일을 엽니다.  
  
-   SQL 편집기의 연결을 끊고 MDX/DMX 편집기를 AS 서버에 연결합니다.  
  
### <a name="22-cannot-create-or-open-tabular-projects-when-builtinadministrators-group-name-cannot-be-resolved"></a>2.2 BUILTIN\Administrators 그룹 이름을 확인할 수 없으면 테이블 형식 프로젝트를 만들거나 열 수 없음  
**문제:** 테이블 형식 프로젝트를 만들거나 열려면 작업 영역 데이터베이스 서버의 관리자여야 합니다. 사용자 이름 또는 그룹 이름을 추가하여 서버 관리자 그룹에 사용자를 추가할 수 있습니다. BUILTIN\Administrator 그룹의 멤버는 작업 영역 데이터베이스 서버가 원래 프로비전된 도메인에 조인되지 않는 한 BIM 파일을 만들거나 편집할 수 없습니다. BIM 파일을 열거나 만드는 경우 다음과 같은 오류 메시지가 나타나며 실패합니다.  
  
`"The BIM file cannot be opened. The server connected to is not valid. Reason: You are not an administrator of server [server name]."`  
  
**해결 방법:**  
  
-   작업 영역 데이터베이스 서버 및 SSDT(SQL Server Data Tools) 컴퓨터를 도메인에 다시 참가시킵니다.  
  
-   작업 영역 데이터베이스 서버 및/또는 SSDT 컴퓨터가 항상 도메인에 조인되지 않으면 작업 영역 데이터베이스 서버에 관리자로 BUILTIN\Administrators 그룹 대신에 개별 사용자 이름을 추가합니다.  
  
### <a name="23-ssis-components-for-as-tabular-models-do-not-work-as-expected"></a>2.3 AS 테이블 형식 모델의 SSIS 구성 요소가 예상대로 작동하지 않음  
AS(Analysis Services)의 SSIS(SQL Server Integration Services) 구성 요소가 테이블 형식 모델에 대해 예상대로 작동하지 않습니다. 다음은 테이블 형식 모델과 함께 작동하기 위해 SSIS 패키지를 쓰려고 시도할 때 발생할 수 있는 알려진 문제입니다.  
  
**문제:** AS 연결 관리자는 테이블 형식 모델을 데이터 원본과 동일한 솔루션에서 사용할 수 없습니다.  
  
**해결 방법:** AS 처리 태스크 또는 AS DDL 실행 태스크를 구성하기 전에 AS 서버에 명시적으로 연결해야 합니다.  
  
테이블 형식 모델과 함께 작업할 때 AS 처리 태스크에 문제가 있습니다.  
  
**:** 데이터베이스, 표, 파티션 대신에 큐브, 측정값 그룹 및 차원을 확인할 수 있습니다. 이것이 태스크의 제한 사항입니다.  
  
**해결 방법:** 큐브/측정값 그룹/차원 구조를 사용하여 여전히 테이블 형식 모델을 처리할 수 있습니다.  
  
**문제:** 테이블 형식 모드에서 실행되는 AS에 의해 지원되는 일부 처리 옵션이 조각 모음 처리와 같은 AS 처리 태스크에 표시되지 않습니다.  
  
**해결 방법:** Analysis Services DDL 실행 태스크를 대신 사용하여 ProcessDefrag 명령이 포함된 XMLA 스크립트를 실행합니다.  
  
**문제:** 도구의 일부 구성 옵션은 해당되지 않습니다. 예를 들어 파티션을 처리할 때 "처리 관련 개체"를 사용해서는 안 되며, "병렬 처리" 구성 옵션에는 표준 SKU에서 병렬 처리가 지원되지 않는다는 내용의 잘못된 오류 메시지가 포함됩니다.  
  
**해결 방법:** 없습니다.  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="BOL"></a>3.0 온라인 설명서  
  
### <a name="31-help-viewer-for-sql-server-crashes-in-environments-configured-to-run-only-ipv6"></a>3.1 IPv6만 실행하도록 구성된 환경에서 SQL Server 도움말 뷰어 충돌  
**문제:**IPv6만 실행하도록 환경이 구성된 경우 SQL Server 2012의 도움말 뷰어가 충돌하고 다음 오류 메시지가 표시됩니다.  
  
`HelpLibAgent.exe has stopped working.`  
  
> [!IMPORTANT]  
> 이는 IPv6만 실행하도록 설정된 모든 환경에 적용됩니다. IPv4(및 IPv6과 함께 사용되는 IPv4)가 활성화된 환경은 영향을 받지 않습니다.  
  
**해결 방법:**이 문제를 방지하려면 IPv4를 사용하도록 설정하거나 다음 단계를 사용하여 레지스트리 항목을 추가하고 ACL을 만들어 IPv6의 도움말 뷰어를 사용하도록 설정합니다.  
  
1.  이름이 “IPv6”이고 값이 “1(DWORD(32비트))”인 레지스트리 키를 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v1.0 아래에 만듭니다.  
  
2.  IPv6용 포트에 대해 보안 ACL을 설정하고 관리 CMD 창에서 다음을 실행합니다.  
  
    ```  
    netsh http add urlacl url=http://[::1]:47873/help/ sddl=D:(A;;GX;;;WD)  
    ```  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="DQS"></a>4.0 Data Quality Services  
  
### <a name="41-dqs-not-supported-in-a-cluster"></a>4.1 DQS는 클러스터에서 지원되지 않음  
**문제:** DQS는 SQL Server 클러스터 설치에서 지원되지 않습니다. SQL Server의 클러스터 인스턴스를 설치하려는 경우 **기능 선택** 페이지에서 **Data Quality Services** 및 **Data Quality Client** 확인란을 선택하지 않아야 합니다. 클러스터 인스턴스를 설치할 때 이 확인란을 선택하고 DQSInstaller.exe 파일을 실행하여 Data Quality 서버 설치를 완료하면 DQS가 이 노드에 설치되지만 클러스터에 노드를 추가할 경우 추가 노드에서 DQS를 사용할 수 없으므로 추가 노드에서 DQS가 작동하지 않습니다.  
  
**해결 방법:** 이 문제를 해결하려면 SQL Server 2012 누적 업데이트 1을 설치합니다. 자세한 내용은 [http://support.microsoft.com/kb/2674817](http://support.microsoft.com/kb/2674817)을 참조하세요.  
  
### <a name="42-to-reinstall-data-quality-server-delete-the-dqs-objects-after-uninstalling-data-quality-server"></a>4.2 Data Quality 서버를 다시 설치하려면 Data Quality 서버를 제거한 후 DQS 개체 삭제하기  
**문제:** Data Quality 서버를 제거하는 경우 SQL Server 인스턴스에서 DQS 개체(DQS 데이터베이스, DQS 로그인 및 DQS 저장 프로시저)가 삭제되지 않습니다.  
  
**해결 방법:** Data Quality 서버를 동일한 컴퓨터 및 동일한 SQL Server 인스턴스에 다시 설치하려면 SQL Server 인스턴스에서 DQS 개체를 수동으로 삭제해야 합니다. 또한, Data Quality 서버를 다시 설치하기 전에 컴퓨터의 C:\Program Files\Microsoft SQL Server\MSSQL11.<SQL_Server_Instance>\MSSQL\DATA 폴더에서 DQS 데이터베이스(DQS_MAIN, DQS_PROJECTS 및 DQS_STAGING_DATA) 파일을 삭제해야 합니다. 그렇지 않으면 Data Quality 서버 설치가 실패합니다. 기술 자료나 데이터 품질 프로젝트와 같은 데이터를 보존하려면 데이터베이스 파일을 삭제하지 말고 이동합니다. 제거 프로세스 완료 후 DQS 개체 제거에 대한 자세한 내용은 [Data Quality 서버 개체 제거](http://msdn.microsoft.com/library/hh231667.aspx)를 참조하세요.  
  
### <a name="43-indication-of-a-terminated-knowledge-discovery-or-interactive-cleansing-activity-is-delayed"></a>4.3 종료된 기술 자료 검색 또는 대화형 정리 작업에 대한 메시지가 지연됨  
**문제:** 관리자가 작업 모니터링 화면에서 작업을 종료하면 기술 자료 검색, 도메인 관리 또는 대화형 정리 작업을 실행 중인 대화형 사용자는 그 다음 작업을 수행할 때까지 자신의 작업이 종료되었다는 메시지를 받지 않게 됩니다.  
  
**해결 방법:** 없습니다.  
  
### <a name="44-a-cancel-operation-discards-work-from-multiple-activities"></a>4.4 취소 작업으로 여러 동작의 작업이 삭제됨  
**문제:** 실행 중인 기술 자료 검색 또는 도메인 관리 동작에 대해 **취소** 를 클릭하는 경우 동작이 실행되는 중에 수행되는 게시 작업 없이 기타 동작들도 이전에 완료되었으면 현재 동작뿐만 아니라 마지막 게시 이후로 수행된 모든 동작의 작업이 삭제됩니다.  
  
**해결 방법:** 이 문제를 방지하려면, 새로운 동작을 시작하기 전에 기술 자료로 유지하고자 하는 작업을 게시합니다.  
  
### <a name="45-controls-do-not-scale-properly-on-large-font-sizes"></a>4.5 큰 글꼴 크기에서 컨트롤의 비율이 제대로 조정되지 않음  
**문제:** 텍스트 크기를 "크게 – 150%"로 변경하거나(Windows Server 2008 또는 Windows 7) 사용자 지정 DPI 설정을 200%로 변경하는 경우(Windows 7) **새 기술 자료** 페이지의 **취소** 및 **만들기** 단추에 액세스할 수 없습니다.  
  
**해결 방법:**이 문제를 해결하려면 글꼴을 더 작은 크기로 설정합니다.  
  
### <a name="46-screen-resolution-of-800x600-is-not-supported"></a>4.6 800x600의 화면 해상도는 지원되지 않음  
**문제:** 화면 해상도를 800x600으로 설정하는 경우 Data Quality Client 응용 프로그램이 올바르게 표시되지 않습니다.  
  
**해결 방법:** 이 문제를 해결하려면 화면 해상도를 더 높은 값으로 설정합니다.  
  
### <a name="47-map-bigint-column-in-the-source-data-to-a-decimal-domain-to-prevent-data-loss"></a>4.7 원본 데이터의 Bigint 열을 십진수 도메인에 매핑하여 데이터 손실을 방지  
**문제:** 원본 데이터의 열이 **bigint** 데이터 형식인 경우 DQS에서 **integer** 데이터 형식 대신 **decimal** 데이터 형식의 도메인에 열을 매핑해야 합니다. 그 이유는 **decimal** 데이터 형식이 **int** 데이터 형식보다 큰 값의 범위를 나타내므로 더 큰 값을 가질 수 있기 때문입니다.  
  
### <a name="48-nvarcharmax-and-varcharmax-data-types-are-not-supported-in-the-dqs-cleansing-component-in-integration-services"></a>4.8 NVARCHAR(MAX) 및 VARCHAR(MAX) 데이터 형식이 Integration Services의 DQS 정리 구성 요소에서 지원되지 않음  
**문제:** **nvarchar(max)** 및 **varchar(max)** 데이터 형식의 데이터 열이 Integration Services의 DQS 정리 구성 요소에서 지원되지 않습니다. 따라서 이러한 데이터 열은 DQS 정리 변환 편집기의 매핑 탭에서 매핑에 사용할 수 없으므로 정리될 수 없습니다.  
  
**해결 방법:** DQS 정리 구성 요소를 사용하여 이러한 데이터 열을 처리하기 전에 데이터 변환을 사용하여 **DT_STR** 또는 **DT_WSTR** 데이터 형식으로 변환해야 합니다.  
  
### <a name="49-the-item-to-run-dqsinstallerexe-on-the-start-menu-is-overwritten-on-new-sql-server-instance-installation"></a>4.9 시작 메뉴에서 DQSInstaller.exe를 실행하는 항목이 새 SQL Server 인스턴스 설치에서 덮어쓰임  
**문제:** SQL Server 인스턴스에서 Data Quality Services를 설치하도록 선택하는 경우 SQL Server 설치를 완료한 후 **시작** 메뉴에서 **Data Quality Services** 프로그램 그룹 아래에 **Data Quality Server Installer** 라는 항목이 만들어집니다. 그러나 한 컴퓨터에 여러 SQL Server 인스턴스를 설치하는 경우에도 **시작** 메뉴에 **Data Quality Server Installer** 항목이 하나만 있습니다. 이 항목을 클릭하면 가장 최근에 설치한 SQL Server 인스턴스에서 DQSInstaller.exe 파일이 실행됩니다.  
  
### <a name="410-activity-monitoring-displays-incorrect-status-for-failed-integration-services-cleansing-activities"></a>4.10 작업 모니터링이 실패한 Integration Services 정리 작업에 대해 잘못된 상태를 표시함  
실패한 Integration Services 정리 작업에 대해서도 작업 모니터링 화면의 **현재 상태** 열에 **성공** 이라고 잘못 표시됩니다.  
  
### <a name="411-schema-name-is-not-displayed-as-part-of-tableview-name"></a>4.11 스키마 이름이 테이블/뷰 이름의 일부로 표시되지 않음  
Data Quality 클라이언트에서 매핑 단계 중에 DQS 작업에서 SQL Server 데이터 원본을 선택하면 테이블과 뷰의 목록이 스키마 이름 없이 표시됩니다. 따라서 이름이 같지만 스키마는 다른 테이블/뷰가 여러 개 있는 경우 데이터 미리 보기에서 확인하거나 테이블/뷰를 선택한 다음 매핑할 수 있는 필드를 확인하는 방법으로만 테이블/뷰를 구분할 수 있습니다.  
  
### <a name="412-issue-with-cleansing-output-and-export-if-data-source-is-mapped-to-a-composite-domain-containing-a-child-domain-of-date-type"></a>4.12 Date 형식의 자식 도메인이 포함된 복합 도메인에 데이터 원본이 매핑되는 경우의 정리 출력 및 내보내기 문제점  
데이터 품질 프로젝트 정리에서 원본 데이터의 필드를 date 데이터 형식의 자식 도메인이 있는 복합 도메인으로 매핑한 경우 정리 결과에 있는 자식 도메인 출력의 날짜 형식이 잘못되고 데이터베이스로 내보내기 작업이 실패합니다.  
  
### <a name="413-error-when-mapping-to-an-excel-sheet-that-contains-a--semicolon-in-its-name"></a>4.13 이름에 ;(세미콜론)이 포함된 Excel 시트에 매핑하는 경우의 오류  
**문제:** Data Quality 클라이언트의 DQS 작업에 대한 **매핑** 페이지에서 이름에 ;(세미콜론)이 포함된 원본 Excel 시트에 매핑하는 경우 **매핑** 페이지에서 **다음** 을 클릭하면 처리되지 않은 예외 메시지가 표시됩니다.  
  
**해결 방법:** 매핑할 원본 데이터가 포함된 Excel 파일의 시트 이름에서 ;(세미콜론)을 제거하고 다시 시도합니다.  
  
### <a name="414-issue-with-date-or-datetime-values-in-unmapped-source-fields-in-excel-during-cleansing-and-matching"></a>4.14 정리 및 일치 중에 Excel의 매핑되지 않은 원본 필드에 있는 Date 또는 DateTime 값의 문제점  
**문제:**원본 데이터가 Excel이고 **날짜** 또는 **날짜/시간** 데이터 형식의 값이 포함된 원본 필드를 매핑하지 않은 경우 정리 및 일치 작업 중에 다음과 같은 현상이 발생합니다.  
  
-   매핑되지 않은 **날짜** 값이 yyyymmdd 형식으로 표시되고 내보내집니다.  
  
-   매핑되지 않은 **날짜/시간** 값의 시간 값이 손실되고, 값이 yyyymmdd 형식으로 표시되고 내보내집니다.  
  
**해결 방법:** 정리 작업의 **결과 관리 및 보기** 페이지와 일치 작업의 **일치** 페이지에 있는 오른쪽 아래 창에서 매핑되지 않은 필드 값을 볼 수 있습니다.  
  
### <a name="415-cannot-import-domain-values-from-an-excel-file-xls-containing-more-than-255-columns-of-data"></a>4.15 데이터 열이 255개가 넘는 Excel 파일(.xls)에서 도메인 값을 가져올 수 없음  
**문제:** 데이터 열이 255개가 넘는 Excel 97-2003 파일(.xls)에서 도메인으로 값을 가져오는 경우 예외 메시지가 나타나고 가져오기가 실패합니다.  
  
**해결 방법:** 이 문제를 해결하려면 다음 작업 중 하나를 수행하세요.  
  
-   .xls 파일을 .xlsx 파일로 저장한 다음 .xlsx 파일의 값을 도메인으로 가져옵니다.  
  
-   .xls 파일에서 열 255 이후의 모든 열에 있는 데이터를 제거하고 파일을 저장한 다음 .xls 파일의 값을 도메인으로 가져옵니다.  
  
### <a name="416-activity-monitoring-feature-is-unavailable-for-roles-other-than-dqsadministrator"></a>4.16 dqs_administrator가 아닌 역할은 작업 모니터링 기능을 사용할 수 없음  
작업 모니터링 기능은 dqs_administrator 역할이 있는 사용자에게만 제공됩니다. 사용자 계정에 dqs_kb_editor 또는 dqs_kb_operator 역할이 있으면 Data Quality 클라이언트 응용 프로그램에서 작업 모니터링 기능이 제공되지 않습니다.  
  
### <a name="417-error-on-opening-a-knowledge-base-in-the-recent-knowledge-base-list-for-domain-management"></a>4.17 최근 기술 자료에서 도메인 관리에 대한 기술 자료를 여는 경우 오류 발생  
Data Quality 클라이언트 홈 화면에서 **최근 기술 자료** 목록의 도메인 관리 작업에 대한 기술 자료를 여는 경우 다음과 같은 오류 메시지가 나타날 수 있습니다.  
  
`"A configuration with name 'RecentList:KB:<domain>\<username>' already exists in the database."`  
  
이 오류는 DQS에서 SQL Server 데이터베이스와 C#에서 문자열을 비교하는 방법의 차이로 인해 발생합니다. SQL Server 데이터베이스의 문자열 비교는 대/소문자를 구분하지 않는 반면 C#에서는 대/소문자를 구분합니다.  
  
한 가지 예를 들어 이러한 경우를 설명하겠습니다. Domain\user1이라는 사용자가 있다고 가정합니다. 사용자가 “user1” 계정을 사용하여 Data Quality 클라이언트 컴퓨터에 로그온하고 기술 자료를 작동합니다. DQS에서는 각 사용자의 최근 기술 자료를 DQS_MAIN 데이터베이스의 A_CONFIGURATION 테이블에 있는 레코드 형태로 저장합니다. 이 경우 보고서는 RecentList:KB:Domain\user1과 같은 이름으로 저장됩니다. 이후에 사용자가 “User1”(대문자 U에 주의)로 Data Quality 클라이언트 컴퓨터에 로그온하고 **최근 기술 자료** 목록에서 도메인 관리 작업에 대한 기술 자료를 열려고 합니다. DQS의 기본 코드는 두 문자열 RecentList:KB:DOMAIN\user1과 DOMAIN\User1을 비교합니다. C#에서는 대/소문자를 구분하여 문자열 비교하기 때문에 문자열이 일치하지 않아 DQS에서는 DQS_MAIN 데이터베이스의 A_CONFIGURATION 테이블에 사용자(User1)에 대한 새 레코드를 삽입하려고 합니다. 그러나 SQL 데이터베이스의 대/소문자를 구분하지 않는 문자열 비교로 인해 DQS_MAIN 데이터베이스의 A_CONFIGURATION 테이블에 문자열이 이미 존재하므로 삽입 작업이 실패합니다.  
  
**해결 방법:** 이 문제를 해결하려면 다음 작업 중 하나를 수행하세요.  
  
-   다음 문을 실행하여 중복 항목이 있는지 확인합니다.  
  
    ```  
    SELECT * FROM DQS_MAIN.dbo.A_CONFIGURATION WHERE NAME like 'RecentList%'  
    ```  
  
    그런 다음 영향을 받는 도메인 및 사용자 이름과 일치하도록 WHERE 절의 값을 변경하여 다음 문을 실행해 영향을 받는 사용자에 대한 레코드만 삭제할 수 있습니다.  
  
    ```  
    DELETE DQS_MAIN.dbo.A_Configuration WHERE NAME LIKE 'RecentList%<domain>\<username>'  
    ```  
  
    또는 다음과 같이 DQS에 있는 모든 사용자의 최근에 사용한 모든 항목을 제거할 수도 있습니다.  
  
    ```  
    DELETE DQS_MAIN.dbo.A_Configuration WHERE NAME LIKE 'RecentList%'  
    ```  
  
-   Data Quality 클라이언트 컴퓨터에 로그온하는 동안 마지막에 사용한 것과 동일한 대/소문자를 사용하여 사용자 계정을 지정합니다.  
  
> [!NOTE]  
> 이 문제를 해결하려면 Data Quality 클라이언트 컴퓨터에 로그온하는 동안 일관된 대/소문자 규칙을 사용하여 사용자 계정을 지정하십시오.  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="DE"></a>5.0 데이터베이스 엔진  
  
### <a name="51-use-of-distributed-replay-controller-and-distributed-replay-client-features"></a>5.1 Distributed Replay Controller 및 Distributed Replay Client 기능 사용  
**문제:** Distributed Replay Controller 및 Distributed Replay Client 기능은 Server Core SKU에서 지원되지 않더라도 Windows Server 2008, Windows Server 2008 R2 및 Windows Server 7의 Server Core SKU에서 사용할 수 있습니다.  
  
**해결 방법:** Windows Server 2008, Windows Server 2008 R2 및 Windows Server 7의 Server Core SKU에서 이 두 기능을 설치 또는 사용하지 마세요.  
  
### <a name="52-sql-server-management-studio-depends-on-visual-studio-2010-sp1"></a>5.2 SQL Server Management Studio가 Visual Studio 2010 SP1에 따라 달라짐  
**문제:**SQL Server 2012 Management Studio가 올바르게 작동하는지 여부는 Visual Studio 2010 SP1에 따라 달라집니다. Visual Studio 2010 SP1을 제거하면 SQL Server Management Studio의 기능이 손상될 수 있고 Management Studio을 지원되지 않는 상태로 두게 됩니다. 이 경우 다음과 같은 문제를 볼 수 있습니다.  
  
-   ssms.exe의 명령줄 매개 변수가 올바르게 작동하지 않습니다.  
  
-   /? 스위치와 함께 ssms.exe를 실행하려고 할 때 표시되는 도움말 정보가 올바르지 않습니다.  
  
-   Windows 탐색기에서 두 번 클릭하여 연 모든 파일에 대해 SSMS의 새 인스턴스에서 파일을 열기 시작합니다.  
  
-   쿼리가 일반 사용자 모드에서 디버깅되지 않습니다.  
  
**해결 방법:**Visual Studio 2010 SP1을 다시 설치하고 Management Studio를 다시 시작합니다.  
  
### <a name="53-x64-operating-systems-require-64-bit-powershell-20"></a>5.3 x64 운영 체제에 64비트 PowerShell 2.0 필요  
**문제:** 64비트 운영 체제의 SQL Server 2012 인스턴스에 대해 Windows PowerShell Extensions for SQL Server의 32비트 설치가 지원되지 않습니다.  
  
**해결 방법:**  
  
-   64비트 관리 도구 및 64비트 Windows PowerShell Extensions for SQL Server와 함께 64비트 SQL Server 2012를 설치합니다.  
  
-   또는 32비트 Windows PowerShell 2.0 프롬프트에서 SQLPS 모듈을 가져옵니다.  
  
### <a name="54-an-error-might-occur-when-navigating-in-the-generate-script-wizard"></a>5.4 스크립트 생성 마법사에서 탐색하는 중에 오류가 발생할 수 있음  
**문제:** **스크립트 저장 또는 게시**를 클릭하여 스크립트 생성 마법사에서 스크립트를 생성한 다음 **옵션 선택** 또는 **스크립팅 옵션 설정**을 클릭하고 다시 **스크립트 저장 및 게시** 를 클릭하여 탐색하면 다음 오류가 발생할 수 있습니다.  
  
<a name="prean-exception-occurred-while-executing-a-transact-sql-statement-or-batch-microsoftsqlserverconnectioninfo"></a><pre>An exception occurred while executing a Transact-SQL statement or batch. (Microsoft.SqlServer.ConnectionInfo)  
------------------------------  
추가 정보:  
개체 이름 'sys.federations'가 잘못되었습니다. (Microsoft SQL Server, 오류: 208)</pre>  
  
**해결 방법:** 스크립트 생성 마법사를 닫고 다시 엽니다.  
  
### <a name="55-new-maintenance-plan-layout-not-compatible-with-earlier-sql-server-tools"></a>5.5 새 유지 관리 계획 레이아웃이 이전 SQL Server 도구와 호환되지 않음  
**문제:** SQL Server 2012 관리 도구가 이전 버전의 SQL Server 관리 도구(SQL Server 2008 R2, SQL Server 2008 또는 SQL Server 2005)에서 만든 기존 유지 관리 계획을 수정하는 데 사용되면 유지 관리 계획이 새로운 형식으로 저장됩니다. 이전 버전의 SQL Server 유지 관리 도구에서는 이 새로운 형식을 지원하지 않습니다.  
  
**해결 방법:**없습니다.  
  
### <a name="56-intellisense-has-limitations-when-logged-in-to-a-contained-database"></a>5.6 포함된 데이터베이스에 로그인할 때 Intellisense에 제약이 따름  
문제: 포함된 사용자가 포함된 데이터베이스에 로그인하면 SSMS(SQL Server Management Studio) 및 SSDT(SQL Server Data Tools)에서 Intellisense가 정상적으로 작동하지 않습니다. 이 경우 다음과 같은 동작이 나타날 수 있습니다.  
  
1.  잘못된 개체의 밑줄이 표시되지 않습니다.  
  
2.  자동 완성 목록이 나타나지 않습니다.  
  
3.  기본 제공 함수의 도구 설명 도움말이 작동하지 않습니다.  
  
**해결 방법:**없습니다.  
  
### <a name="57-alwayson-availability-groups"></a>5.7 AlwaysOn 가용성 그룹  
가용성 그룹을 만들기 전에 온라인 설명서의 [AlwaysOn 가용성 그룹(SQL Server)에 대한 사전 요구 사항, 제한 사항 및 권장 사항](http://go.microsoft.com/?linkid=9753168) 을 참조하세요. AlwaysOn 가용성 그룹에 대한 소개는 온라인 설명서의 [AlwaysOn 가용성 그룹(SQL Server)](http://go.microsoft.com/?linkid=9753166)을 참조하세요.  
  
#### <a name="571-client-connectivity-for-alwayson-availability-groups"></a>5.7.1 AlwaysOn 가용성 그룹의 클라이언트 연결  
**업데이트한 날짜:** 2012년 8월 13일  
  
이 섹션에서는 AlwaysOn 가용성 그룹의 드라이버 지원과 지원되지 않는 드라이버에 대한 문제 해결을 설명합니다.  
  
**드라이버 지원**  
  
다음 표에서는 AlwaysOn 가용성 그룹의 드라이버 지원에 대해 간략하게 설명합니다.  
  
|드라이버|다중 서브넷 장애 조치(Failover)|응용 프로그램 의도|읽기 전용 라우팅|다중 서브넷 장애 조치(Failover): 보다 빠른 단일 서브넷 끝점 장애 조치(Failover)|다중 서브넷 장애 조치(Failover): SQL 클러스터형 인스턴스에 대한 명명된 인스턴스 확인|  
|----------|--------------------------|----------------------|----------------------|------------------------------------------------------------------|---------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|예|예|예|예|예|  
|SQL Native Client 11.0 OLEDB|아니요|예|예|아니오|아니요|  
|연결 패치가 포함된 .NET Framework 4.0이 있는 ADO.NET**\&#42;**|사용자 계정 컨트롤|예|예|예|사용자 계정 컨트롤|  
|연결 패치가 포함된 .NET Framework 3.5 SP1이 있는 ADO.NET **\&#42;\&#42;**|사용자 계정 컨트롤|예|예|예|예|  
|SQL Server용 Microsoft JDBC Driver 4.0|예|예|예|예|사용자 계정 컨트롤|  
  
**\&#42;** .NET Framework 4.0이 있는 ADO.NET용 연결 패치 다운로드: [http://support.microsoft.com/kb/2600211](http://support.microsoft.com/kb/2600211)  
  
**\&#42;\&#42;** .NET Framework 3.5 SP1이 있는 ADO.NET용 연결 패치 다운로드: [http://support.microsoft.com/kb/2654347](http://support.microsoft.com/kb/2654347)  
  
**MultiSubnetFailover 키워드 및 관련 기능**  
  
MultiSubnetFailover는 SQL Server 2012에서 AlwaysOn 가용성 그룹과 AlwaysOn 장애 조치(Failover) 클러스터 인스턴스를 사용하여 보다 빠르게 장애 조치할 수 있도록 하는 데 사용되는 새로운 연결 문자열 키워드입니다. MultiSubnetFailover=True가 연결 문자열에서 설정되면 다음 세 가지 하위 기능을 사용할 수 있습니다.  
  
-   AlwaysOn 가용성 그룹 또는 장애 조치(Failover) 클러스터 인스턴스에 대한 다중 서브넷 수신기로 보다 빠른 다중 서브넷 장애 조치  
  
    -   다중 서브넷 AlwaysOn 장애 조치(Failover) 클러스터 인스턴스로 명명된 인스턴스 확인  
  
-   AlwaysOn 가용성 그룹 또는 장애 조치(Failover) 클러스터 인스턴스에 대한 단일 서브넷 수신기로 보다 빠른 단일 서브넷 장애 조치  
  
    -   이 기능은 단일 서브넷의 단일 IP가 있는 수신기에 연결할 때 사용되며, 단일 서브넷 장애 조치(Failover) 속도를 높이기 위해 보다 적극적으로 TCP 연결을 다시 시도합니다.  
  
-   다중 서브넷 AlwaysOn 장애 조치(Failover) 클러스터 인스턴스로 명명된 인스턴스 확인  
  
    -   서브넷 끝점이 여러 개인 AlwaysOn 장애 조치(Failover) 클러스터 인스턴스에 대한 명명된 인스턴스 확인 지원을 추가합니다.  
  
**MultiSubnetFailover=True가 .NET Framework 3.5 또는 OLEDB에서 지원되지 않음**  
  
**문제:** 가용성 그룹 또는 장애 조치(Failover) 클러스터 인스턴스에 각기 다른 서브넷의 여러 IP 주소를 사용하는 수신기 이름(WSFC 클러스터 관리자에서는 네트워크 이름 또는 클라이언트 액세스 지점이라고도 함)이 있고 .NET Framework 3.5 SP1 또는 SQL Native Client 11.0 OLEDB가 있는 ADO.NET을 사용하는 경우 가용성 그룹 수신기에 대한 클라이언트 연결 요청 중 50%가 연결 제한 시간을 초과할 수 있습니다.  
  
**해결 방법:** 다음 작업 중 하나를 수행하는 것이 좋습니다.  
  
-   클러스터 리소스를 조작할 권한이 없는 경우 연결 제한 시간을 30초로 변경합니다. 이 값은 20초 TCP 제한 시간 기간과 10초 버퍼를 더한 값입니다.  
  
    **장점**: 서브넷 간 장애 조치(Failover)가 발생하는 경우 클라이언트 복구 시간이 짧습니다.  
  
    **단점**: 클라이언트 연결 중 절반이 20초 이상 걸립니다.  
  
-   클러스터 리소스를 조작할 권한이 있는 경우 더 권장하는 방법은 가용성 그룹 수신기의 네트워크 이름을 **RegisterAllProvidersIP**=0으로 설정하는 것입니다. 자세한 내용은 이 섹션 뒷부분에 나오는 "RegisterAllProvidersIP를 비활성화하고 TTL을 줄이는 샘플 PowerShell 스크립트"를 참조하십시오.  
  
    **장점** : 클라이언트 연결 제한 시간 값을 증가시키지 않아도 됩니다.  
  
    **단점:** 서브넷 간 장애 조치(Failover)가 발생하는 경우 클라이언트 복구 시간은 HostRecordTTL 설정 및 사이트 간 DNS/AD 복제 일정의 설정에 따라 15분 이상이 될 수 있습니다.  
  
**RegisterAllProvidersIP를 비활성화하고 TTL을 줄이는 샘플 PowerShell 스크립트**  
  
다음 샘플 PowerShell 스크립트는 `RegisterAllProvidersIP` 를 비활성화하고 TTL을 줄이는 방법을 보여줍니다. `yourListenerName` 을 변경할 수신기의 이름으로 바꿉니다.  
  
```  
Import-Module FailoverClusters  
Get-ClusterResource yourListenerName|Set-ClusterParameter RegisterAllProvidersIP 0  
Get-ClusterResource yourListenerName|Set-ClusterParameter HostRecordTTL 300  
```  
  
#### <a name="572-upgrading-from-ctp3-with-availability-group-configured-is-not-supported"></a>5.7.2 가용성 그룹이 구성된 CTP3에서의 업그레이드가 지원되지 않음  
업그레이드하기 전에 가용성 그룹을 삭제하고 다시 만듭니다. 이는 CTP3 빌드의 제한 때문입니다. 이후 빌드에는 이러한 제한이 없습니다.  
  
#### <a name="573-side-by-side-installation-of-ctp3-with-later-versions-is-not-supported-if-you-have-an-availability-group-configured-in-your-instance"></a>5.7.3 인스턴스에서 가용성 그룹이 구성된 경우 CTP3과 최신 버전의 병렬 설치가 지원되지 않음  
이는 CTP3 빌드의 제한 때문입니다. 이후 빌드에는 이러한 제한이 없습니다.  
  
#### <a name="574-side-by-side-installation-of-ctp3-with-later-versions-of-failover-cluster-instances-is-not-supported"></a>5.7.4 CTP3과 장애 조치(Failover) 클러스터 인스턴스의 최신 버전의 병렬 설치가 지원되지 않음  
이는 CTP3 빌드의 제한 때문입니다. 이후 빌드에는 이러한 제한이 없습니다. CTP3에서 장애 조치(Failover) 클러스터 인스턴스를 업그레이드하면 노드의 모든 인스턴스가 동시에 업그레이드됩니다.  
  
#### <a name="575--timeouts-may-occur-when-using-multi-ips-in-the-same-subnet-with-alwayson"></a>5.7.5 AlwaysOn을 사용하는 동일한 서브넷에서 여러 IP를 사용할 때 시간 초과가 발생할 수 있음  
**문제:** AlwaysOn을 사용하는 동일한 서브넷에서 여러 IP를 사용할 때 가끔씩 고객이 제한 시간을 봅니다. 이 문제는 목록의 최상위 IP 상태가 불량일 때 발생합니다.  
  
**해결 방법:** 연결 문자열에 'multisubnetfailover = true'를 사용합니다.  
  
#### <a name="576-failure-to-create-new-availability-group-listeners-because-of-active-directory-quotas"></a>5.7.6 Active Directory 할당량 때문에 새로운 가용성 그룹 수신기 만들기 실패  
**문제:** 참여하는 클러스터 노드 컴퓨터 계정에 대한 Active Directory 할당량에 도달하여 새 가용성 그룹 수신기를 만들지 못할 수도 있습니다. 자세한 내용은 [컴퓨터 개체 수정 시 클러스터 서비스 계정 문제를 해결하는 방법](http://support.microsoft.com/kb/307532) 및 [Active Directory 할당량](http://technet.microsoft.com/library/cc904295(WS.10).aspx)을 참조하세요.  
  
#### <a name="577-netbios-conflicts-because-availability-group-listener-names-use-an-identical-15-character-prefix"></a>5.7.7 가용성 그룹 수신기 이름에 동일한 15자 접두사를 사용하여 NetBIOS 충돌  
두 WSFC 클러스터가 동일한 Active Directory에 의해 제어될 때 15자 이상의 이름과 동일한 15자 접두사를 사용하여 두 클러스터 모두에서 가용성 그룹 수신기를 만들려고 하면 가상 네트워크 이름 리소스를 온라인으로 전환할 수 없다는 오류 메시지가 표시됩니다. DNS 이름의 접두사 명명 규칙에 대한 자세한 내용은 [도메인 이름 할당](http://technet.microsoft.com/library/cc731265(WS.10).aspx)을 참조하세요.  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="IS"></a>6.0 Integration Services  
  
### <a name="61-the-change-data-capture-service-for-oracle-and-the-change-data-capture-designer-console-for-oracle"></a>6.1 Change Data Capture Service for Oracle 및 Change Data Capture Designer Console for Oracle  
Oracle용 CDC 서비스는 Oracle 트랜잭션 로그를 검색하고 관련 Oracle 테이블의 변경 내용을 SQL Server 변경 테이블에 캡처하는 Windows 서비스입니다. CDC Designer 콘솔은 Oracle CDC 인스턴스를 개발하고 유지 관리하는 데 사용됩니다. CDC 디자이너 콘솔은 MMC(Microsoft Management Console) 스냅인입니다.  
  
#### <a name="611-install-the-cdc-service-for-oracle-and-the-cdc-designer-for-oracle"></a>6.1.1 Oracle용 CDC 서비스 및 Oracle용 CDC 디자이너 설치  
**문제:** CDC Service 및 CDC Designer는 SQL Server 설치 프로그램으로 설치되지 않습니다. 업데이트된 도움말 파일에 설명된 대로 요구 사항 및 사전 요구 사항을 충족하는 컴퓨터에 CDC 서비스 또는 CDD 디자이너를 수동으로 설치해야 합니다.  
  
**해결 방법:** Oracle CDC Service를 설치하려면 SQL Server 설치 미디어에서 AttunityOracleCdcService.msi를 수동으로 실행합니다. CDC 디자이너 콘솔을 설치하려면 SQL Server 설치 미디어에서 AttunityOracleCdcDesigner.msi를 수동으로 실행합니다.  X86 및 x64에 대한 설치 패키지는 SQL Server 설치 미디어의 \Tools\AttunityCDCOracle\에 있습니다.  
  
#### <a name="612-f1-help-functionality-points-to-incorrect-documentation-files"></a>6.1.2 F1 도움말 기능이 잘못된 설명서 파일을 가리킴  
**문제:** F1 도움말 드롭다운 목록을 사용하거나 Attunity 콘솔에서 "?"를 클릭하여 올바른 도움말 설명서에 액세스할 수 없습니다. 이러한 방법은 잘못된 chm 파일을 가리킵니다.  
  
**해결 방법:** Oracle CDC Service와 Oracle CDC Designer를 설치할 때 올바른 chm 파일이 설치됩니다. 올바른 도움말 콘텐츠를 보려면 다음 위치에서 chm 파일을 직접 시작하세요. `%Program Files%\Change Data Capture for Oracle by Attunity\*.chm`  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="MDS"></a>7.0 MDS(Master Data Services)  
  
### <a name="71-fixing-an-mds-installation-in-a-cluster"></a>7.1 클러스터에서 MDS 설치 수정  
**문제:** **Master Data Services** 확인란이 선택된 상태로 SQL Server 2012 RTM 버전의 클러스터형 인스턴스를 설치하는 경우 단일 노드에 MDS가 설치되지만 MDS를 사용할 수 없고 클러스터에 추가하는 추가 노드에서 작동하지 않습니다.  
  
**해결 방법:**이 문제를 해결하려면 다음 단계를 수행하여 SQL Server 2012 누적 릴리스 1(CU1)을 설치해야 합니다.  
  
1.  기존 SQL/MDS 설치가 없는지 확인합니다.  
  
2.  SQL Server 2012 CU1을 로컬 디렉터리에 다운로드합니다.  
  
3.  MDS 기능이 포함된 SQL Server 2012를 주 클러스터 노드에 설치한 다음 MDS 기능이 포함된 SQL Server 2012를 추가 클러스터 노드에 설치합니다.  
  
문제에 대한 자세한 내용 및 위 단계를 수행하는 방법은 [http://support.microsoft.com/kb/2683467](http://support.microsoft.com/kb/2683467)을 참조하세요.  
  
### <a name="72-microsoft-silverlight-5-required"></a>7.2 Microsoft Silverlight 5 필요  
마스터 데이터 관리자 웹 응용 프로그램에서 작업하려면 클라이언트 컴퓨터에 Silverlight 5.0이 설치되어 있어야 합니다. 필요한 Silverlight 버전이 설치되어 있지 않으면 Silverlight이 필요한 웹 응용 프로그램 영역으로 이동할 때 Silverlight를 설치하라는 메시지가 표시됩니다. [http://go.microsoft.com/fwlink/?LinkId=243096](http://go.microsoft.com/fwlink/?LinkId=243096)에서 Silverlight 5를 설치할 수 있습니다.  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="RS"></a>8.0 Reporting Services  
  
### <a name="81-reporting-services-connectivity-to-sql-server-pdw-requires-updated-drivers"></a>8.1 SQL Server PDW에 대한 Reporting Services 연결 시 업데이트된 드라이버가 필요함  
SQL Server 2012 Reporting Services에서 Microsoft SQL Server PDW Appliance Update 2 이상으로 연결하려면 PDW 연결 드라이버에 대한 업데이트가 필요합니다. SQL Server PDW 고객의 경우 자세한 내용은 Microsoft 고객 지원에 문의하십시오.  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="SI"></a>9.0 StreamInsight  
SQL Server 2012에는 StreamInsight 2.0이 포함되어 있습니다. StreamInsight 2.0을 사용하려면 Microsoft SQL Server 2012 라이선스와 .NET Framework 4.0이 필요합니다. StreamInsight&2;.0에서는 여러 가지 버그를 수정하고 성능을 높였습니다. 자세한 내용은 [Microsoft StreamInsight 2.0 릴리스 정보](http://social.technet.microsoft.com/wiki/contents/articles/6539.aspx)를 참조하세요. StreamInsight 2.0을 별도로 다운로드하려면 Microsoft 다운로드 센터의 [Microsoft StreamInsight 2.0 다운로드 페이지](http://go.microsoft.com/fwlink/?LinkId=241593) 를 방문하세요.  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
## <a name="UA"></a>10.0 업그레이드 관리자  
  
### <a name="101-link-to-install-upgrade-advisor-is-not-enabled-on-chinese-hk-operating-systems"></a>10.1 업그레이드 관리자 설치에 대한 링크가 중국어(HK) 운영 체제에서 활성화되지 않음  
문제: 중국어(홍콩 특별행정구) 운영 체제(OS)가 지원되는 Windows 버전에 업그레이드 관리자를 설치하려고 할 때 업그레이드 관리자 설치에 대한 링크가 사용하도록 설정되지 않은 것을 발견할 수 있습니다.  
  
**해결 방법:**해당 운영 체제 아키텍처에 따라 **또는** 에서 SQL Server 2012 미디어에 있는 `\1028_CHT_LP\x64\redist\Upgrade Advisor` SQLUA.msi `\1028_CHT_LP\x86\redist\Upgrade Advisor`파일을 찾습니다.  
  
![horizontal_bar](media/horizontal-bar.png "horizontal_bar")  
  
