---
title: '배포 검사 목록: SharePoint용 PowerPivot 2010의 다중 서버 설치 | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 4380040a-1368-4a47-8930-47c65a192e59
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 33bbaf46bb4dee5e0e7b58f6dc179ae5647ee3e7
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890734"
---
# <a name="deployment-checklist-multi-server-installation-of-powerpivot-for-sharepoint-2010"></a>배포 검사 목록: SharePoint 2010용 PowerPivot의 다중 서버 설치
  이 검사 목록에서는 처음부터 작성 하는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 3 계층 sharepoint 2010 팜에 sharepoint 용을 추가 하는 단계를 안내 합니다. 3계층 팜에는 데이터베이스, 애플리케이션 및 웹 계층이 포함되어 있습니다. 이 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 토폴로지에를 추가 하려면 SQL Server 설치 프로그램을 실행 하 여 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 응용 프로그램 계층에를 설치 해야 합니다. PowerPivot 프로그램 파일은 웹 계층에 추가 되지만 웹 응용 프로그램을 배포할 때 설치 후 작업 으로만 추가 됩니다. 웹 계층이나 데이터 계층에는 배포 단계는 있지만 별도로 수행해야 하는 설치 단계는 없습니다. 응용 프로그램 서버에를 설치 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 하는 경우에만 수행 해야 하는 설치 단계가 있습니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
  
  
## <a name="prerequisites"></a>사전 요구 사항  
 SQL Server 및 SharePoint 2010을 설치하려면 로컬 관리자여야 합니다.  
  
 SharePoint를 설치하는 관리자가 팜도 구성해야 합니다. 팜을 구성하려면 데이터베이스 서버에 SQL Server 로그인이 있어야 합니다. 로그인은, `dbcreator` `securityadmin` 및 `public`역할에 할당 되어야 합니다.  
  
 SharePoint Server 2010의 엔터프라이즈 또는 엔터프라이즈 평가판 버전이 있어야 합니다.  
  
 컴퓨터가 도메인에 조인되어 있어야 합니다.  
  
 SharePoint 통합 모드에서 데이터베이스 엔진, 팜의 서비스 및 Analysis Services를 실행하는 데 사용할 계정을 알고 있어야 합니다. 이들 계정은 설치 과정에서 처음으로 지정합니다. 나중에 이러한 계정을 변경할 수 있습니다.  
  
 설치 중 지정하는 서비스 계정은 도메인 사용자 계정이어야 합니다.  
  
 설치를 시작하기 전에 브라우저 설정을 확인하여 인터넷에 연결되어 있는지 확인합니다. 필수 구성 요소 설치 관리자가 필요한 소프트웨어를 다운로드하기 위해 인터넷 연결을 엽니다. 필요한 소프트웨어를 모두 가져오려면 다음 사항을 변경해야 합니다.  
  
-   서버 관리자에서 Internet Explorer 보안 강화 구성을 임시로 해제하여 서버로의 다운로드를 허용합니다. 필요한 소프트웨어를 다운로드하기 위해 관리자에 대해서만 IE ESC를 해제할 수 있습니다.  
  
-   Internet Explorer에서 프록시 서버를 무시하도록 브라우저를 구성하여 로컬 호스트가 인터넷 URL에 액세스하도록 허용해야 할 수도 있습니다.  
  
    1.  Internet Explorer의 도구 메뉴에서 인터넷 옵션을 클릭합니다.  
  
    2.  연결 탭의 LAN(Local Area Network) 설정 영역에서 LAN 설정을 클릭합니다.  
  
    3.  자동 구성 영역에서 자동으로 설정 검색 확인란의 선택을 취소합니다.  
  
    4.  프록시 서버 영역에서 사용자 LAN에 프록시 서버 사용 확인란을 선택합니다.  
  
    5.  주소 상자에 프록시 서버의 주소를 입력합니다.  
  
    6.  포트 상자에 프록시 서버의 포트 번호를 입력합니다.  
  
    7.  로컬 주소에 프록시 서버 사용 안 함 확인란을 선택합니다.  
  
    8.  확인을 클릭하여 LAN(Local Area Network) 설정 대화 상자를 닫습니다.  
  
    9. 확인을 클릭하여 인터넷 옵션 대화 상자를 닫습니다.  
  
