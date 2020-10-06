---
title: 지원되는 버전 업그레이드(SQL Server 2016)
description: SQL Server 2016에 대해 지원되는 버전 업그레이드입니다.
ms.custom: ''
ms.date: 06/27/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server], adding to existing installations
- versions [SQL Server], upgrading
- upgrading SQL Server, upgrades supported
- cross-language support
ms.assetid: 702359c4-6ca9-42a8-860c-a95a802898a1
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 784e005a9a7851c6e088255d8ff8b9e671796367
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91671006"
---
# <a name="supported-version--edition-upgrades-sql-server-2016"></a>지원되는 버전 업그레이드(SQL Server 2016)

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]
  
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]및 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 업그레이드할 수 있습니다. 이 문서에서는 이러한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 지원되는 업그레이드 경로 및 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]에 대해 지원되는 버전 업그레이드에 대해 설명합니다.  
  
## <a name="pre-upgrade-checklist"></a>업그레이드 전 검사 목록  
  
-   한 버전의 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 에서 다른 버전으로 업그레이드하기 전에 현재 사용 중인 기능이 이동할 버전에서 지원되는지 확인합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 업그레이드하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에 대해 Windows 인증을 사용하도록 설정하고 기본 구성, 즉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin 그룹의 멤버인지를 확인합니다.  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]로 업그레이드하려면 지원되는 운영 체제를 실행해야 합니다. 자세한 내용은 [SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 참조하세요.  
  
-   다시 시작이 보류 중인 경우 업그레이드가 차단됩니다.  
  
-   Windows Installer 서비스가 실행되고 있지 않은 경우 업그레이드가 차단됩니다.  
  
## <a name="unsupported-scenarios"></a>지원되지 않는 시나리오  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]에서는 버전 간 인스턴스가 지원되지 않습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소의 버전 번호는 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]인스턴스에서 동일해야 합니다.  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]은 64비트 플랫폼에서만 사용할 수 있습니다. 플랫폼 간 업그레이드는 지원되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 32비트 인스턴스를 네이티브 64비트로 업그레이드할 수 없습니다. 하지만 데이터베이스를 복제에 게시하지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 32비트 인스턴스에서 데이터베이스를 분리하거나 백업한 다음 이를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (64비트)의 새 인스턴스에 연결하거나 이 인스턴스로 복원할 수 있습니다. master, msdb 및 model 시스템 데이터베이스의 모든 로그인과 기타 사용자 개체를 다시 만들어야 합니다.  
  
-   기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 업그레이드하는 동안에는 새 기능을 추가할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]로 업그레이드한 후 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 설치 프로그램을 사용하여 기능을 추가할 수 있습니다. 자세한 내용은 [SQL Server 2016 인스턴스에 기능 추가&#40;설치 프로그램&#41;](./add-features-to-an-instance-of-sql-server-setup.md)를 참조하세요.  
 
-   WOW 모드에서는 장애 조치(Failover) 클러스터가 지원되지 않습니다.  
  
-   이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 평가판에서는 업그레이드가 지원되지 않습니다.

-   RC1 또는 SQL Server 2016 이전 버전을 RC3 이상 버전으로 업그레이드하는 경우, 업그레이드하기 전에 PolyBase를 제거한 다음 업그레이드한 후에 다시 설치해야 합니다.
  
## <a name="upgrades-from-earlier-versions-to-sssql15-md"></a>이전 버전에서 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]로 업그레이드  
 
SQL Server 2016은 다음 버전의 SQL Server에서 업그레이드할 수 있습니다.
 
- [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] SP4 이상
- [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] SP3 이상
- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 이상
- [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 
 
> [!NOTE]  
> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 에서 데이터베이스를 업그레이드하려면 [2005에 대한 지원](#SupportFor2005)을 참조하세요.  
  
다음 표에는 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]로 업그레이드하는 데 지원되는 시나리오가 나열되어 있습니다.  
  
|업그레이드할 버전|지원되는 업그레이드 경로|  
|------------------|----------------------------|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Small Business|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Workgroup|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Datacenter|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Small Business|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Workgroup|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express <br/> <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 비즈니스 인텔리전스|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Evaluation|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Evaluation|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer|  
|[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 출시 후보* |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise |  
|[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] Developer |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise | 

 \* Microsoft는 특별히 TAP(기술 채택 프로그램)에 참여하는 고객들을 위해 릴리스 후보 소프트웨어에서의 업그레이드를 지원합니다. 
   
###  <a name="sssql15-md-support-for-ssversion2005"></a><a name="SupportFor2005"></a> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]의 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 지원  
이 섹션에서는 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 에 대한 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]지원에 대해 설명합니다. [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]에서는 다음을 수행할 수 있습니다.  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스(mdf/ldf 파일)를 데이터베이스 엔진의 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 인스턴스에 연결합니다.  
  
-   백업에서 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스를 데이터베이스 엔진의 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 인스턴스로 복원합니다.  
  
-   [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] 큐브를 백업하고 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]에 복원합니다.  
  
> [!NOTE]  
> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스를 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]로 업그레이드하는 경우 데이터베이스 호환성 수준이 90에서 100으로 변경됩니다. [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]에서 데이터베이스 호환성 수준에 유효한 값은 100, 110, 120 및 130입니다. [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)에서는 호환성 수준 변경이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 애플리케이션에 미칠 수 있는 영향에 대해 설명합니다.  
  
