---
title: 데이터베이스 엔진 업그레이드 방법 선택 | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- server-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5e57a427-2e88-4ef6-b142-4ccad97bcecc
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9049db61b062dc9211b47094886b831bc6667890
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="choose-a-database-engine-upgrade-method"></a>데이터베이스 엔진 업그레이드 방법 선택

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  가동 중지와 위험을 최소화하기 위해 이전 릴리스의 SQL Server에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 업그레이드하려는 경우 고려해야 할 몇 가지 방식이 있습니다. 전체 업그레이드를 실행하거나 새 설치로 마이그레이션하거나 롤링 업그레이드를 실행할 수 있습니다. 아래 다이어그램에 따라 적절한 방식을 선택할 수 있습니다. 다이어그램의 각 방식은 아래에서도 설명합니다. 다이어그램의 어느 지점에서 결정해야 하는지 알아보려면 [Plan and Test the Database Engine Upgrade Plan](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)를 참조하십시오.  
  
 ![데이터베이스 엔진 업그레이드 방법에 대한 의사 결정 트리](../../database-engine/install-windows/media/database-engine-upgrade-method-decision-tree.png "데이터베이스 엔진 업그레이드 방법에 대한 의사 결정 트리")  
  
 **다운로드**  
  
-   [!INCLUDE[SSnoversion](../../includes/ssnoversion-md.md)]를 다운로드하려면  **[평가 센터](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server)** 로 이동하세요.  
  
