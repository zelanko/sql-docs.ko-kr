---
title: SharePoint용 PowerPivot 2010 | 설치 Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: eec38696-5e26-46fa-bc83-aa776f470ce8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 4eab56329c2b51f792394ffc37921e8a1ed8e117
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952250"
---
# <a name="install-powerpivot-for-sharepoint-2010"></a>SharePoint 2010용 PowerPivot 설치
  
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]은 SharePoint 2010 팜에서 PowerPivot 데이터 액세스를 제공하는 중간 계층 및 백 엔드 서비스의 모음입니다. 조직에서 클라이언트 애플리케이션인 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 2010을 사용하여 분석 데이터가 포함된 통합 문서를 만드는 경우 서버 환경에서 이러한 데이터에 액세스하려면 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 이 있어야 합니다. 이 항목에서는 기본 설치 과정을 안내하고 PowerPivot 구성에 도움이 되는 추가 항목에 대한 링크를 제공합니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2010|  
  
 
  
 동일한 서버에 및 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 를 설치 하는 방법에 대 한 지침은 [배포 검사 목록: Reporting Services, 파워 뷰 및 SharePoint용 PowerPivot](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)를 참조 하세요.  
  
## <a name="prerequisites"></a>사전 요구 사항  
  
1.  SQL Server 설치 프로그램을 실행하려면 로컬 관리자여야 합니다.  
  
2.  
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]을 사용하려면 SharePoint Server 2010 Enterprise Edition이 필요합니다. Evaluation Enterprise Edition을 사용할 수도 있습니다.  
  
3.  SharePoint Server 2010 SP2를 설치해야 합니다. 없을 경우 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기능을 사용하도록 팜을 구성할 수 없습니다.  
  
4.  컴퓨터가 도메인에 조인되어 있어야 합니다.  
  
5.  
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 프로비전하려면 도메인 사용자 계정이 있어야 합니다. 
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치 시에는 중앙 관리에서 관리할 수 있도록 Analysis Services 서비스 계정이 도메인 사용자 계정이어야 합니다. 이 문서의 단계를 수행하면서 **서버 구성** 페이지에 해당 계정 및 자격 증명을 입력하게 됩니다.  
  
6.  
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 인스턴스 이름을 사용할 수 있어야 합니다. SharePoint용 PowerPivot을 설치 중인 컴퓨터에 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 이라고 명명된 기존 인스턴스가 있어서는 안 됩니다.  
  
