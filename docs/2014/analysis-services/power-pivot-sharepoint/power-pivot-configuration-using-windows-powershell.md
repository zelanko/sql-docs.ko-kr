---
title: Windows PowerShell을 사용 하 여 PowerPivot 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4d83e53e-04f1-417d-9039-d9e81ae0483d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9282fce8e0004495ae8c10b0b3f75fec205d6b34
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72782812"
---
# <a name="powerpivot-configuration-using-windows-powershell"></a>Windows PowerShell을 사용하여 PowerPivot 구성
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]의 설치를 구성하는 데 사용할 수 있는 Windows PowerShell cmdlet이 포함되어 있습니다. PowerShell을 사용하여 설치를 완전히 구성하려면 SharePoint cmdlet과 SharePoint용 PowerPivot cmdlet을 모두 사용해야 합니다. 대부분의 구성은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 도구 중 하나를 사용하여 완료할 수 있습니다. 도구에 대한 자세한 내용은 [PowerPivot Configuration Tools](power-pivot-configuration-tools.md)를 참조하십시오.  
  
> [!IMPORTANT]  
>  SharePoint 2010 팜의 경우 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 데이터베이스 서버를 사용하는 SharePoint 팜이나 SharePoint용 PowerPivot을 구성하려면 먼저 SharePoint 2010 SP1을 설치해야 합니다. 서비스 팩을 아직 설치하지 않았으면 서버를 구성하기 전에 설치합니다.  
  
## <a name="benefits-of-configuring-powerpivot-for-sharepoint-using-powershell"></a>PowerShell을 사용하여 SharePoint용 PowerPivot을 구성할 때의 이점  
 Windows PowerShell 스크립트(.ps1) 파일을 작성하여 구성 태스크를 자동화할 수 있습니다. 모든 서버에서 실행할 수 있는 스크립팅된 설치 및 구성 단계가 필요한 경우 이 방법을 사용하는 것이 좋습니다. 하드웨어 오류가 발생할 경우 서버를 다시 작성하기 위한 재해 복구 계획의 일부로 이러한 스크립트가 필요할 수 있습니다.  
  
## <a name="view-a-list-of-the-powerpivot-cmdlets-on-a-server"></a>서버의 PowerPivot Cmdlet 목록 보기  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Cmdlet의 내용과 예제를 보려면 [SharePoint용 PowerPivot에 대 한 PowerShell 참조](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)를 참조 하세요.  
  
 PowerShell을 사용하여 PowerPivot cmdlet의 목록을 보려면  
  
1.  **관리자 권한으로 실행** 옵션을 사용하여 SharePoint 관리 셸을 엽니다.  
  
2.  다음 명령을 입력합니다.  
  
    ```powershell
    Get-Help *powerpivot*  
    ```  
  
     cmdlet 이름에 PowerPivot이 포함된 cmdlet 목록이 표시됩니다. 예: `Get-PowerPivotServiceApplication`. 사용 가능한 cmdlet 수는 사용 중인 Analysis Services의 버전에 따라 다릅니다.  
  
    -   SharePoint 모드 및 SharePoint 2013에 대해 구성한 SQL Server 2012 SP1 Analysis Services 서버에서는 cmdlet을 10개까지 사용할 수 있습니다. 2012 SP1 버전에서는 Analysis Server를 SharePoint 팜 외부에서 실행할 수 있고 더 적은 수의 Windows PowerShell cmdlet을 필요로 하는 새로운 아키텍처를 사용합니다.  
  
    -   SharePoint 모드 및 SharePoint 2010에서 구성한 SQL Server 2012 Analysis Services 서버에서는 cmdlet을 17개까지 사용할 수 있습니다.  
  
     목록에 반환 되는 명령이 없거나 "`get-help could not find *powerpivot* in a help file in this session.`"와 유사한 오류 메시지가 표시 되는 경우 서버에서 PowerPivot cmdlet을 사용 하도록 설정 하는 방법에 대 한 지침은이 항목의 다음 섹션을 참조 하십시오.  
  
     모든 cmdlet에는 온라인 도움말이 있습니다. 다음 예에서는 `New-PowerPivotServiceApplication` cmdlet에 대한 온라인 도움말을 보는 방법을 보여 줍니다.  
  
    ```powershell
    Get-Help new-powerpivotserviceapplication -Full  
    ```  
  
     예만 보려면 다음 구문을 사용합니다.  
  
    ```powershell
    Get-Help new-powerpivotserviceapplication -Example  
    ```  
  
## <a name="enable-powerpivot-cmdlets-on-a-server"></a>서버에서 PowerPivot Cmdlet 사용  
 SharePoint용 PowerPivot을 설치하고 팜 솔루션을 배포한 후 PowerPivot cmdlet을 사용할 수 있습니다. PowerPivot 구성 도구를 실행하면 솔루션이 배포됩니다. Cmdlet을 사용하려면 다음 단계를 수행합니다.  
  
1.  **관리자 권한으로 실행** 옵션을 사용하여 SharePoint 관리 셸을 엽니다.  
  
2.  첫 번째 cmdlet을 실행합니다.  
  
    ```powershell
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     이 cmdlet을 실행하면 솔루션의 이름,  솔루션 ID  및 Deployed=False가 반환됩니다. 다음 단계에서는 솔루션을 배포합니다.  
  
3.  두 번째 cmdlet을 실행하여 솔루션을 배포합니다.  
  
    ```powershell
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
4.  창을 닫습니다. **관리자 권한으로 실행** 옵션을 사용하여 창을 다시 엽니다.  
  
## <a name="related-content"></a>관련 내용  
 [중앙 관리에서 PowerPivot 서버 관리 및 구성](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [PowerPivot Configuration Tools](power-pivot-configuration-tools.md)  
  
 [SharePoint용 PowerPivot에 대한 PowerShell 참조](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
