---
title: SharePoint 용 PowerPivot 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 80ba9e43-f3f0-4730-9fb1-2afd2dd3e6fc
author: Minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 956503602a4a9266427f7242097755f3ff6a7294
ms.sourcegitcommit: 87f29b23d5ab174248dab5d558830eeca2a6a0a4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51019028"
---
# <a name="upgrade-powerpivot-for-sharepoint"></a>SharePoint용 PowerPivot 업그레이드
  이 항목에서는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 배포를 [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)]으로 업그레이드하는 데 필요한 단계에 대해 간략하게 설명합니다. 구체적인 단계는 사용자 환경에서 현재 실행 중인 SharePoint 버전에 따라 달라 집니다 및 SharePoint 추가 기능에 대 한 PowerPivot 포함 (**spPowerPivot.msi**).  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010 | SharePoint 2013  
  
 릴리스 정보 참조 [SQL Server 2014 릴리스 정보](http://go.microsoft.com/fwlink/?LinkID=296445)합니다.  
  

  
## <a name="background"></a>배경  
  
-   둘 이상의 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 이 포함된 다중 서버 SharePoint 2010 팜을 업그레이드하는 경우 한 서버에 대해 전체 업그레이드를 수행한 **후** 다음 서버로 이동해야 합니다. 전체 업그레이드는 SQL Server 설치 프로그램을 실행하여 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 프로그램 파일을 업그레이드한 다음 업그레이드된 서비스를 구성하는 SharePoint 업그레이드 동작을 실행합니다. 적합한 PowerPivot 구성 도구 또는 Windows PowerShell에서 업그레이드 동작을 실행할 때까지 서버 가용성이 제한됩니다.  
  
-   SharePoint 2010 팜에서 PowerPivot 시스템 서비스 및 Analysis Services의 모든 인스턴스는 버전이 같아야 합니다. 버전을 확인 하는 방법에 대 한 자세한 내용은 섹션을 참조 하세요 [PowerPivot 구성 요소의 버전 및 서비스 확인](#bkmk_verify_versions) 이 항목의 합니다.  
  
-   PowerPivot 구성 도구는 SQL Server 공유 기능 중 하나인 동시에 모든 공유 기능 업그레이드 중 하나입니다. 업그레이드 프로세스 중에 공유 기능 업그레이드가 필요한 다른 SQL Server 인스턴스 또는 기능을 선택하면 PowerPivot 구성 도구도 업그레이드됩니다. PowerPivot 구성 도구가 업그레이드되었지만 PowerPivot 인스턴스가 업그레이드되지 않은 경우 문제가 있을 수 있습니다. SQL Server 공유 기능에 대 한 자세한 내용은 참조 하세요. [설치 마법사를 사용 하 여 SQL Server 2014로 업그레이드 &#40;설치&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)합니다.  
  
-   SharePoint 용 PowerPivot 추가 기능 (**spPowerPivot.msi**) 이전 버전과 나란히 설치 합니다. 예를 들어 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 추가 기능은 `c:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools`폴더에 설치됩니다.  
  

  
##  <a name="bkmk_prereq"></a> 필수 구성 요소  
 **사용 권한**  
  
-   SharePoint용 PowerPivot 설치를 업그레이드하려면 팜 관리자여야 합니다. SQL Server 설치 프로그램을 실행하려면 로컬 관리자여야 합니다.  
  
-   팜 구성 데이터베이스에서 **db_owner** 권한을 가지고 있어야 합니다.  
  
 **SQL Server:**  
  
-   기존 PowerPivot 설치가 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]서 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 서비스 팩 2(sp2)로 업그레이드 하기 위해 반드시 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]합니다.  
  
-   기존 PowerPivot 설치가 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]서 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 서비스 팩 1(sp1)로의 업그레이드에 필요 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]합니다.  
  
 **SharePoint  2010:**  
  
