---
title: 통합 문서 및 예약 된 데이터 새로 고침 (SharePoint 2013) 업그레이드 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5f0d49d6aeb8231dbffb56b42fe1151ae90d0e41
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52505219"
---
# <a name="upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013"></a>통합 문서 업그레이드 및 예약된 데이터 새로 고침(SharePoint 2013)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  이 항목은 이전 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 환경에서 사용자의 통합 문서 환경과 이 릴리스에 새로 도입된 기능을 이용할 수 있도록 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 통합 문서를 업그레이드 하는 방법에 대해 설명합니다. 새 기능에 대 한 자세한 내용은 참조 하세요 [What's New in Power Pivot](http://go.microsoft.com/fwlink/?LinkID=203917)합니다.  
  
> [!WARNING]  
>  서버에서 자동으로 업그레이드된 통합 문서에 대한 업그레이드를 롤백할 수는 없습니다. 업그레이드된 통합 문서는 업그레이드된 상태로 유지됩니다. 이전 버전을 사용하려면 이전 통합 문서를 SharePoint에 다시 게시하거나 이전 버전을 복원하거나 통합 문서를 재활용합니다. SharePoint에서 문서를 복원하거나 재활용하는 방법은 [휴지통 및 버전 관리를 사용한 콘텐츠 보호 계획](http://go.microsoft.com/fwlink/?LinkId=238669)을 참조하세요.  
  
  
##  <a name="bkmk_overview"></a> 통합 문서 업그레이드 개요  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 통합 문서는 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 데이터를 포함하는 Excel 통합 문서입니다. 통합 문서를 업그레이드하면 두 가지 이점이 있습니다.  
  
-   [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]의 새로운 기능을 사용합니다.  
  
-   [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] Analysis Services 서버와 함께 SharePoint 모드로 실행되는 통합 문서에 대해 예약된 데이터 새로 고침을 사용합니다.  
  
> [!IMPORTANT]  
>  업그레이드된 통합 문서를 롤백할 수 없으므로 이전 버전의 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]또는 이전 버전의 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)]에서 통합 문서를 사용하려는 경우 파일 복사본을 만드십시오.  
  
 다음 표에서는 통합 문서가 만들어진 환경을 기준으로 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 통합 문서의 지원 및 동작을 보여 줍니다. 일반 사용자 환경, 특정 환경으로 통합 문서를 업그레이드하도록 지원되는 업그레이드 옵션 및 아직 업그레이드되지 않은 통합 문서의 예약된 데이터 새로 고침 동작 등이 설명됩니다.  
  
### <a name="workbook-behavior-and-upgrade-options"></a>통합 문서 동작 및 업그레이드 옵션  
  
|통합 문서 작성 환경|\<|지원 및 동작|>|  
|----------------|--------|--------------------------|--------|  
||**2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2010**|**2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2010**|**2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013**|  
|**2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010**|모든 기능|**환경:** 사용자가 브라우저에서 통합 문서와 상호 작용하고 이를 다른 솔루션의 데이터 원본으로 사용할 수 있습니다.<br /><br /> **업그레이드:** 통합 문서는 경우 자동으로 업그레이드 문서 라이브러리에 대해 자동 업그레이드가 사용 되는 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] SharePoint 팜에서 시스템 서비스에<br /><br /> **데이터 새로 고침을 예약 합니다.** 지원되지 않습니다. 통합 문서를 업그레이드해야 합니다.|**환경:** 사용자가 통합 문서와 상호 작용하고 이를 다른 솔루션의 데이터 원본으로 사용할 수 있습니다.<br /><br /> **업그레이드:** 자동 업그레이드를 사용할 수 없습니다. 사용자가 2008 R2 통합 문서를 2012 버전이나 office 2013 버전으로 직접 업그레이드해야 합니다.<br /><br /> **데이터 새로 고침을 예약 합니다.** 지원되지 않습니다. 통합 문서를 업그레이드해야 합니다.|  
|**Excel용 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]**|지원되지 않음|모든 기능|**환경:** 사용자가 브라우저에서 통합 문서와 상호 작용하고 이를 다른 솔루션의 데이터 원본으로 사용할 수 있습니다. 데이터 새로 고침 예약을 사용할 수 있습니다.<br /><br /> **업그레이드:** 자동 업그레이드는 지원되지 않습니다. 사용자가 통합 문서를 Office 2013 버전으로 직접 업그레이드할 수 있습니다.<br /><br /> **데이터 새로고침 예약:** 을 지원합니다.|  
|**Excel 2013**|지원되지 않음|지원되지 않음|모든 기능|  
  