7.  
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 인스턴스는 SQL Server 장애 조치(Failover) 클러스터의 일부가 될 수 없습니다. SharePoint 제품의 고가용성 기능 사용 예를 들어, Excel Services는 SharePoint용 PowerPivot 서버의 부하 분산을 관리합니다. 자세한 내용은 [Excel Services 데이터 모델 설정 관리 (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx) (https://technet.microsoft.com/library/jj219780.aspx))를 참조 하세요.  
  
8.  기존 팜에 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 을 설치하는 경우 클래식 모드 인증을 사용하도록 구성된 SharePoint 웹 애플리케이션이 하나 이상 필요합니다. 
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 액세스는 웹 애플리케이션에서 클래식 모드 인증이 지원되는 경우에만 작동합니다. 클래식 모드 요구 사항에 대한 자세한 내용은 [PowerPivot Authentication and Authorization](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization)를 참조하십시오.  
  
9. 시스템 및 버전 요구 사항을 이해하려면 다음 항목을 검토하십시오.  
  
    -   [SharePoint 2010 팜에서 SQL Server BI 기능을 사용하기 위한 지침](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
##  <a name="InstallSQL"></a>1 단계: SharePoint용 PowerPivot 설치  
 이 단계에서는 SQL Server 설치 프로그램을 실행하여 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]을 설치합니다. 이후 단계에서는 서버를 사후 설치 태스크로 구성합니다.  
  
1.  설치 미디어를 삽입하거나 SQL Server에 대한 설치 파일이 포함된 폴더를 열고 **setup.exe**를 두 번 클릭합니다.  
  
2.  왼쪽 탐색 창에서 **설치** 를 클릭합니다.  
  
3.  
  **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**를 클릭합니다.  
  
4.  
  **제품 키** 페이지에서 평가판 버전을 지정하거나 라이선스를 받은 엔터프라이즈 버전의 제품 키를 입력하고  
  
     **다음**을 클릭합니다.  
  
5.  Microsoft 소프트웨어 사용권 계약에 동의합니다. 사용자 환경 및 오류 보고를 설정해 주시면 감사하겠습니다. **다음**을 클릭합니다.  
  
6.  설치 파일을 업그레이드할 것인지 묻는 메시지가 나타나면 설치 파일을 업그레이드합니다.  
  
7.  
  **설치 규칙** 페이지에는 설치에 방해가 될 수 있는 모든 문제가 표시됩니다. 목록을 검토하여 설치 프로그램이 시스템에 잠재적 문제를 감지했는지 여부를 확인합니다.  
  
    > [!NOTE]  
    >  Windows 방화벽이 설정되었기 때문에 원격 액세스를 사용할 수 있도록 포트를 열라는 경고가 표시됩니다. 일반적으로 이 경고는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치에는 해당되지 않습니다. 
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 및 데이터 파일에 연결할 때는 이미 SharePoint 서비스 간 통신용으로 열려 있는 SharePoint 포트를 사용합니다.  
  
     **다음**을 클릭합니다. SQL Server 설치 프로그램 파일이 서버에 설치되는 동안 기다려 주십시오.  
  
8.  
  **설치 역할** 페이지에서 **SQL Server SharePoint용 PowerPivot**을 선택합니다.  
  
9. 또는 설치에 데이터베이스 엔진 인스턴스를 추가할 수 있습니다. 새 팜을 설정 하 고 팜의 구성 및 콘텐츠 데이터베이스를 실행 하기 위해 데이터베이스 서버가 필요한 경우이 작업을 수행할 수 있습니다. 데이터베이스 엔진을 추가할 경우 PowerPivot이라고 명명된 인스턴스로 설치됩니다. 이 인스턴스에 대 한 연결을 지정 해야 하는 경우 (예: 팜 구성 마법사에서 해당 마법사를 사용 하 여 팜을 구성 하는 경우), <`servername`> \powerpivot. 형식으로 데이터베이스 이름을 입력 합니다.  
  
     ![GMNI_SetupUI_FeatureRole](../../../2014/sql-server/install/media/gmni-setupui-featurerole.gif "GMNI_SetupUI_FeatureRole")  
  
10. **다음**을 클릭합니다.  
  
11. 
  **기능 선택** 페이지에서 설치할 기능의 읽기 전용 목록이 확인용으로 표시됩니다. 해당 역할에 대해 미리 선택되어 있는 항목을 추가하거나 제거할 수는 없습니다. **다음**을 클릭합니다.  
  
12. 
  **기능 규칙** 페이지에서 **다음**을 클릭합니다. 이 페이지는 건너뛸 수 있습니다.  
  
13. 
  **인스턴스 구성** 페이지에서 확인용으로 'PowerPivot'이라는 읽기 전용 인스턴스 이름이 표시됩니다. 
  **POWERPIVOT** 이라는 인스턴스 이름은 **필수이며 수정할 수 없습니다**. 그러나 고유한 인스턴스 ID를 입력해 인스턴스를 설명하는 디렉터리 이름과 레지스트리 키를 지정할 수는 있습니다. **다음**을 클릭합니다.  
  
14. 
  **서버 구성** 페이지에서 원하는 계정 정보를 입력합니다.  
  
     SQL Server Analysis Services에 대해서는 도메인 사용자 계정을 지정해야 합니다. 기본 제공 계정을 지정하지 마십시오. 도메인 계정은 SharePoint 중앙 관리에서 Analysis Services 서비스 계정을 *관리 계정* 으로 관리하는 데 필요합니다.  
  
     ![SSAS Server 구성](../../../2014/sql-server/install/media/ssas-powerpivotsetupsql2012sp1-serverconfiguration.gif "SSAS Server 구성")  
  
     SQL Server 데이터베이스 엔진 및 SQL Server 에이전트를 추가한 경우 도메인 사용자 계정으로 실행하거나 기본 가상 계정으로 실행하도록 서비스를 구성할 수 있습니다.  
  
     서비스를 제공하기 위해 사용자의 도메인 사용자 계정을 사용하지 마십시오. 그렇게 하면 네트워크에서 리소스에 대해 갖는 권한과 동일한 권한이 서버에 부여됩니다. 악의적인 사용자가 서버를 침해한 경우 해당 사용자가 사용자의 도메인 자격 증명으로 로그인한 후 사용자와 동일한 데이터 및 애플리케이션을 다운로드하거나 사용할 수 있습니다.  
  
15. **다음**을 클릭합니다.  
  
16. 데이터베이스 엔진을 설치하는 경우 데이터베이스 엔진 구성 페이지가 나타납니다. 데이터베이스 엔진 구성에서 **현재 사용자 추가** 를 클릭하여 사용자 계정에 데이터베이스 엔진 인스턴스에 대한 관리자 권한을 부여합니다. 다른 계정을 추가하려면 **추가** 를 클릭합니다. **다음**을 클릭합니다.  
  
17. 
  **Analysis Services 구성** 페이지에서 **현재 사용자 추가** 를 클릭하여 사용자 계정에 관리 권한을 부여합니다. 설치가 완료된 후 서버를 구성하려면 관리 권한이 필요합니다.  
  
18. 같은 페이지에서 관리 권한이 필요한 모든 사용자의 Windows 사용자 계정을 추가합니다. 예를 들어 SQL Server Management Studio에서 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 인스턴스에 연결하여 데이터베이스 연결 문제를 해결하거나 버전 정보를 가져오려는 모든 사용자에게는 서버에 대한 시스템 관리자 권한이 있어야 합니다. 현재 서버 문제를 해결하거나 서버를 관리해야 하는 사용자의 계정을 추가합니다.  
  
19. **다음**을 클릭합니다.  
  
20. 나머지 페이지에서 각각 **다음** 을 클릭하여 설치 준비 페이지까지 이동합니다.  
  
21. 
  **설치**를 클릭합니다.  
  
> [!TIP]  
>  SQL Server 설치 문제를 해결하려면 [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)를 참조하십시오.  
  
##  <a name="bkmk_config"></a>2 단계: 서버 구성  
  
> [!IMPORTANT]  
>  
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 데이터베이스 서버를 사용하는 SharePoint 팜 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 을 구성하려면 먼저 SharePoint 2010 SP2를 설치해야 합니다. 서비스 팩을 아직 설치하지 않았으면 서버를 구성하기 전에 지금 설치합니다.  
  
 서버가 구성되기 전에는 설치가 완료되지 않습니다. 이 버전에서는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구, 중앙 관리 또는 PowerShell 중 하나를 사용하여 서버 구성이 항상 사후 설치 태스크로 수행됩니다. 계속하려면 다음 방법 중 하나를 선택합니다.  
  
-   [SharePoint용 PowerPivot 2010 &#40;PowerPivot 구성 도구&#41;구성 또는 복구](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md)  
  
-   [중앙 관리에서 PowerPivot 서버 관리 및 구성](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)  
  
-   [Windows PowerShell을 사용하여 PowerPivot 구성](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)  
  
 **데이터베이스 엔진 인스턴스에 연결합니다.** 
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]을 설치한 경우 SQL Server 설치 프로그램에서 설치에 데이터베이스 엔진 인스턴스를 추가할 수 있는 옵션을 제공했습니다. 새 팜을 설정 하 고 팜의 구성 및 콘텐츠 데이터베이스를 실행 하기 위해 데이터베이스 서버가 필요한 경우 설치에 데이터베이스 엔진 인스턴스를 추가 했을 수 있습니다. 데이터베이스 엔진을 추가한 경우 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 이라고 명명된 인스턴스로 설치되었습니다. 이 인스턴스에 대 한 연결을 지정 해야 하는 경우 (예: 팜 구성 마법사에서 해당 마법사를 사용 하 여 팜을 구성 하는 경우)에는 <`servername`> \powerpivot. 형식으로 데이터베이스 이름을 입력 해야 합니다.  
  
##  <a name="bkmk_redist"></a>3 단계: Excel Services 응용 프로그램 서버에 Analysis Services OLE DB 공급자 설치  
 별도의 애플리케이션 서버에서 Excel 계산 서비스 및 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을 실행하는 경우 추가 설치 단계가 필요합니다. Excel Calculation Services를 실행하는 애플리케이션 서버에서 적절한 Analysis Services OLE DB(MSOLAP) 공급자 버전을 설치합니다.  
  
-   MSOLAP의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전은 SQL Server 설치 프로그램에 포함되어 있으므로 애플리케이션 서버가 PowerPivot 애플리케이션 서버가 아닌 경우에만 MSOLAP의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전을 명시적으로 설치할 필요가 있습니다.  
  
    > [!NOTE]  
    >  Excel Calculation Services 애플리케이션 서버에도 전역 어셈블리의 **Microsoft.AnalysisServices.Xmla.dll** 파일 인스턴스가 필요합니다. 애플리케이션 서버에 .dll을 설치하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 설치해야 합니다. SQL Server 설치 마법사의 **기능 선택** 페이지에서 "관리 도구-전체"를 선택 합니다.  
  
-   애플리케이션 서버에서 이전 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서를 지원하도록 하려면 MSOLAP의 SQL Server 2008 R2 버전을 설치해야 합니다.  
  
 확인 단계를 포함하여 공급자를 설치하는 방법은 [Install the Analysis Services OLE DB Provider on SharePoint Servers](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)를 참조하십시오.  
  
##  <a name="bkmk_verify"></a>4 단계: 설치 확인  
 이 마지막 단계에서는 SharePoint 2010과 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 이 완벽하게 작동하는지 확인합니다. 자세한 내용은 [Verify a PowerPivot for SharePoint Installation](https://docs.microsoft.com/analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SharePoint용 PowerPivot 2010 설치](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [배포 검사 목록: Reporting Services, 파워 뷰 및 SharePoint용 PowerPivot](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)   
 [배포 검사 목록: SharePoint 2010 팜에 PowerPivot 서버를 추가 하 여 확장](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)   
 [배포 검사 목록: SharePoint용 PowerPivot 2010의 다중 서버 설치](../../../2014/sql-server/install/deployment-checklist-multiserver-installation-powerpivot-sharepoint-2010.md)  
  
  