-   Azure 계정이 있으세요?  계정이 있으면 **[여기](http://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016)** 로 이동하여 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Developer Edition이 이미 설치되어 있는 가상 컴퓨터를 실행합니다.  
  
> [!NOTE]  
>  또한 Azure SQL 데이터베이스 업그레이드 또는 SQL Server 환경 가상화를 업그레이드 계획에 포함하여 고려할 수 있습니다. 이러한 문서는 본 문서의 범위를 벗어나지만, 일부 링크를 준비했습니다.
>   - [Azure Virtual Machines의 SQL Server 개요](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/)
>   - [Azure SQL Database](https://azure.microsoft.com/en-us/services/sql-database/) 
>   - [Azure에서 SQL Server 옵션 선택](https://azure.microsoft.com/documentation/articles/data-management-azure-sql-database-and-sql-server-iaas/)  
  
##  <a name="UpgradeInPlace"></a> 전체 업그레이드  
 이 방식에서는 SQL Server 설치 프로그램에서 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 비트를 새 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 비트로 바꾼 다음 시스템 및 사용자 데이터베이스 각각을 업그레이드하여 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치를 업그레이드합니다.  전체 업그레이드가 가장 쉽고 약간의 가동 중지 시간이 필요하며 대체가 필요할 경우 대체 시간이 더 오래 소요되고 일부 시나리오에서는 지원되지 않습니다. 지원되는 현재 위치 업그레이드 및 지원되지 않는 전체 업그레이드 시나리오에 대한 자세한 내용은 [지원되는 버전 및 에디션 업그레이드](../../database-engine/install-windows/supported-version-and-edition-upgrades-2017.md)를 참조하세요.  
  
 이 방식은 다음과 같은 시나리오에서 빈번하게 사용됩니다.  
  
-   고가용성(HA) 구성이 없는 개발 환경  
  
-   가동 중시 시간이 허용되고 최근 하드웨어 및 소프트웨어에서 실행되는 중요 업무와 관련 없는 운영 환경 가동 중지 시간은 데이터베이스의 크기와 I/O 하위 시스템의 속도에 따라 달라집니다. 메모리 최적화 테이블을 사용하는 경우 SQL Server 2014를 업그레이드하려면 시간이 다소 더 걸립니다. 자세한 내용은 [Plan and Test the Database Engine Upgrade Plan](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)를 참조하세요.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행할 때에는 업그레이드 사전 검사가 실행되는 과정에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 중지된 다음 다시 실행됩니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 업그레이드하면 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 덮어쓰게 되므로 이러한 인스턴스는 시스템에 더 이상 존재하지 않게 됩니다. 따라서 업그레이드 전에 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 및 기타 개체를 백업하세요.  
  
 다음은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 현재 위치 업그레이드에 필요한 단계를 개략적으로 표시한 다이어그램입니다.  
  
 ![데이터베이스 엔진 업그레이드- 비HA 전체 업그레이드](../../database-engine/install-windows/media/database-engine-upgrade-non-ha-in-place-upgrade.png "데이터베이스 엔진 업그레이드- 비HA 전체 업그레이드")  
  
 자세한 내용은 [설치 마법사를 사용하여 SQL Server 업그레이드&#40;설치 프로그램&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)를 참조하세요.  
  
##  <a name="NewInstallationUpgrade"></a> 새 설치로 마이그레이션  
 이 방식에서는 현재 환경을 유지하면서 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경을 빌드합니다. 이때 새 하드웨어와 새 버전의 운영 체제를 사용하는 경우가 많습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 새 환경에 설치한 다음에는 기존 사용자 데이터베이스를 기존 환경에서 새 환경으로 마이그레이션하고 가동 중지 시간을 최소화할 수 있도록 새 환경을 준비하기 위한 여러 단계를 수행합니다. 이러한 단계에는 다음을 마이그레이션하는 작업이 포함됩니다.  
  
-   **시스템 개체:** 일부 응용 프로그램은 단일 사용자 데이터베이스 범위 밖에 있는 정보, 엔터티 및/또는 개체에 따라 달라집니다. 일반적으로 응용 프로그램은 master 및 msdb 데이터베이스뿐만 아니라 사용자 데이터베이스에 따라 달라집니다. 사용자 데이터베이스의 올바른 작동을 위해 해당 데이터베이스 외부에 저장되어 있는 모든 요소는 대상 서버 인스턴스에서 사용할 수 있어야 합니다. 예를 들어 응용 프로그램에 대한 로그인은 master 데이터베이스에서 메타데이터로 저장되어 있으며 대상 서버에서 다시 생성되어야 합니다. 메타데이터가 msdb 데이터베이스에 저장되어 있는 SQL Server 에이전트 작업에 따라 응용 프로그램이나 데이터베이스 유지 관리 계획이 달라지는 경우 대상 서버 인스턴스에서 이러한 작업을 다시 만들어야 합니다. 마찬가지로 서버 수준 트리거에 대한 메타데이터는 master에 저장되어 있습니다.  
 
   응용 프로그램에 대한 데이터베이스를 다른 서버 인스턴스로 이동할 경우 대상 서버 인스턴스의 master 및 msdb에서 종속 개체와 엔터티의 모든 메타데이터를 다시 만들어야 합니다. 예를 들어 데이터베이스 응용 프로그램이 서비스 수준 트리거를 사용하는 경우 단순히 새 시스템에서 데이터베이스를 연결하거나 복원하는 것만으로 충분하지 않습니다. master 데이터베이스에서 이러한 트리거에 대한 모든 메타데이터를 수동으로 다시 만들지 않으면 데이터베이스가 예상대로 작동하지 않습니다. 자세한 내용은 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)를 참조하세요.  
  
-   **MSDB에 저장된 Integration Services 패키지:** 패키지를 MSDB에 저장하는 경우 [dtutil Utility](../../integration-services/dtutil-utility.md) 를 사용하여 이러한 패키지를 제외하거나 새 서버에 재배포해야 합니다. 새 서버에서 패키지를 사용하기 전에 패키지를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]으로 업그레이드해야 합니다. 자세한 내용은 [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md)를 참조하세요.  
  
-   **Reporting Services 암호화 키:** 보고서 서버 구성의 중요한 부분은 중요한 정보의 암호화에 사용되는 대칭 키의 백업 복사본을 만드는 것입니다. 대칭 키의 백업 복사본은 여러 일상 작업에 필요하며 새 설치에서 기존 보고서 서버 데이터베이스를 다시 사용할 수 있도록 합니다. 자세한 내용은 [Reporting Services 암호화 키 백업 및 복원](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md) 및 [Upgrade 및 Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)을 참조하세요.  
  
 새   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경의 시스템 개체가 기존 환경과 동일할 경우 기존 시스템의 사용자 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 마이그레이션할 때 기존 시스템의 가동 중시 시간을 최소화해야 합니다. 데이터베이스 마이그레이션은 백업 및 복원을 사용하여 수행하며 SAN 환경인 경우에는 LUN을 변경합니다. 두 방법의 단계는 아래 다이어그램에 나와 있습니다.  
  
> [!CAUTION]  
>  가동 중지 시간은 데이터베이스의 크기와 I/O 하위 시스템의 속도에 따라 달라집니다. 메모리 최적화 테이블을 사용하는 경우 SQL Server 2014를 업그레이드하려면 시간이 다소 더 걸립니다. 자세한 내용은 [Plan and Test the Database Engine Upgrade Plan](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)를 참조하세요.  
  
 사용자 데이터베이스를 마이그레이션한 후에는 다양한 방법 중 하나(예: 서버 이름 변경, DNS 항목 사용, 연결 문자열 수정)를 사용하여 새 사용자가 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 가리키도록 합니다.  새 설치 방식에서는 현재 위치 업그레이드에 비해 위험과 가동 중지 시간이 줄어들며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]으로 업그레이드할 때 하드웨어와 운영 체제도 함께 손쉽게 업그레이드할 수 있습니다.  
  
> [!NOTE]  
>  이미 HA(고가용성) 솔루션이 설치되어 있거나 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 환경이 실행 중인 경우에는 [롤링 업그레이드](#RollingUpgrade)를 진행합니다. 고가용성 솔루션이 없는 경우에는 임시로 [데이터베이스 미러링](http://msdn.microsoft.com/library/ms190941.aspx) 을 구성하여 가동 중지 시간을 더욱 최소화할 수 있습니다. 그럴 경우 이 업그레이드를 더 손쉽게 실행하거나 이 기회를 통해 영구 HA 솔루션으로 [Always On 가용성 그룹](http://msdn.microsoft.com/library/hh510260.aspx) 을 구성할 수 있습니다.  
  
 예를 들어 이 방식으로 다음을 업그레이드할 수 있습니다.  
  
-   지원되지 않는 운영 체제에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업그레이드  
  
-   [!INCLUDE[ss2016](../../includes/sssql15-md.md)] 이상에서 x86 설치를 지원하지 않으므로 SQL Server x86 설치 업그레이드  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 새 하드웨어 및/또는 새 운영 체제 버전으로 업그레이드  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업그레이드  
  
-   [!INCLUDE[ss2016](../../includes/sssql15-md.md)] 이상에서 SQL Server 2005 전체 업그레이드를 지원하지 않으므로 SQL Server 2005 업그레이드 - 자세한 내용은 [SQL Server 2005에서 업그레이드하나요?](../../database-engine/install-windows/are-you-upgrading-from-sql-server-2005.md)를 참조하세요.  
  
 새 설치 업그레이드에 필요한 단계는 연결된 스토리지를 사용하는 경우나 SAN 스토리지를 사용하는 경우에 따라 약간 달라집니다.  
  
-   **연결된 저장소 환경:** 연결된 저장소를 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경에서는 다음 다이어그램과 다이어그램 내의 링크를 통해 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 새 설치 업그레이드에 필요한 단계를 안내합니다.  
  
     ![연결된 저장소에 대한 백업 및 복원을 사용한 새 설치 업그레이드 방법](../../database-engine/install-windows/media/new-installation-upgrade-method-using-backup-and-restore-for-attached-storage.png "연결된 저장소에 대한 백업 및 복원을 사용한 새 설치 업그레이드 방법")  
  
-   **SAN 저장소 환경:** SAN 저장소를 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경에서는 다음 다이어그램과 다이어그램 내의 링크를 통해 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 새 설치 업그레이드에 필요한 단계를 안내합니다.  
  
     ![SAN 저장소에 대한 분리 및 연결을 사용한 새 설치 업그레이드 방법](../../database-engine/install-windows/media/new-installation-upgrade-method-using-detach-and-attach-for-san-storage.png "SAN 저장소에 대한 분리 및 연결을 사용한 새 설치 업그레이드 방법")  
  
##  <a name="RollingUpgrade"></a> 롤링 업그레이드  
 롤링 업그레이드는 가동 시간을 극대화하고 위험을 최소화하며 기능을 보존하기 위해 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 특정 순서로 업그레이드해야 하는 SQL Server 솔루션 환경에 필요합니다. 롤링 업그레이드는 업그레이드 프로젝트에서 하드웨어 및/또는 운영 체제를 더욱 쉽게 업그레이드하기 위해 각각의 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 현재 위치 업그레이드를 수행하거나 새 설치 업그레이드를 수행하여 기본적으로 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 특정 순서로 업그레이드하는 것입니다. 롤링 업그레이드 방식을 사용해야 하는 여러 시나리오가 있습니다. 이러한 방식에 대해서는 다음 문서에서 설명합니다.  
  
-   Always-On 가용성 그룹: 이 환경에서 롤링 업그레이드를 수행하는 자세한 단계는 [Always On 가용성 그룹 복제본 인스턴스 업그레이드](../../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)를 참조하세요.  
  
-   장애 조치 클러스터 인스턴스: 이 환경에서 롤링 업그레이드를 수행하는 자세한 단계는 [SQL Server 장애 조치(failover) 클러스터 인스턴스 업그레이드](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)를 참조하세요.  
  
-   미러링된 인스턴스: 이 환경에서 롤링 업그레이드를 수행하는 자세한 단계는 [미러된 인스턴스 업그레이드](../../database-engine/database-mirroring/upgrading-mirrored-instances.md)를 참조하세요.  
  
-   로그 전달 인스턴스: 이 환경에서 롤링 업그레이드를 수행하는 자세한 단계는 [SQL Server용 로그 전달 업그레이드&#40;Transact-SQL&#41;](../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)를 참조하세요.  
  
-   복제 환경: 이 환경에서 롤링 업그레이드를 수행하는 자세한 단계는 [복제된 데이터베이스 업그레이드](../../database-engine/install-windows/upgrade-replicated-databases.md)를 참조하세요.
  
-   SQL Server Reporting Services 확장 환경: 이 환경에서 롤링 업그레이드를 수행하는 자세한 단계는 [Reporting Services 업그레이드 및 마이그레이션](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)을 참조하세요.  
  
## <a name="next-steps"></a>다음 단계
 [Plan and Test the Database Engine Upgrade Plan](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)   
 [데이터베이스 엔진 업그레이드 완료](../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
  
