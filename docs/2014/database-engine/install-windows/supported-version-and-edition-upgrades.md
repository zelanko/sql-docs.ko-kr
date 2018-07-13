---
title: 지원되는 버전 및 에디션 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server], adding to existing installations
- versions [SQL Server], upgrading
- upgrading SQL Server, upgrades supported
- cross-language support
ms.assetid: 702359c4-6ca9-42a8-860c-a95a802898a1
caps.latest.revision: 132
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ce657b9b4b832e1c880edd3d2c6d966cd5a78dc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37252645"
---
# <a name="supported-version-and-edition-upgrades"></a>지원되는 버전 및 에디션 업그레이드
  업그레이드할 수 있습니다 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], 및 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], 및 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]합니다. 이 항목에서는 이러한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 지원되는 업그레이드 경로 및 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에 대해 지원되는 버전 업그레이드에 대해 설명합니다.  
  
## <a name="pre-upgrade-checklist"></a>업그레이드 전 검사 목록  
  
-   한 버전의 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 에서 다른 버전으로 업그레이드하기 전에 현재 사용 중인 기능이 이동할 버전에서 지원되는지 확인합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 업그레이드하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에 대해 Windows 인증을 사용하도록 설정하고 기본 구성, 즉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin 그룹의 멤버인지를 확인합니다.  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]로 업그레이드하려면 지원되는 운영 체제를 실행해야 합니다. 자세한 내용은 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 참조하세요.  
  
-   다시 시작이 보류 중인 경우 업그레이드가 차단됩니다.  
  
-   Windows Installer 서비스가 실행되고 있지 않은 경우 업그레이드가 차단됩니다.  
  
## <a name="unsupported-scenarios"></a>지원되지 않는 시나리오  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서는 버전 간 인스턴스가 지원되지 않습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소의 버전 번호는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인스턴스에서 동일해야 합니다.  
  
-   플랫폼 간 업그레이드는 지원되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 32비트 인스턴스를 네이티브 64비트로 업그레이드할 수 없습니다. 하지만 데이터베이스를 복제에 게시하지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 32비트 인스턴스에서 데이터베이스를 분리하거나 백업한 다음 이를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (64비트)의 새 인스턴스에 연결하거나 이 인스턴스로 복원할 수 있습니다. master, msdb 및 model 시스템 데이터베이스의 모든 로그인과 기타 사용자 개체를 다시 만들어야 합니다.  
  
-   기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 업그레이드하는 동안에는 새 기능을 추가할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드한 후 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 프로그램을 사용하여 기능을 추가할 수 있습니다. 자세한 내용은 [는 인스턴스가 SQL Server 2014의 기능 추가 &#40;설치&#41;](add-features-to-an-instance-of-sql-server-setup.md)합니다.  
  
-   WOW 모드에서는 장애 조치(Failover) 클러스터가 지원되지 않습니다.  
  
-   이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 평가판에서는 업그레이드가 지원되지 않습니다.  
  
## <a name="upgrades-from-earlier-versions-to-includesssql14includessssql14-mdmd"></a>이전 버전에서 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]로 업그레이드  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에 대한 지원은 다음에 나오는 '[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에 대한 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 지원' 섹션에서 자세하게 설명합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 32 비트 버전으로 업그레이드할 수 있습니다 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 64 비트 서버의 32 비트 하위 시스템 (WOW64).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 64 비트 버전으로 업그레이드할 수 있습니다 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 64 비트 서버로 합니다.  
  
> [!NOTE]  
>  이전 버전의 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise Edition에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 업그레이드하는 경우 엔터프라이즈 버전: 코어 기반 라이선스와 엔터프라이즈 버전 중에서 선택합니다. 이러한 엔터프라이즈 버전은 지원되는 최대 코어 수 및 라이선스 모드와 관련해서만 다릅니다. 자세한 내용은 [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)을 참조하세요.  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 다음 버전에서의 업그레이드가 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 이상  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 이상  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 이상  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 이상  
  
 다음 표에는 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]로 업그레이드하는 데 지원되는 시나리오가 나열되어 있습니다.  
  
|업그레이드할 버전|지원되는 업그레이드 경로|  
|------------------|----------------------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express,<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express with Tools 및<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Small Business|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express with Tools 및<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Datacenter|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Small Business|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express,<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express with Tools 및<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express with Tools 및<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express Management Studio<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Business Intelligence|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
  
### <a name="includesssql14includessssql14-mdmd-support-for-includessversion2005includesssversion2005-mdmd"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 에 대 한 지원 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
 이 섹션에서는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 에 대한 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]지원에 대해 설명합니다. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서는 다음을 수행할 수 있습니다.  
  
