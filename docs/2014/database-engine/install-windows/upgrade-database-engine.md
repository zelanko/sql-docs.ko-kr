---
title: 데이터베이스 엔진 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84f032e89730aa9828dada1208c6d794db97260b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62774984"
---
# <a name="upgrade-database-engine"></a>데이터베이스 엔진 업그레이드
  이 항목에서는 업그레이드 프로세스를 준비하고 이해하는 데 필요한 다음과 같은 정보를 제공합니다.  
  
-   알려진 업그레이드 문제  
  
-   업그레이드 전 태스크 및 고려 사항  
  
-   
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]업그레이드 절차 항목에 대한 링크  
  
-   데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 마이그레이션하는 절차 항목에 대한 링크  
  
-   장애 조치(Failover) 클러스터에 대한 고려 사항  
  
-   업그레이드 후 태스크 및 고려 사항  
  
## <a name="known-upgrade-issues"></a>알려진 업그레이드 문제  
 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 업그레이드하기 전에 [SQL Server 데이터베이스 엔진의 이전 버전과의 호환성](../sql-server-database-engine-backward-compatibility.md)을 검토하세요. 지원되는 업그레이드 시나리오와 알려진 업그레이드 문제에 대한 자세한 내용은 [지원되는 버전 및 에디션 업그레이드](supported-version-and-edition-upgrades.md)를 참조하세요. 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소에 대한 이전 버전과의 호환성 정보는 [이전 버전과의 호환성](../../getting-started/backward-compatibility.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  한 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 다른 버전으로 업그레이드하기 전에 현재 사용 중인 기능이 업그레이드할 버전에서 지원되는지 확인하세요.  
  
> [!NOTE]  
>  이전 버전의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise Edition에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 업그레이드하는 경우 엔터프라이즈 버전: 코어 기반 라이선스와 엔터프라이즈 버전 중에서 선택합니다. 이러한 엔터프라이즈 버전은 라이선스 모드와 관련해서만 다릅니다. 자세한 내용은 [SQL Server의 버전별 계산 용량 제한](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)을 참조 하세요.  
  
## <a name="pre-upgrade-checklist"></a>업그레이드 전 검사 목록  
 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서의 업그레이드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 지원됩니다. 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 데이터베이스를 마이그레이션할 수도 있습니다. 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 같은 컴퓨터에 있는 다른 인스턴스로, 또는 다른 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 마이그레이션할 수 있습니다. 마이그레이션 옵션에는 데이터베이스 복사 마법사, 백업 및 복원 기능, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가져오기 및 내보내기 마법사, 대량 내보내기/대량 가져오기 방법의 사용이 포함됩니다.  
  
 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 업그레이드하기 전에 다음을 검토하세요.  
  
-   
  [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 검토합니다.  
  
-   
  [Check Parameters for the System Configuration Checker](check-parameters-for-the-system-configuration-checker.md)을 검토합니다.  
  
-   
  [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)을 검토합니다.  
  
-   
  [지원되는 버전 및 에디션 업그레이드](supported-version-and-edition-upgrades.md)를 검토합니다.  
  
-   
  [업그레이드 관리자를 사용하여 업그레이드 준비](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)를 검토합니다.  
  
-   
  [Distributed Replay Utility를 사용하여 업그레이드 준비](../../sql-server/install/use-the-distributed-replay-utility-to-prepare-for-upgrades.md)를 검토합니다.  
  
-   
  [SQL Server 데이터베이스 엔진의 이전 버전과의 호환성](../sql-server-database-engine-backward-compatibility.md)을 검토합니다.  
  
-   
  [쿼리 계획 마이그레이션](change-the-database-compatibility-mode-and-use-the-query-store.md)을 검토합니다.  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 업그레이드하기 전에 다음 사항을 검토하고 변경합니다.  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 MSX/TSX 관계에 나열되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 업그레이드할 때는 마스터 서버를 업그레이드하기 전에 대상 서버를 업그레이드합니다. 대상 서버 전에 마스터 서버를 업그레이드하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 마스터 인스턴스에 연결할 수 없습니다.  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 64비트 버전에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]64비트 버전으로 업그레이드하는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 을 업그레이드하기 전에 [!INCLUDE[ssDE](../../includes/ssde-md.md)]를 업그레이드해야 합니다.  
  
-   필요할 때 복원할 수 있도록 업그레이드할 인스턴스의 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 파일을 백업합니다.  
  
-   업그레이드할 데이터베이스에서 적절한 DBCC(데이터베이스 콘솔 명령)를 실행하여 데이터베이스가 일관된 상태를 유지하도록 합니다.  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소 및 사용자 데이터베이스 업그레이드에 필요한 디스크 공간을 예측합니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소에 필요한 디스크 공간은 [SQL Server 2014 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 참조하세요.  
  
-   기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터베이스(master, model, msdb 및 tempdb)가 자동 증가하도록 구성되어 있는지 확인하고 하드 디스크 공간이 충분한지 확인합니다.  
  
-   master 데이터베이스에 모든 데이터베이스 서버에 대한 로그온 정보가 있는지 확인합니다. 시스템 로그온 정보는 master 데이터베이스에 있으므로 이는 데이터베이스 복원을 위해 중요합니다.  
  
-   업그레이드 프로세스를 수행할 경우 업그레이드 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 서비스가 중지되었다가 시작되므로 모든 시작 저장 프로시저를 해제합니다. 시작 시 처리되는 저장 프로시저로 인해 업그레이드 프로세스가 중단될 수 있습니다.  
  
-   복제가 현재 상태인지 확인한 다음 복제를 중지합니다.  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 종속성을 갖는 모든 서비스를 포함한 모든 애플리케이션을 끝냅니다. 로컬 애플리케이션이 업그레이드 중인 인스턴스에 연결되어 있으면 업그레이드가 실패할 수 있습니다.  
  
-   데이터베이스 미러링을 사용하는 경우 [서버 인스턴스 업그레이드 시 미러된 데이터베이스의 작동 중단 최소화](../database-mirroring/upgrading-mirrored-instances.md)를 참조하세요.  
  
## <a name="upgrading-the-database-engine"></a>데이터베이스 엔진 업그레이드  
 버전 업그레이드로 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상을 덮어쓸 수 있습니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행할 때 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 검색되면 이전의 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로그램 파일이 업그레이드되고 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 저장된 모든 데이터는 그대로 보존됩니다. 또한 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서도 변경되지 않고 컴퓨터에 남아 있습니다.  
  
> [!WARNING]  
>  SQL Server 2014 설치 프로그램을 실행할 때에는 업그레이드 사전 검사가 실행되는 과정에서 SQL Server 인스턴스가 중지되었다가 다시 시작됩니다.  
  
> [!CAUTION]  
>  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 업그레이드하면 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 덮어쓰게 되므로 이러한 인스턴스는 시스템에 더 이상 존재하지 않게 됩니다. 따라서 업그레이드 전에 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 및 기타 개체를 백업하세요.  
  
 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 설치 마법사를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 업그레이드할 수 있습니다.  
  
### <a name="database-compatibility-level-after-upgrade"></a>업그레이드 후 데이터베이스 호환성 수준  
 업그레이드 후에 `tempdb`는, `model` `msdb` 및 **리소스** 데이터베이스의 호환성 수준이 120로 설정 됩니다. 
  `master` 시스템 데이터베이스는 업그레이드 이전의 호환성 수준으로 유지됩니다.  
  
 사용자 데이터베이스의 호환성 수준이 업그레이드 이전에 100 이상이었다면 업그레이드 후에도 동일하게 유지됩니다. 업그레이드 이전에 호환성 수준이 90이었다면 업그레이드된 데이터베이스에서는 호환성 수준이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지원되는 가장 낮은 호환성 수준인 100으로 설정됩니다.  
  
> [!NOTE]  
>  새 사용자 데이터베이스는 `model` 데이터베이스의 호환성 수준을 상속합니다.  
  
## <a name="migrating-databases"></a>데이터베이스 마이그레이션  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 백업 및 복원 기능이나 분리 및 연결 기능을 사용하여 사용자 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 이동할 수 있습니다. 자세한 내용은 [백업 및 복원으로 데이터베이스 복사](../../relational-databases/databases/copy-databases-with-backup-and-restore.md) 또는 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  원본 서버와 대상 서버에서 이름이 같은 데이터베이스는 이동하거나 복사할 수 없습니다. 이 경우 "이미 존재하는 것"으로 인식됩니다.  
  
 자세한 내용은 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)을 참조하세요.  
  
## <a name="after-upgrading-the-database-engine"></a>데이터베이스 엔진 업그레이드 후 수행할 작업  
 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 업그레이드한 후에 다음 태스크를 완료하세요.  
  
-   서버를 다시 등록합니다. 서버 등록에 대한 자세한 내용은 [서버 등록](../../ssms/register-servers/register-servers.md)을 참조하세요.  
  
-   쿼리 결과가 의미적으로 일관성이 유지되도록 하려면 전체 텍스트 카탈로그를 다시 작성합니다.  
  
     
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 는 전체 텍스트 및 의미 체계 검색에서 사용할 새로운 단어 분리기를 설치합니다. 단어 분리기는 인덱싱 및 쿼리 시에 모두 사용됩니다. 전체 텍스트 카탈로그를 다시 작성하지 않으면 검색 결과가 일관적이지 않을 수 있습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 단어 분리기와 현재 단어 분리기에서 다르게 분리되는 구를 찾는 전체 텍스트 쿼리를 실행하면 해당 구가 포함된 문서 또는 행이 검색되지 않을 수 있습니다. 그 이유는 인덱싱된 구가 현재 사용되는 쿼리와 다른 논리를 사용하여 분리되었기 때문입니다. 이를 해결하려면 인덱스 시 및 쿼리 시 동작이 동일하도록 새 단어 분리기를 사용하여 전체 텍스트 카탈로그를 다시 채우면(다시 작성하면) 됩니다.  
  
     자세한 내용은 [sp_fulltext_catalog&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql)를 참조하세요.  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치를 구성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 공격받을 수 있는 시스템의 노출 영역을 줄이기 위해 핵심 서비스와 기능을 선별적으로 설치하고 활성화합니다.  
  
-   
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 에서 생성되어 분할된 테이블 및 인덱스에 대한 쿼리에 적용되는 USE PLAN 힌트의 유효성을 검사하거나 이러한 힌트를 제거합니다.  
  
     
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 분할된 테이블 및 인덱스에 대한 쿼리의 처리 방법이 달라졌습니다. 
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 에서 생성된 계획에 USE PLAN 힌트를 사용하는 분할된 개체에 대한 쿼리에는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 사용할 수 없는 계획이 포함될 수 있습니다. 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드한 후 다음 절차를 수행하는 것이 좋습니다.  
  
     **USE PLAN 힌트가 쿼리에 직접 지정된 경우**  
  
    1.  쿼리에서 USE PLAN 힌트를 제거합니다.  
  
    2.  쿼리를 테스트합니다.  
  
    3.  최적화 프로그램에서 적절한 계획을 선택하지 못하는 경우 쿼리를 조정하고 원하는 쿼리 계획에서 USE PLAN 힌트를 지정하는 방법을 고려합니다.  
  
     **USE PLAN 힌트가 계획 지침에 지정된 경우**  
  
    1.  sys.fn_validate_plan_guide 함수를 사용하여 계획 지침의 유효성을 검사합니다. 또는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에서 Plan Guide Unsuccessful 이벤트를 사용하여 잘못된 계획이 있는지 확인할 수 있습니다.  
  
    2.  계획 지침이 올바르지 않으면 해당 계획 지침을 삭제합니다. 최적화 프로그램에서 적절한 계획을 선택하지 못하는 경우 쿼리를 조정하고 원하는 쿼리 계획에서 USE PLAN 힌트를 지정하는 방법을 고려합니다.  
  
     계획 지침에 USE PLAN 힌트가 지정된 경우 잘못된 계획 지침은 쿼리 실패를 유발하지 않습니다. 대신 USE PLAN 힌트를 사용하지 않은 채 쿼리가 컴파일됩니다.  
  
 업그레이드 전에 전체 텍스트 카탈로그가 설정 또는 해제된 것으로 표시된 데이터베이스는 업그레이드 후에도 해당 상태가 유지됩니다. 전체 텍스트 카탈로그가 설정된 데이터베이스의 경우 업그레이드 후에 전체 텍스트 카탈로그가 자동으로 다시 작성되고 채워집니다. 이 작업에는 시간과 리소스가 많이 소요됩니다. 전체 텍스트 인덱싱 작업을 일시적으로 중지하려면 다음 문을 실행합니다.  
  
```  
EXEC sp_fulltext_service 'pause_indexing', 1;  
```  
  
 전체 텍스트 인덱스 채우기를 재개하려면 다음 문을 실행합니다.  
  
```  
EXEC sp_fulltext_service 'pause_indexing', 0;  
```  
  
## <a name="see-also"></a>참고 항목  
 [지원되는 버전 및 에디션 업그레이드](supported-version-and-edition-upgrades.md)   
 [SQL Server의 여러 버전 및 인스턴스 작업](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)   
 [이전 버전과의 호환성](../../getting-started/backward-compatibility.md)   
 [복제된 데이터베이스 업그레이드](upgrade-replicated-databases.md)  
  
  
