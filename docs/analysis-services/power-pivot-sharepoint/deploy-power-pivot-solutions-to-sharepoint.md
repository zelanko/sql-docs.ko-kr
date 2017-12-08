---
title: "SharePoint에 Powerpivot 솔루션 배포 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f202a2b7-34e0-43aa-90d5-c9a085a37c32
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 206b31adec86e7ea2213746687d535d56ca3b617
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="deploy-power-pivot-solutions-to-sharepoint"></a>SharePoint에 PowerPivot 솔루션 배포
  다음 지침을 사용하여 SharePoint Server 2010 환경에 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 기능을 추가하는 두 개의 솔루션 패키지를 수동으로 배포할 수 있습니다. 솔루션 배포는 SharePoint 2010 서버에서 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을(를) 구성하기 위한 필수 단계입니다. 필수 단계의 전체 목록을 보려면 [중앙 관리에서 파워 피벗 서버 관리 및 구성](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)을 참조하세요.  
  
 또는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구를 사용하여 솔루션을 배포할 수 있습니다. 구성 도구를 사용하는 방법은 단일 서버 설치의 경우 더 쉽고 효율적인 방법이지만 친숙한 도구를 사용하고 싶거나 동시에 여러 기능을 구성하려는 경우 중앙 관리 및 Powershell을 사용할 수도 있습니다. 구성 도구 사용에 대한 자세한 내용은 [파워 피벗 구성 도구](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)를 참조하세요.  
  
 솔루션을 배포하기 전에 먼저 SQL Server 2012 설치 미디어를 사용하여 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을(를) 설치해야 합니다. SQL Server 설치 프로그램은 배포할 솔루션 패키지를 설치합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [사전 요구 사항: 웹 응용 프로그램에서 클래식 모드 인증을 사용하는지 확인](#bkmk_classic)  
  
 [1단계: 팜 솔루션 배포](#bkmk_farm)  
  
 [2단계: 중앙 관리에 Power Pivot 웹 응용 프로그램 솔루션 배포](#deployCA)  
  
 [3단계: 다른 웹 응용 프로그램에 Power Pivot 웹 응용 프로그램 솔루션 배포](#deployUI)  
  
 [솔루션 다시 배포 또는 취소](#retract)  
  
 [Power Pivot 솔루션 정보](#intro)  
  
##  <a name="bkmk_classic"></a> 사전 요구 사항: 웹 응용 프로그램에서 클래식 모드 인증을 사용하는지 확인  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (SharePoint용)은 Windows 클래식 모드 인증을 사용하는 웹 응용 프로그램에서만 지원됩니다. 다음 PowerShell cmdlet을 실행 하는 응용 프로그램에서 클래식 모드가 사용 여부를 확인 하려면는 **SharePoint 2010 관리 셸을**, 대체 **http://\<최상위 사이트 이름 >** 와 SharePoint 사이트의 이름:  
  
```  
Get-spwebapplication http://<top-level site name> | format-list UseClaimsAuthentication  
```  
  
 반환 값은 **false**여야 합니다. 값이 **true**이면 이 웹 응용 프로그램으로 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 액세스할 수 없습니다.  
  
##  <a name="bkmk_farm"></a> 1단계: 팜 솔루션 배포  
 이 섹션에서는 PowerShell을 사용하여 솔루션을 배포하는 방법을 보여 주지만 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구를 사용하여 이 태스크를 완료할 수도 있습니다. 자세한 내용은 [SharePoint 2010용 파워 피벗 구성 또는 복구(파워 피벗 구성 도구)](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046)를 참조하세요.  
  
 이 태스크는 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을(를) 설치한 후 한 번만 수행해야 합니다.  
  
1.  SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 이(가) 설치된 서버에서 **관리자 권한으로 실행** 옵션을 사용하여 SharePoint 2010 관리 셸을 엽니다.  
  
2.  다음 cmdlet을 실행하여 팜 솔루션을 추가합니다.  
  
    ```  
    Add-SPSolution –LiteralPath “C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp”  
    ```  
  
     이 cmdlet을 실행하면 솔루션의 이름,  솔루션 ID  및 Deployed=False가 반환됩니다. 다음 단계에서는 솔루션을 배포합니다.  
  
3.  다음 cmdlet을 실행하여 팜 솔루션을 배포합니다.  
  
    ```  
    Install-SPSolution –Identity PowerPivotFarm.wsp –GACDeployment -Force  
    ```  
  
##  <a name="deployCA"></a> 2단계: 중앙 관리에 Power Pivot 웹 응용 프로그램 솔루션 배포  
 팜 솔루션을 배포한 후 중앙 관리에 웹 응용 프로그램 솔루션을 배포해야 합니다. 이 단계에서는 중앙 관리에 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 관리 대시보드를 추가합니다.  
  
1.  **관리자 권한으로 실행** 옵션을 사용하여 SharePoint  2010  관리 셸을 엽니다.  
  
2.  다음 cmdlet을 실행하여 중앙 관리에 대한 참조를 만듭니다.  
  
    ```  
    $centralAdmin = $(Get-SPWebApplication -IncludeCentralAdministration | Where { $_.IsAdministrationWebApplication -eq $TRUE})  
    ```  
  
3.  다음 cmdlet을 실행하여 팜 솔루션을 추가합니다.  
  
    ```  
    Add-SPSolution –LiteralPath “C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotWebApp.wsp”  
    ```  
  
     이 cmdlet을 실행하면 솔루션의 이름,  솔루션 ID  및 Deployed=False가 반환됩니다. 다음 단계에서는 솔루션을 배포합니다.  
  
4.  다음 cmdlet을 실행하여 중앙 관리에 웹 응용 프로그램 솔루션을 설치합니다.  
  
    ```  
    Install-SPSolution -Identity PowerPivotWebApp.wsp -GACDeployment -Force -WebApplication $centralAdmin  
    ```  
  
 이제 중앙 관리에 웹 응용 프로그램 솔루션이 배포되었으므로 중앙 관리를 사용하여 모든 나머지 구성 단계를 완료할 수 있습니다.  
  
##  <a name="deployUI"></a> 3단계: 다른 웹 응용 프로그램에 Power Pivot 웹 응용 프로그램 솔루션 배포  
 앞에서는 Powerpivotwebapp.wsp를 중앙 관리로 배포했습니다. 이 섹션에서는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 액세스를 지원하는 각각의 기존 웹 응용 프로그램에 powerpivotwebapp.wsp를 배포합니다. 나중에 웹 응용 프로그램을 더 많이 추가하는 경우 추가 웹 응용 프로그램에 대해 이 단계를 반복해야 합니다.  
  
1.  중앙 관리의 시스템 설정에서 **팜 솔루션 관리**를 클릭합니다.  
  
2.  **powerpivotwebapp.wsp**를 클릭합니다.  
  
3.  **솔루션 배포**를 클릭합니다.  
  
4.  **배포 위치**에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 기능 지원을 추가할 SharePoint 웹 응용 프로그램을 선택합니다.  
  
5.  **확인**을 클릭합니다.  
  
6.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 액세스를 지원할 다른 SharePoint 웹 응용 프로그램에 대해서도 반복합니다.  
  
##  <a name="retract"></a> 솔루션 다시 배포 또는 취소  
 SharePoint 중앙 관리에서 솔루션 취소 기능을 제공하기는 하지만 설치 또는 패치 배포 문제를 체계적으로 해결하는 경우가 아니면 powerpivotwebapp.wsp 파일을 취소할 필요가 없습니다.  
  
1.  SharePoint  2010  중앙 관리의 시스템 설정에서 **팜 솔루션 관리**를 클릭합니다.  
  
2.  **Powerpivotwebapp.wsp**를 클릭합니다.  
  
3.  **솔루션 취소**를 클릭합니다.  
  
 팜 솔루션이 원인이 되어 서버 배포 문제가 발생하는 경우 **구성 도구에서** 복구 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 옵션을 실행하여 솔루션을 다시 배포할 수 있습니다. 사용자가 수행할 단계가 더 적으므로 도구를 통해 복구 작업을 수행하는 것이 좋습니다. 자세한 내용은 [SharePoint 2010용 파워 피벗 구성 또는 복구(파워 피벗 구성 도구)](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046)를 참조하세요.  
  
 모든 솔루션을 다시 배포하려는 경우에는 다음 순서로 작업을 수행합니다.  
  
1.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 웹 응용 프로그램 솔루션을 사용하는 모든 SharePoint 웹 응용 프로그램을 취소합니다.  
  
2.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 팜 솔루션 제거  
  
3.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 팜 솔루션을 제거합니다.  
  
4.  모든 SharePoint 웹 응용 프로그램에 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 웹 응용 프로그램 솔루션을 다시 배포합니다.  
  
##  <a name="intro"></a> Power Pivot 솔루션 정보  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 에서는 두 가지 솔루션 패키지를 사용하여 해당 응용 프로그램 페이지 및 프로그램 파일을 팜과 개별 웹 응용 프로그램에 배포합니다.  
  
-   팜 솔루션은 전역적으로 사용됩니다. 이 솔루션은 한 번 배포되고 나면 나중에 팜에 추가하는 모든 새 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버에서 자동으로 사용할 수 있습니다.  
  
-   웹 응용 프로그램 솔루션은 응용 프로그램별로 적용되므로 중앙 관리 웹 응용 프로그램을 비롯한 팜의 각 웹 응용 프로그램에 배포되어야 합니다.  
  
 각 솔루션은 다른 방식으로 배포됩니다.  팜 솔루션은 첫 번째 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 인스턴스가 설치된 후 한 번 배포됩니다. 팜 솔루션을 배포하려면 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구 또는 PowerShell cmdlet을 사용합니다.  
  
 웹 응용 프로그램 솔루션은 처음 중앙 관리에 배포된 다음 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 대한 요청을 지원하는 모든 추가 웹 응용 프로그램에 배포됩니다. 중앙 관리에 웹 응용 프로그램 솔루션을 배포하려면 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 도구 또는 PowerShell cmdlet을 사용해야 합니다. 다른 모든 웹 응용 프로그램의 경우 중앙 관리 또는 PowerShell을 사용하여 수동으로 웹 응용 프로그램 솔루션을 배포할 수 있습니다.  
  
|해결 방법|Description|  
|--------------|-----------------|  
|Powerpivotfarm.wsp|Microsoft.AnalysisServices.SharePoint.Integration.dll을 전역 어셈블리에 추가합니다.<br /><br /> Microsoft.AnalysisServices.ChannelTransport.dll을 전역 어셈블리에 추가합니다.<br /><br /> 기능 및 리소스 파일을 설치하고 내용 유형을 등록합니다.<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 갤러리 및 데이터 피드 라이브러리용 라이브러리 템플릿을 추가합니다.<br /><br /> 서비스 응용 프로그램 구성, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 관리 대시보드, 데이터 새로 고침, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 갤러리를 위한 응용 프로그램 페이지를 추가합니다.|  
|powerpivotwebapp.wsp|Microsoft.AnalysisServices.SharePoint.Integration.dll 리소스 파일을 웹 프런트 엔드의 웹 서버 확장 폴더에 추가합니다.<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 웹 서비스를 웹 프런트 엔드에 추가합니다.<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 갤러리용 축소판 이미지 생성 기능을 추가합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [SharePoint용 파워 피벗 업그레이드](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [중앙 관리에서 파워 피벗 서버 관리 및 구성](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Windows PowerShell을 사용하여 파워 피벗 구성](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
  