##  <a name="bkmk_to_2012sp1_from_2008r2"></a> SQL Server 2008 R2 통합 문서에서 2012 서비스 팩 1(SP1) 통합 문서로 업그레이드  
 이 섹션에서는 SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010 통합 문서에서 SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2013 통합 문서로 업그레이드에 대해 설명합니다.  
  
 **동작 변경 내용:** SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 통합 문서 자동 업그레이드 되지 SQL Server 2012 SP1에서 사용할 때 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] SharePoint 2013 용입니다. 따라서 예약된 데이터 새로 고침이 SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 통합 문서에 대해 작동하지 않습니다.  
  
 2008 R2 통합 문서는 SharePoint 2013용 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 에서 열리지만 예약된 데이터 새로 고침은 작동하지 않습니다. 새로 고침 기록을 검토하면 다음과 유사한 오류 메시지가 표시됩니다.  
  
 "통합 문서에는 지원 되지 않는 포함 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 모델입니다. 통합 문서에서 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 모델은 SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010 형식으로 되어 있습니다. 지원되는 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 모델은 다음과 같습니다.  
  
-   SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2010  
  
-   SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 2013  
  
 **통합 문서 업그레이드 방법:** 통합 문서를 2012 통합 문서로 업그레이드할 때까지 예약된 데이터 새로 고침이 작동하지 않습니다. 통합 문서와 통합 문서에 포함된 모델을 업그레이드하려면 다음 중 하나를 수행하세요.  
  
