---
title: "Power Pivot 가용성 및 재해 복구 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4aaf008c-3bcb-4dbf-862c-65747d1a668c
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7c2534d88a10602dcabb594e5a18925ce2547194
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="power-pivot-availability-and-disaster-recovery"></a>Power Pivot 가용성 및 재해 복구
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 에 대한 가용성 및 재해 복구 계획은 주로 SharePoint 팜 디자인, 다른 구성 요소에 허용되는 작동 중단 시간 및 SharePoint 가용성에 구현하는 도구 및 최선의 방법에 따라 달라집니다. 이 항목에서는 기술을 요약하고 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 배포에 대한 가용성 및 재해 복구를 계획할 때 고려할 예제 토폴로지 다이어그램을 포함합니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010|  
  
 **항목 내용**  
  
-   [Power Pivot 고가용성에 대한 SharePoint 2013 토폴로지 예제](#bkmk_sharepoint2013)  
  
-   [Power Pivot 고가용성에 대한 SharePoint 2010 토폴로지 예제](#bkmk_sharepoint2010)  
  
-   [PowerPivot 서비스 응용 프로그램 데이터베이스 및 SQL Server 가용성 및 복구 기술](#bkmk_sql_server_technologies)  
  
-   [추가 정보 링크](#bkmk_more_resources)  
  
##  <a name="bkmk_sharepoint2013"></a> Power Pivot 고가용성에 대한 SharePoint 2013 토폴로지 예제  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 배포에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 가용성을 디자인하는 방법에 더 많은 유연성을 제공합니다. SharePoint 2013에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버라고도 하는 SharePoint 모드로 배포된 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 인스턴스는 SharePoint 팜 외부에서 실행되고 별도의 서버에 설치할 수 있습니다. SharePoint 모드의 각 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스는 Excel Services에 등록됩니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 공유 서비스 및 서비스 응용 프로그램은 SharePoint 응용 프로그램 서버에서 실행됩니다.  
  
 다음 다이어그램에서는 예제 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 배포를 보여 줍니다. 이 예제는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 서비스의 적합한 가용성을 지원하고 데이터베이스가 정기적으로 백업된다고 가정합니다.  
  
 ![2013에서 powerpivot 가용성](../../analysis-services/power-pivot-sharepoint/media/ssas-powerpivot-services-2013.png "2013에서 powerpivot 가용성")  
  
-   **(1)** 웹 프런트 엔드 서버입니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 추가 기능을 사용하여 각 서버에 데이터 공급자를 설치합니다. 설치에 대한 자세한 내용은 [SharePoint용 PowerPivot 추가 기능 설치 또는 제거&#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)를 참조하세요.  
  
-   **(2)** [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 공유 서비스는 **각** 응용 프로그램 서버에서 실행되고 서비스 응용 프로그램을 응용 프로그램 서버 **간에** 실행할 수 있습니다. 따라서 단일 응용 프로그램 서버가 오프라인이 되는 경우 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 응용 프로그램을 여전히 사용할 수 있습니다.  
  
-   **(3)** Excel 계산 서비스는 응용 프로그램 서버를 각각 하나씩 실행하고 서비스 응용 프로그램을 응용 프로그램 서버 간에 실행할 수 있도록 합니다. 따라서 단일 응용 프로그램 서버가 오프라인이 되는 경우 Excel 계산 서비스를 여전히 사용할 수 있습니다.  
  
-   **(4)** 및 **(6)** SharePoint 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스는 SharePoint 팜 외부의 서버에서 실행되고 이는 Windows 서비스 **SQL Server Analysis Services([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])**를 포함합니다. 이러한 각각의 인스턴스는 Excel Services**(3)**에 등록되어 있습니다. Excel Services는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 서버 요청의 부하 분산을 관리합니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 아키텍처를 사용하면 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 에 대한 여러 서버를 가질 수 있으므로 필요한 만큼 더 많은 인스턴스를 쉽게 추가할 수 있습니다. 자세한 내용은 [Excel Services 데이터 모델 설정 관리(SharePoint Server 2013)](http://technet.microsoft.com/library/jj219780\(v=office.15\).aspx)를 참조하세요.  
  
-   **(5)** 콘텐츠, 구성 및 응용 프로그램 데이터베이스에 사용되는 SQL Server 데이터베이스입니다. 여기에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 데이터베이스가 포함됩니다. DR 계획에는 데이터베이스 계층이 포함되어야 합니다. 이 디자인에서 데이터베이스는 **(4)** [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 인스턴스 중 하나와 동일한 서버에서 실행됩니다. **(4)** 및 **(5)** 는 다른 서버에 있을 수도 있습니다.  
  
-   **(7)** SQL Server 데이터베이스 백업 또는 중복성의 일부 형식입니다.  
  
##  <a name="bkmk_sharepoint2010"></a> Power Pivot 고가용성에 대한 SharePoint 2010 토폴로지 예제  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 아키텍처에서 모든 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 구성 요소가 같은 SharePoint 응용 프로그램 서버에서 실행되어야 합니다. 여기에는 SharePoint 모드에서 배포된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스와 SharePoint 2013 배포 중 하나와만 비교되는 공유 서비스 2개가 포함됩니다.  
  
 다음 다이어그램에서는 예제 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 배포를 보여 줍니다. 이 예제는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 서비스의 적합한 가용성을 지원하고 데이터베이스가 정기적으로 백업된다고 가정합니다.  
  
 ![sharepoint 2010에서에서 powerpivot 가용성](../../analysis-services/power-pivot-sharepoint/media/ssas-powerpivot-services-2010.png "sharepoint 2010에서에서 powerpivot 가용성")  
  
-   **(1)** 웹 프런트 엔드 서버입니다. 각 서버에서 데이터 공급자를 설치합니다. 자세한 내용은 [SharePoint 서버에서 Analysis Services OLE DB 공급자 설치](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859)를 참조하세요.  
  
-   **(2)** 두 개의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 공유 서비스 및 **(4)** Windows Service **SQL Server Analysis Services([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])**는 SharePoint 응용 프로그램 서버에 설치되어 있습니다.  
  
     [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스는 **각** 응용 프로그램 서버에서 실행되고 서비스 응용 프로그램을 응용 프로그램 서버 **간에** 실행할 수 있습니다. 단일 응용 프로그램 서버가 오프라인이 되는 경우 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 서비스 응용 프로그램을 여전히 사용할 수 있습니다.  
  
     SharePoint 2010에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 용량을 늘리려면 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스를 실행하는 SharePoint 응용 프로그램 서버를 추가로 배포하세요.  
  
-   **(3)** Excel 계산 서비스는 각각의 응용 프로그램 서버에서 실행되고 서비스 응용 프로그램을 응용 프로그램 서버 간에 실행할 수 있도록 합니다. 따라서 단일 응용 프로그램 서버가 오프라인이 되는 경우 Excel 계산 서비스를 여전히 사용할 수 있습니다.  
  
-   **(5)** 콘텐츠, 구성 및 응용 프로그램 데이터베이스에 사용되는 SQL Server 데이터베이스입니다. 여기에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 데이터베이스가 포함됩니다. DR 계획에는 데이터베이스 계층이 포함되어야 합니다.  
  
-   **(6)** SQL Server 데이터베이스 백업 또는 중복성의 일부 형식입니다.  
  
##  <a name="bkmk_sql_server_technologies"></a> PowerPivot 서비스 응용 프로그램 데이터베이스 및 SQL Server 가용성 및 복구 기술  
 SharePoint 고가용성 계획에 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 서비스 응용 프로그램 데이터베이스를 포함합니다. 이 데이터베이스 기본 이름은 `DefaultPowerPivotServiceApplicationDB-<GUID>`입니다. 다음은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가용성 기술과, [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 데이터베이스에 사용할 때의 권장 사항에 대한 요약입니다. 자세한 내용은 [SharePoint 데이터베이스에 지원되는 고가용성 및 재해 복구 옵션(SharePoint 2013)](http://technet.microsoft.com/library/jj841106.aspx)을 참조하세요.  
  
||설명|  
|-|--------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (4) [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 동기화 미러링.|지원되나 이 옵션은 사용하지 않는 것이 좋습니다. 동기-커밋 모드에서 Always On을 사용하는 것이 좋습니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 동기-커밋 모드의|지원 및 권장합니다.|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 비동기 미러링 또는 재해 복구를 위해 다른 팜으로 로그 전달.|지원됩니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 재해 복구를 위한 비동기-커밋이 적용된|지원됨|  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 전달  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]을 사용하여 코드 대기 시나리오를 계획하는 방법에 대한 자세한 내용은 [PowerPivot 재해 복구](http://social.technet.microsoft.com/wiki/contents/articles/22137.sharepoint-powerpivot-disaster-recovery.aspx)를 참조하세요.  
  
## <a name="verification"></a>확인  
 재해 복구 주기 전후로 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 배포를 확인하기 위한 지침 및 스크립트는 [검사 목록: PowerShell을 사용하여 SharePoint용 파워 피벗 확인](../../analysis-services/instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md)을 참조하세요.  
  
##  <a name="bkmk_more_resources"></a> 추가 정보 링크  
  
-   [SharePoint 데이터베이스에 지원되는 고가용성 및 재해 복구 옵션(SharePoint 2013)](http://technet.microsoft.com/library/jj841106.aspx)  
  
-   [재해 복구 계획(SharePoint Server 2010)](http://technet.microsoft.com/library/ff628971\(v=office.14\).aspx)  
  
-   [SQL Server 클라우드 백업 및 복구 백서](http://www.microsoft.com/server-cloud/solutions/cloud-backup-recovery.aspx?WT.srch=1&WT.mc_ID=SEM_BING_USEvergreenSearch_Unassigned&CR_CC=Unassigned#fbid=RjU2Nbzu2dT)  
  
-   [Microsoft® SQL Server Backup to Microsoft Windows® Azure®Tool](http://www.microsoft.com/download/details.aspx?id=40740)  
  
 **커뮤니티 콘텐츠**  
  
-   [SharePoint 2013에서 서비스 인스턴스 관리](http://www.petri.co.il/manage-service-instances-sharepoint-2013.htm)  
  

