---
title: SharePoint 용 PowerPivot 2013 설치 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: d3310562-82c1-454f-9c48-33a241749238
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 561a62b81e36ea5de39eda52a2ea70e04ea5a50c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48162943"
---
# <a name="powerpivot-for-sharepoint-2013-installation"></a>PowerPivot for SharePoint 2013 Installation
  이 항목의에서 절차를 안내의 단일 서버 설치를 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] SharePoint 배포 모드의 서버. 이 단계에는 SharePoint 2013 중앙 관리를 사용하는 SQL Server 설치 마법사 및 구성 태스크가 포합됩니다.  
  
 **[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 201  
  
 **항목 내용**  
  
 [배경](#bkmk_background)  
  
 [필수 구성 요소](#bkmk_prereq)  
  
 [1 단계: SharePoint 용 PowerPivot 설치](#InstallSQL)  
  
 [2단계: Basic Analysis Services SharePoint 통합 구성](#bkmk_config)  
  
 [3단계 통합 확인](#bkmk_verify)  
  
 [Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](#bkmk_firewall)  
  
 [통합 문서 업그레이드 및 예약된 데이터 새로 고침](#bkmk_upgrade_workbook)  
  
 [Microsoft SharePoint 용 PowerPivot 단일 서버 설치 – 초과](#bkmk_multiple_servers)  
  
##  <a name="bkmk_background"></a> 배경  
 SharePoint용 PowerPivot은 SharePoint 2013 팜에서 PowerPivot 데이터 액세스를 제공하는 중간 계층 및 백 엔드 서비스의 모음입니다.  
  
-   **백 엔드 서비스:** PowerPivot for Excel을 사용하여 분석 데이터가 포함된 통합 문서를 만드는 경우 서버 환경에서 이러한 데이터에 액세스하려면 SharePoint용 PowerPivot이 있어야 합니다. SharePoint Server 2013이 설치된 컴퓨터 또는 SharePoint 소프트웨어가 설치되지 않은 다른 컴퓨터에서 SQL Server 설치 프로그램을 실행할 수 있습니다. Analysis Services는 SharePoint에 종속성이 없습니다.  
  
     **고:** 이 항목에서는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서버와 백 엔드 서비스의 설치에 대해 설명합니다.  
  
-   **중간 계층:** PowerPivot 갤러리, 데이터 새로 고침 예약, 관리 대시보드 및 데이터 공급자를 포함한 SharePoint의 PowerPivot 환경 향상. 중간 계층 설치 및 구성에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
    -   [설치 하거나 SharePoint 추가 기능에 대 한 PowerPivot을 제거할 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
    -   [PowerPivot 구성 및 솔루션 배포 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
##  <a name="bkmk_prereq"></a> 필수 구성 요소  
  
1.  SQL Server 설치 프로그램을 실행하려면 로컬 관리자여야 합니다.  
  
2.  SharePoint용 PowerPivot를 사용하려면 SharePoint Server 2013 Enterprise Edition이 필요합니다. Evaluation Enterprise Edition을 사용할 수도 있습니다.  
  
3.  Excel Services와 동일한 Active Directory 포리스트의 도메인에 컴퓨터가 참가해야 합니다.  
  
4.  PowerPivot 인스턴스 이름을 사용할 수 있어야 합니다. SharePoint 모드에서 Analysis Services를 설치 중인 컴퓨터에 PowerPivot이라고 명명된 기존 인스턴스가 있어서는 안 됩니다.  
  
5.  검토 [Hardware and Software Requirements SharePoint 모드의 Analysis Services 서버에 대 한 &#40;SQL Server 2014&#41;](../../../sql-server/install/hardware-software-requirements-analysis-services-server-sharepoint-mode.md)합니다.  
  
6.  릴리스 정보를 검토 [SQL Server 2012 서비스 팩 1 릴리스 정보](http://go.microsoft.com/fwlink/?LinkID=248389) (http://go.microsoft.com/fwlink/?LinkID=248389)합니다.  
  
###  <a name="bkmk_sqleditions"></a> SQL Server 버전 요구 사항  
 비즈니스 인텔리전스 기능은 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]의 일부 버전에서만 사용할 수 있습니다. 세부 정보를 참조 하세요 [SQL Server 2012 버전에서 지 원하는 기능 (http://go.microsoft.com/fwlink/?linkid=232473) ](http://go.microsoft.com/fwlink/?linkid=232473) 하 고 [Edition 및 SQL Server 2014 구성 요소](../../../sql-server/editions-and-components-of-sql-server-2016.md)합니다.  
  
 현재 릴리스 정보에서 찾을 수 있습니다 [SQL Server 2012 SP1 릴리스 정보](ttp://go.microsoft.com/fwlink/?LinkID=248389) (http://go.microsoft.com/fwlink/?LinkID=248389)합니다.  
  
 [Microsoft SQL Server 2012 릴리스 정보 (http://go.microsoft.com/fwlink/?LinkId=236893)](http://go.microsoft.com/fwlink/?LinkId=236893)합니다.  
  
##  <a name="InstallSQL"></a> 1 단계: SharePoint 용 PowerPivot 설치  
 이 단계에서는 SQL Server 설치 프로그램을 실행하여 SharePoint 모드에서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서버를 설치합니다. 이후 단계에서는 통합 문서 데이터 모델에 이 서버를 사용하도록 Excel Services를 구성합니다.  
  
1.  SQL Server 설치 마법사(Setup.exe)를 실행합니다.  
  
2.  왼쪽 탐색 창에서 **설치** 를 클릭합니다.  
  
3.  **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**를 클릭합니다.  
  
4.  **제품 키** 페이지가 표시되면 평가판 버전을 지정하거나 라이선스를 받은 엔터프라이즈 버전의 제품 키를 입력하고 **다음**을 클릭합니다. 버전에 대 한 자세한 내용은 참조 하세요. [버전 및 SQL Server 2014 구성 요소](../../../sql-server/editions-and-components-of-sql-server-2016.md)합니다.  
  
5.  Microsoft 소프트웨어 사용권 계약을 검토한 후 동의하고 **다음**을 클릭합니다.  
  
6.  **전역 규칙** 페이지가 나타나면 설치 마법사에 표시되는 규칙 정보를 검토합니다.  
  
7.  **Microsoft Update** 페이지에서 Microsoft Update를 사용하여 업데이트를 확인한 후 **다음**을 클릭하는 것이 좋습니다.  
  
8.  **설치 파일 설치** 페이지가 몇 분 동안 실행됩니다. 규칙 경고 또는 실패한 규칙을 검토한 후 **다음**을 클릭합니다.  
  
9. 다른 **설치 지원 규칙**이 표시되면 경고를 검토하고 **다음**을 클릭합니다.  
  
     **참고:** Windows 방화벽이 설정되었기 때문에 원격 액세스를 사용할 수 있도록 포트를 열라는 경고가 표시됩니다.  
  
10. **설치 역할** 페이지에서 **SQL Server SharePoint용 PowerPivot**을 선택합니다. 이 옵션을 선택하면 SharePoint 모드에서 Analysis Services를 설치합니다.  
  
     또는 설치에 데이터베이스 엔진 인스턴스를 추가할 수 있습니다. 팜의 구성 및 콘텐츠 데이터베이스를 실행하기 위해 새로운 팜을 설정하고 데이터베이스 서버가 필요한 경우 데이터베이스 엔진을 추가할 수도 있습니다. 이 옵션을 선택해도 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]가 설치됩니다.  
  
     데이터베이스 엔진을 추가하는 경우 **PowerPivot** 이라는 인스턴스로 설치됩니다. 이 인스턴스에 대 한 연결을 지정 하면이 형식으로 데이터베이스 이름을 입력 합니다. [`servername`] \PowerPivot 합니다.  
  
     **다음**을 클릭합니다.  
  
     ![설치 역할](../../../sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "설치 역할")  
  
11. 기능 선택에서 기능의 읽기 전용 목록이 확인용으로 표시됩니다. 해당 역할에 대해 미리 선택되어 있는 항목을 추가하거나 제거할 수는 없습니다. **다음**을 클릭합니다.  
  
12. **인스턴스 구성** 페이지에서 확인용으로 'PowerPivot'이라는 읽기 전용 인스턴스 이름이 표시됩니다. 이 인스턴스 이름은 필수 항목이며 수정할 수 없습니다. 그러나 고유한 인스턴스 ID를 입력해 인스턴스를 설명하는 디렉터리 이름과 레지스트리 키를 지정할 수는 있습니다. **다음**을 클릭합니다.  
  
13. **서버 구성** 페이지에서 자동 **시작 유형**에 대해 모든 서비스를 구성합니다. 다음 다이어그램의 **SQL Server Analysis Services**, **(1)** 에 대해 원하는 도메인 계정과 암호를 지정합니다.  
  
    -   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 경우 **도메인 사용자** 계정 또는 **NetworkService** 계정을 사용할 수 있습니다. LocalSystem 또는 LocalService 계정을 사용하지 마세요.  
  
    -   SQL Server 데이터베이스 엔진 및 SQL Server 에이전트를 추가한 경우 도메인 사용자 계정으로 실행하거나 기본 가상 계정으로 실행하도록 서비스를 구성할 수 있습니다.  
  
    -   사용자의 도메인 사용자 계정으로 서비스 계정을 프로비전하지 마세요. 그렇게 하면 네트워크에서 리소스에 대해 갖는 권한과 동일한 권한이 서버에 부여됩니다. 악의적인 사용자가 서버를 침해할 경우 해당 사용자가 사용자의 도메인 자격 증명으로 로그인한 후 사용자와 동일한 데이터 및 애플리케이션을 다운로드하거나 사용할 수 있습니다.  
  
     **다음**을 클릭합니다.  
  
     ![SSAS 서버 구성](../../../sql-server/install/media/ssas-powerpivotsetupsql2012sp1-serverconfiguration.gif "SSAS Server 구성")  
  
14. [!INCLUDE[ssDE](../../../includes/ssde-md.md)]을 설치하는 경우 **데이터베이스 엔진 구성** 페이지가 나타납니다. [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 구성을 클릭 **현재 사용자 추가** 사용자 계정에 데이터베이스 엔진 인스턴스에 대 한 관리자 권한을 부여 하려면.  
  
     **다음**을 클릭합니다.  
  
15. **Analysis Services 구성** 페이지에서 **현재 사용자 추가** 를 클릭하여 사용자 계정에 관리 권한을 부여합니다. 설치가 완료된 후 서버를 구성하려면 관리 권한이 필요합니다.  
  
    -   같은 페이지에서 관리 권한이 필요한 모든 사용자의 Windows 사용자 계정을 추가합니다. 예를 들어 SQL [!INCLUDE[ssGeminiSrv](../../../includes/ssgeminisrv-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 인스턴스에 연결하여 데이터베이스 연결 문제를 해결하려는 모든 사용자에게는 시스템 관리자 권한이 있어야 합니다. 현재 서버 문제를 해결하거나 서버를 관리해야 하는 사용자의 계정을 추가합니다.  
  
    -   > [!NOTE]  
        >  Analysis Services 서버 인스턴스에 액세스해야 하는 모든 서비스 애플리케이션에는 Analysis Services 관리 권한이 필요합니다. 예를 들어 Excel Services, Power View 및 Performance Point Services에 서비스 계정을 추가합니다. 또한 SharePoint 팜 계정을 추가합니다. 이 계정은 중앙 관리를 호스팅하는 웹 애플리케이션의 ID로 사용됩니다.  
  
     **다음**을 클릭합니다.  
  
16. **오류 보고** 페이지에서 **다음**을 클릭합니다.  
  
17. **설치 준비** 페이지에서 **설치**를 클릭합니다.  
  
18. **컴퓨터 다시 시작 필요**대화 상자가 표시되면 **확인**을 클릭합니다.  
  
19. 설치가 완료되면 **닫기**를 클릭합니다.  
  
20. 컴퓨터를 다시 시작합니다.  
  
21. 사용자 환경에 방화벽이 있는 경우 SQL Server 온라인 설명서의 [Configure the Windows Firewall to Allow Analysis Services Access](../configure-the-windows-firewall-to-allow-analysis-services-access.md)항목을 검토하세요.  
  
### <a name="verify-the-sql-server-installation"></a>SQL Server 설치 확인  
 Analysis Services Service가 실행 중인지 확인합니다.  
  
1.  Microsoft Windows에서 **시작**, **모든 프로그램**, **Microsoft SQL Server 2012** 그룹을 차례로 클릭합니다.  
  
2.  **SQL Server Management Studio**를 클릭합니다.  
  
3.  Analysis Services 인스턴스(예: **[서버 이름]\POWERPIVOT**)에 연결합니다. 인스턴스에 연결할 수 있는 경우 서비스가 실행 중인 것입니다.  
  
##  <a name="bkmk_config"></a> 2단계: Basic Analysis Services SharePoint 통합 구성  
 다음 단계에서는 SharePoint 문서 라이브러리에서 Excel 고급 데이터 모델과 상호 작용하는 데 필요한 구성 변경 내용에 대해 설명합니다. SharePoint Server 2013 및 SQL Server Analysis Services를 설치한 후 이 단계를 수행합니다.  
  
### <a name="grant-excel-services-server-administration-rights-on-analysis-services"></a>Analysis Services에 Excel Services 서버 관리 권한 부여  
 Analysis Services를 설치하는 동안 Excel Services 애플리케이션 서비스 계정을 Analysis Services 관리자로 추가했다면 이 섹션을 완료하지 않아도 됩니다.  
  
1.  Analysis Services 서버에서 SQL Server Management Studio를 시작하고 Analysis Services 인스턴스에 연결합니다(예: `[MyServer]\POWERPIVOT`).  
  
2.  개체 탐색기에서 인스턴스 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
     ![SSAS 서버 속성 보기](../../../sql-server/install/media/as-ssms-proeprties.gif "SSAS 서버 속성 보기")  
  
3.  왼쪽 창에서 **보안**을 클릭합니다. 1단계에서 Excel Services 애플리케이션에 대해 구성한 도메인 로그인을 추가합니다.  
  
     ![SSAS 서버의 보안 설정을](../../../sql-server/install/media/as-ssms-security.gif "SSAS 서버의 보안 설정")  
  
### <a name="configure-excel-services-for-analysis-services-integration"></a>Analysis Services 통합을 위한 Excel Services 구성  
  
1.  SharePoint 중앙 관리의 애플리케이션 관리 그룹에서 **서비스 애플리케이션 관리**를 클릭합니다.  
  
2.  서비스 애플리케이션 이름을 클릭합니다. 기본값은 **Excel Services 애플리케이션**입니다.  
  
3.  **Excel Services 응용 프로그램 관리 페이지**에서 **데이터 모델 설정**을 클릭합니다.  
  
4.  **서버 추가**를 클릭합니다.  
  
5.  **서버 이름**에 Analysis Services 서버 이름과 PowerPivot 인스턴스 이름을 입력합니다. 예를 들면 `MyServer\POWERPIVOT`입니다. PowerPivot 인스턴스 이름이 필요합니다.  
  
     설명을 입력합니다.  
  
6.  **확인**을 클릭합니다.  
  
7.  변경 내용은 몇 분 후에 적용됩니다. 또는 **Excel 계산 서비스** 를 **중지** 하고 **시작**할 수 있습니다. 수행할 작업  
  
     다른 옵션은 관리 권한으로 명령 프롬프트를 열고 `iisreset /noforce`를 입력하는 것입니다.  
  
     ULS 블로그의 항목을 검토하여 서버가 Excel Services에서 인식되는지 확인할 수 있습니다. 다음과 유사한 항목이 표시됩니다.  
  
    ```  
    Excel Services Application            Data Model        27           Medium                Check Administrator Access ([ServerName]\POWERPIVOT): Pass.        f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Server Version ([ServerName]\POWERPIVOT): Pass (11.0.2809.24 >= 11.0.2800.0).         f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Deployment Mode ([ServerName]\POWERPIVOT): Pass.            f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
  
    ```  
  
##  <a name="bkmk_verify"></a> 3단계 통합 확인  
 다음 단계에서는 새 통합 문서를 만들고 업로드하여 Analysis Services 통합을 확인하는 방법을 단계별로 설명합니다. 이들 단계를 완료하려면 SQL Server 데이터베이스가 필요합니다.  
  
1.  **참고:** 슬라이서 또는 필터가 포함된 고급 통합 문서가 이미 있는 경우 이 통합 문서를 SharePoint 문서 라이브러리에 업로드하고 문서 라이브러리 뷰에서 슬라이서 및 필터와 상호 작용할 수 있는지 확인할 수 있습니다.  
  
2.  Excel에서 새 통합 문서를 시작합니다.  
  
3.  데이터 탭의 **외부 데이터 가져오기** 에 있는 리본에서 **기타 원본**을 클릭합니다.  
  
4.  **SQL Server**를 선택합니다.  
  
5.  **데이터 연결 마법사**에 사용할 데이터베이스가 있는 SQL Server 인스턴스 이름을 입력합니다.  
  
6.  또는 로그온 자격 증명을 통해 **Windows 인증 사용** 이 선택되어 있는지 확인한 후 **다음**을 클릭합니다.  
  
7.  사용할 데이터베이스를 선택합니다.  
  
8.  **특정 테이블에 연결** 확인란이 선택되어 있는지 확인합니다.  
  
9. **여러 테이블 선택 가능 및 Excel 데이터 모델에 테이블 추가** 확인란을 클릭합니다.  
  
10. 가져올 테이블을 선택합니다.  
  
11. **선택한 테이블 간의 관계 가져오기**확인란을 클릭한 후 **다음**을 클릭합니다. 관계형 데이터베이스에서 여러 테이블을 가져오면 이미 관련된 테이블로 작업할 수 있습니다. 관계를 수동으로 만들지 않아도 되므로 단계를 저장합니다.  
  
12. 마법사의 **데이터 연결 파일 저장 및 마침** 페이지에서 연결의 이름을 입력하고 **마침**을 클릭합니다.  
  
13. **데이터 가져오기** 대화 상자가 표시됩니다. **PivotTable 보고서**를 선택한 다음 **확인**을 클릭합니다.  
  
14. PivotTable 필드 목록이 통합 문서에 나타납니다.   
    필드 목록에서 **모두** 탭을 클릭합니다.  
  
15. 필드 목록의 행, 열 및 값 영역에 필드를 추가합니다.  
  
16. 슬라이서 또는 필터를 PivotTable에 추가합니다. **이 단계를 건너뛰지 마세요**. 슬라이서 또는 필터는 Analysis Services 설치를 확인하는 데 도움을 주는 요소입니다.  
  
17. 통합 문서를 Excel Services가 구성된 SharePoint Server 2013의 문서 라이브러리에 저장합니다. 파일 공유에 통합 문서를 저장한 다음 SharePoint Server 2013 문서 라이브러리에 업로드할 수도 있습니다.  
  
18. 통합 문서 이름을 클릭하여 SharePoint에서 보고 슬라이서를 클릭하거나 이전에 추가한 필터를 변경합니다. 데이터 업데이트가 발생하면 Analysis Services가 설치되었고 Excel Services에 사용할 수 있음을 의미합니다. Excel에서 통합 문서를 여는 경우 Analysis Services 서버를 사용하지 않고 캐시된 복사본을 사용하게 됩니다.  
  
##  <a name="bkmk_firewall"></a> Analysis Services 액세스를 허용하도록 Windows 방화벽 구성  
 항목의 정보를 사용 [Analysis Services 액세스를 허용 하도록 Windows 방화벽 구성](../configure-the-windows-firewall-to-allow-analysis-services-access.md) SharePoint 용 PowerPivot 또는 Analysis Services에 대 한 액세스를 허용 하도록 방화벽의 포트 차단을 해제 해야 하는지 여부를 확인 하려면. 이 항목에서 제공하는 단계를 수행하여 포트와 방화벽 설정을 모두 구성할 수 있습니다. 실제로는 Analysis Services 서버에 대한 액세스를 허용하기 위해 이러한 단계를 함께 수행해야 합니다.  
  
##  <a name="bkmk_upgrade_workbook"></a> 통합 문서 업그레이드 및 예약된 데이터 새로 고침  
 이전 버전의 PowerPivot에서 만든 통합 문서를 업그레이드 하는 데 필요한 단계는 통합 문서를 만든 PowerPivot의 버전에 따라 달라집니다. 자세한 내용은 [통합 문서 업그레이드 및 예약된 데이터 새로 고침&#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)을 검토하세요.  
  
##  <a name="bkmk_multiple_servers"></a> Microsoft SharePoint 용 PowerPivot 단일 서버 설치 – 초과  
 **WFE (웹 프런트 엔드)** 나 **중간 계층:**: 사용 하는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 설치관리자패키지를실행하는서버를팜에추가PowerPivot기능을설치하려면더큰SharePoint팜에SharePoint모드의**spPowerPivot.msi** 각 SharePoint 서버에 있습니다. Sppowerpivot.msi는 필요한 데이터 공급자와 SharePoint 2013용 PowerPivot 구성 도구를 설치합니다.  
  
 중간 계층 설치 및 구성에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [설치 하거나 SharePoint 추가 기능에 대 한 PowerPivot을 제거할 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   .msi를 다운로드하려면 [Microsoft SharePoint 2013용 Microsoft SQL Server 2014 PowerPivot](http://go.microsoft.com/fwlink/?LinkID=324854)을 참조하십시오.  
  
-   [PowerPivot 구성 및 솔루션 배포 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
 **중복 및 서버 부하:** 설치는 두 번째 이상의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] SharePoint 모드의 서버 중복성을 제공 합니다는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서버 기능입니다. 또한 서버 간에 부하가 분산됩니다. 자세한 내용은 다음 항목을 참조하세요.  
  
-   [Excel 서비스에서 데이터 모델 처리를 위해 Analysis Services 구성](http://technet.microsoft.com/library/jj614437\(v=office.15\)) (http://technet.microsoft.com/library/jj614437(v=office.15))합니다.  
  
-   [Excel Services 데이터 모델 설정 (SharePoint Server 2013)를 관리할](http://technet.microsoft.com/library/jj219780\(v=office.15\)) (http://technet.microsoft.com/library/jj219780(v=office.15))합니다.  
  
 ![SharePoint 설정](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 설정") [Microsoft SQL Server Connect를 통해 사용자 의견 및 담당자 정보 제출](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [PowerPivot을 SharePoint 2013으로 마이그레이션](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [설치 하거나 SharePoint 추가 기능에 대 한 PowerPivot을 제거할 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [예약 된 데이터 새로 고침 및 통합 문서 업그레이드 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
