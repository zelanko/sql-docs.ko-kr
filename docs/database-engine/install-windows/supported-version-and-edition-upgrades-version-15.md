---
title: 지원되는 버전 업그레이드(SQL Server 2019)
description: SQL Server 2019에 대해 지원되는 버전 업그레이드입니다.
ms.custom: ''
ms.date: 11/04/2019
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
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: ec6c743ea40da4d7ee6846c3a1373d3912ec0dc9
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900308"
---
# <a name="supported-version--edition-upgrades-sql-server-2019"></a>지원되는 버전 업그레이드(SQL Server 2019)

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]
  
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)]및 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]에서 업그레이드할 수 있습니다. 이 문서에서는 이러한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 지원되는 업그레이드 경로 및 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]에 대해 지원되는 버전 업그레이드에 대해 설명합니다.  
  
## <a name="pre-upgrade-checklist"></a>업그레이드 전 검사 목록  

- 한 버전의 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] 에서 다른 버전으로 업그레이드하기 전에 현재 사용 중인 기능이 이동할 버전에서 지원되는지 확인합니다.  
- 지원되는 [하드웨어 및 소프트웨어](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)를 확인합니다.
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 업그레이드하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에 대해 Windows 인증을 사용하도록 설정하고 기본 구성, 즉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin 그룹의 멤버인지를 확인합니다.
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]로 업그레이드하려면 지원되는 운영 체제를 실행해야 합니다. 자세한 내용은 [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)을 참조하세요.  
- 다시 시작이 보류 중인 경우 업그레이드가 차단됩니다.  
- Windows Installer 서비스가 실행되고 있지 않은 경우 업그레이드가 차단됩니다.

## <a name="unsupported-scenarios"></a>지원되지 않는 시나리오

- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]에서는 버전 간 인스턴스가 지원되지 않습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성 요소의 버전 번호는 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]의 인스턴스에서 동일해야 합니다.  
  
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]은 64비트 플랫폼에서만 사용할 수 있습니다. 플랫폼 간 업그레이드는 지원되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 32비트 인스턴스를 네이티브 64비트로 업그레이드할 수 없습니다. 하지만 데이터베이스를 복제에 게시하지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 32비트 인스턴스에서 데이터베이스를 분리하거나 백업한 다음 이를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (64비트)의 새 인스턴스에 연결하거나 이 인스턴스로 복원할 수 있습니다. master, msdb 및 model 시스템 데이터베이스의 모든 로그인과 기타 사용자 개체를 다시 만들어야 합니다.  
  
