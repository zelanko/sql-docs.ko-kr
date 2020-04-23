---
title: 데이터베이스 엔진 업그레이드 계획 및 테스트 | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2018
ms.prod: sql
ms.technology: install
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 19c5b725-7400-4881-af8f-fd232ca28234
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 8deba047941509d294f6eb331fa610a453a71e82
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81529457"
---
# <a name="plan-and-test-the-database-engine-upgrade-plan"></a>데이터베이스 엔진 업그레이드 계획 및 테스트

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
 방법과 상관없이 성공적인 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 업그레이드를 수행하려면 적절한 계획이 필요합니다.  
  
## <a name="release-notes-and-known-upgrade-issues"></a>릴리스 정보 및 알려진 업그레이드 문제  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 업그레이드하기 전에 다음 항목을 검토하세요.

- [SQL Server 2017 릴리스 정보](../../sql-server/sql-server-2017-release-notes.md) 
- [SQL Server 2016 릴리스 정보](../../sql-server/sql-server-2016-release-notes.md) 
- [SQL Server 데이터베이스 엔진 이전 버전과의 호환성](../../database-engine/sql-server-database-engine-backward-compatibility.md) 문서.  
  
## <a name="pre-upgrade-planning-checklist"></a>사전 업그레이드 계획 검사 목록  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 업그레이드하기 전에 다음 검사 목록 및 연결된 문서를 검토하세요. 이러한 문서는 업그레이드 방법과 상관없이 모든 업그레이드에 적용되며 가장 적절한 업그레이드 방법을 결정하는 데 도움이 됩니다. 즉 롤링 업그레이드, 새 설치 업그레이드 또는 내부 업그레이드가 있습니다. 예를 들어 운영 체제를 업그레이드하거나 SQL Server 2005에서 업그레이드하거나 SQL Server의 32비트 버전에서 업그레이드하는 경우 내부 또는 롤링 업그레이드를 수행하지 못할 수 있습니다. 의사 결정 트리에 대해서는 [Choose a Database Engine Upgrade Method](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)을 참조하세요.  
  
-   **하드웨어 및 소프트웨어 요구 사항:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치를 위한 하드웨어 및 소프트웨어 요구 사항을 검토합니다. 이러한 요구 사항은 다음에서 확인할 수 있습니다. [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md). 업그레이드 계획 주기의 한 부분은 하드웨어 업그레이드(최신 하드웨어는 더 빠르며 프로세서 수가 적거나 데이터베이스와 서버의 통합으로 라이선스가 감소할 수 있음) 및 운영 체제 업그레이드를 고려하는 것입니다. 이러한 유형의 하드웨어 및 소프트웨어 변경은 선택하는 업그레이드 방법의 유형에 영향을 미칩니다.  
  
