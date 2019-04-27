---
title: SQL Server 2014의에서 기능을 서비스의 주요 변경 내용 분석 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- breaking changes [Analysis Services]
- upgrading Analysis Services
ms.assetid: aeb02542-5a6c-458c-a110-13413dd3e9d9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 944385d23b39938a6cb4a28afa16c3d2d67dca23
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62658152"
---
# <a name="breaking-changes-to-analysis-services-features-in-sql-server-2014"></a>SQL Server 2014에서 Analysis Services 기능의 주요 변경 내용
  이 항목에서는 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]의 주요 변경 내용에 대해 설명합니다. 이러한 변경 내용에 따라 이전 버전의 SQL Server을 기반으로 한 애플리케이션, 스크립트 또는 기능을 사용하지 못할 수도 있습니다.  
  
 항목 내용  
  
-   [SQL Server 2014의에서 주요 변경 내용](#bkmk_sql2014)  
  
-   [SQL Server 2012 SP1의 주요 변경 내용](#bkmk_2012Sp1)  
  
-   [SQL Server 2012의에서 주요 변경 내용](#bkmk_sql11)  
  
-   [SQL Server 2008/s q L Server 2008 R2의 주요 변경 내용](#bkmk_sql10)  
  
##  <a name="bkmk_sql2014"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]의 주요 변경 내용  
 이 릴리스에는 테이블 형식, 다차원, 데이터 마이닝 또는 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 기능에 대해 발표된 새로운 변경이 없습니다.  그러나  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 이(가) [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 버전과 아주 유사하므로 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서 업그레이드하는 경우의 편의를 위해 두 이전 릴리스의 새로운 변경을 여기에 제공합니다.  
  
##  <a name="bkmk_2012Sp1"></a> SQL Server 2012 SP1의 주요 변경 내용  
 세계화 관련 코드 변경 내용에 따라 일부 애플리케이션을 사용할 수 없습니다. 알려진 문제는 다음과 같습니다.  
  
 **개체 식별자의 대/소문자 구분**  
 코드 변경은 모든 개체 식별자의 대/소문자가 일부 언어에서 반대의 결과를 나타내도록 하기 위한 것입니다. 데이터 정렬에 관계없이 의도적으로 모든 개체 식별자의 대/소문자를 구분합니다. 이 변경은 Analysis Services를 동일한 솔루션 스택에서 일반적으로 사용되는 다른 애플리케이션에 맞게 조정합니다.  
  
 기본 라틴어 알파벳 26자를 기반으로 하는 언어의 경우 이제 개체 식별자에서 대/소문자를 구분하며 이는 의도된 동작입니다.  
  
 키릴자모와 대/소문자를 구분하는 다른 이원법 언어 스크립트의 경우 이제 개체 식별자의 대/소문자를 구분합니다. 주요 변경 내용은 개체 식별자와 개체 식별자 참조 간에 대/소문자가 다른 경우에 주로 발생합니다(예: 모두 대/소문자로 된 개체 식별자를 참조하는 처리 스크립트). 이 동작은 나중에 변경될 가능성이 있지만 일시적인 해결 방법으로 개체 식별자와 동일한 대/소문자를 사용하도록 스크립트를 수정하는 것이 좋습니다.  
  
##  <a name="bkmk_sql11"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]의 주요 변경 내용  
 이 섹션에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 의 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]기능에 대해 보고된 주요 변경 내용을 설명합니다.  
  
|문제점|Description|  
|-----------|-----------------|  
|[!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 설치를 위한 설치 명령이 제거되었습니다.|설치 프로그램은 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]를 설치하지만 더 이상 구성하지는 않습니다. 이제 구성 동작에 사용되는 값을 수집하는 설치 명령이 제거되었습니다. 해당 명령으로는 /FARMACCOUNT, /FARMPASSWORD, /PASSPHRASE, /FARMADMINPORT 등이 있습니다.<br /><br /> 무인 설치를 위한 설치 스크립트를 만든 경우 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 설치를 위한 해당 스크립트를 수정해야 합니다. 또는 PowerShell cmdlet을 사용하여 무인 모드에서 서버를 구성하면 됩니다. 자세한 내용은 [명령 프롬프트에서 PowerPivot 설치](../../2014/sql-server/install/install-powerpivot-from-the-command-prompt.md) 하 고 [Windows PowerShell을 사용 하 여 PowerPivot 구성](power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)합니다.|  
  
##  <a name="bkmk_sql10"></a> 주요 변경 내용 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]/[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
 이 섹션에는 이전 릴리스에서 변경된 주요 변경 내용이 포함되어 있습니다. [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]에서 업그레이드하는 경우, [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]에 도입된 주요 변경 내용을 검토해야 합니다.  
  
|문제점|Description|  
|-----------|-----------------|  
|열거된 멤버 또는 열거 집합의 크로스 조인이 들어 있는 명명된 집합에 대해 단순 Exists 함수의 동작이 달라졌습니다.|[!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]에서는 열거된 멤버 또는 열거 집합의 크로스 조인이 들어 있는 명명된 집합에 대해 단순 Exists 함수가 작동하지 않았습니다. [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]의 원래 릴리스 버전 및 SP1과 호환성을 유지하려면 "ConfigurationSettings\OLAP\Query\NamedSetShallowExistsMode" 구성 속성을 1로 설정하고, [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] SP2와 호환성을 유지하려면 2로 설정합니다.|  
|VBA 함수에서 null 값과 비어 있는 값을 처리하는 방식이 [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]와 달라졌습니다.|[!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]에서는 null 값이나 빈 값을 인수로 사용하면 VBA 함수가 0이나 빈 문자열을 반환했지만 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서는 null을 반환합니다.|  
|DSO가 기본적으로 설치되지 않기 때문에 마이그레이션 마법사가 실패합니다.|기본적으로 SQL Server 2008에서는 이전 버전과의 호환성을 위한 DSO(의사 결정 지원 개체) 구성 요소가 설치되지 않습니다. 이전 버전과의 호환성 패키지는 기본적으로 설치되지만 이 패키지에서 DSO 구성 요소는 사용되지 않습니다. SQL Server Analysis Services 마이그레이션 마법사는 이 구성 요소를 사용하기 때문에 이 구성 요소를 설치하지 않으면 마법사가 실패합니다. DSO 구성 요소를 설치하려면 다음을 수행합니다.<br /><br /> 1) 제어판을 엽니다.<br />Windows XP 또는 Windows Server 2003, 2)에서 선택 **프로그램 추가 / 제거**합니다. Windows Vista 및 Windows Server 2008의 경우 **프로그램 및 기능**을 선택합니다.<br />3) 마우스 오른쪽 단추로 클릭 **Microsoft SQL Server 2005 Backward Compatibility**, 선택한 **변경**합니다.<br />이전 버전과 호환성 설치 마법사 4)에서 클릭 **다음**합니다.<br />5) 프로그램 유지 관리 페이지에서 선택 **수정**를 클릭 하 고 **다음**합니다.<br />6) 기능 선택 페이지에서 의사 결정 지원 개체 (DSO)를 사용할 수 없는 경우 아래쪽 화살표를 클릭 하 고 선택 **이 기능은 로컬 하드 드라이브에 설치 됩니다**합니다. **다음**을 클릭합니다.<br />프로그램 페이지를 수정 하려면 준비, 7)에서 클릭 **설치**합니다.<br />설치가 완료 되 면 8) 클릭 **완료**합니다.<br /><br /> <br /><br /> 이전 단계를 수행 하 여 마이그레이션이 완료 된 후에 DSO를 제거할 수에 DSO 옵션을 변경 합니다. "**이 기능을 사용할 수 없습니다**."<br /><br /> 이전 버전과의 호환성 패키지가 설치되지 않은 경우 SQL Server 2008 배포 미디어를 통해 설치할 수 있습니다. 각 대상 아키텍처마다 해당하는 버전이 있습니다(x86, x64, ia64). 이러한 버전은 다음 위치에서 찾을 수 있습니다.<br /><br /> x86\Setup\x86\SQLServer2005_BC.msi<br /><br /> x64\Setup\x64\SQLServer2005_BC.msi<br /><br /> ia64\Setup\ia64\SQLServer2005_BC.msi|  
|Data 폴더에는 파티션 위치를 배치하지 않는 것이 좋습니다.|서버는 Data 폴더를 관리하고 개체가 생성, 삭제 및 수정될 때 폴더를 만들거나 삭제합니다. 따라서 데이터베이스, 큐브 및 차원에 대한 하위 폴더에서는 특히 Data 폴더 내에 파티션 스토리지 위치를 지정하지 않는 것이 좋습니다. 서버에서 Create 또는 Alter를 사용하여 이 작업을 수행할 수는 있지만 경고가 표시됩니다. SQL Server 2005 Analysis Services에서 Data 폴더에 파티션 스토리지 위치가 있는 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services로 데이터베이스를 업그레이드할 경우에는 이 방식이 효과적입니다. Restore 또는 Sync를 사용하려면 Data 폴더 외부로 파티션 스토리지 위치를 이동해야 합니다.|  
|ProClarity Analytics Server 및 Microsoft Office PerformancePoint Server 2007에서 쿼리에 "EXISTING" MDX 키워드를 사용하면 예상치 못한 결과를 얻을 수 있습니다.|ProClarity Analytics Server 및 Microsoft Office PerformancePoint Server 2007은 특정한 경우에 MDX의 EXISTING 키워드를 잘못된 방식으로 사용합니다. [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services에 적용된 변경 내용으로 인해 이러한 쿼리가 예상치 못한 결과를 반환할 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 이전 버전과의 호환성](analysis-services-backward-compatibility.md)  
  
  