- 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 업그레이드하는 동안에는 새 기능을 추가할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]로 업그레이드한 후 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] 설치 프로그램을 사용하여 기능을 추가할 수 있습니다. 자세한 내용은 [SQL Server 인스턴스에 기능 추가&#40;설치 프로그램&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)를 참조하세요.  
 
## <a name="upgrades-from-earlier-versions-to-sssqlv15-md"></a>이전 버전에서 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]로 업그레이드  
 
[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]은 다음 버전의 SQL Server에서 업그레이드할 수 있습니다.

- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 이상
- [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP3 이상
- [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] SP2 이상
- [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]

다음 표에는 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]로 업그레이드하는 데 지원되는 시나리오가 나열되어 있습니다.  
  
|업그레이드할 버전|지원되는 업그레이드 경로|  
|:------|:------|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Enterprise|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Developer|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/>[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Standard|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Express |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express <br/> <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Business Intelligence|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 Evaluation|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Enterprise|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Developer|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Standard|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Express |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 비즈니스 인텔리전스|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 Evaluation|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Enterprise|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Developer|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Standard|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Express |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Business Intelligence|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] 13.0.1601.5 Evaluation|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Enterprise|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Developer|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Standard|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Express |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Business Intelligence|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/> |  
|[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] Evaluation|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer|
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] 출시 후보* |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise |  
|[!INCLUDE[sssqlv15_md](../../includes/sssqlv15-md.md)] Developer |[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise | 

 \* Microsoft는 특별히 얼리어답터 프로그램에 참여한 고객들을 위해 릴리스 후보 소프트웨어에서 업그레이드하는 것을 지원합니다.

## <a name="migrate-to-sql-server-2019"></a>SQL Server 2019로 마이그레이션

이전 버전에서 데이터베이스를 마이그레이션할 수 있습니다. 예를 들어 [!INCLUDE [sskilimanjaro-md](../../includes/sskilimanjaro-md.md)]에서 SQL Server 2019로 데이터베이스를 마이그레이션할 수 있습니다.

자세한 내용은 [Azure 데이터베이스 마이그레이션 가이드](https://datamigration.microsoft.com/scenario/sql-to-sqlserver)를 참조하세요.

다음은 마이그레이션을 계획하고 구현하는 데 도움이 되는 팁과 도구입니다.

- 마이그레이션 도구: 마이그레이션은 [DMA(Data Migration Assistant)](https://aka.ms/dma)를 통해 지원됩니다.
- 백업 및 복원: SQL Server 2008 또는 SQL Server 2008 R2에서 수행된 백업을 SQL Server 2019로 복원할 수 있습니다.
- 로그 전달: 주 데이터베이스에서 SQL Server 2008 SP3 이상 또는 SQL Server 2008 R2 SP2 이상을 실행하고 보조 데이터베이스에서 SQL Server 2019를 실행하는 경우 로그 전달이 지원됩니다. 

   > [!WARNING]
   > 자동 또는 수동 장애 조치(failover)가 발생하고 SQL Server 2019 인스턴스가 주 데이터베이스가 되면 SQL Server 2008 또는 SQL Server 2008 R2 인스턴스는 보조 데이터베이스가 되어 주 데이터베이스의 변경 내용을 받을 수 없습니다.

- 대량 로드: 테이블을 SQL Server 2008 또는 SQL Server 2008 R2에서 SQL Server 2019로 대량 복사할 수 있습니다.

## <a name="sssqlv15-md-edition-upgrade"></a>[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Edition Upgrade 

다음 표에는 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]에서 지원되는 버전 업그레이드 시나리오가 나열되어 있습니다.  

버전 업그레이드를 수행하는 방법에 대한 단계별 지침은 [다른 SQL Server 버전으로 업그레이드&#40;설치 프로그램&#41;](../../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md)를 참조하세요.  
  
|업그레이드할 버전|업그레이드 버전|  
|------------------|----------------|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise(Server+CAL 및 코어)**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise |  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation Enterprise**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise(Server+CAL 또는 코어 라이선스) <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> Evaluation(무료 버전)에서 유료 버전으로 업그레이드할 경우 독립 실행형 설치는 지원되지만 클러스터형 설치는 지원되지 않습니다. 가용성 그룹에 참여하는 Windows 장애 조치(failover) 클러스터에 설치된 독립 실행형 인스턴스에는 이 제한이 적용되지 않습니다. |  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise(Server+CAL 또는 코어 라이선스)|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise(Server+CAL 또는 코어 라이선스) <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise(Server+CAL 또는 코어 라이선스) <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express*|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise(Server+CAL 또는 코어 라이선스) <br/><br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Web|  
  
 또한 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise(Server+CAL 라이선스)와 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise(코어 라이선스) 간의 에디션 업그레이드를 수행할 수도 있습니다.  
  
|에디션 업그레이드 원본|에디션 업그레이드 대상|  
|--------------------------|------------------------|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise(Server+CAL 라이선스)**|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise(코어 라이선스)|  
|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise(코어 라이선스)|[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise(Server+CAL 라이선스)|  
  
 \*[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express with Tools 및 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Express with Advanced Services에도 적용됩니다.  
  
 ** [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]의 클러스터된 인스턴스 버전을 변경하는 것은 제한되어 있습니다. 다음과 같은 시나리오는 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] 장애 조치(Failover) 클러스터에서 지원되지 않습니다.  
  
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Enterprise를 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer, Standard 또는 Evaluation으로 변경  
  
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Developer를 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard 또는 Evaluation으로 변경  
  
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard를 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation으로 변경  
  
- [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Evaluation을 [!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)] Standard로 변경  
  
## <a name="see-also"></a>참고 항목  

 [[!INCLUDE[sssqlv15-md](../../includes/sssqlv15-md.md)]의 버전 및 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-version-15.md)

 [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)

 [SQL Server 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)  