##  <a name="installdb"></a>데이터베이스 서버 설치  
 이 항목에서는 팜 토폴로지가 [3 계층 팜을 위한 다중 서버](https://go.microsoft.com/fwlink/?LinkId=182771)문서에 설명 된 것을 기반으로 한다고 가정 합니다. 작동 중인 팜이 이미 있는 경우 [SharePoint용 PowerPivot 설치](#installppapp)로 건너뜁니다.  
  
 토폴로지를 처음 사용하려는 경우 SQL Server 데이터베이스 엔진 설치부터 시작합니다. 이 지침을 따르면 팜의 SharePoint 서버에서 액세스할 수 있는 데이터베이스 서버가 만들어집니다.  
  
1.  데이터베이스 서버에 사용 하는 컴퓨터에서 SQL Server 설치 프로그램을 실행 하 여 SQL Server 데이터베이스 엔진를 설치 합니다 ( [설치 마법사 &#40;&#41;설치에서 SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)참조).  
  
     설치할 기능을 선택할 때 다음을 선택합니다.  
  
    -   데이터베이스 엔진 서비스  
  
    -   클라이언트 도구 연결  
  
    -   관리 도구 - 전체(기본은 자동으로 포함됨)  
  
2.  데이터베이스 엔진이 설치되면 원격 연결에 대한 TCP/IP를 사용하도록 설정하고 서비스를 다시 시작합니다.  
  
    1.  SQL Server 구성 관리자를 시작합니다.  
  
    2.  SQL Server 네트워크 구성을 엽니다.  
  
    3.  **MSSQLSERVER에 대한 프로토콜**을 선택합니다.  
  
    4.  **Tcp/ip** 를 마우스 오른쪽 단추로 클릭 하 고 **사용**을 선택 합니다.  
  
    5.  **SQL Server Services**를 클릭 합니다.  
  
    6.  **SQL Server (MSSQLSERVER)** 를 마우스 오른쪽 단추로 클릭 하 고 **다시 시작**을 클릭 합니다.  
  
3.  Windows 방화벽을 통한 데이터베이스 서버로의 인바운드 액세스를 사용하도록 설정합니다. 이렇게 하면 팜의 SharePoint 서버가 SharePoint 데이터베이스에 연결할 수 있습니다. 자세한 내용은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)을 참조하세요.  
  
    1.  Windows 제어판의 관리 도구에서 **고급 보안이 포함 된 Windows 방화벽**을 클릭 합니다.  
  
    2.  **인바운드 규칙**을 클릭 합니다.  
  
    3.  **새 규칙**을 클릭 합니다.  
  
    4.  규칙 유형에서 **사용자 지정**을 클릭 합니다.  
  
    5.  **다음**을 클릭합니다.  
  
    6.  프로그램의 서비스 섹션에서 **사용자 지정**을 클릭 합니다.  
  
    7.  **이 서비스에 적용을**클릭 합니다.  
  
    8.  SQL Server를 기본 인스턴스로 설치한 경우 **SQL Server (MSSQLSERVER)** 를 선택 하 고 **확인**을 클릭 합니다.  
  
    9. **다음**을 클릭합니다.  
  
    10. 프로토콜 및 포트에서 기본 설정을 그대로 적용 하 고 **다음**을 클릭 합니다.  
  
    11. 범위에서 기본 설정을 그대로 적용 하 고 **다음**을 클릭 합니다.  
  
    12. 작업에서 기본 설정을 그대로 적용 하 고 **다음**을 클릭 합니다.  
  
    13. 프로필에서 **개인** 및 **공용**에 대 한 확인란의 선택을 취소 하 고 **다음**을 클릭 합니다.  
  
    14. 이름에 인바운드 규칙을 설명 하는 이름을 입력 합니다 (예: **SQL Server**).  
  
    15. **마침**을 클릭합니다.  
  
##  <a name="installsp"></a>3 계층 SharePoint 2010 팜 설치 및 구성  
 SharePoint 서버로 사용할 컴퓨터 각각에서 SharePoint 필수 구성 요소 설치 관리자 프로그램을 실행한 다음 SharePoint Server 설치 프로그램을 실행합니다.  
  
 SharePoint 2010 설명서의 다음 지침을 사용하여 두 개의 웹 서버와 한 개의 애플리케이션 서버가 포함된 SharePoint 2010 팜을 설치하고 구성합니다.  
  
 [3 계층 팜을 위한 다중 서버 (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=182771)  
  
 데이터베이스 서버를 지정하라는 메시지가 표시되면 앞서 설치한 데이터베이스 서버를 지정합니다.  
  
 이후의 절차에서는 3계층 팜 설치에 대해 제공된 지침을 사용하여 팜을 구성했다고 가정합니다. 팜에는 다음 서비스 및 기능이 포함되어야 합니다.  
  
-   Excel 서비스, 검색 서비스 및 Secure Store Service  
  
-   웹 애플리케이션 및 사이트 컬렉션  
  
-   사용 현황 및 상태 데이터 수집  
  
-   진단 로깅  
  
##  <a name="installppapp"></a>응용 프로그램 서버에 SharePoint용 PowerPivot 설치  
 SQL Server 설치 프로그램을 실행하여 SharePoint 팜에 SharePoint용 PowerPivot을 추가합니다. 팜이 여러 SharePoint 서버로 구성된 경우에는 이미 팜에 조인된 애플리케이션 서버에서 SQL Server 설치 프로그램을 실행해야 합니다.  
  
 항상 애플리케이션 서버에 SharePoint용 PowerPivot을 설치합니다. 또한 웹 프런트 엔드 서버도 SharePoint용 PowerPivot 서버 구성 요소를 실행하지만 웹 프런트 엔드에서 실행되는 구성 요소는 팜에 솔루션 배포 시 SharePoint용 PowerPivot 구성 단계 동안 설치됩니다. 설치에 대 한 자세한 내용은 [SharePoint용 PowerPivot 2010 설치](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)를 참조 하세요.  
  
 배포 토폴로지가 2개의 SharePoint용 PowerPivot 인스턴스를 호출할 경우 각 애플리케이션 서버에서 SQL Server 설치를 실행합니다. 하나의 컴퓨터에서 SharePoint용 PowerPivot 인스턴스를 하나만 사용할 수 있습니다. 여러 인스턴스가 필요하면 추가 서버를 사용해야 합니다. 동일한 팜에 [여러 SharePoint용 PowerPivot 서버를 추가 하는 방법에 대 한 자세한 내용은 배포 검사 목록: SharePoint 2010 팜에](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)PowerPivot 서버를 추가 하 여 확장 합니다.  
  
##  <a name="installclientlib"></a>SharePoint용 PowerPivot가 설치 되지 않은 SharePoint 응용 프로그램 서버에 Analysis Services 클라이언트 라이브러리를 설치 합니다.  
 동일 컴퓨터에 SharePoint용 PowerPivot을 설치하지 않은 상태로 다음 애플리케이션을 실행하는 웹 프런트 또는 애플리케이션 서버를 포함하는 팜 토폴로지에는 PowerPivot 데이터 액세스 및 기능을 지원하기 위해 추가 소프트웨어가 필요합니다.  
  
-   Excel 서비스 또는 PerformancePoint 서비스  
  
-   고유 서버에서 독립 실행형 애플리케이션으로 실행되는 중앙 관리  
  
 PowerPivot 데이터 액세스를 지원하기 위해서는 Excel Services 및 PerformancePoint Services 모두 새 버전의 Analysis Services OLE DB Provider가 필요합니다. 최신 OLE DB Provider가 없는 컴퓨터에서 애플리케이션을 실행할 경우 공급자를 수동으로 설치해야 합니다. 자세한 내용은 [SharePoint 서버에 Analysis Services OLE DB Provider 설치](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) 를 참조 하세요.  
  
 마찬가지로 동일 컴퓨터에 SharePoint용 PowerPivot 없이 중앙 관리만 있는 컴퓨터에는 ADOMD.NET 클라이언트 라이브러리가 필요합니다. 이 라이브러리는 대시보드를 채우기 위해 사용하는 내부 데이터에 액세스하기 위해 PowerPivot 관리 대시보드에서 사용됩니다. 자세한 내용은 [중앙 관리를 실행하는 웹 프런트 엔드 서버에 ADOMD.NET 설치](../../../2014/sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md)를 참조하세요.  
  
##  <a name="configsrvr"></a>서버 구성  
 PowerPivot 구성 도구를 사용하여 SharePoint용 PowerPivot을 구성합니다. 이 도구는 팜의 기존 구성을 검사 하 고 SharePoint용 PowerPivot에 필요한 SharePoint 기능을 설치 하거나 활성화 하는 옵션을 제공 합니다. 이 단계 동안 Windows 토큰 서비스에 대한 클레임이 시작됩니다. 또한 다른 필요한 SharePoint 기능이 아직 활성화되지 않은 경우 구성 도구가 이러한 기능을 목록에 추가하고 기능 활성화를 위한 작업을 포함합니다.  
  
 자세한 내용은 [구성 또는 복구 SharePoint용 PowerPivot 2010 &#40;PowerPivot 구성 도구&#41;](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md)를 참조 하세요.  
  
##  <a name="AAM"></a>웹 프런트 엔드 서버에 대 한 대체 액세스 매핑 구성  
 PowerPivot 데이터 액세스 또는 데이터 새로 고침에 대한 요청을 각 웹 프런트 엔드 서버에서 처리하도록 하려면 각 서버의 서로 다른 URL을 동일한 웹 애플리케이션에 매핑해야 합니다.  
  
1.  중앙 관리의 응용 프로그램 관리에서 **대체 액세스 매핑 구성**을 클릭 합니다.  
  
2.  대체 액세스 매핑 컬렉션에서 사용하는 웹 응응 프로그램을 선택합니다.  
  
3.  **내부 URL 추가**를 클릭 합니다.  
  
4.  첫 번째 웹 프런트 엔드 서버의 URL을 지정합니다.  
  
5.  이전 단계를 반복하여 두 번째 웹 프런트 엔드 서버의 URL을 추가합니다.  
  
##  <a name="activatePP"></a>사이트 모음에 대 한 PowerPivot 기능 통합 활성화  
 사이트 컬렉션 수준에서 기능을 활성화하면 사이트에서 애플리케이션 페이지 및 템플릿을 사용할 수 있습니다. 여기에는 예약된 데이터 새로 고침에 대한 구성 페이지와 PowerPivot 갤러리 및 데이터 피드 라이브러리에 대한 애플리케이션 페이지가 포함됩니다.  
  
 PowerPivot 구성 도구가 지정한 사이트 컬렉션에 대한 기능 통합을 활성화합니다. 도구를 여러 번 실행하여 추가 사이트 컬렉션을 선택할 수 있습니다. 또한 사이트 관리자가 SharePoint 내에서 기능 활성화를 구성할 수 있습니다. 자세한 내용은 [중앙 관리에서 사이트 모음에 대 한 PowerPivot 기능 통합 활성화](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)를 참조 하세요.  
  
##  <a name="verify"></a>통합 및 서버 가용성 확인  
 사용자 또는 애플리케이션이 PowerPivot 데이터를 포함하는 Excel 통합 문서를 열면 팜에서 PowerPivot 쿼리 처리가 수행됩니다. 최소한 SharePoint 사이트에서 페이지를 검사하여 PowerPivot 기능이 사용 가능한지를 확인할 수는 있습니다. 그러나 설치를 전체적으로 확인하려면 SharePoint에 게시하여 라이브러리에서 액세스할 수 있는 PowerPivot 통합 문서가 있어야 합니다. 테스트를 위해 이미 PowerPivot 데이터가 포함된 예제 통합 문서를 게시하여 SharePoint 통합이 올바르게 구성되어 있는지 확인하는 데 사용할 수 있습니다.  
  
 SharePoint 사이트와 PowerPivot의 통합을 확인하려면 다음을 수행하십시오.  
  
1.  앞서 만든 웹 애플리케이션을 브라우저에서 엽니다. 기본값을 사용 하는 경우 URL 주소 > http://\<your computer name을 지정할 수 있습니다.  
  
2.  PowerPivot 데이터 액세스 및 처리 기능을 애플리케이션에서 사용할 수 있는지 확인합니다. 이렇게 하려면 PowerPivot 제공 라이브러리 템플릿이 있는지 확인하면 됩니다.  
  
    1.  사이트 작업에서 **기타 옵션...** 을 클릭합니다.  
  
    2.  라이브러리에 **데이터 피드 라이브러리** 와 **PowerPivot 갤러리**가 모두 표시되어야 합니다. 이러한 라이브러리 템플릿은 PowerPivot 기능에서 제공하는 것이며 기능이 올바르게 통합되는 경우 라이브러리 목록에 표시됩니다.  
  
 서버에서 PowerPivot 데이터 액세스를 확인하려면 다음을 수행하십시오.  
  
1.  Reporting Services 자습서와 함께 제공되는 Picnic 데이터 예제를[다운로드](https://go.microsoft.com/fwlink/?LinkID=219108) 합니다. 이 다운로드에 포함된 예제 통합 문서를 사용하여 PowerPivot 데이터 액세스를 확인합니다. 파일의 압축을 풉니다.  
  
2.  PowerPivot 갤러리 또는 SharePoint 라이브러리에 PowerPivot 통합 문서를 업로드합니다.  
  
3.  문서를 클릭하여 라이브러리에서 엽니다.  
  
4.  슬라이서를 클릭하거나 데이터를 필터링하여 PowerPivot 쿼리를 시작합니다. 서버에서 PowerPivot 데이터가 백그라운드로 로드되고 결과가 반환됩니다. 다음 단계에서는 서버에 연결하여 데이터가 로드 및 캐시되는지 확인합니다.  
  
5.  시작 메뉴의 Microsoft SQL Server 2008 R2 프로그램 그룹에서 SQL Server Management Studio를 시작합니다. 이 도구가 서버에 설치되어 있지 않으면 마지막 단계로 건너뛰어 캐시된 파일이 있는지 확인하면 됩니다.  
  
6.  서버 유형에서 **Analysis  Services**를 선택합니다.  
  
7.  서버 이름에 서버 이름  **\<> \powerpivot**을 입력 합니다. 여기서  **\<server-name >** 은 SharePoint용 PowerPivot가 설치 된 컴퓨터의 이름입니다.  
  
8.  **연결**을 클릭합니다.  
  
9. 개체 탐색기에서 **데이터베이스** 를 클릭하여 로드된 PowerPivot 데이터 파일 목록을 확인합니다.  
  
10. 컴퓨터 파일 시스템의 다음 폴더에서 파일이 디스크로 캐시되었는지 확인합니다. 배포가 작동하는지 확인하려면 캐시된 파일이 있는지도 확인해야 합니다. 파일 캐시는 \Program Files\Microsoft SQL Server\MSAS10_50.POWERPIVOT\OLAP\Backup 폴더에서 확인할 수 있습니다.  
  
##  <a name="nextsteps"></a>사후 설치 단계  
 설치를 확인한 후에 PowerPivot 갤러리를 만들거나 개별 구성 설정을 조정하여 서비스 구성을 마칩니다. 앞서 설치한 모든 서버 구성 요소를 사용하려면 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]을 다운로드하여 첫 번째 PowerPivot  통합 문서를 만든 후에 게시하면 됩니다.  
  
####  <a name="bkmk_disk"></a>디스크 공간 사용량에 대 한 상한을 설정 합니다.  
 디스크로 캐시되는 PowerPivot 데이터 파일에 사용할 디스크 공간의 상한을 설정할 수 있습니다. 기본적으로 사용 가능한 모든 디스크 공간을 사용하도록 설정되어 있습니다. 디스크 공간 사용을 제한 하는 방법에 대 한 지침은 [디스크 공간 사용 &#40;SharePoint용 PowerPivot&#41;구성](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-disk-space-usage-power-pivot-for-sharepoint)을 참조 하세요.  
  
####  <a name="Upload"></a>SharePoint 웹 응용 프로그램에 대 한 파일 최대 업로드 크기 늘리기  
 PowerPivot 통합 문서는 대규모일 수 있으므로 최대 파일 업로드 크기를 늘려야 할 수 있습니다. 웹 응용 프로그램에 대한 최대 업로드 크기와 Excel 서비스의 최대 통합 문서 크기 등 두 가지 파일 크기 설정을 구성할 수 있습니다. 최대 파일 크기는 두 애플리케이션에서 같은 값으로 설정해야 합니다. 자세한 내용은 [SharePoint용 PowerPivot &#40;&#41;최대 파일 업로드 크기 구성](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint)을 참조 하세요.  
  
#### <a name="grant-sharepoint-permissions-to-workbook-users"></a>통합 문서 사용자에게 SharePoint 사용 권한 부여  
 통합 문서를 게시하거나 보려는 사용자에게는 SharePoint 사용 권한이 필요합니다. 게시 된 통합 문서를 확인 해야 하는 사용자에 게 **보기** 권한을 부여 하 고 통합 문서를 게시 또는 관리 하는 사용자에 게 사용 권한을 부여 해야 합니다. 사용 권한을 부여하려면 사이트 컬렉션 관리자여야 합니다.  
  
1.  사이트에서 **사이트 작업**을 클릭합니다.  
  
2.  **사이트 사용 권한**을 클릭합니다.  
  
3.  사이트 모음 **구성원** 그룹에 대 한 확인란을 선택 합니다.  
  
4.  리본 메뉴에서 **사용 권한 부여**를 클릭 합니다.  
  
5.  문서 추가 또는 제거 권한이 있어야 하는 Windows 도메인 사용자 또는 그룹 계정을 입력합니다.  
  
6.  **확인**을 클릭합니다.  
  
7.  사이트 모음 **방문자** 그룹의 확인란을 선택 합니다.  
  
8.  리본 메뉴에서 **사용 권한 부여**를 클릭 합니다.  
  
9. 문서 보기 권한이 있어야 하는 Windows 도메인 사용자 또는 그룹 계정을 입력합니다. 앞서 수행한 단계와 마찬가지로 애플리케이션이 기본 인증용으로 구성된 경우에는 전자 메일 주소 또는 메일 그룹을 사용하지 마십시오.  
  
10. **확인**을 클릭합니다.  
  
#### <a name="install-adonet-data-services-35-sp1"></a>ADO.NET Data Services 3.5 SP1 설치  
 SharePoint 목록의 데이터 피드 내보내기를 수행하려면 ADO.NET Data Services가 필요합니다. 이 구성 요소는 SharePoint 2010의 PrerequisiteInstaller 프로그램에 포함되어 있지 않으므로 수동으로 설치해야 합니다. ADO.NET Data Services를 설치 하는 방법에 대 한 자세한 내용은 [install ADO.NET Data Services를 참조 하 여 SharePoint 목록의 데이터 피드 내보내기를 지원](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)합니다.  
  
#### <a name="install-data-providers-used-in-data-refresh-and-check-user-permissions"></a>데이터 새로 고침 및 사용자 권한 확인에 사용된 데이터 공급자 설치  
 서버 쪽 데이터 새로 고침을 사용하면 사용자가 무인 모드에서 자신의 통합 문서로 업데이트된 데이터를 다시 가져올 수 있습니다. 데이터 새로 고침을 성공하려면 서버에 원래 데이터를 가져오는 데 사용된 것과 동일한 데이터 공급자가 있어야 합니다. 또한 데이터 새로 고침이 실행되는 사용자 계정에도 외부 데이터 원본에 대한 읽기 권한이 필요한 경우가 많습니다. 성공적인 결과를 얻기 위해서는 데이터 새로 고침 설정 및 구성에 대한 요구 사항을 확인해야 합니다. 자세한 내용은 [SharePoint 2010를 사용 하 여 PowerPivot 데이터 새로 고침](../../../2014/analysis-services/powerpivot-data-refresh-with-sharepoint-2010.md)을 참조 하세요.  
  
#### <a name="create-a-powerpivot-gallery"></a>PowerPivot 갤러리 만들기  
 PowerPivot 갤러리는 SharePoint 사이트에서 PowerPivot 통합 문서를 보는 데 사용되는 미리 보기 및 프레젠테이션 옵션을 포함하는 라이브러리입니다. 해당 미리 보기 기능을 사용하려면 PowerPivot 갤러리를 사용하여 PowerPivot 통합 문서를 게시하고 보는 것이 좋습니다. 또한 같은 SharePoint 서버에 Reporting Services도 배포하는 경우 PowerPivot 갤러리를 사용하여 보고서를 쉽게 만들 수 있습니다. PowerPivot 갤러리에서 보고서 작성기를 시작하여 게시된 PowerPivot 통합 문서를 기반으로 새 보고서를 만들 수 있습니다. 라이브러리를 만들고 사용 하는 방법에 대 한 자세한 내용은 [Powerpivot 갤러리 만들기 및 사용자 지정](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery) 및 [powerpivot 갤러리 사용](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/use-power-pivot-gallery)을 참조 하세요.  
  
#### <a name="tune-configuration-settings"></a>구성 설정 조정  
 PowerPivot 서비스 애플리케이션은 기본 속성 및 값을 사용하여 만들어집니다. 개별 서비스 애플리케이션에 대한 구성 설정을 수정하여 요청을 할당하는 방법을 변경하거나, 서버 제한 시간을 설정하거나, 쿼리 응답 보고서 이벤트의 임계값을 변경하거나, 사용 데이터 보관 기간을 지정할 수 있습니다. 중앙 관리의 구성 또는 SharePoint 웹 응용 프로그램에서 PowerPivot 기능을 사용 하는 방법에 대 한 자세한 내용은 [중앙 관리에서 Powerpivot 서버 관리 및 구성](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)을 참조 하세요.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2012 버전에서 지 원하는 기능](https://go.microsoft.com/fwlink/?linkid=232473)   
 [SharePoint용 PowerPivot 2010 설치](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)   
 [배포 검사 목록: SharePoint 2010 팜에 PowerPivot 서버를 추가 하 여 확장](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)  
  
  