위의 목록에 지정되지 않은 모든 시나리오는 지원되지 않습니다. 여기에는 다음이 포함되지만 이에 제한되지 않습니다.  
  
-   동일한 컴퓨터에 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 및 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]를 함께 설치  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스를 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 인스턴스가 포함된 복제 토폴로지의 멤버로 사용  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 및 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스 간의 데이터베이스 미러링 구성  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 및 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스 간의 로그 전달을 사용하여 트랜잭션 로그 백업  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 및 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스 간의 연결된 서버 구성  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Management Studio에서 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 인스턴스 관리  
  
-   [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] Management Studio에서 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 큐브 연결  
  
-   [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio에서 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 에 연결  
  
-   [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio에서 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 서비스 관리  
  
-   실행 및 업그레이드와 같은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 타사 사용자 지정 Integration Services 구성 요소에 대한 지원  
  
## <a name="sssql15-md-edition-upgrade"></a>[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Edition Upgrade  
다음 표에는 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]에서 지원되는 버전 업그레이드 시나리오가 나열되어 있습니다.  
  
버전 업그레이드를 수행하는 방법에 대한 단계별 지침은 [다른 SQL Server 2016 버전으로 업그레이드&#40;설치 프로그램&#41;](../../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md)를 참조하세요.  
  
|업그레이드할 버전|업그레이드 버전|  
|------------------|----------------|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise(Server+CAL 및 코어)**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise |  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation Enterprise**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise(Server+CAL 또는 코어 라이선스) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> Evaluation(무료 버전)에서 유료 버전으로 업그레이드할 경우 독립 실행형 설치는 지원되지만 클러스터형 설치는 지원되지 않습니다. 가용성 그룹에 참여하는 Windows 장애 조치(failover) 클러스터에 설치된 독립 실행형 인스턴스에는 이 제한이 적용되지 않습니다.|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise(Server+CAL 또는 코어 라이선스)|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise(Server+CAL 또는 코어 라이선스) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise(Server+CAL 또는 코어 라이선스) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express*|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise(Server+CAL 또는 코어 라이선스) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
  
또한 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise(Server+CAL 라이선스)와 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise(코어 라이선스) 간의 에디션 업그레이드를 수행할 수도 있습니다.  
  
|에디션 업그레이드 원본|에디션 업그레이드 대상|  
|--------------------------|------------------------|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise(Server+CAL 라이선스)**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise(코어 라이선스)|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise(코어 라이선스)|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise(Server+CAL 라이선스)|  
  
 \*[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express with Tools 및 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express with Advanced Services에도 적용됩니다.  
  
 ** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 장애 조치(failover) 클러스터의 버전 변경은 제한됩니다. 다음과 같은 시나리오는 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 장애 조치(Failover) 클러스터에서 지원되지 않습니다.  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise를 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer, Standard 또는 Evaluation으로 변경  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer를 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard 또는 Evaluation으로 변경  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard를 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation으로 변경  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation을 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard로 변경  
  
## <a name="see-also"></a>참고 항목  

[SQL Server 2016의 버전 및 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2016.md)     
[SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)     
[SQL Server 2016으로 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)    
  
