---
title: "데이터베이스 엔진 업그레이드 계획 및 테스트 | Microsoft Docs"
ms.custom: ""
ms.date: "01/20/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 19c5b725-7400-4881-af8f-fd232ca28234
caps.latest.revision: 16
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 16
---
# 데이터베이스 엔진 업그레이드 계획 및 테스트
  방법과 상관없이 성공적인 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업그레이드를 수행하려면 적절한 계획이 필요합니다.  
  
## 릴리스 정보 및 알려진 업그레이드 문제  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 업그레이드하기 전에 [SQL Server 2016 릴리스 정보](../../sql-server/sql-server-2016-release-notes.md) 및 [SQL Server 데이터베이스 엔진의 이전 버전과의 호환성](../../database-engine/sql-server-database-engine-backward-compatibility.md) 항목을 검토하세요.  
  
## 업그레이드 전 검사 목록 계획  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 업그레이드하기 전에 다음 검사 목록 및 연결된 항목을 검토하세요. 이러한 항목은 업그레이드 방법과 상관없이 모든 업그레이드에 적용되며 가장 적절한 업그레이드 방법: 즉, 롤링 업그레이드, 새 설치 업그레이드 또는 내부 업그레이드를 결정하는 데 도움이 됩니다. 예를 들어 운영 체제를 업그레이드하거나 SQL Server 2005에서 업그레이드하거나 SQL Server의 32비트 버전에서 업그레이드하는 경우 내부 또는 롤링 업그레이드를 수행하지 못할 수 있습니다. 의사 결정 트리에 대해서는 [Choose a Database Engine Upgrade Method](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)을 참조하세요.  
  
-   **하드웨어 및 소프트웨어 요구 사항:** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 설치하기 위한 하드웨어 및 소프트웨어 요구 사항을 검토하세요. 이러한 요구 사항을 확인할 수 있는 위치: [Hardware and Software Requirements for Installing SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md). 업그레이드 계획 주기의 한 부분은 하드웨어 업그레이드(최신 하드웨어는 더 빠르며 프로세서 수가 적거나 데이터베이스와 서버의 통합으로 라이선스가 감소할 수 있음) 및 운영 체제 업그레이드를 고려하는 것입니다. 이러한 유형의 하드웨어 및 소프트웨어 변경은 선택하는 업그레이드 방법의 유형에 영향을 미칩니다.  
  