-   **현재 환경:** 현재 환경에서 사용 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소 및 사용자의 환경에 연결하는 클라이언트를 조사합니다.  
  
    -   **클라이언트 공급자:** 업그레이드가 필요하지 않지만 각 클라이언트에 대한 공급자를 업데이트해야 하는 경우 그렇게 하도록 선택할 수 있습니다. [!INCLUDE[sql14](../../includes/sssql14-md.md)] 이전 버전에서 업그레이드하는 경우 다음 [!INCLUDE[sql15](../../includes/sssql15-md.md)] 기능에서는 각 클라이언트의 업데이트된 공급자 또는 업데이트된 공급자가 추가 기능을 제공해야 합니다.  
  
       -   [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
       -   [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
       -   [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
       -   TLS 보안 업데이트  

   >[!NOTE]
   >앞의 목록은 [!INCLUDE[sscurrent](../../includes/sscurrent-md.md)]에도 적용됩니다.
  
-   **타사 구성 요소:** 통합된 백업 등과 같은 타사 구성 요소의 호환성을 확인합니다.  
  
-   **대상 환경:** 대상 환경이 하드웨어 및 소프트웨어 요구 사항을 충족하는지, 그리고 원래 시스템의 요구 사항을 지원할 수 있는지 확인합니다. 예를 들어 업그레이드 과정에서 여러 SQL Server 인스턴스를 새 단일 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 인스턴스로 통합하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경의 가상화를 프라이빗 또는 퍼블릭 클라우드에 통합해야 할 수 있습니다.  
  
-   **버전:** 업그레이드에 적절한 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]의 버전을 결정하고 업그레이드에 유효한 업그레이드 경로를 결정합니다. 자세한 내용은 [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)을 참조하십시오. 한 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 다른 버전으로 업그레이드하기 전에 현재 사용 중인 기능이 업그레이드할 버전에서 지원되는지 확인하세요.  
  
    > [!NOTE]  
    >  이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise edition에서 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]를 업그레이드하는 경우 엔터프라이즈 버전: 코어 기반 라이선스와 엔터프라이즈 버전 중에서 선택합니다. 이러한 엔터프라이즈 버전은 라이선스 모드와 관련해서만 다릅니다. 자세한 내용은 [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)를 참조하세요.  
  
-   **이전 버전과의 호환성:** [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 데이터베이스 엔진의 이전 버전과의 호환성 문서를 검토하여 업그레이드 중인 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 간의 동작 변화를 검토합니다. [SQL Server Database Engine Backward Compatibility](../../database-engine/sql-server-database-engine-backward-compatibility.md)을 참조하세요.  
  
-   **Data Migration Assistant:** Data Migration Assistant를 실행하여 업그레이드 프로세스를 방해하거나 주요 변경 내용으로 인해 기존 스크립트 또는 애플리케이션의 수정이 필요할 수 있는 문제를 진단하는 데 도움을 줍니다.
    [여기](https://aka.ms/get-dma)에서 Data Migration Assistant를 다운로드할 수 있습니다.  
  
-   **시스템 구성 검사기:** 업그레이드를 실제로 예약하기 전에 SQL Server 설치 프로그램이 차단 문제를 검색하는지 여부를 결정하려면 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] SCC(시스템 구성 검사기)를 실행합니다. 자세한 내용은 [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)을 참조하세요.  
  
-   **메모리 최적화 테이블 업그레이드:** 메모리 최적화 테이블이 포함된 SQL Server 2014 데이터베이스 인스턴스를 SQL Server 2016으로 업그레이드하는 경우 메모리 최적화 테이블을 새 디스크상 형식으로 업그레이드하기 위해 업그레이드 프로세스에 추가 시간이 필요하며 이 단계가 수행되는 동안 데이터베이스가 오프라인 상태가 됩니다.   시간의 양은 메모리 최적화 테이블의 크기 및 I/O 하위 시스템의 속도에 따라 달라집니다. 업그레이드를 위해 내부 및 새 설치 업그레이드의 경우 데이터 작업 크기 세 개가 필요합니다(롤링 업그레이드의 경우 1단계가 필요 없지만 2단계와 3단계는 필요함).  
  
    1.  이전의 디스크상 형식을 사용하여 데이터베이스 복구 실행(메모리 최적화 테이블을 디스크에서 메모리로 로드하는 작업이 포함됨)  
  
    2.  데이터를 새 디스크상 형식으로 디스크에 직렬화  
  
    3.  새로운 형식을 사용하여 데이터베이스 복구 실행(메모리 최적화 테이블을 디스크에서 메모리로 로드하는 작업이 포함됨)  
  
     또한 이 과정 중에 디스크의 공간이 부족하면 복구가 실패합니다. 현재 위치 업그레이드를 수행하거나 SQL Server 2014 데이터베이스를 SQL Server 2016 인스턴스에 연결하기 위해 데이터베이스의 MEMORY_OPTIMIZED_DATA 파일 그룹에 있는 컨테이너의 현재 크기와 동등한 기존 데이터베이스 및 추가 스토리지를 저장할 디스크 공간이 충분한지 확인합니다. 다음 쿼리를 사용하여 MEMORY_OPTIMIZED_DATA 파일 그룹에 현재 필요한 디스크 공간 및 이에 따라 업그레이드가 성공하기 위해 필요한 사용 가능한 디스크 공간의 크기를 확인합니다.  
  
    ```  
    select cast(sum(size) as float)*8/1024/1024 'size in GB'   
    from sys.database_files  
    where data_space_id in (select data_space_id from sys.filegroups where type=N'FX')  
    ```  
  
## <a name="develop-and-test-the-upgrade-plan"></a>업그레이드 계획 개발 및 테스트  
 업그레이드를 IT 프로젝트의 경우처럼 처리하는 것이 최선의 방법입니다. 데이터베이스 관리, 네트워크, 추출, 변환 및 로드(ETL), 그리고 업그레이드에 필요한 다른 기술을 가진 업그레이드 팀을 구성합니다. 팀이 수행해야 할 작업:  
  
-   **업그레이드 방법 선택:** [데이터베이스 엔진 업그레이드 방법 선택](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)을 참조하세요.  
  
-   **롤백 계획 수립:** 이 계획을 실행하면 롤백이 필요한 경우 원래 환경을 복원할 수 있습니다.  
  
-   **승인 기준 결정:** 사용자를 업그레이드된 환경으로 전환하기 전에 업그레이드가 성공했는지를 확인합니다.  
  
-   **업그레이드 계획 테스트:** 실제 작업을 사용하여 성능을 테스트하려면 Microsoft SQL Server Distributed Replay Utility를 사용합니다. 이 유틸리티를 사용하면 여러 컴퓨터를 사용해 추적 데이터를 재생하여 중요한 작업을 효율적으로 시뮬레이션할 수 있습니다. SQL Server 업그레이드 이전 및 이후에 테스트 서버에서 재생을 수행하면 성능 차이를 측정하고 업그레이드와의 애플리케이션 비호환성을 확인할 수 있습니다. 자세한 내용은 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md) 및 [관리 도구 명령줄 옵션&#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)을 참조하세요.  
  
## <a name="next-steps"></a>다음 단계  
[데이터베이스 엔진 업그레이드](../../database-engine/install-windows/upgrade-database-engine.md) 
  
## <a name="additional-resources"></a>추가 리소스 
[데이터베이스 마이그레이션 가이드](https://aka.ms/datamigration)  
