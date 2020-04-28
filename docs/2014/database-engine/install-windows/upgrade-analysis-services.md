---
title: Analysis Services 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
author: Minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cdd9e34e57694efc1234a2f0245833596644cb73
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68889189"
---
# <a name="upgrade-analysis-services"></a>Analysis Services 업그레이드
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 업그레이드할 수 있습니다. SharePoint 모드에서 업그레이드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하는 방법에 대 한 자세한 내용은 [SharePoint용 PowerPivot 업그레이드](upgrade-power-pivot-for-sharepoint.md)를 참조 하세요. 기존 SQL Server 인스턴스를 업그레이드 하는 방법에 대 한 자세한 내용은 [설치 마법사를 사용 하 여 SQL Server 2014로 업그레이드 &#40;설치&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)를 참조 하세요.  
  
## <a name="known-upgrade-issues"></a>알려진 업그레이드 문제  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]으로 업그레이드하기 전에 다음을 검토하십시오.  
  
-   [SQL Server 2014 릴리스 정보](https://go.microsoft.com/fwlink/?LinkID=296445)  
  
-   더 이상 사용 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 되지 않거나 사용 되지 않거나 변경 된 기능에 대 한 자세한 내용은 [Analysis Services 이전 버전과의 호환성](https://docs.microsoft.com/analysis-services/analysis-services-backward-compatibility)을 참조 하세요.  
  
## <a name="pre-upgrade-checklist"></a>업그레이드 전 검사 목록  
 업그레이드 전에 다음 정보를 검토하십시오.  
  
-   [지원되는 버전 및 에디션 업그레이드](supported-version-and-edition-upgrades.md)  
  
-   [SQL Server 2014 설치에 대한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [시스템 구성 검사기의 검사 매개 변수](check-parameters-for-the-system-configuration-checker.md)  
  
-   [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [Analysis Services 데이터베이스 백업 및 복원](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)  
  
-   [업그레이드 관리자를 사용하여 업그레이드 준비](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)  
  
## <a name="upgrading-analysis-services"></a>Analysis Services 업그레이드  
 다음의 여러 방법 중에서 선택하여 서버 및 데이터를 업그레이드할 수 있습니다.  
  
-   **내부 업그레이드** 는 기존 프로그램 파일을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 프로그램 파일로 바꿉니다. 데이터베이스 위치는 동일하게 유지됩니다. 프로그램 폴더는 새 이름을 반영하여 업데이트됩니다.  
  
-   **Side-by-side 업그레이드** 는 기존 Analysis Services 인스턴스가 있는 동일한 컴퓨터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에를 새로 설치 하는 것입니다. 같은 컴퓨터의 새 인스턴스로 데이터베이스를 이동한 후에 더 이상 사용하지 않는 이전 버전을 제거할 수 있습니다.  
  
-   새 하드웨어에 Analysis Services를 설치한 후에 기존 데이터베이스를 해당 서버로 마이그레이션할 수도 있습니다.  
  
## <a name="in-place-upgrade"></a>내부 업그레이드  
 기존 인스턴스를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 로 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 업그레이드 하 고, 업그레이드 프로세스의 일부로 기존 인스턴스에서 기존 데이터베이스를 새 인스턴스로 자동 마이그레이션할 수 있습니다. 메타데이터와 이진 데이터는 두 버전 간에 호환되므로 업그레이드 후 이 데이터를 보존하면 수동으로 마이그레이션할 필요가 없습니다.  
  
 기존 인스턴스를 업그레이드하려면 설치 프로그램을 실행하고 기존 인스턴스의 이름을 새 인스턴스의 이름으로 지정합니다.  
  
## <a name="upgrading-databases"></a>데이터베이스 업그레이드  
 이전 버전 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 작성된 데이터베이스는 이전 데이터베이스 호환성 수준 설정을 사용하여 업그레이드된 서버에서 실행됩니다. 다음 버전에서 만든 데이터베이스의 데이터베이스 호환성 수준은 105입니다. 새로운 데이터베이스 호환성 수준을 필요로 하는 기능을 사용하려면 호환성 수준을 변경할 수 있습니다. 그렇지 않은 경우에는 원래 설정을 사용하여 업그레이드된 서버에서 데이터베이스를 실행하면 됩니다. 자세한 내용은 [다차원 데이터베이스의 호환성 수준 설정 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services)를 참조 하세요.  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Microsoft OLAP 아키텍처 이해](https://docs.microsoft.com/analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture)   
 [업그레이드 SharePoint용 PowerPivot](upgrade-power-pivot-for-sharepoint.md)   
 [다차원 및 데이터 마이닝 모드에서 Analysis Services 설치](../../sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)   
 [SharePoint 2010용 PowerPivot 설치](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
