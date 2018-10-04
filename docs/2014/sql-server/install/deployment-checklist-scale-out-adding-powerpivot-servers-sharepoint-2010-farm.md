---
title: 'SharePoint 2010 팜에 PowerPivot 서버를 추가 하 여 배포 검사 목록: 확장 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 2dbddcc7-427a-4537-a8e2-56d99b9d967d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9a9e726aea4428ac061ca57a4c1bc28199492492
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218139"
---
# <a name="deployment-checklist-scale-out-by-adding-powerpivot-servers-to-a-sharepoint-2010-farm"></a>SharePoint 2010 팜에 PowerPivot 서버를 추가 하 여 배포 검사 목록: 확장
  SharePoint 팜에서 PowerPivot 쿼리 처리 요청이 많을 것으로 예상되는 경우에는 새 쿼리 및 데이터 처리 지원을 원활하게 추가하기 위해 추가 SharePoint용 PowerPivot 인스턴스를 추가할 수 있습니다.  
  
 새 인스턴스를 설치하면 PowerPivot 데이터 쿼리 또는 PowerPivot 데이터 새로 고침 작업 처리를 위한 추가 용량이 제공됩니다. 선택적으로 서버마다 쿼리 또는 데이터 새로 고침 등, 하나의 요청 유형을 처리하도록 구성할 수 있는 선택 항목이 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 SharePoint Server 2010을 설치하고 구성해야 합니다.  
  
 SharePoint Server 2010 SP1을 적용하고 팜을 업그레이드해야 합니다.  
  
 팜의 기존 SharePoint용 PowerPivot 인스턴스는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)](새 설치 또는 SQL Server 2008 R2에서 업그레이드)입니다.  
  
 새 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SharePoint용 PowerPivot 서버를 설치하는 컴퓨터가 팜에 연결되어야 합니다. 팜의 컴퓨터 및 기타 서버가 동일한 도메인에 있어야 합니다.  
  
 시스템 및 버전 요구 사항을 이해하려면 다음 항목을 검토하십시오.  
  
