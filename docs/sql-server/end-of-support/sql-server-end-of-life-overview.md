---
title: 지원 종료 옵션
description: SQL Server 2005, SQL Server 2008 및 SQL Server 2008 R2와 같이 지원 종료에 도달하는 SQL Server 제품에 사용할 수 있는 다양한 옵션에 대해 알아봅니다.
ms.date: 08/12/2020
ms.prod: sql
ms.technology: install
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: pmasl
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 378af311994d2aa478df0c673e0a1f0162d4dbfd
ms.sourcegitcommit: bf5acef60627f77883249bcec4c502b0205300a4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88200298"
---
# <a name="sql-server-end-of-support-options"></a>SQL Server 지원 종료 옵션 
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

이 문서에서는 지원 종료에 도달한 SQL Server 제품을 위한 옵션을 설명합니다.

## <a name="understanding-the-sql-server-lifecycle"></a>SQL Server 수명 주기 이해

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 각 버전은 최소 10년간 지원이 제공됩니다. 이 지원에는 5년간 일반 지원과 5년간 연장 지원이 포함됩니다.
-  **기본 지원**은 기능, 성능, 확장성 및 보안 업데이트를 포함합니다. 
-  **연장 지원**은 보안 업데이트만 포함합니다. 

**지원 종료**(종종 수명 종료라고도 함)는 제품이 수명 주기 끝에 도달하여 제품에 대한 서비스 및 지원을 더 이상 사용할 수 없음을 나타냅니다. Microsoft 수명 주기에 대한 자세한 내용은 [Microsoft 수명 주기 정책](https://support.microsoft.com/hub/4095338/microsoft-lifecycle-policy)을 참조하세요.



## <a name="options"></a>옵션

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 지원 종료 단계에 도달하면 다음 중에서 선택할 수 있습니다.
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 최신 버전으로 업그레이드합니다.
- [연장 보안 업데이트 구독](https://www.microsoft.com/cloud-platform/extended-security-updates)을 구매합니다. 
- [무료 연장 보안 업데이트](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)를 위해 워크로드를 Azure 가상 머신으로 현재 상태로 마이그레이션합니다.
- 워크로드를 [Azure SQL Database 서비스](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas)로 마이그레이션합니다. 

업그레이드 또는 마이그레이션을 계획하고 자동화하기 위한 자세한 정보, 지침 및 도구는 [SQL Server 2005 지원 종료](https://www.microsoft.com/sql-server/sql-server-2005) 및 [SQL Server 2008 지원 종료](https://www.microsoft.com/cloud-platform/windows-sql-server-2008)를 참조하세요.  

![지원 종료 옵션](media/sql-server-end-of-life-overview/sql-server-upgrade-paths.png)

이 문서에서는 각 접근 방식에 대한 이점 및 고려 사항을 설명하고 의사 결정 과정에 도움이 될 수 있는 추가 리소스를 제공합니다.

## <a name="upgrade-sql-server"></a>SQL Server 업그레이드

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지원 종료에 도달하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 최신 버전 및 지원되는 버전으로 업그레이드하도록 선택할 수 있습니다. 그러면 환경 일관성을 확보하고 최신 기능 집합을 사용할 수 있으며 새 버전의 지원 수명 주기를 적용할 수 있습니다.

### <a name="benefits"></a>이점
- **최신 기술**: 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에는 성능, 확장성 및 고가용성 기능이 포함된 혁신과 향상된 보안이 도입되었습니다. 
- **제어**: 하드웨어와 소프트웨어를 모두 관리하기 때문에 기능과 확장성을 최대한으로 제어할 수 있습니다.
- **친숙한 환경**: 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드하는 경우 환경이 가장 유사합니다.
- **광범위한 적용 가능성**: OLTP 시스템 및 데이터 웨어하우징을 포함하여 모든 종류의 데이터베이스 애플리케이션에 적용할 수 있습니다.
- **낮은 데이터베이스 애플리케이션 위험**: 레거시 시스템과 동일한 수준으로 데이터베이스 호환성을 유지하여 기존 데이터베이스 애플리케이션이 유해한 영향을 미칠 수 있는 기능 및 성능 변경으로부터 보호됩니다. 최신 데이터베이스 호환성 설정에 의해 제어되는 기능을 사용해야 하는 경우에만 애플리케이션을 완전히 다시 인증해야 합니다. 자세한 내용은 [호환성 인증](../../database-engine/install-windows/compatibility-certification.md)을 참조하세요.

### <a name="considerations"></a>고려 사항

- **비용**: 이 접근 방식은 가장 큰 선행 투자와 가장 지속적인 관리가 필요합니다. 자체 하드웨어 및 소프트웨어를 구입, 유지 관리 및 관리해야 합니다.
- **가동 중지 시간**: 업그레이드 전략에 따라 가동 중지 시간이 발생할 수 있습니다. 또한 내부 업그레이드 프로세스 중 문제가 발생할 수 있는 것은 본질적 위험입니다.
- **복잡성**: Windows Server 2008 또는 [!INCLUDE[winserver2008r2-md](../../includes/winserver2008r2-md.md)]의 경우 해당 Windows 버전에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 최신 버전이 지원되지 않을 수 있으므로 OS도 업그레이드해야 합니다. OS 업그레이드 프로세스에서 위험이 추가되므로 병렬 마이그레이션을 수행하는 것이 더 좋습니다. Windows Server 2008 또는 [!INCLUDE[winserver2008r2-md](../../includes/winserver2008r2-md.md)]용 장애 조치(failover) 클러스터 인스턴스에서는 내부 OS 업그레이드가 지원되지 않습니다. 

  > [!NOTE]
  > 클러스터 OS 롤링 업그레이드는 Windows Server 2016부터 사용할 수 있습니다.

### <a name="resources"></a>리소스

[설치 미디어](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-rtm)   
[설치 마법사를 사용하여 SQL Server 업그레이드](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

각 버전의 새로운 기능:
- [SQL Server 2016](../what-s-new-in-sql-server-2016.md)
- [SQL Server 2017](../what-s-new-in-sql-server-2017.md) 
- [SQL Server 2019](../what-s-new-in-sql-server-ver15.md)   

하드웨어 요구 사항:
- [SQL Server 2017 이전](../install/hardware-and-software-requirements-for-installing-sql-server.md)  
- [SQL Server 2019](../install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)    

지원되는 버전 및 에디션 업그레이드:
- [SQL Server 2016](../../database-engine/install-windows/supported-version-and-edition-upgrades.md?view=sql-server-2016&preserve-view=true) 
- [SQL Server 2017](../../database-engine/install-windows/supported-version-and-edition-upgrades-2017.md)
- [SQL Server 2019](../../database-engine/install-windows/supported-version-and-edition-upgrades-version-15.md)

도구:
-  [데이터베이스 실험 도우미](../../dea/database-experimentation-assistant-overview.md)는 대상 버전의[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 특정 워크로드를 평가하는 데 도움이 됩니다. 
-  [Data Migration Assistant](../../dma/dma-overview.md)는 새 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스 기능에 영향을 줄 수 있는 호환성 문제를 감지하는 데 도움이 됩니다. 
-  [쿼리 튜닝 길잡이](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)는 데이터베이스 호환성을 업그레이드할 때 부작용이 발생할 수 있는 작업을 튜닝하는 데 도움이 됩니다.

다음 이미지는 다양한 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 도입된 혁신의 예를 보여 줍니다. 

![25년간의 SQL Server 혁신](media/sql-server-end-of-life-overview/sql-server-version-improvements.png)

## <a name="extend-support"></a>지원 연장 

업그레이드할 준비가 되지 않고 클라우드로 이동할 준비가 되지 않은 경우 연장 보안 업데이트 구독을 구매하여 지원 종료 날짜 이후 최대 3년 동안 **중요** 보안 업데이트를 받을 수 있습니다.  

### <a name="benefits"></a>이점 

- **애플리케이션 지원**: 애플리케이션에서 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대해 재인증이 필요한 경우 이 옵션을 사용하는 것이 가장 좋습니다. 이는 [호환성 인증](../../database-engine/install-windows/compatibility-certification.md)을 사용하지 않는 애플리케이션에 일반적입니다. 
- **일관된 인프라**: 어떤 방식으로든 인프라를 변경할 필요가 없습니다. 
- **기술 지원**: Software Assurance나 다른 지원 플랜이 있는 경우 지원 종료 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품의 [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서 기술 지원을 계속 받을 수 있습니다. 이는 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]에 대한 지원을 받을 수 있는 유일한 방법입니다. 
- **Time**: 이 옵션은 3년 동안 사용할 수 있으며, 애플리케이션을 인증하기 위한 추가 시간을 제공합니다. 

### <a name="considerations"></a>고려 사항 

- **제한적 가용성**: 이 옵션은 Software Assurance 또는 구독 라이선스가 있는 고객만 사용할 수 있습니다. 
- **비용**: 연장 보안 업데이트는 매년 온-프레미스 라이선스 비용의 약 75%이므로 이 옵션을 사용하면 비용이 많이 들 수 있습니다.
- **제한된 시간 프레임**: 이 옵션은 3년 동안만 사용할 수 있으므로 보안 및 규정 준수를 보장하려면 3년 기간 만료 시 업그레이드 또는 마이그레이션해야 합니다.
- **버그 수정 없음**: 제품에 비보안 버그가 발생하는 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)]는 버그 수정을 릴리스하지 않습니다. 
- **제한적 지원**: 연장 보안 업데이트에는 새로운 기능, 기능 향상 또는 고객이 요청한 수정 사항이 포함되지 않습니다. 보안 수정 사항은 [Microsoft 보안 대응 센터(MSRC)](https://portal.msrc.microsoft.com/)에서 중요하다고 평가한 것으로 제한됩니다.

### <a name="resources"></a>리소스

[연장 보안 업데이트(ESU) 개요](sql-server-extended-security-updates.md)       
[자세한 ESU 질문과 대답](https://www.microsoft.com/cloud-platform/extended-security-updates)       
[Azure VM으로 현재 상태로 마이그레이션하여 무료로 지원 연장](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)       
[Software Assurance](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default)       

## <a name="azure-virtual-machine"></a>Azure Virtual Machine

또 다른 옵션은 [SQL Server를 실행하는 Azure 가상 머신](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)으로 워크로드를 마이그레이션하는 것입니다. 시스템을 현재 상태로 마이그레이션하고 지원 종료 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 유지하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 최신 버전으로 업그레이드할 수 있습니다. OS 수준 액세스가 필요한 마이그레이션 및 애플리케이션에 가장 적합합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가상 머신은 변경 내용을 최소화하거나 변경하지 않고 클라우드로 신속하게 마이그레이션해야 하는 기존 애플리케이션을 위한 리프트 앤 시프트가 준비되어 있습니다. 

### <a name="benefits"></a>이점

- **무료 연장 보안 업데이트**: [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 또는 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 현재 상태로 유지하도록 선택하는 경우 Software Assurance가 없어도 지원 종료 날짜 이후 3년 동안 연장 보안 업데이트를 무료로 사용할 수 있습니다. 
- **비용 절감**: 하드웨어 및 서버 소프트웨어 비용을 절감하고 시간당 사용량에 대해서만 비용을 지불합니다. 
- **리프트 앤 시프트**: 변경 내용을 최소화하거나 변경 없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 애플리케이션 인프라를 클라우드로 리프트 앤 시프트할 수 있습니다. 
- **호스팅 환경**: 하드웨어 및 소프트웨어 유지 관리 오프로딩과 같은 호스팅 환경의 이점을 얻을 수 있습니다. 
- **자동화**: [!INCLUDE[winserver2008r2-md](../../includes/winserver2008r2-md.md)] 이상에서는 자동화된 패치와 자동화된 백업의 이점을 얻을 수 있습니다. 
- **OS 제어**: 운영 체제 환경을 제어할 수 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 친숙한 기능 집합을 사용합니다. 
- **신속한 배포**: 가상 머신 이미지의 라이브러리에서 신속하게 배포할 수 있습니다. 
- **라이선스 이동**: 자체 라이선스를 사용할 수 있으므로 운영 비용을 절감할 수 있습니다. 
- **고가용성**: Azure 인프라에서 최대 99.99%까지 보장하는 기본 제공 가상 머신 가용성뿐만 아니라 장애 조치(failover) 클러스터 인스턴스 및 Always On 가용성 그룹 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고가용성 옵션을 활용할 수도 있습니다. 
- **낮은 데이터베이스 애플리케이션 위험**: 레거시 데이터베이스와 동일한 수준으로 데이터베이스 호환성을 유지하여 기존 데이터베이스 애플리케이션이 유해한 영향을 미칠 수 있는 기능 및 성능 변경으로부터 보호됩니다. 최신 데이터베이스 호환성 설정에 의해 제어되는 기능을 사용해야 하는 경우에만 애플리케이션을 완전히 다시 인증해야 합니다. 자세한 내용은 [호환성 인증](../../database-engine/install-windows/compatibility-certification.md)을 참조하세요.

### <a name="considerations"></a>고려 사항

- **관리 효율성**: 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 운영 체제 소프트웨어를 관리해야 합니다. 
- **네트워킹**: 사용자가 네트워킹 및 Active Directory 인프라와 통합되도록 가상 머신을 구성해야 합니다. 이로 인해 복잡성이 추가됩니다. 
- **공유 스토리지 FCI**: Azure 가상 머신은 스토리지 공간 다이렉트 또는 프리미엄 파일 공유를 사용하는 장애 조치(failover) 클러스터 인스턴스만 지원하며 공유 스토리지를 사용하는 장애 조치(failover) 클러스터 인스턴스는 지원하지 않습니다. 따라서 Azure 가상 머신은 Windows Server 2012 이상을 사용하는 경우에만 장애 조치(failover) 클러스터 인스턴스를 지원합니다.
- **확장성 가동 중지 시간**: CPU 및 스토리지 리소스를 변경하는 동안 가동 중지 시간이 발생합니다. 
- **크기 제한**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 필요한 만큼의 데이터베이스를 지원할 수 있지만, 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 모든 데이터베이스의 누적 합계는 온-프레미스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 524PB와 달리 최대 256TB입니다. 

### <a name="resources"></a>리소스

[SQL Server VM 개요](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)       
[Azure SQL 옵션 선택](/azure/sql-database/sql-database-paas-vs-sql-server-iaas)       
[SQL Server를 Azure VM으로 마이그레이션](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)       
[Azure로 현재 상태로 마이그레이션하기 위한 무료 연장 보안 업데이트(ESU)](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)       
[연장 보안 업데이트(ESU) 개요](sql-server-extended-security-updates.md)       
[자세한 ESU 질문과 대답](https://www.microsoft.com/cloud-platform/extended-security-updates)       
[SQL 가상 머신 자동화된 패치 적용](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)       
[SQL 가상 머신 자동화된 백업](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-backup-v2)       
[SQL 가상 머신 고가용성](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr)       
[SQL 가상 머신 질문과 대답](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-faq)       

## <a name="azure-sql-database-single-database"></a>Azure SQL Database 단일 데이터베이스

유지 관리를 오프로드하고, 비용을 절감하고, 향후 업그레이드를 걱정하지 않으려면 워크로드를 [Azure SQL Database 단일 데이터베이스](/azure/sql-database/sql-database-single-database)로 이동할 수 있습니다. 이 옵션은 개발 및 마케팅에서 시간 제약 조건이 있고 안정적인 최신 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 기능을 사용하려는 최신 클라우드 애플리케이션에 가장 적합합니다. 

### <a name="benefits"></a>이점

- **비용**: 단일 데이터베이스는 하드웨어, 소프트웨어 및 유지 관리가 오프로드되고 초당 또는 시간당 사용량에 대해 비용을 지불할 수 있으므로 비용 효율적일 수 있습니다. 
- **유연성**: 단일 데이터베이스는 개발자 생산성과 신속한 솔루션 출시가 중요하거나 외부 액세스가 필요한 클라우드용 애플리케이션에 특히 적합합니다.  
- **일반 기능**: 흔히 사용되는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 기능을 사용할 수 있지만 SQL Managed Instance만큼 많지는 않습니다.  
- **신속한 배포**: 단일 데이터베이스를 신속하게 배포할 수 있습니다. 
- **확장성**: 비즈니스 필요에 따라 빠르고 쉽게 확장 및 축소할 수 있어 추가로 비용 절감 혜택을 제공합니다. 
- **가용성**: 서비스 비용은 스토리지 및 고가용성(99.995% 가용성을 보장)을 모두 포함합니다.  
- **자동화**: 패치 적용 및 백업이 자동으로 이루어지므로 소중한 유지 관리 시간을 절약할 수 있습니다.  
- **Intelligent Insights**: 기본 제공 인텔리전스 분석을 사용하여 데이터베이스의 성능에 대한 인사이트를 얻습니다.  
- **무버전**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 항상 최신 버전으로 설정되어 있으므로 업그레이드 또는 가동 중지 시간을 걱정하지 않아도 됩니다. 또한 항상 최신, 최고의 기능을 제공하고 있으며, 안정적인 최신 기능을 먼저 클라우드로 출시하고 있습니다.
- **낮은 데이터베이스 애플리케이션 위험**: 온-프레미스 시스템과 동일한 수준으로 데이터베이스 호환성을 유지하여 기존 애플리케이션이 유해한 영향을 미칠 수 있는 기능 및 성능 변경으로부터 보호됩니다. 최신 데이터베이스 호환성 설정에 의해 제어되는 기능을 사용해야 하는 경우에만 애플리케이션을 완전히 다시 인증해야 합니다. 자세한 내용은 [호환성 인증](../../database-engine/install-windows/compatibility-certification.md)을 참조하세요.

### <a name="considerations"></a>고려 사항

- **제한된 마이그레이션 옵션**:  전체 인스턴스가 아니라 한 번에 하나의 데이터베이스만 마이그레이션할 수 있습니다.   
- **기능 제한**:  가장 일반적으로 사용되는 Azure SQL Database 기능을 사용할 수 있지만 단일 데이터베이스의 기능 집합은 Azure SQL Managed Instance 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]만큼 완벽하지 않습니다. 
- **Transact-SQL 차이점**:  단일 데이터베이스와 온-프레미스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 간에는 몇 가지 [!INCLUDE[tsql](../../includes/tsql-md.md)](T-SQL) 차이가 있습니다. 
- **크기 제한**:  단일 데이터베이스의 최대 데이터베이스 크기는 100TB로, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 524PB와는 차이가 있습니다. 
- **유지 관리 시간**: 거의 투명하기는 하지만 정확한 유지 관리 시간에 대한 보장은 없습니다. 

### <a name="resources"></a>리소스

[Azure SQL Database 개요](/azure/sql-database/sql-database-technical-overview)       
[Azure SQL 옵션 선택](/azure/sql-database/sql-database-paas-vs-sql-server-iaas)       
[SQL Database 기능 비교](/azure/sql-database/sql-database-features)       
[SQL Server를 단일 데이터베이스로 마이그레이션](/azure/sql-database/sql-database-single-database-migrate)       
[광범위한 마이그레이션 프로세스](/azure/cloud-adoption-framework/migrate/expanded-scope/sql-migration)       
[단일 데이터베이스 T-SQL 차이점](/azure/sql-database/sql-database-transact-sql-information)       
[vCore](/azure/sql-database/sql-database-vcore-resource-limits-single-databases) 및 [DTU](/azure/sql-database/sql-database-dtu-resource-limits-single-databases) 리소스 제한       
[Intelligent Insights](/azure/sql-database/sql-database-intelligent-insights)       

도구:
- [데이터 Migration Assistant](../../dma/dma-overview.md)
- [Database Migration Service](/azure/dms/dms-overview)

## <a name="sql-managed-instance"></a>SQL Managed Instance

유지 관리 오프로딩과 비용을 활용하고 싶지만 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 단일 데이터베이스의 기능 집합이 너무 제한적이라면 [SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)로 이동할 수 있습니다. 관리되는 인스턴스는 온-프레미스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 매우 비슷하지만 하드웨어 오류 또는 패치 적용 등은 걱정할 필요가 없습니다. Managed Instance는 공유 리소스 집합을 사용하는 시스템 및 사용자 데이터베이스 컬렉션으로, 리프트 앤 시프트가 준비되어 대부분의 클라우드 마이그레이션에 사용할 수 있습니다. 이 옵션은 최소한의 변경으로 클라우드 마이그레이션이 가능하고 안정적인 최신 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 기능을 사용하려는 새 애플리케이션 또는 기존 온-프레미스 애플리케이션에 가장 적합합니다. 

### <a name="benefits"></a>이점

- **비용**: 소프트웨어 및 하드웨어 유지 관리를 오프로드하여 비용을 절감할 수 있습니다.  
- **리프트 앤 시프트**: 최소한의 데이터베이스 변경으로 또는 전혀 변경 없이 모든 데이터베이스를 포함하여 전체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온-프레미스 인스턴스를 관리되는 인스턴스로 리프트 앤 시프트할 수 있습니다. 
- **기능**: 관리되는 인스턴스의 기능 집합은 데이터베이스 간 쿼리, 트랜잭션 복제 게시 및 배포, SQL 작업 예약, CLR 지원 등 온-프레미스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 거의 일치합니다. 
- **확장성**: 관리되는 인스턴스 내의 모든 데이터베이스는 리소스를 공유하며 가동 중지 시간 없이 언제든지 규모를 확장 및 축소할 수 있습니다.   
- **자동화**: 패치 적용 및 백업이 자동으로 이루어지므로 소중한 유지 관리 시간을 절약할 수 있습니다.  
- **가용성**: 서비스 비용은 스토리지 및 고가용성(99.99% 가용성을 보장)을 모두 포함합니다.  
- **Intelligent Insights**: 기본 제공 인텔리전스 분석을 사용하여 데이터베이스의 성능에 대한 인사이트를 얻습니다.  
- **무버전**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 항상 최신 버전으로 설정되어 있으므로 업그레이드 또는 가동 중지 시간을 걱정하지 않아도 됩니다. 또한 항상 최신, 최고의 기능을 제공하고 있으며, 안정적인 최신 기능을 먼저 클라우드로 출시하고 있습니다.
- **낮은 데이터베이스 애플리케이션 위험**: 온-프레미스 데이터베이스와 동일한 수준으로 데이터베이스 호환성을 유지하여 기존 데이터베이스 애플리케이션이 유해한 영향을 미칠 수 있는 기능 및 성능 변경으로부터 보호됩니다. 최신 데이터베이스 호환성 설정에 의해 제어되는 기능을 사용해야 하는 경우에만 애플리케이션을 완전히 다시 인증해야 합니다. 자세한 내용은 [호환성 인증](../../database-engine/install-windows/compatibility-certification.md)을 참조하세요.

### <a name="considerations"></a>고려 사항

- **비용**: 관리되는 인스턴스 옵션은 단일 데이터베이스 옵션보다 비용이 더 많이 들 수 있습니다.  
- **Transact-SQL 차이점**: 단일 데이터베이스와 온-프레미스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 간에는 몇 가지 [!INCLUDE[tsql](../../includes/tsql-md.md)](T-SQL) 차이가 있습니다.  
- **배포**:  관리되는 인스턴스를 배포하는 데는 단일 데이터베이스보다 시간이 더 걸릴 수 있습니다.  
- **기능 제한**: 관리되는 인스턴스는 대부분의 기능을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 공유하지만 아직 지원되지 않는 기능이 일부 있습니다. 
- **크기 제한**: 관리되는 인스턴스 내의 모든 데이터베이스에 대한 결합된 스토리지 크기는 온-프레미스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 524PB와 달리 8TB로 제한됩니다.  
- **네트워킹**: 관리되는 인스턴스의 네트워킹 요구 사항은 인프라에 복잡한 계층을 추가하며 Azure ExpressRoute 또는 VPN Gateway가 필요합니다.
- **유지 관리 시간**: 거의 투명하기는 하지만 정확한 유지 관리 시간에 대한 보장은 없습니다. 

### <a name="resources"></a>리소스

[SQL Managed Instance 개요](/azure/sql-database/sql-database-managed-instance)       
[Azure SQL 옵션 선택](/azure/sql-database/sql-database-paas-vs-sql-server-iaas)       
[SQL Database 기능 비교](/azure/sql-database/sql-database-features)       
[SQL Server를 Azure SQL Managed Instance로 마이그레이션](/azure/sql-database/sql-database-managed-instance-migrate)       
[광범위한 마이그레이션 프로세스](/azure/cloud-adoption-framework/migrate/expanded-scope/sql-migration)       

도구:
- [데이터 Migration Assistant](../../dma/dma-overview.md)
- [Database Migration Service](/azure/dms/dms-overview)

## <a name="non-sql-options"></a>SQL 이외의 옵션

특정 유형의 애플리케이션의 경우 Azure Cosmos DB 또는 Azure 테이블 스토리지와 같은 비관계형 또는 NoSQL 솔루션을 고려할 수도 있습니다.

### <a name="azure-cosmos-db"></a>Azure Cosmos DB

JSON 데이터를 사용하고 강력한 쿼리와 트랜잭션 데이터 처리를 함께 필요로 하는 확장 가능한 최신 모바일 및 웹 애플리케이션의 경우 Azure Cosmos DB를 고려합니다. 자세한 내용은 [Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)를 참조하세요. 데이터 가져오기에 대한 자세한 내용은 [Cosmos DB에 데이터 가져오기](https://docs.microsoft.com/azure/cosmos-db/import-data/)를 참조하세요.

Azure Cosmos DB는 다음과 같은 이점이 있습니다.
- 문서는 인덱싱되며 익숙한 SQL 구문을 사용하여 문서를 쿼리할 수 있습니다.
- 데이터베이스는 스키마 없는 데이터베이스입니다.
- 인덱스를 다시 작성하지 않고도 문서에 속성을 추가할 수 있습니다.
- 데이터베이스 엔진 내에서 직접 JSON 및 JavaScript 지원을 이용합니다.
- Azure 검색, HDInsight, Data Factory 등 다른 Azure 서비스와의 통합 및 지리 공간적 데이터에 대한 기본 지원을 이용합니다.
- 예약된 처리량 수준을 통해 대기 시간이 짧은 고성능 스토리지를 사용합니다.

### <a name="azure-table-storage"></a>Azure 테이블 스토리지

비용 효율적인 솔루션에서 페타바이트 규모의 반구조적 데이터를 저장하려면 Azure 테이블 스토리지를 고려합니다. 자세한 내용은 [테이블 스토리지](https://azure.microsoft.com/services/storage/tables/)를 참조하세요.

Azure 테이블 스토리지에는 다음과 같은 이점이 있습니다.
- 데이터를 오프라인으로 전환하지 않고도 앱과 테이블 스키마를 개발할 수 있습니다.
- 데이터 세트를 분할하지 않고도 확장할 수 있습니다.
- 여러 지역에 걸쳐 데이터를 복제하는 지역 중복 스토리지를 사용합니다.

## <a name="lifecycle-dates"></a>수명 주기 날짜

다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 수명 주기 날짜(대략적)를 제공합니다. 자세한 내용은 [Microsoft 수명 주기 정책](https://support.microsoft.com/hub/4095338/microsoft-lifecycle-policy) 페이지를 참조하세요. 

| **버전**     | **릴리스 연도** | **일반 지원 종료 날짜** | **연장 지원 종료 날짜** |
| :---------------| :--------------- | :------------------------------ | :---------------------------- |
| [SQL Server 2019](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202019) | 2019 | 2025 | 2030 |
| [SQL Server 2017](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017) | 2017 | 2022 | 2027 |
| [SQL Server 2016](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202016) | 2016 | 2021 | 2026 |
| [SQL Server 2014](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202014) | 2014 | 2019 | 2024 |
| [SQL Server 2012](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202012) | 2012 | 2017 | 2022 |
| [SQL Server 2008 R2](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202008%20R2) | 2010 | 2012 | [2019](https://www.microsoft.com/sql-server/sql-server-2008) |
| [SQL Server 2008](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202008) | 2008 | 2012 | [2019](https://www.microsoft.com/sql-server/sql-server-2008) |
| [SQL Server 2005](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202005) | 2006 | 2011 | [2016](https://www.microsoft.com/sql-server/sql-server-2005) |
| [SQL Server 2000](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202000) | 2000 | 2005 | [2013](https://blogs.technet.microsoft.com/cdnitmanagers/2012/12/06/sql-server-2000-end-of-support-april-2013/) |

> [!IMPORTANT]
> 이 표는 대략적 참조이며 표 내용과 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 수명 주기 페이지 사이에 차이가 있는 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 수명 주기를 우선적으로 참조하세요.  

## <a name="next-steps"></a>다음 단계  
[SQL Server 2019](https://www.microsoft.com/sql-server/sql-server-2019)   
[SQL Server 2005 지원 종료](https://www.microsoft.com/sql-server/sql-server-2005)   
[SQL Server 2008 지원 종료](https://www.microsoft.com/cloud-platform/windows-sql-server-2008)   
[연장 보안 업데이트(ESU) 개요](sql-server-extended-security-updates.md)   
[Azure로 현재 상태로 마이그레이션하기 위한 무료 연장 보안 업데이트(ESU)](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)   
[SQL Server VM 개요](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)   
[Azure SQL Database 개요](/azure/sql-database/sql-database-technical-overview)    