-   기존 설치가 SharePoint 2010을 실행 중인 경우 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. 자세한 내용은 [Microsoft SharePoint 2010용 서비스 팩 2](http://www.microsoft.com/download/details.aspx?id=39672)를 참조하세요. PowerShell 명령 `(Get-SPfarm).BuildVersion.ToString()` 을 사용하여 버전을 확인하십시오. 출시 날짜에 대한 빌드 버전을 참조하려면 [SharePoint 2010 빌드 번호](http://www.toddklindt.com/blog/Lists/Posts/Post.aspx?ID=224)를 참조하세요.  
  
 
  
##  <a name="bkmk_uprgade_sharepoint2013"></a> 기존 SharePoint 2013 팜 업그레이드  
 SharePoint 2013에 배포된 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 을 업그레이드하려면 다음을 수행하십시오.  
  
 ![SharePoint 2013용 파워 피벗 업그레이드](../../../2014/sql-server/install/media/as-powepivot-upgrade-flow-sharepoint2013.png "SharePoint 2013용 파워 피벗 업그레이드")  
  
1.  SharePoint 모드에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 실행하는 백 엔드 서버에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 설치 프로그램을 실행합니다. 서버가 여러 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스를 호스팅하는 경우 최소한 **POWERPIVOT** 인스턴스를 업그레이드합니다. 다음 목록은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 업그레이드와 관련된 설치 마법사 단계를 요약한 내용입니다.  
  
    1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사에서 **설치**를 클릭합니다.  
  
    2.  **SQL Server에서 업그레이드…..** 를 클릭합니다.  
  
    3.  **인스턴스 선택** 페이지에서 **POWERPIVOT** 인스턴스 이름을 선택한 후 **다음**을 클릭합니다.  
  
    4.  자세한 내용은 [설치 마법사를 사용 하 여 SQL Server 2014로 업그레이드 &#40;설치&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
2.  서버를 다시 시작합니다.  
  
3.  SharePoint 2013 팜의 각 서버에서 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 추가 기능(**spPowerPivot.msi**)을 실행하여 데이터 공급자를 설치합니다. 데이터베이스 공급자를 업그레이드하는 SQL 서버 설치 마법사를 실행한 서버는 예외입니다. 자세한 내용은 [다운로드 Microsoft SQL Server 2014 PowerPivot for Microsoft SharePoint 2013](http://www.microsoft.com/download/details.aspx?id=40737) 하 고 [설치 하거나 SharePoint 추가 기능에 대 한 PowerPivot을 제거할 &#40;SharePoint 2013&#41; ](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
4.  **SharePoint 용 PowerPivot 2013 구성 실행** 추가 설치는 업데이트 된 솔루션 파일을 사용 하 여 SharePoint 팜을 구성 하려면 SharePoint 응용 프로그램 서버 중 하나에 도구입니다. 이 단계에서는 SharePoint 중앙 관리를 사용할 수 없습니다. 자세한 내용은 다음 항목을 참조하세요.  
  
    1.  Windows 시작 페이지에서 입력 **PowerPivot** 검색 결과에서 클릭 **SharePoint 용 PowerPivot 2013 구성**합니다. 검색 결과로 두 버전의 구성 도구가 반환될 수 있습니다.  
  
         ![두 개의 파워 피벗 구성 도구](../../../2014/analysis-services/media/as-powerpivot-configtools-bothicons.gif "두 개의 파워 피벗 구성 도구")  
  
         또는  
  
         에 **시작** 메뉴에서 **프로그램도**, 클릭 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], 클릭 **구성 도구**, 클릭 하 고 **SharePoint 2013 용 PowerPivot 구성 너무**합니다. 이 도구는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 이 로컬 서버에 설치된 경우에만 표시됩니다.  
  
    2.  시작 시 구성 도구에서 PowerPivot 팜 솔루션과 PowerPivot 웹 응용 프로그램 솔루션의 업그레이드 상태를 확인합니다. 이 솔루션의 이전 버전이 검색될 경우 “**최신 버전의 PowerPivot 솔루션 파일이 검색되었습니다. 팜을 업그레이드하려면 업그레이드 옵션을 선택하세요**.” **확인** 을 클릭하여 시스템 유효성 검사 메시지를 닫습니다.  
  
    3.  **기능, 서비스, 응용 프로그램 및 솔루션 업그레이드**를 클릭한 다음 **확인**을 클릭합니다.  
  
    4.  왼쪽 창의 태스크 목록에서 동작을 검토하고 도구에서 수행하지 않으려는 동작을 제외합니다. 모든 동작은 기본적으로 포함됩니다. 동작을 제거하려면 왼쪽 태스크 목록에서 동작을 선택한 다음 **매개 변수** 페이지에서 **태스크 목록에 이 동작 포함** 확인란의 선택을 취소합니다.  
  
    5.  필요한 경우 **스크립트** 또는 **출력** 탭에서 자세한 정보를 검토합니다.  
  
         출력 탭은 도구에서 수행되는 동작의 요약입니다. 이 정보는 `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Log`의 로그 파일에 저장됩니다.  
  
         스크립트 탭은 PowerShell cmdlet을 표시하거나 도구에서 실행할 PowerShell 스크립트 파일을 참조합니다.  
  
    6.  **유효성 검사** 를 클릭하여 각 동작이 유효한지 여부를 확인합니다. **유효성 검사** 를 사용할 수 없는 경우 모든 동작이 시스템에 유효한 것입니다. **유효성 검사** 를 사용할 수 있는 경우 입력 값(예: Excel 서비스 응용 프로그램 이름)을 수정했거나 도구에서 특정 동작을 수행할 수 없음을 확인했을 수 있습니다. 동작을 수행할 수 없는 경우 해당 동작을 제외하거나 동작이 유효하지 않은 것으로 플래그가 지정되게 하는 기본 조건을 수정해야 합니다.  
  
        > [!IMPORTANT]  
        >  첫 번째 동작인 **팜 솔루션 업그레이드**를 항상 먼저 처리해야 합니다. 이 동작은 서버를 구성하는 데 사용되는 PowerShell cmdlet을 등록합니다. 이 동작에서 오류가 발생하는 경우 계속하지 마십시오. 태스크 목록의 추가 동작을 처리하기 전에 오류에서 제공하는 정보를 사용하여 문제를 진단하고 해결합니다.  
  
    7.  **실행** 을 클릭하여 이 태스크에 유효한 모든 동작을 수행합니다. **실행** 은 유효성 검사를 통과한 후에만 사용할 수 있습니다. **실행**을 클릭하면 동작이 일괄 처리 모드로 처리됨을 알리는 다음 경고가 나타납니다. “**도구에서 유효한 것으로 플래그가 지정되는 모든 구성 설정이 SharePoint 팜에 적용됩니다. 계속하시겠습니까?**”  
  
    8.  계속하려면 **예** 를 클릭합니다.  
  
    9. 팜에서 솔루션 및 기능 업그레이드를 완료하는 데 몇 분 정도 걸릴 수 있습니다. 이 시간 동안 PowerPivot 데이터에 대 한 연결 요청 **못합니다** 유사한 오류로 "**데이터를 새로 고칠 수 없습니다**"또는"**요청 된 작업을 수행 하는 동안 오류가 발생 했습니다. 다시 시도하세요**.” 업그레이드가 완료된 후에는 서버를 사용할 수 있으며 이러한 오류가 더 이상 발생하지 않습니다.  
  
     자세한 내용은 다음 항목을 참조하세요.  
  
    -   [PowerPivot 구성 도구](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
    -   [SharePoint 2013 용 PowerPivot 구성 또는 복구 &#40;PowerPivot 구성 도구&#41;](../../analysis-services/power-pivot-sharepoint/configure-or-repair-power-pivot-for-sharepoint-2013.md)  
  
    -   [Windows PowerShell을 사용하여 PowerPivot 구성](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
    -   [SharePoint 용 PowerPivot에 대 한 PowerShell 참조](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
5.  업그레이드 후 단계를 수행하고 팜의 PowerPivot 서버 버전을 확인하여 업그레이드에 성공했는지 확인합니다. 자세한 내용은 이 항목의 [업그레이드 후 확인 태스크](#verify) 와 다음 섹션을 참조하세요.  
  
 
  
##  <a name="bkmk_uprgade_sharepoint2010"></a> 기존 SharePoint 2010 팜 업그레이드  
 SharePoint 2013에 배포된 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 를 업그레이드하려면 다음을 수행하십시오.  
  
 ![SharePoint 2010용 파워 피벗 업그레이드](../../../2014/sql-server/install/media/as-powepivot-upgrade-flow-sharepoint2010.png "SharePoint 2010용 파워 피벗 업그레이드")  
  
1.  [Microsoft SharePoint 2010용 서비스 팩 2](http://www.microsoft.com/download/details.aspx?id=39672) 를 다운로드하여 팜의 모든 서버에 적용합니다. SharePoint SP2가 성공적으로 설치되었는지 확인합니다. 중앙 관리의 업그레이드 및 마이그레이션 페이지에서 제품 및 패치 설치 상태 확인 페이지를 열고 SP2와 관련된 상태 메시지를 확인합니다.  
  
2.  SharePoint 2010 관리 Windows 서비스가 실행되고 있는지 확인합니다.  
  
    ```  
    Get-Service | where {$_.displayname -like "*SharePoint*"}  
    ```  
  
3.  확인 합니다 **SharePoint** services **SQL Server Analysis Services** 및 **SQL Server PowerPivot 시스템 서비스** SharePoint 중앙 관리에서 시작 하거나 사용 합니다 다음 PowerShell 명령을:입니다.  
  
    ```  
    get-SPserviceinstance | where {$_.typename -like "*sql*"}  
    ```  
  
4.  확인 합니다 **Windows** service **SQL Server Analysis Services (PowerPivot)** 실행 합니다.  
  
    ```  
    Get-Service | where {$_.displayname -like "*powerpivot*"}  
    ```  
  
5.  **실행 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치** 실행 하는 첫 번째 SharePoint 응용 프로그램 서버는 **SQL Server Analysis Services (PowerPivot)** POWERPIVOT 인스턴스를 업그레이드 하려면 Windows 서비스입니다. SQL Server 설치 마법사의 설치 페이지에서 업그레이드 옵션을 선택합니다. 자세한 내용은 [설치 마법사를 사용 하 여 SQL Server 2014로 업그레이드 &#40;설치&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)합니다.  
  
6.  구성 도구를 실행하기 전에**서버를 다시 시작** 합니다. 이 단계를 수행하면 SQL Server 설치 프로그램에서 설치하는 업데이트나 필수 구성 요소가 시스템에 완전히 구성됩니다.  
  
7.  **PowerPivot 구성 도구를 실행** SharePoint에서 솔루션을 업그레이드 하려면 SQL Server Analysis Services (PowerPivot) 서비스 및 웹 서비스를 실행 하는 첫 번째 SharePoint 응용 프로그램 서버. 이 단계에서는 중앙 관리를 사용할 수 없습니다.  
  
    1.  **시작** 메뉴에서 **모든 프로그램**을 가리키고 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **구성 도구**, **PowerPivot 구성 도구**를 차례로 클릭합니다. 이 도구는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 이 로컬 서버에 설치된 경우에만 표시됩니다.  
  
    2.  시작 시 구성 도구에서 PowerPivot 팜 솔루션과 PowerPivot 웹 응용 프로그램 솔루션의 업그레이드 상태를 확인합니다. 이 솔루션의 이전 버전이 검색될 경우 “최신 버전의 PowerPivot 솔루션 파일이 검색되었습니다. 팜을 업그레이드 하려면 업그레이드 옵션을 선택하십시오." **확인** 을 클릭하여 메시지를 닫습니다.  
  
    3.  **기능, 서비스, 응용 프로그램 및 솔루션 업그레이드**를 클릭한 다음 **확인** 을 클릭하여 계속합니다.  
  
    4.  다음 경고가 나타납니다. "PowerPivot 관리 대시보드의 통합 문서가 최신 버전으로 업그레이드 됩니다. 기존 통합 문서에 대한 사용자 지정은 모두 손실됩니다. 계속하시겠습니까?”  
  
         이 경고는 데이터 새로 고침 작업에 대해 보고하는 PowerPivot 관리 대시보드의 통합 문서를 참조합니다. 이 통합 문서를 사용자 지정한 경우 기존 파일을 최신 버전으로 바꾸면 해당 통합 문서의 변경 내용이 모두 손실됩니다.  
  
         통합 문서를 최신 버전으로 덮어쓰려면 **예** 를 클릭합니다. 그렇지 않으면 **아니요** 를 클릭하여 홈 페이지로 돌아갑니다. 통합 문서를 다른 위치에 저장하여 복사본을 만든 다음 계속할 준비가 되면 이 단계로 돌아옵니다.  
  
         대시보드에 사용 된 통합 문서를 사용자 지정 하는 방법에 대 한 자세한 내용은 참조 하세요. [PowerPivot 관리 대시보드 사용자 지정](http://go.microsoft.com/fwlink/?linkID=229639)합니다.  
  
    5.  태스크 목록에서 동작을 검토하고 도구에서 수행하지 않으려는 동작을 제외합니다. 모든 동작은 기본적으로 포함됩니다. 동작을 제거하려면 태스크 목록에서 동작을 선택한 다음 매개 변수 페이지에서 **태스크 목록에 이 동작 포함** 확인란의 선택을 취소합니다.  
  
    6.  필요한 경우 **출력** 탭 또는 **스크립트** 탭에서 자세한 정보를 검토합니다.  
  
         출력 탭은 도구에서 수행되는 동작의 요약입니다. 이 정보는 `c:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\ConfigurationTool\Log`의 로그 파일에 저장됩니다.  
  
         스크립트 탭은 PowerShell cmdlet을 표시하거나 도구에서 실행할 PowerShell 스크립트 파일을 참조합니다.  
  
    7.  **유효성 검사** 를 클릭하여 각 동작이 유효한지 여부를 확인합니다. **유효성 검사** 를 사용할 수 없는 경우 모든 동작이 시스템에 유효한 것입니다. **유효성 검사** 를 사용할 수 있는 경우 입력 값(예: Excel 서비스 응용 프로그램 이름)을 수정했거나 도구에서 특정 동작을 수행할 수 없음을 확인했을 수 있습니다. 동작을 수행할 수 없는 경우 해당 동작을 제외하거나 동작이 유효하지 않은 것으로 플래그가 지정되게 하는 기본 조건을 수정해야 합니다.  
  
        > [!IMPORTANT]  
        >  첫 번째 동작인 **팜 솔루션 업그레이드**를 항상 먼저 처리해야 합니다. 이 동작은 서버를 구성하는 데 사용되는 PowerShell cmdlet을 등록합니다. 이 동작에서 오류가 발생하는 경우 계속하지 마십시오. 태스크 목록의 추가 동작을 처리하기 전에 오류에서 제공하는 정보를 사용하여 문제를 진단하고 해결합니다.  
  
    8.  **실행** 을 클릭하여 이 태스크에 유효한 모든 동작을 수행합니다. **실행** 은 유효성 검사를 통과한 후에만 사용할 수 있습니다. **실행**을 클릭하면 동작이 일괄 처리 모드로 처리됨을 알리는 다음 경고가 나타납니다. “도구에서 유효한 것으로 플래그가 지정되는 모든 구성 설정이 SharePoint 팜에 적용됩니다. 계속하시겠습니까?”  
  
    9. 계속하려면 **예** 를 클릭합니다.  
  
    10. 팜에서 솔루션 및 기능 업그레이드를 완료하는 데 몇 분 정도 걸릴 수 있습니다. 이 시간 동안 PowerPivot 데이터에 대한 연결 요청은 실패하며 “데이터를 새로 고칠 수 없습니다.” 또는 “요청된 작업을 수행하는 동안 오류가 발생했습니다. 다시 시도하십시오.”와 같은 오류가 발생합니다. 업그레이드가 완료된 후에는 서버를 사용할 수 있으며 이러한 오류가 더 이상 발생하지 않습니다.  
  
8.  **프로세스를 반복** 팜의 각 SQL Server Analysis Services (PowerPivot) 서비스에 대 한: 1) 실행 SQL Server 설치 프로그램 2) PowerPivot 구성 도구를 실행 합니다.  
  
9. 업그레이드 후 단계를 수행하고 팜의 PowerPivot 서버 버전을 확인하여 업그레이드에 성공했는지 확인합니다. 자세한 내용은 이 항목의 [업그레이드 후 확인 태스크](#verify) 와 다음 섹션을 참조하세요.  
  
10. **오류 문제 해결**  
  
     각 동작에 대한 매개 변수 창에서 오류 정보를 볼 수 있습니다.  
  
     솔루션 배포 또는 취소와 관련된 문제의 경우 SharePoint 2010 관리자 서비스가 시작되는지 확인합니다. 이 서비스는 팜에서 구성 변경 내용을 트리거하는 타이머 작업을 실행합니다. 서비스가 실행되고 있지 않은 경우 솔루션 배포 또는 취소가 실패합니다. 오류가 지속되면 기존 배포 또는 취소 작업이 큐에 이미 있으며 구성 도구의 추가 동작을 차단하고 있는 것입니다.  
  
    1.  SharePoint 2010 관리 셸을 관리자 권한으로 시작하고 다음 명령을 실행하여 큐에 있는 작업을 봅니다.  
  
        ```  
        Stsadm –o enumdeployments  
        ```  
  
    2.  기존 배포에서 **유형** 이 취소 또는 배포인지, **파일** 이 powerpivotwebapp.wsp 또는 powerpivotfarm.wsp인지 검토합니다.  
  
    3.  배포 또는 취소의 경우 PowerPivot 솔루션에 관련 된 GUID 값을 복사에 대 한 **JobId** 다음 명령에 붙여 넣습니다 (셸의 편집 메뉴에서 GUID를 복사 하려면 표시, 복사 및 붙여넣기 명령의 사용):  
  
        ```  
        Stsadm –o canceldeployment –id “<GUID>”  
        ```  
  
    4.  **유효성 검사** 를 클릭한 다음 **실행**을 클릭하여 구성 도구에서 태스크를 다시 시도합니다.  
  
     다른 모든 오류에 대해서는 ULS 로그를 확인합니다. 자세한 내용은 [구성 및 보기 SharePoint 로그 파일과 진단 로깅 &#40;SharePoint 용 PowerPivot&#41;](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)합니다.  
  

  
##  <a name="bkmk_workbooks"></a> 통합 문서  
 서버를 업그레이드해도 해당 서버에서 실행되는 PowerPivot 통합 문서는 업그레이드되지 않지만 이전 버전의 PowerPivot for Excel에서 만든 통합 문서는 해당 릴리스에 포함된 기능을 사용하여 전처럼 계속 작동합니다. 업그레이드된 서버에는 이전 설치의 일부인 Analysis Services OLE DB 공급자 버전이 포함되기 때문에 통합 문서가 계속 작동합니다.  
  
  
  
##  <a name="bkmk_datarefresh"></a> 데이터 새로 고침  
 업그레이드는 데이터 새로 고침 작업에 영향을 줍니다. 서버의 예약된 데이터 새로 고침은 서버 버전과 일치하는 통합 문서에만 사용 가능합니다. 이전 버전의 통합 문서를 호스팅하는 경우 해당 통합 문서에 대해 데이터 새로 고침이 더 이상 작동하지 않을 수 있습니다. 데이터 새로 고침을 다시 활성화하려면 통합 문서를 업그레이드해야 합니다. PowerPivot for Excel에서 각 통합 문서를 수동으로 업그레이드하거나 SharePoint 2010의 데이터 새로 고침 예약 기능에 대한 자동 업그레이드를 활성화할 수 있습니다. 자동 업그레이드를 사용하면 데이터 새로 고침을 실행하기 전에 통합 문서를 현재 버전으로 업그레이드하여 일정에 따라 데이터 새로 고침 작업이 수행되도록 합니다.  
  

  
##  <a name="bkmk_verify_versions"></a> PowerPivot 구성 요소 및 서비스의 버전 확인  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스와 Analysis Services 인스턴스 버전은 모두 같아야 합니다. 모든 서버 구성 요소가 동일한 버전인지 확인하려면 다음에 대한 버전 정보를 확인합니다.  
  
### <a name="verify-the-version-of-powerpivot-solutions-and-the-powerpivot-system-service"></a>PowerPivot 솔루션 및 PowerPivot 시스템 서비스 버전 확인  
 다음 PowerShell 명령을 실행합니다.  
  
```  
Get-PowerPivotSystemService  
```  
  
 **CurrentSolutionVersion**을 확인합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전은 12.0입니다. \<주 빌드 >. \<부 빌드 >  
  
### <a name="verify-the-version-of-the-analysis-services-windows-service"></a>Analysis Services Windows 서비스 버전 확인  
 SharePoint 2010 팜에서 일부 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 서버만 업그레이드한 경우 업그레이드하지 않은 서버의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스가 팜에 있어야 하는 버전보다 이전 버전이 됩니다. 모든 서버를 사용하려면 모든 서버를 같은 버전으로 업그레이드해야 합니다. 각 컴퓨터에서 Windows SQL Server Analysis Services (PowerPivot) 서비스의 버전을 확인 하려면 다음 방법 중 하나를 사용 합니다.  
  
 **Windows 파일 탐색기**:  
  
1.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 인스턴스에 대한 **Bin** 폴더로 이동합니다. 예를 들면 `C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT\OLAP\bin`입니다.  
  
2.  `msmdsrv.exe`를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  **세부 정보**를 클릭합니다.  
  
4.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 파일 버전에 12.00.< 이어야 합니다. \<주 빌드 >. \<부 빌드 >.  
  
5.  이 번호가 PowerPivot 솔루션 및 시스템 서비스 버전과 동일한지 확인합니다.  
  
 **서비스 시작 정보:**  
  
 PowerPivot 서비스를 시작하면 버전 정보가 Windows 이벤트 로그에 기록됩니다.  
  
1.  Windows `eventvwr`을 실행합니다.  
  
2.  원본 `MSOLAP$POWERPIVOT`에 대한 필터를 만듭니다.  
  
3.  다음과 비슷한 정보 수준 이벤트를 찾습니다.  
  
     서비스가 시작되었습니다. Microsoft SQL Server Analysis Services 64 비트 평가판 (x64) RTM **12.0.2000.8**합니다.  
  
 **PowerShell을 사용하여 파일 버전을 확인합니다.**  
  
 PowerShell을 사용하여 제품 버전을 확인할 수 있습니다. PowerShell은 버전 확인을 스크립팅하거나 자동화하려는 경우 좋은 옵션입니다.  
  
```  
(get-childitem "C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT2000\OLAP\bin\msmdsrv.exe").VersionInfo  
```  
  
 위의 PowerShell 명령은 다음과 비슷한 정보를 반환합니다.  
  
 ProductVersion   FileVersion           FileName  
  
 **12.0.2000.8** 2014.0120.200 C:\Program Files\Microsoft SQL Server\MSAS12 합니다. POWERPIVOT2000\OLAP\bin\msmdsrv.exe  
  
### <a name="verify-the-msolap-data-provider-version-on-sharepoint"></a>SharePoint에서 MSOLAP 데이터 공급자 버전 확인  
 다음 지침에 따라 Analysis Services OLE DB 공급자 버전 중 Excel 서비스에서 신뢰할 수 있는 버전을 확인합니다. Excel 서비스에 대한 신뢰할 수 있는 데이터 공급자 설정을 확인하려면 팜 또는 서비스 응용 프로그램의 관리자여야 합니다.  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭합니다.  
  
2.  Excel Services 서비스 응용 프로그램의 이름(예: **ExcelServiceApp1**)을 클릭합니다.  
  
3.  **신뢰할 수 있는 데이터 공급자**를 클릭합니다. MSOLAP.5(OLAP Services 11.0용 Microsoft OLE DB 공급자)가 나타납니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치를 업그레이드한 경우에는 이전 버전의 MSOLAP.4도 나타납니다.  
  
4.  자세한 내용은 [Add MSOLAP.5 as a Trusted Data Provider in Excel Services](../../analysis-services/power-pivot-sharepoint/add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)을 참조하세요.  
  
 MSOLAP.4는 OLAP Services 10.0의 Microsoft OLE DB 공급자로 설명되어 있습니다. 이 버전은 Excel 서비스로 설치된 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]의 기본 버전이어야 하며, [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전일 수도 있습니다. SharePoint 설치의 기본 버전은 PowerPivot 데이터 액세스를 지원하지 않습니다. SharePoint에서 PowerPivot 통합 문서에 연결하려면 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전 이상이 있어야 합니다. [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전이 있는지 확인하려면 파일 속성을 보고 버전을 확인하는 방법이 설명된 이전 섹션의 지침을 따르십시오.  
  
### <a name="verify-the-adomdnet-data-provider-version"></a>ADOMD.NET 데이터 공급자 버전 확인  
 다음 지침을 사용하여, 설치된 ADOMD.NET의 버전을 확인합니다. Excel 서비스에 대한 신뢰할 수 있는 데이터 공급자 설정을 확인하려면 팜 또는 서비스 응용 프로그램의 관리자여야 합니다.  
  
1.  SharePoint 응용 프로그램 서버에서 `c:\Windows\Assembly`를 찾습니다.  
  
2.  어셈블리 이름을 기준으로 정렬하고 **Microsoft.Analysis Services.Adomd.Client**를 찾습니다.  
  
3.  버전이 12.0.< 확인 합니다. \<빌드 번호 >.  
  
  
  
##  <a name="geminifarm"></a> 여러 PowerPivot for SharePoint 팜에 SharePoint 서버 업그레이드  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 서버가 둘 이상 포함된 다중 서버 토폴로지에서는 모든 서버 인스턴스와 구성 요소의 버전이 같아야 합니다. 가장 높은 소프트웨어 버전을 실행하는 서버에 따라 팜의 모든 서버에 대한 수준이 설정됩니다. 서버 중 일부만 업그레이드하면 이전 버전 소프트웨어를 실행하는 서버의 경우 업그레이드하기 전까지 사용할 수 없게 됩니다.  
  
 첫 번째 서버를 업그레이드하면 아직 업그레이드되지 않은 다른 서버들을 **사용할 수 없게 됩니다**. 모든 서버가 동일한 수준에서 실행되어야 가용성이 복원됩니다.  
  
 SQL Server 설치 프로그램은 실제 컴퓨터에서 직접 PowerPivot 솔루션 파일을 업그레이드하지만 팜에서 사용하는 솔루션을 업그레이드하려면 이 항목의 앞쪽 섹션에서 설명한 PowerPivot 구성 도구를 사용해야 합니다.  
  
 
  
##  <a name="qfe"></a> 팜의 PowerPivot 인스턴스에 QFE 적용  
 SharePoint용 PowerPivot 서버에 패치를 적용하면 기존 프로그램 파일이 특정 문제에 대한 수정 프로그램이 포함된 새 버전으로 업데이트됩니다. 다중 서버 토폴로지에 QFE를 적용하는 경우에는 먼저 시작해야 하는 주 서버가 없습니다. 팜의 다른 PowerPivot 서버에 동일한 QFE를 적용하기만 한다면 원하는 서버 어디에서든지 시작할 수 있습니다.  
  
 QFE를 적용하는 경우 팜 구성 데이터베이스의 서버 버전 정보를 업데이트하는 구성 단계도 수행해야 합니다. 패치가 적용된 서버의 버전이 팜의 새 예상 버전이 됩니다. QFE를 모든 컴퓨터에 적용하고 구성할 때까지는 QFE가 있는 SharePoint용 PowerPivot 인스턴스를 PowerPivot 데이터 요청 처리에 사용할 수 없습니다.  
  
 QFE를 올바르게 적용하고 구성하려면 다음 지침을 따르십시오.  
  
1.  QFE에 제공된 지침을 사용하여 패치를 설치합니다.  
  
2.  PowerPivot 구성 도구를 시작합니다.  
  
3.  **기능, 서비스, 응용 프로그램 및 솔루션 업그레이드**를 클릭한 다음 **확인**을 클릭합니다.  
  
4.  업그레이드 태스크에 포함된 동작을 검토한 다음 **유효성 검사**를 클릭합니다.  
  
5.  **실행** 을 클릭하여 동작을 적용합니다.  
  
6.  팜의 추가 SharePoint용 PowerPivot 인스턴스에 대해 위 단계를 반복합니다.  
  
    > [!IMPORTANT]  
    >  다중 서버 배포에서 다음 컴퓨터로 진행하기 전에 각 인스턴스를 패치 및 구성해야 합니다. 다음 인스턴스로 이동하기 전에 PowerPivot 구성 도구에서 현재 인스턴스에 대한 업그레이드 태스크를 완료해야 합니다.  
  
 팜에 있는 서비스의 버전 정보를 확인하려면 중앙 관리의 업그레이드 및 패치 관리 섹션에서 **제품 및 패치 설치 상태 확인** 페이지를 사용합니다.  
  
##  <a name="verify"></a> 업그레이드 후 확인 태스크  
 업그레이드가 완료된 후 다음 단계에 따라 서버가 작동하는지 확인합니다.  
  
|태스크|링크|  
|----------|----------|  
|서비스가 SharePoint용 PowerPivot을 실행하는 모든 컴퓨터에서 실행되고 있는지 확인합니다.|[PowerPivot for SharePoint 서버 시작 또는 중지](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md)|  
|사이트 모음 수준에서 기능이 활성화되어 있는지 확인합니다.|[중앙 관리에서 사이트 모음에 대해 PowerPivot 기능 통합 활성화](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)|  
|통합 문서를 연 다음 쿼리를 시작하는 필터나 슬라이서를 클릭하여 개별 PowerPivot 통합 문서가 제대로 로드되는지 확인합니다.|하드 드라이브에 캐시된 파일이 있는지 확인합니다. 캐시된 파일이 있으면 실제 해당 서버에 데이터 파일이 로드된 것입니다. c:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT\OLAP\Backup 폴더에서 캐시된 파일을 찾습니다.|  
|데이터 새로 고침에 대해 구성된 선택한 통합 문서에서 새로 고침을 테스트합니다.|데이터 새로 고침을 테스트하는 가장 쉬운 방법은 데이터 새로 고침이 즉시 실행되도록 **가능한 빨리 새로 고치십시오.** 확인란을 선택하여 데이터 새로 고침 일정을 수정하는 것입니다. 이 단계는 현재 통합 문서에 대한 데이터 새로 고침 성공 여부를 확인합니다. 자주 사용하는 다른 통합 문서에 대해 이 단계를 반복하여 데이터 새로 고침이 작동하는지 확인합니다. 새로 고침 예약에 대 한 자세한 내용은 [데이터 새로 고침 예약 &#40;SharePoint 용 PowerPivot&#41;](../../../2014/analysis-services/schedule-a-data-refresh-powerpivot-for-sharepoint.md)합니다.|  
|이후에 PowerPivot 관리 대시보드의 데이터 새로 고침 보고서에서 데이터 새로 고침 오류가 없는지 모니터링합니다.|[PowerPivot 관리 대시보드 및 사용 데이터](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)|  
  
 PowerPivot 설정 및 기능을 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [중앙 관리에서 PowerPivot 서버 관리 및 구성](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)합니다.  
  
 설치 후 구성 작업의 모든 과정을 안내 하는 단계별 지침을 참조 하세요 [초기 구성 &#40;SharePoint 용 PowerPivot&#41;](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)합니다.  
  

  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2014 버전에서 지 원하는 기능](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [SharePoint 2010용 PowerPivot 설치](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
