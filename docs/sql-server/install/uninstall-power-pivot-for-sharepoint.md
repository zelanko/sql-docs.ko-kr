---
title: SharePoint용 파워 피벗 제거 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: install
ms.reviewer: ''
ms.suite: sql
ms.technology: setup-install
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3941a2f0-0d0c-4d1a-8618-7a6a7751beac
caps.latest.revision: 27
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 702a6dc176d2f3a86f8691f181c4a4728a605a95
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="uninstall-power-pivot-for-sharepoint"></a>SharePoint용 Power Pivot 제거
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치 제거는 제거를 준비하고, 팜에서 기능과 솔루션을 제거하고, 프로그램 파일과 레지스트리 설정을 제거하는 작업으로 구성된 다단계 작업입니다.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **문서 내용:**  
  
-   [필수 구성 요소](#prereq)  
  
-   [1단계: 제거 전 검사 목록](#bkmk_before)  
  
-   [2단계: SharePoint에서 기능 및 솔루션 제거](#bkmk_remove)  
  
-   [3단계: SQL Server 설치 프로그램을 실행하여 로컬 컴퓨터에서 프로그램 제거](#bkmk_uninstall)  
  
-   [4단계: SharePoint용 Power Pivot 추가 기능 제거](#bkmk_addin)  
  
-   [5단계: 제거 확인](#verify)  
  
-   [6단계: 제거 후 검사 목록](#bkmk_post)  
  
##  <a name="prereq"></a> 필수 구성 요소  
  
-   팜의 기능과 솔루션을 제거하려면 SharePoint 팜 관리자 또는 서비스 응용 프로그램 관리자여야 합니다.  
  
-   데이터베이스 엔진도 제거할 경우 SQL Server 시스템 관리자 및 로컬 Administrators 그룹의 구성원이어야 합니다.  
  
-   Analysis Services 및 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]를 제거하려면 Analysis Services 시스템 관리자 및 로컬 Administrators 그룹의 구성원이어야 합니다.  
  
##  <a name="bkmk_before"></a> 1단계: 제거 전 검사 목록  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 액세스할 수 없게 됩니다. 맨 먼저 더 이상 작동되지 않는 파일 및 라이브러리를 삭제해야 합니다. 이렇게 하면 소프트웨어를 제거하기 전에 '누락된 데이터'에 대한 질문이나 문제를 해결할 수 있습니다.  
  
1.  SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치와 연결된 모든 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서, 문서 및 라이브러리를 삭제합니다. 소프트웨어가 제거되면 라이브러리와 문서가 작동하지 않습니다.  
  
    -   [파워 피벗 갤러리 삭제](../../analysis-services/power-pivot-sharepoint/delete-power-pivot-gallery.md)  
  
    -   [Power Pivot 데이터 피드 라이브러리 삭제](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)  
  
2.  다른 라이브러리에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터를 포함하거나 참조하는 Excel 통합 문서 또는 Reporting Services 보고서를 삭제합니다.  
  
3.  PerformancePoint 대시보드에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터를 참조하는 모든 웹 파트를 제거합니다.  
  
4.  기존 사이트 및 라이브러리에서 SharePoint 사용 권한을 검토하여 이러한 권한을 변경해야 하는지 확인합니다. 일부 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 액세스 시나리오, 특히 URL 연결 문자열을 통해 다른 통합 문서의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 액세스하는 보조 데이터 액세스에는 일반적으로 사이트를 방문하기만 하는 SharePoint 사용자에게 할당되는 보기 권한보다 높은 읽기 권한이 필요합니다. 읽기 권한이 더 이상 필요하지 않은 경우에는 사용 권한을 적절히 축소할 수 있습니다.  
  
5.  필요한 경우 서비스를 중지하고 소프트웨어를 제거하기 전에 며칠 정도 기다립니다. 이 단계는 제거에 반드시 필요한 것은 아니지만 데이터 마이그레이션 또는 기술 대체 문제가 발생한 경우 서비스를 일시적으로 재개할 수 있는 기회를 제공합니다.  
  
##  <a name="bkmk_remove"></a> 2단계: SharePoint에서 기능 및 솔루션 제거  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구를 사용하여 SharePoint에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 및 응용 프로그램을 제거합니다.  
  
-   팜 관리자, Analysis Services 인스턴스의 서버 관리자 및 팜의 구성 데이터베이스의 **db_owner** 여야 합니다.  
  
-   SharePoint 버전에 대한 구성 도구의 해당 버전을 사용하세요. [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 설치에는 이러한 도구를 사용하지 마세요.  
  
-   SharePoint 관리 서비스가 실행되고 있는지 확인합니다.  
  
1.  **구성 도구 실행:** 구성 도구는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 가 로컬 서버에 설치되어 있을 때만 나열됩니다. **시작** 메뉴에서 **모든 프로그램**을 가리키고 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]를 클릭하고 **구성 도구**를 클릭한 후 다음 중 하나를 클릭합니다.  
  
    -   **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성**  
  
    -   **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구**  
  
2.  **기능, 서비스, 응용 프로그램 및 솔루션 제거** 를 선택한 다음 **확인**을 클릭합니다.  
  
3.  필요한 경우 창을 전체 크기로 확장합니다. 창 아래쪽에 **유효성 검사**, **실행**및 **끝내기** 명령이 포함된 단추 모음이 표시됩니다.  
  
4.  태스크 목록의 각 동작을 검토하여 각 동작이 수행하는 작업을 이해합니다.  
  
     **제거 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 제거**에는 서비스 응용 프로그램과 관련된 응용 프로그램 데이터를 삭제할 수 있는 옵션이 제공됩니다. 응용 프로그램 데이터는 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 에서 사용되는 데이터 새로 고침 일정, 데이터베이스 인스턴스 정보, 사용 데이터 및 기타 데이터를 저장하기 위해 서비스 응용 프로그램에서 만드는 SQL Server 데이터베이스입니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서와 같은 사용자 파일은 저장되지 않습니다. 응용 프로그램 데이터를 보관할 특정 이유가 있는 경우(예: 데이터 새로 고침 또는 데이터 액세스와 관련된 데이터 보존 정책이 있는 경우)가 아니면 SharePoint 사용자가 만들거나 저장한 파일을 제거하지 않고 응용 프로그램 데이터베이스를 삭제할 수 있습니다.  
  
     데이터베이스를 삭제하려면 **제거 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 제거** 를 선택한 다음 **이 서비스 응용 프로그램에 연결된 응용 프로그램 데이터를 삭제합니다.**를 제거하려면 Analysis Services 시스템 관리자 및 로컬 Administrators 그룹의 구성원이어야 합니다.  
  
5.  필요한 경우 **출력** 탭 또는 **스크립트** 탭에서 자세한 정보를 검토합니다.  
  
     출력 탭은 도구에서 수행되는 동작의 요약입니다. 이 정보는 다음 위치의 로그 파일에 저장됩니다.  
  
     `C:\Program Files\Microsoft SQL Server\130\Tools\PowerPivotTools\SPAddinConfiguration\Log`  
  
     스크립트 탭은 PowerShell cmdlet을 표시하거나 도구에서 실행할 PowerShell 스크립트 파일을 참조합니다.  
  
6.  **유효성 검사** 를 클릭하여 각 동작이 유효한지 여부를 확인합니다. **유효성 검사** 를 사용할 수 없는 경우 모든 동작이 시스템에 유효한 것입니다.  
  
7.  **실행** 을 클릭하여 이 태스크에 유효한 모든 동작을 수행합니다. **실행** 은 유효성 검사를 통과한 후에만 사용할 수 있습니다. **실행**을 클릭하면 동작이 일괄 처리 모드로 처리됨을 알리는 다음 경고가 나타납니다. “도구에서 유효한 것으로 플래그가 지정되는 모든 구성 설정이 SharePoint 팜에 적용됩니다. 계속하시겠습니까?”  
  
8.  계속하려면 **예** 를 클릭합니다.  
  
 **오류 문제 해결:**  
  
 구성 도구의 각 동작에 대한 매개 변수 창에서 오류 정보를 볼 수 있습니다. 솔루션 배포 또는 취소와 관련된 문제의 경우 SharePoint 관리 서비스가 시작되었는지 확인합니다. 이 서비스는 팜에서 구성 변경 내용을 트리거하는 타이머 작업을 실행합니다. 서비스가 실행되고 있지 않은 경우 솔루션 배포 또는 취소가 실패합니다. 오류가 지속되면 기존 배포 또는 취소 작업이 큐에 이미 있으며 구성 도구의 추가 동작을 차단하고 있는 것입니다. 다음 PowerShell 명령을 사용하여 서비스가 실행되고 있는지 확인할 수 있습니다.  
  
```  
Get-Service | where {$_.displayname -like "*sharepoint* administration*"}  
```  
  
 큐에 이미 있는 배포 또는 취소 작업을 찾아서 제거하려면 다음을 수행합니다.  
  
1.  다른 모든 오류에 대해서는 ULS 로그를 확인합니다. 자세한 내용은 [SharePoint 로그 파일과 진단 로깅 구성 및 보기&#40;SharePoint용 파워 피벗&#41;](~/analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)를 참조하세요.  
  
2.  SharePoint 관리 셸을 관리자 권한으로 시작하고 다음 명령을 실행하여 큐에 있는 작업을 봅니다.  
  
    ```  
    Stsadm –o enumdeployments  
    ```  
  
3.  기존 배포에서 **유형** 이 취소 또는 배포인지, **파일** 이 powerpivotwebapp.wsp 또는 powerpivotfarm.wsp인지 검토합니다.  
  
4.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 솔루션에 관련된 배포 또는 취소의 경우 **JobId** 의 GUID 값을 복사하여 다음 명령에 붙여넣습니다(셸의 편집 메뉴에서 표시, 복사 및 붙여넣기 명령을 사용하여 GUID 복사).  
  
    ```  
    Stsadm –o canceldeployment –id “<GUID>”  
    ```  
  
5.  **유효성 검사** 를 클릭한 다음 **실행**을 클릭하여 구성 도구에서 태스크를 다시 시도합니다.  
  
 PowerShell을 사용하여 팜에서 기능과 솔루션을 제거할 수도 있습니다. 자세한 내용은 [SharePoint용 파워 피벗에 대한 PowerShell 참조](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md)를 참조하세요.  
  
##  <a name="bkmk_uninstall"></a> 3단계: SQL Server 설치 프로그램을 실행하여 로컬 컴퓨터에서 프로그램 제거  
 프로그램 파일을 삭제하려면 소프트웨어를 제거하기 위해 SQL Server 설치 프로그램을 실행해야 합니다. 제거하면 설치 프로그램에서 생성된 파일과 레지스트리 항목이 모두 제거됩니다. 프로그램 및 기능 페이지를 사용하여 소프트웨어를 제거할 수 있습니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 은 SQL Server를 설치할 때 함께 설치됩니다.  
  
 이미 설치된 다른 SQL Server 인스턴스(또는 동일한 인스턴스의 기능)에 영향을 주지 않고 설치 일부를 제거할 수 있습니다. 예를 들어 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , 데이터베이스 엔진 등의 다른 인스턴스는 설치된 상태로 두고 SharePoint용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 을 제거할 수 있습니다.  
  
1.  프로그램 목록에서 **Microsoft SQL Server 2014(64비트)** 를 선택합니다.  
  
2.  **제거/변경**을 클릭합니다.  
  
3.  **제거**를 클릭합니다. SQL Server 설치 프로그램이 시작됩니다.  
  
     설치 프로그램에서 **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]** 인스턴스를 선택한 다음 **Analysis Services** 및 **Analysis Services SharePoint 통합** 을 선택하여 해당 기능만 제거하고 나머지 모든 기능을 그대로 둘 수 있습니다.  
  
##  <a name="bkmk_addin"></a> 4단계: SharePoint용 Power Pivot 추가 기능 제거  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 배포에 두 개 이상의 서버가 포함되었고 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 추가 기능이 설치된 경우 모든 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 파일을 완전히 제거하려면 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 추가 기능이 설치된 각 서버에서 이 추가 기능을 제거합니다. 자세한 내용은 [SharePoint용 파워 피벗 추가 기능 설치 또는 제거&#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)를 제거하려면 Analysis Services 시스템 관리자 및 로컬 Administrators 그룹의 구성원이어야 합니다.  
  
##  <a name="verify"></a> 5단계: 제거 확인  
  
1.  중앙 관리의 **서버의 서비스 관리**에서 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을 제거한 서버에 연결합니다.  
  
2.  -   [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013을 제거한 경우 **SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스**가 더 이상 목록에 표시되지 않는지 확인합니다.  
  
    -   [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010을 제거한 경우, **SQL Server Analysis Services** 및 **SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스**가 목록에 더 이상 표시되지 않는지 확인합니다.  
  
3.  팜에서 마지막 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버를 제거한 후 다음을 수행합니다.  
  
    1.  응용 프로그램 관리의 **서비스 응용 프로그램 관리**에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램이 목록에 더 이상 표시되지 않는지 확인합니다.  
  
    2.  시스템 설정의 **팜 기능 관리**에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 기능이 페이지에 더 이상 없는지 확인합니다. **팜 솔루션 관리**에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 솔루션이 페이지에 더 이상 표시되지 않는지 확인합니다.  
  
    3.  모니터링의 **진단 로깅 구성** 및 **사용 현황 및 상태 데이터 수집 구성**에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 이벤트 및 이벤트 범주가 더 이상 표시되지 않는지 확인합니다.  
  
    4.  일반 응용 프로그램 설정에서 **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 관리 대시보드** 가 페이지에 더 이상 없는지 확인합니다.  
  
##  <a name="bkmk_post"></a> 6단계: 제거 후 검사 목록  
 다음 목록을 사용하여 제거 중에 삭제되지 않은 소프트웨어 및 파일을 제거할 수 있습니다.  
  
1.  `C:\Program Files\Microsoft SQL Server\MSAS13.PowerPivot`에서 모든 데이터 파일과 하위 폴더를 삭제한 다음 폴더를 삭제합니다. 이 단계는 DATA 디렉터리에서 이전에 캐시된 파일도 삭제합니다.  
  
2.  모든 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서, 문서 및 라이브러리를 삭제합니다(아직 삭제하지 않은 경우).  
  
    -   [파워 피벗 갤러리 삭제](../../analysis-services/power-pivot-sharepoint/delete-power-pivot-gallery.md)  
  
    -   [Power Pivot 데이터 피드 라이브러리 삭제](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)  
  
3.  보안 저장소 서비스에서 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 에 사용되는 저장된 자격 증명이 있는 모든 대상 응용 프로그램을 삭제합니다. 보안 저장소 서비스의 일부 항목은 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을 제거할 때 삭제됩니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 무인 데이터 새로 고침 계정에 대해 만든 대상 응용 프로그램 및 데이터 새로 고침을 위해 만든 모든 대상 응용 프로그램은 아직 삭제되지 않으므로 수동으로 삭제해야 합니다.  
  
     반면, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스에 의해 자동 생성된 개별 대상 응용 프로그램은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을 제거할 때 자동으로 삭제됩니다.  
  
4.  제어판에서 **프로그램**, **프로그램 제거** 를 차례로 클릭합니다. 더 이상 사용되지 않는 모든 Analysis Services 클라이언트 라이브러리를 제거합니다. Analysis Services ADOMD.NET 및 Microsoft SQL Server Analysis Management Objects는 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을 제거할 때 제거되지 않습니다. 이러한 라이브러리는 Analysis Services 데이터를 사용하는 다른 프로그램에서 사용할 수 있으므로 SQL Server 설치 프로그램이 자동으로 제거하지 않습니다. 더 이상 필요하지 않은 경우 클라이언트 라이브러리를 개별적으로 제거해야 합니다.  
  
     SQL Server Reporting Services SharePoint 2010 추가 기능은 제거와 관련하여 특별히 안내된 다음 문제 해결 또는 설치 지침에 따라서만 제거해야 합니다. Reporting Services 추가 기능은 Access 서비스에서 사용됩니다. 또한 SharePoint 2010 제품 준비 도구에 의해 설치되므로 SharePoint에 필요한 기능을 지원하려면 시스템에 그대로 유지되어야 합니다.  
  
     Analysis Services OLE DB 공급자를 제거하지 마세요. SharePoint는 OLE DB 공급자를 Analysis Services 데이터베이스에 연결하는 Excel 통합 문서의 필수 구성 요소로 설치합니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 에서 최신 버전을 설치하지만 이 버전은 이전 버전과 호환되므로 나중에 데이터 연결 문제를 피하려면 OLE DB 공급자를 시스템에 그대로 두어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SharePoint용 파워 피벗 추가 기능 설치 또는 제거&#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [파워 피벗 구성 도구](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
  