-   통합 문서를 다운로드하고 SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 추가 기능이 설치된 Microsoft Excel 2010에서 통합 문서를 엽니다.  
  
     [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 창을 열고 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 모델을 업그레이드합니다.  
  
     그런 다음 통합 문서를 저장하고 SharePoint에 게시합니다.  
  
-   통합 문서를 다운로드하고 Microsoft Excel 2013에서 엽니다.  
  
     [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 창을 열고 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 모델을 업그레이드합니다.  
  
     그런 다음 통합 문서를 저장하고 SharePoint 서버에 게시합니다.  
  
 Analysis Services 기능 변경 사항에 대한 자세한 내용은 [SQL Server 2016 Analysis Services 기능의 동작 변경 내용](../../../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md)을 참조하세요.  
  
 새로 고침 기록에 대한 자세한 내용은 [데이터 새로 고침 기록 보기&#40;SharePoint용 파워 피벗&#41;](../../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)을 참조하세요.  
  
##  <a name="bkmk_to_2012sp1_from_2012"></a> 2012 PowerPivot for Excel 추가 기능으로 만든 버전에서 Office 2013 통합 문서로 업그레이드  
 이 섹션에서는 SQL Server 2012 **for Excel 2010 통합 문서** 에서 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] SQL Server 2012 SP1 **in Excel 2013 업그레이드에** 대해 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 설명합니다.  
  
 통합 문서를 업그레이드하면 이전 버전의 통합 문서에서 예약한 데이터 새로 고침을 시도할 때 발생하는 다음 오류를 해결할 수 있습니다.  
  
 "새로 고침 작업의 이전 버전을 사용 하 여 만든 통합 문서에 대 한 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 를 사용할 수 없습니다."  
  
 **통합 문서 업그레이드 방법**  
  
1.  Microsoft Excel 2013에서 각 통합 문서를 열어서 수동으로 업그레이드합니다.  
  
2.  통합 문서 및 통합 문서에 포함된 모델을 업그레이드하려면 통합 문서를 다운로드하고 Microsoft Excel 2013에서 엽니다.  
  
3.  [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 창을 열고 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 모델을 업그레이드합니다.  
  
4.  그런 다음 통합 문서를 저장하고 SharePoint 2013 서버에 게시합니다.  
  
##  <a name="bkmk_to_2012_from_2008R2"></a> 2008 R2 PowerPivot for Excel 2010 추가 기능으로 만든 버전에서 SQL Server 2012 통합 문서로 업그레이드  
 이 섹션에서는 SQL Server 2008 R2 **for Excel 2010 통합 문서** 에서 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] SQL Server 2012 **for Excel 2010으로 업그레이드에** 대해 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 설명합니다.  
  
 통합 문서를 업그레이드하면 이전 버전의 통합 문서에서 예약한 데이터 새로 고침을 시도할 때 발생하는 다음 오류를 해결할 수 있습니다.  
  
 "새로 고침 작업의 이전 버전을 사용 하 여 만든 통합 문서에 대 한 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 를 사용할 수 없습니다."  
  
 **통합 문서 업그레이드 방법**  
  
 업그레이드할 때 다음과 같은 두 가지 방법을 사용할 수 있습니다.  
  
1.  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 버전의 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel이 있는 컴퓨터의 Excel에서 통합 문서를 각각 열어 수동으로 업그레이드한 다음 서버에 다시 게시합니다. 추가 기능의 새 버전에서 통합 문서를 열면 내부 작업이 수행됩니다. 즉 통합 문서 데이터 연결 문자열에서 데이터 공급자가 MSOLAP.5로 업데이트되고 메타데이터가 업데이트되며 새 구현에 맞게 관계가 다시 만들어집니다.  
  
2.  또는 예약 데이터 새로 고침을 실행할 때 SharePoint 팜의 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 시스템 서비스가 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)][!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 통합 문서로 자동으로 업그레이드되는 자동 업그레이드 기능을 SharePoint 관리자가 사용하도록 설정할 수 있습니다(예약된 데이터 새로 고침에 대해 구성된 통합 문서만 업그레이드됨).  
  
    > [!NOTE]  
    >  자동 업그레이드는 서버 구성 기능이며 특정 통합 문서, 라이브러리 또는 사이트 모음에 대해 활성화하거나 비활성화할 수 없습니다.  
  
 **데이터 새로 고침 중에 자동 업그레이드를 구성하는 방법**  
  
 자동 업그레이드를 사용하려면 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 구성 도구에서 **서버에서 데이터 새로 고침을 사용하여 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 통합 문서 자동 업그레이드** 확인란을 선택해야 합니다. 도구 내에서 확인란은 **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 시스템 서비스 업그레이드** 페이지와 새 설치를 구성하는 경우 **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 서비스 애플리케이션 만들기** 페이지에 있습니다.  
  
 다음 cmdlet을 실행하여 자동 업그레이드가 설정되어 있는지 확인할 수 있습니다.  
  
```  
PS C:\Windows\system32> Get-PowerPivotSystemService  
```  
  
 Get-PowerPivotSystemService의 출력은 속성 및 해당 값의 목록입니다. 속성 목록에 **WorkbookUpgradeOnDataRefresh** 가 있어야 합니다. 자동 업그레이드를 사용하는 경우 **true** 로 설정됩니다. **false**인 경우 다음 단계를 계속하여 자동 통합 문서 업그레이드를 활성화합니다.  
  
 자동 통합 문서 업그레이드를 활성화하려면 다음 명령을 실행합니다.  
  
```  
PS C:\Windows\system32> Set-PowerPivotSystemService -WorkbookUpgradeOnDataRefresh:$true -Confirm:$false  
```  
  
 통합 문서를 업그레이드한 후에 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 추가 기능에서 예약된 데이터 새로 고침과 새 기능을 사용할 수 있습니다.  
  
##  <a name="bkmk_runold"></a> 최신 서버에서 여러 통합 문서 버전 실행  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 의 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] 인스턴스에서 이전 버전과 최신 버전의 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)]통합 문서를 함께 실행할 수 있습니다.  
  
 서버를 설치한 방법에 따라 이전 버전의 Analysis Services OLE DB 공급자를 설치 **해야** 동일한 서버에서 이전 통합 문서와 새 통합 문서에 액세스할 수 있는 경우도 있습니다.  
  
 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 의 이전 SQL Server 인스턴스에 최신 버전의 통합 문서를 게시할 수 없습니다. [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 인스턴스는 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 버전의 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]에서 만든 통합 문서를 로드하지 않으며, SQL Server 2012 인스턴스는 Excel의 [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 버전을 사용하여 만든 고급 데이터 모델의 Office 2013 통합 문서를 로드하지 않습니다.  
  
###  <a name="bkmk_msolapxslx"></a> PowerPivot 통합 문서에서 MSOLAP 데이터 공급자 정보를 확인하는 방법  
 다음 지침에 따라 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 통합 문서에서 사용되는 OLE DB 공급자를 확인합니다. [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] 추가 기능을 설치하지 않아도 데이터 연결 정보를 확인할 수 있습니다.  
  
1.  Excel의 데이터 탭에서 **연결**을 클릭합니다. **속성**을 클릭합니다.  
  
2.  **정의** 탭에서 공급자 버전이 연결 문자열의 시작 부분에 나타납니다.  
  
     **Provider=MSOLAP.5** 는 통합 문서가 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]임을 나타냅니다.  
  
     **Provider=MSOLAP.4** 는 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]를 나타냅니다.  
  
     **Data Source=$Embedded$** 는 통합 문서가 포함된 데이터베이스를 사용하는 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 통합 문서입니다.  
  
###  <a name="bkmk_msolappc"></a> 로컬 컴퓨터에서 MSOLAP 데이터 공급자의 현재 버전을 확인하는 방법  
 아래 지침을 사용하여 OLE DB 공급자가 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 통합 문서를 실행하는 서버 또는 워크스테이션에서 최신 버전인지 확인합니다. 현재 버전을 알고 있으면 업그레이드 후 데이터 연결 오류 문제를 해결하는 데 도움이 될 수 있습니다.  
  
1.  레지스트리 편집기에서 HKEY_CLASSES_ROOT로 이동합니다.  
  
2.  MSOLAP이 나타날 때까지 아래로 스크롤합니다. 시스템에 설치된 OLAP 공급자 중에 MSOLAP.5가 나열되었는지 확인합니다. MSOLAP | CurVer이 MSOLAP.5로 설정되었는지 확인합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SharePoint 2013으로 파워 피벗 마이그레이션](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [SharePoint용 파워 피벗 업그레이드](../../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Analysis Services의 새로운 기능](../../../analysis-services/what-s-new-in-analysis-services.md)   
 [데이터 새로 고침 기록 보기&#40;SharePoint용 파워 피벗&#41;](../../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
  