-   [SharePoint 2010 팜에서 SQL Server BI 기능을 사용하기 위한 지침](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
> [!NOTE]  
>  다중 서버 팜에서 모든 SharePoint용 PowerPivot 인스턴스의 버전은 같아야 합니다. 이미 팜에 있는 다른 PowerPivot 서버에 서비스 팩이나 업데이트를 적용한 경우 새로 추가하는 인스턴스도 설치를 완료한 후 같은 버전으로 업데이트해야 합니다. 업데이트를 적용할 때까지는 새 인스턴스를 사용할 수 없습니다.  
  
## <a name="steps"></a>단계  
 이 검사 목록을 사용하여 추가 PowerPivot 서버를 SharePoint 팜에 추가합니다. 이 항목의 지침에서는 팜에 이미 SharePoint용 PowerPivot 서버가 있으며 추가 처리 로드를 처리하기 위한 두 번째 서버를 추가한다고 가정합니다. 설치 요구 사항, 설치 후 구성 및 확인 작업만 다를 뿐 확장 솔루션 배포 단계도 기존 팜에 단일 PowerPivot 서버를 추가하는 단계와 동일합니다.  
  
|단계|링크|  
|----------|----------|  
|팜에 이미 있는 Analysis Services 인스턴스의 서비스 계정을 확인합니다.|설치할 각 추가 인스턴스는 첫 번째 인스턴스와 동일한 계정으로 실행해야 합니다. 다음 방법 중 하나를 사용하여 서비스 계정을 결정합니다.<br /><br /> 중앙 관리의 보안 섹션에서 클릭 **Configure Service Accounts**합니다. 선택 **Windows 서비스-SQL Server Analysis Services**합니다. 서비스를 선택하면 서비스 계정 이름이 페이지에 표시됩니다.<br /><br /> 이미 PowerPivot 서비스가 설치 된 서버의 엽니다는 **Services** 콘솔 관리 도구에서 응용 프로그램. 두 번 클릭 **SQL Server Analysis Services**합니다. 클릭 합니다 **로그온** 탭 하 여 서비스 계정을 확인 합니다.<br />**\*\* 중요 \* \***  만 중앙 관리를 사용 하 여 서비스 계정을 변경 합니다. 다른 도구나 방법을 사용하는 경우 팜에서 사용 권한이 제대로 업데이트되지 않습니다.|  
|설치 프로그램을 실행하여 SharePoint용 PowerPivot의 두 번째 인스턴스를 설치합니다.|[SharePoint 2010용 PowerPivot 설치](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)<br /><br /> 팜에 연결되어 있지만 서버에 기존 PowerPivot 인스턴스가 없는 응용 프로그램 서버를 선택합니다.<br /><br /> 설치하는 동안 서비스 계정을 지정하라는 메시지가 표시되면 이전 단계의 계정을 입력합니다. Analysis Services 서비스의 모든 인스턴스가 동일한 계정으로 실행되어야 합니다. 이 요구 사항을 사용하면 SharePoint의 관리되는 계정 기능을 사용할 수 있으므로 동일한 유형의 모든 서비스 인스턴스에 대해 한 곳에서 암호를 업데이트할 수 있습니다.|  
|두 번째 인스턴스 구성|방법 중 하나를 사용 하 여 인스턴스를 구성할 수 있습니다: [PowerPivot 구성 도구](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md) 또는 [Windows PowerShell을 사용 하 여 PowerPivot 구성](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)<br /><br /> 두 번째 인스턴스 구성 시 로컬 서비스를 설치해야 합니다. 다른 모든 구성 태스크(예를 들어 서비스 응용 프로그램 구성 또는 데이터 새로 고침 구성)는 초기 구성 중에 수행되며 설치한 후속 인스턴스에 의해 사용됩니다.|  
|사후 설치 태스크|추가 단계를 수행할 필요가 없습니다. 즉, 서비스 응용 프로그램을 만들거나 기능을 활성화하거나 솔루션을 배포하거나 서비스 응용 프로그램 ID를 변경하지 않아도 됩니다. 기존 웹 응용 프로그램 및 서비스 응용 프로그램이 새 서버 소프트웨어를 자동으로 검색해 사용합니다.<br /><br /> 선택적으로, 쿼리용 서버 및 데이터 새로 고침용 서버를 사용하기 위해 두 번째 서버를 설치한 경우 지금 각 서버에 의해 처리되는 요청 유형을 지정하도록 서버 인스턴스 속성을 구성할 수 있습니다. 자세한 내용은 [Query-Only 처리 또는 구성 전용 데이터 새로 고침 &#40;SharePoint 용 PowerPivot&#41;](../../analysis-services/configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)합니다.|  
|두 번째 인스턴스 설치 확인|다음 단계를 수행하여 앞서 설치한 서버에서 PowerPivot 쿼리 처리를 확인할 수 있습니다.<br /><br /> 1) 중앙 관리의에서 관리 서비스는 서버와 해당 서비스가 표시 되는지 확인 하려면 페이지를 엽니다.<br />-서버에서 아래쪽 화살표를 클릭 하 고 서버 변경을 다음 새 PowerPivot for SharePoint 설치 된 서버를 선택 합니다.<br />-SQL Server Analysis Services 및 SQL Server PowerPivot 시스템 서비스가 시작 되었는지 확인 합니다.<br /><br /> 2)에서는 중앙 관리에서 방금 설치한 서버를 사용할 수 있도록 다른 PowerPivot for SharePoint 서버를 중지 합니다. 자세한 내용은 [시작 또는 Stop a PowerPivot for SharePoint 서버](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md)합니다.<br /><br /> 3) 라이브러리에서 PowerPivot 통합 문서를 클릭 합니다.<br /><br /> 4) 슬라이서를 클릭 하거나 쿼리를 시작 하려면 데이터를 피벗 합니다. 서버에서 PowerPivot 데이터가 백그라운드에 로드됩니다. 다음 단계에서는 서버에 연결하여 데이터가 로드 및 캐시되는지 확인합니다.<br /><br /> 5) 시작 메뉴에서 Microsoft SQL Server 프로그램 그룹에서 SQL Server Management Studio를 시작 합니다. 이 도구가 서버에 설치되어 있지 않으면 마지막 단계로 건너뛰어 캐시된 파일이 있는지 확인하면 됩니다.<br /><br /> 6)에서 서버 유형 선택 **Analysis Services**합니다.<br /><br /> 7)에서 서버 이름을 입력  **\<서버 이름 > \powerpivot**여기서  **\<서버 이름 >** 새 PowerPivot for SharePoint 설치 된 컴퓨터의 이름입니다.<br /><br /> 8) 클릭 **연결**합니다.<br /><br /> 9) 개체 탐색기에서에서 클릭 **데이터베이스** 로드 된 PowerPivot 데이터 파일 목록을 볼 수 있습니다.<br /><br /> 10)에서 컴퓨터 파일 시스템 파일 캐시 되는지 여부를 확인 하려면 다음 폴더를 확인 합니다. 디스크에 있습니다. 배포가 작동하는지 확인하려면 캐시된 파일이 있는지도 확인해야 합니다. 파일 캐시는 \Program Files\Microsoft SQL Server\MSAS11.POWERPIVOT\OLAP\Backup 폴더에서 확인할 수 있습니다.<br /><br /> 11) 앞서 중지 했던 서비스를 다시 시작 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [초기 구성 &#40;SharePoint 용 PowerPivot&#41;](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [PowerPivot for SharePoint 2010 설치](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [중앙 관리에서 PowerPivot 서버 관리 및 구성](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