-   업그레이드는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스 엔진의 인스턴스에 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 실행 하 여 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 설치 마법사 또는 명령 프롬프트를 사용 하 여 설치 합니다.  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스(mdf/ldf 파일)를 데이터베이스 엔진의 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 인스턴스에 연결합니다.  
  
-   백업에서 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스를 데이터베이스 엔진의 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 인스턴스로 복원합니다.  
  
-   [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 패키지를 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]로 업그레이드합니다. 자동 전체 업그레이드를 사용하여 패키지를 실행합니다.  
  
-   업그레이드는 [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] 하 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 실행 하 여 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 설치 합니다.  
  
-   [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] 큐브를 백업하고 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에 복원합니다.  
  
-   [!INCLUDE[ssRSversion2005](../../includes/ssrsversion2005-md.md)] 설치 프로그램을 실행하여 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]를 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]로 업그레이드합니다.  
  
-   연결할 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]를 사용 하 여 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 2014입니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스를 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]로 업그레이드하는 경우 데이터베이스 호환성 수준이 90에서 100으로 변경됩니다. (에서 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], 데이터베이스 호환성 수준의 유효한 값은 100, 110 및 120입니다.) [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)에서는 호환성 수준 변경이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 응용 프로그램에 미칠 수 있는 영향에 대해 설명합니다.  
  
 위의 목록에 지정되지 않은 모든 시나리오는 지원되지 않습니다. 여기에는 다음이 포함되지만 이에 제한되지 않습니다.  
  
-   동일한 컴퓨터에 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 및 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]를 함께 설치  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스를 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 인스턴스가 포함된 복제 토폴로지의 멤버로 사용  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 및 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스 간의 데이터베이스 미러링 구성  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 및 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스 간의 로그 전달을 사용하여 트랜잭션 로그 백업  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 및 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스 간의 연결된 서버 구성  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Management Studio에서 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 인스턴스 관리  
  
-   [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] Management Studio에서 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 큐브 연결  
  
-   [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio에서 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 에 연결  
  
-   [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio에서 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 서비스 관리  
  
-   실행 및 업그레이드와 같은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 타사 사용자 지정 Integration Services 구성 요소에 대한 지원  
  
## <a name="includesssql14includessssql14-mdmd-edition-upgrade"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Edition Upgrade  
 다음 표에는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 지원되는 버전 업그레이드 시나리오가 나열되어 있습니다.  
  
 버전 업그레이드를 수행 하는 방법에 대 한 단계별 지침을 참조 하세요 [서로 다른 버전의 SQL Server 2014로 업그레이드 &#40;설치&#41;](upgrade-to-a-different-edition-of-sql-server-setup.md)합니다.  
  
|업그레이드할 버전|업그레이드 버전|  
|------------------|----------------|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server + CAL 및 코어) <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise(Server+CAL 또는 코어 라이선스)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Evaluation Enterprise <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise(Server+CAL 또는 코어 라이선스)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> Evaluation Enterprise(무료 버전)에서 유료 버전으로 업그레이드할 경우 독립 실행형 설치는 지원되지만 클러스터형 설치는 지원되지 않습니다.|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 표준 <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise(Server+CAL 또는 코어 라이선스)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 개발자 <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise(Server+CAL 또는 코어 라이선스)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise(Server+CAL 또는 코어 라이선스)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express <sup>1</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise(Server+CAL 또는 코어 라이선스)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
  
 또한 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise(Server+CAL 라이선스)와 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise(코어 라이선스) 간의 에디션 업그레이드를 수행할 수도 있습니다.  
  
|에디션 업그레이드 원본|에디션 업그레이드 대상|  
|--------------------------|------------------------|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server + CAL 라이선스) <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise(코어 라이선스)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise(코어 라이선스)|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise(Server+CAL 라이선스)|  
  
 <sup>1</sup> 에 적용 됩니다 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express with Tools 및 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express with Advanced Services.  
  
 <sup>2</sup> 의 버전 변경은 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 장애 조치 클러스터는 제한 됩니다. 다음과 같은 시나리오는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 장애 조치(Failover) 클러스터에서 지원되지 않습니다.  
  
-   SQL Server 2014 Enterprise를 SQL Server 2014 Developer, Standard 또는 Enterprise Evaluation으로 업그레이드  
  
-   SQL Server 2014 Developer를 SQL Server 2014 Standard 또는 Enterprise Evaluation으로 업그레이드  
  
-   SQL Server 2014 Standard를 SQL Server 2014 Enterprise Evaluation으로 업그레이드  
  
-   SQL Server 2014 Enterprise Evaluation을 SQL Server 2014 Standard로 업그레이드  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2014 버전에서 지 원하는 기능](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [SQL Server 2014로 업그레이드](upgrade-sql-server.md)   
 [업그레이드 관리자를 사용하여 업그레이드 준비](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)  
  
  