-   **현재 환경:** 사용 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소 및 사용자의 환경에 연결하는 클라이언트를 조사합니다.  
  
    -   **클라이언트 공급자:** 업그레이드가 필요하지 않지만 각 클라이언트에 대한 공급자를 업데이트해야 하는 경우 그렇게 하도록 선택할 수 있습니다. 다음 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기능을 사용하려면 각 클라이언트에 대해 업데이트된 공급자가 필요하거나 업데이트된 공급자가 추가 기능을 제공해야 합니다.  
  
        -   [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
        -   [스트레치 데이터베이스](../../sql-server/stretch-database/stretch-database.md)  
  
        -   [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치(failover)&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/listeners, client connectivity, application failover.md)  
  
        -   SSL 보안 업데이트  
  
    -   **타사 구성 요소:** 통합된 백업 등과 같은 타사 구성 요소의 호환성을 확인합니다.  
  
-   **대상 환경:** 대상 환경이 하드웨어 및 소프트웨어 요구 사항을 충족하는지, 그리고 원래 시스템의 요구 사항을 지원할 수 있는지 확인합니다. 예를 들어 업그레이드 과정에서 여러 SQL Server 인스턴스를 새 단일 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스로 통합하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경의 가상화를 개인 또는 공용 클라우드에 통합해야 할 수 있습니다.  
  
-   **버전:** 업그레이드에 적절한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 의 버전을 결정하고 업그레이드에 유효한 업그레이드 경로를 결정합니다. 자세한 내용은 [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)을 참조하십시오. 한 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 다른 버전으로 업그레이드하기 전에 현재 사용 중인 기능이 업그레이드할 버전에서 지원되는지 확인하세요.  
  
    > [!NOTE]  
    >  이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드하는 경우 엔터프라이즈 버전: 코어 기반 라이선스와 엔터프라이즈 버전 중에서 선택합니다. 이러한 엔터프라이즈 버전은 라이선스 모드와 관련해서만 다릅니다. 자세한 내용은 [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)을 참조하세요.  
  
-   **이전 버전과의 호환성:** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 데이터베이스 엔진의 이전 버전과의 호환성 항목을 검토하여 업그레이드 중인 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 간의 동작 변화를 검토합니다. [SQL Server Database Engine Backward Compatibility](../../database-engine/sql-server-database-engine-backward-compatibility.md)을 참조하세요.  
  
-   **업그레이드 관리자:**  업그레이드 프로세스를 방해하거나 주요 변경 내용 때문에 기존 스크립트 또는 응용 프로그램의 수정이 필요할 수 있는 문제를 진단하는 데 도움을 얻으려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업그레이드 관리자를 실행합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 은 고객이 기존 시스템의 업그레이드를 준비하도록 도와 주는 업그레이드 관리자의 새 버전을 포함하고 있습니다.  또한 이 도구는 기존 데이터베이스를 검사하여 업그레이드가 완료된 후 스트레치 테이블과 같은 새 기능을 이용할 수 있는지 확인할 수 있는 기능도 포함하고 있습니다.   
    [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]업그레이드 관리자  [여기](https://www.microsoft.com/en-us/download/details.aspx?id=48119)서 다운로드할 수 있습니다.  
  
-   **시스템 구성 검사기:** 업그레이드를 실제로 예약하기 전에 SQL Server 설치 프로그램이 차단 문제를 검색하는지 여부를 결정하려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SCC(시스템 구성 검사기)를 실행합니다. 자세한 내용은 [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)을 참조하세요.  
  
-   **메모리 액세스에 최적화된 테이블 업그레이드:** 메모리 액세스에 최적화된 테이블이 포함된 SQL Server 2014 데이터베이스 인스턴스를 SQL Server 2016으로 업그레이드하는 경우 메모리 액세스에 최적화된 테이블을 새 디스크상 형식으로 업그레이드하기 위해 업그레이드 프로세스에 추가 시간이 필요하며 이 단계가 수행되는 동안 데이터베이스가 오프라인 상태가 됩니다.   시간의 양은 메모리 액세스에 최적화된 테이블의 크기 및 I/O 하위 시스템의 속도에 따라 달라집니다. 업그레이드를 위해 내부 및 새 설치 업그레이드의 경우 데이터 작업 크기 세 개가 필요합니다(롤링 업그레이드의 경우 1단계가 필요 없지만 2단계와 3단계는 필요함).  
  
    1.  이전의 디스크상 형식을 사용하여 데이터베이스 복구 실행(메모리 액세스에 최적화된 테이블을 디스크에서 메모리로 로드하는 작업이 포함됨)  
  
    2.  데이터를 새 디스크상 형식으로 디스크에 직렬화  
  
    3.  새 형식을 사용하여 데이터베이스 복구 실행(메모리 액세스에 최적화된 테이블을 디스크에서 메모리로 로드하는 작업이 포함됨)  
  
     또한 이 과정 중에 디스크의 공간이 부족하면 복구가 실패합니다. 내부 업그레이드를 수행하기 위해 또는 SQL Server 2014 데이터베이스를 SQL Server 2016 인스턴스에 연결하는 경우 데이터베이스의 MEMORY_OPTIMIZED_DATA 파일 그룹에 있는 컨테이너의 현재 크기와 같은 추가 공간에 기존 데이터베이스를 저장할 공간을 더한 충분한 공간이 디스크에 있는지 확인합니다. 다음 쿼리를 사용하여 MEMORY_OPTIMIZED_DATA 파일 그룹에 현재 필요한 디스크 공간 및 그에 따라 업그레이드가 성공하는 데 필요한 사용 가능 디스크 공간의 양을 결정합니다.  
  
    ```  
    select cast(sum(size) as float)*8/1024/1024 'size in GB'   
    from sys.database_files  
    where data_space_id in (select data_space_id from sys.filegroups where type=N'FX')  
    ```  
  
## 업그레이드 계획 개발 및 테스트  
 업그레이드를 IT 프로젝트의 경우처럼 처리하는 것이 최선의 방법입니다. 데이터베이스 관리, 네트워크, 추출, 변환 및 로드(ETL), 그리고 업그레이드에 필요한 다른 기술을 가진 업그레이드 팀을 구성해야 합니다. 팀이 수행해야 할 작업:  
  
-   **업그레이드 방법 선택:** [데이터베이스 엔진 업그레이드 방법 선택](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)을 참조하세요.  
  
-   **롤백 계획 수립:**. 이 계획을 실행하면 롤백이 필요한 경우 원래 환경을 복원할 수 있습니다.  
  
-   **승인 기준 결정:** 사용자를 업그레이드된 환경으로 전환하기 전에 업그레이드가 성공적인지 알아야 합니다.  
  
-   **업그레이드 계획 테스트:** 실제 작업을 사용하여 성능을 테스트하려면 Microsoft SQL Server Distributed Replay Utility를 사용합니다. 이 유틸리티를 사용하면 여러 컴퓨터를 사용해 추적 데이터를 재생하여 중요한 작업을 효율적으로 시뮬레이션할 수 있습니다. SQL Server 업그레이드 이전 및 이후에 테스트 서버에서 재생을 수행하면 성능 차이를 측정하고 업그레이드와의 응용 프로그램 비호환성을 확인할 수 있습니다. 자세한 내용은 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md) 및 [관리 도구 명령줄 옵션&#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)을 참조하세요.  
  
## 이 문서가 도움이 되었나요? 여러분의 의견을 환영합니다.  
 어떤 정보를 찾고 계세요? 정보를 찾으셨나요? 여러분의 의견은 문서의 내용을 개선하는 데 많은 도움이 됩니다. 의견이 있으면 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Plan%20and%20Test%20the%20Database%20Engine%20Upgrade%20Plan%20page)으로 보내 주세요.  
  
## 참고 항목  
 [데이터베이스 엔진 업그레이드](../../database-engine/install-windows/upgrade-database-engine.md)  
  
  