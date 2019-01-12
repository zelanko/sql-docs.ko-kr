---
title: 일반적인 복제 성능 향상 | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- designing databases [SQL Server], replication performance
- Snapshot Agent, performance
- snapshots [SQL Server replication], performance considerations
- merge replication performance [SQL Server replication]
- snapshot replication [SQL Server], performance
- subscriptions [SQL Server replication], performance considerations
- agents [SQL Server replication], performance
- performance [SQL Server replication], general considerations
- transactional replication, performance
ms.assetid: 895b1ad7-ffb9-4a5c-bda6-e1dfbd56d9bf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 71bd15f01cc69371765c4af17fb184ce28481f65
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129283"
---
# <a name="enhance-general-replication-performance"></a>일반적인 복제 성능 향상
  이 항목에서 설명하는 지침을 따르면 애플리케이션 및 네트워크에서 모든 복제 유형의 일반적인 성능을 향상시킬 수 있습니다.  
  
## <a name="server-and-network"></a>서버 및 네트워크  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]에 할당될 최소 및 최대 메모리 양을 설정합니다.  
  
     기본적으로 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 은 사용할 수 있는 시스템 리소스에 따라 메모리 요구 사항을 동적으로 변경합니다. 복제 작업 중 사용 가능한 메모리의 부족을 방지하기 위해 **min server memory** 옵션을 사용해서 사용 가능한 최소 메모리를 설정합니다. 메모리를 확보하기 위해 운영 체제가 디스크로 페이징하지 않도록 하기 위해 **max server memory** 옵션을 사용하여 최대 메모리를 설정할 수도 있습니다. 자세한 내용은 [서버 메모리 서버 구성 옵션](../../../database-engine/configure-windows/server-memory-server-configuration-options.md)을 참조하세요.  
  
-   데이터베이스 데이터 파일 및 로그 파일이 적절히 할당되도록 합니다. 복제와 관련된 모든 데이터베이스의 트랜잭션 로그에 별도의 디스크 드라이브를 사용합니다.  
  
     데이터베이스를 저장하는 데 사용한 디스크 드라이브가 아닌 별개의 디스크 드라이브에 로그 파일을 기록해서 트랜잭션을 기록하는 데 필요한 시간을 줄일 수 있습니다. 내결함성이 필요하다면 RAID(Redundant Array of Inexpensive Disks)-1을 사용하여 이 드라이브를 미러링할 수 있습니다. 다른 데이터베이스 파일에 대해서는 내결함성에 대한 필요에 따라 RAID 0 또는 0+1을 사용합니다. 이는 복제가 사용 중인지 여부에 상관없이 일반적으로 사용됩니다.  
  
-   복제에 사용하는 서버, 특히 배포자에 메모리를 추가해 봅니다.  
  
-   다중 프로세서 컴퓨터를 사용합니다.  
  
     서버에 프로세서를 추가하면 복제 에이전트의 성능이 향상됩니다. CPU 사용량이 높은 경우 보다 빠른 CPU 하나를 설치하거나 CPU를 여러 개 설치해 봅니다.  
  
-   빠른 네트워크를 사용합니다.  
  
     트랜잭션 복제의 경우 특히 네트워크로 인해 심각한 성능 병목 상태가 발생할 수 있습니다. 100Mbps 이상의 빠른 네트워크를 사용하여 변경 내용을 구독자로 전파하는 기능을 크게 향상시킬 수 있습니다. 네트워크 속도가 느린 경우 네트워크 설정 및 에이전트 매개 변수를 적절히 지정합니다.  
  
## <a name="database-design"></a>데이터베이스 디자인  
  
-   최상의 데이터베이스 디자인 방법을 따릅니다.  
  
     일반적으로 복제된 데이터베이스에 대한 성능 최적화의 영향은 복제되지 않은 데이터베이스에 대한 성능 최적화의 영향과 거의 동일합니다. 그러나 구독자에서 인덱스를 사용할 때는 주의해야 합니다. 구독자의 기본 키 열을 인덱싱해야 하지만 추가 인덱스가 삽입, 업데이트 및 삭제 성능에 영향을 줄 수 있습니다.  
  
-   READ_COMMITTED_SNAPSHOT 데이터베이스 옵션을 설정해 봅니다.  
  
     사용자 작업과 복제 에이전트 작업 간 경합을 줄이려면 게시 및 구독 데이터베이스에 대해 이 옵션을 설정하십시오.  
  
    ```  
    ALTER DATABASE AdventureWorks  
    SET READ_COMMITTED_SNAPSHOT ON  
    ```  
  
     자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)를 참조하세요.  
  
-   트리거의 애플리케이션 논리에 유의합니다.  
  
     구독자의 사용자 정의 트리거에 있는 비즈니스 논리로 인해 구독자에 대한 변경 내용 복제의 속도가 느려질 수 있습니다.  
  
    -   트랜잭션 복제의 경우 복제된 명령을 적용하는 데 사용되는 사용자 지정 저장 프로시저에 이 논리를 포함하는 것이 더 효율적입니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
    -   병합 복제의 경우 비즈니스 논리 처리기를 사용하는 것이 보다 효율적일 수 있습니다. 자세한 내용은 [병합 동기화 중 비즈니스 논리 실행](../merge/execute-business-logic-during-merge-synchronization.md)을 참조하세요.  
  
     트리거를 사용하여 병합 복제에 대해 게시된 테이블의 참조 무결성을 유지 관리하려면 병합 에이전트에 필요한 다시 시도 횟수를 줄이도록 테이블 처리 순서를 지정합니다. 자세한 내용은 [병합 복제 지정할 속성](../publish/specify-merge-replication-properties.md)합니다.  
  
-   LOB(Large Object) 데이터 형식의 사용을 제한합니다.  
  
     LOB은 다른 열 데이터 형식보다 많은 스토리지 공간과 처리 작업을 필요로 합니다. 애플리케이션에 필요한 경우가 아니면 이러한 열을 아티클에 포함하지 마십시오. `text`, `ntext` 및 `image` 데이터 형식은 사용되지 않습니다. LOB를 포함시킬 경우 데이터 형식 `varchar(max)`, `nvarchar(max)`, `varbinary(max)`를 각각 사용하는 것이 좋습니다.  
  
     트랜잭션 복제의 경우 **OLEDB 스트리밍에 대한 배포 프로필**이라고 하는 배포 에이전트 프로필을 사용해 보십시오. 자세한 내용은 [Replication Agent Profiles](../agents/replication-agent-profiles.md)을(를) 참조하세요.  
  
## <a name="publication-design"></a>게시 디자인  
  
-   필요한 데이터만 게시합니다.  
  
     복제는 설정하기가 쉽기 때문에 실제로 필요한 것보다 많은 데이터를 게시하는 경향이 있습니다. 이로 인해 배포 데이터베이스 및 스냅숏 파일에서 리소스가 추가로 소모될 뿐만 아니라 필요한 데이터에 대한 처리량이 낮아질 수 있습니다. 불필요한 테이블 게시를 피하고 게시 업데이트 빈도를 줄일 것을 고려합니다.  
  
-   게시 디자인 및 애플리케이션 동작을 통해 충돌을 최소화합니다.  
  
     병합 복제, 업데이트할 수 있는 구독이 있는 트랜잭션 복제 또는 피어 투 피어 트랜잭션 복제를 사용하여 구독자에서 데이터를 변경할 수 있습니다. 병합 복제 및 업데이트할 수 있는 구독이 있는 트랜잭션 복제에서는 동기화 중 두 개 이상의 노드에서 지정된 행이 업데이트되는 경우 데이터 충돌이 지원됩니다. 피어 투 피어 복제에서는 데이터 충돌이 지원되지 않으므로 데이터 변경 내용을 분할해야 합니다. 사용된 복제 유형에 관계없이 가능하면 변경 내용을 분할하는 것이 좋습니다. 이렇게 하면 충돌 감지 및 해결 과정이 간단해집니다.  
  
     데이터 하위 집합을 각 구독자에 게시하거나 애플리케이션이 지정된 행의 변경 내용을 지정된 노드로 직접 게시하도록 하여 변경 내용을 분할할 수 있습니다.  
  
    -   병합 복제에서는 단일 게시에서 매개 변수가 있는 필터를 사용하여 데이터 하위 집합을 게시할 수 있습니다. 자세한 내용은 [매개 변수가 있는 행 필터](../merge/parameterized-filters-parameterized-row-filters.md)를 참조하십시오.  
  
    -   트랜잭션 복제에서는 여러 게시에서 정적 필터를 사용하여 데이터 하위 집합을 게시할 수 있습니다. 자세한 내용은 [게시된 데이터 필터링](../publish/filter-published-data.md)을 참조하세요.  
  
-   행 필터를 주의해서 사용합니다.  
  
     트랜잭션 게시에 행 필터를 사용하는 아티클이 하나 이상 있을 경우 로그 판독기 에이전트는 트랜잭션 로그를 검색할 때 테이블 업데이트에 의해 영향을 받는 각 행에 필터를 적용해야 합니다. 따라서 로그 판독기 에이전트의 처리량은 영향을 받게 됩니다.  
  
     마찬가지로 병합 에이전트는 변경되거나 삭제된 행을 평가하여 이러한 행을 받을 구독자를 결정해야 합니다. 구독자에 필요한 데이터를 줄이는 데 행 필터가 사용되면 이러한 처리는 모든 행을 한 테이블에서 게시할 때 보다 복잡해지고 느려질 수 있습니다. 각 구독자에서 스토리지 요구 사항을 줄이는 것과 최대 처리량을 달성해야 할 필요성 간의 관계를 신중하게 고려합니다. 필터링에 대한 자세한 내용은 [게시된 데이터 필터링](../publish/filter-published-data.md)을 참조하세요.  
  
## <a name="subscription-considerations"></a>구독 고려 사항  
  
-   다수의 구독자가 있을 경우 끌어오기 구독을 사용합니다.  
  
     배포 에이전트와 병합 에이전트는 밀어넣기 구독의 경우에는 배포자에서, 끌어오기 구독의 경우에는 구독자에서 실행됩니다. 끌어오기 구독을 사용하면 배포자에서 구독자로 에이전트 처리를 이동하여 성능을 향상시킬 수 있습니다. 자세한 내용은 [게시 구독](../subscribe-to-publications.md)을 참조하세요.  
  
-   구독자가 너무 오래된 경우 구독을 다시 초기화합니다.  
  
     많은 양의 변경 내용을 구독자로 보내야 할 경우 이를 새 스냅숏과 함께 다시 초기화하면 복제를 사용하여 개별 변경 내용을 이동하는 것보다 빠르게 보낼 수 있습니다. 자세한 내용은 [구독 다시 초기화](../reinitialize-subscriptions.md)를 참조하세요.  
  
     트랜잭션 복제의 경우 복제 모니터는 **배포되지 않은 명령** 탭에 구독자로 아직 배포되지 않은 배포 데이터베이스의 트랜잭션 수와 이러한 트랜잭션에 대한 예상 배포 시간 등을 표시합니다. 자세한 내용은 [ 정보 보기 및 태스크 수행 복제 모니터를 사용 하 여](../monitor/view-information-and-perform-tasks-replication-monitor.md)입니다.  
  
## <a name="snapshot-considerations"></a>스냅숏 고려 사항  
  
-   필요할 경우와 사용률이 낮은 시간에만 스냅숏 에이전트를 실행합니다.  
  
     스냅숏 에이전트는 게시자에 있는 게시된 테이블의 데이터를 배포자에 있는 스냅숏 폴더의 파일에 대량 복사합니다. 스냅숏 생성 프로세스는 리소스를 많이 소모할 수 있으며 사용률이 낮은 시간에 사용하는 것이 좋습니다.  
  
-   문자 모드 스냅숏이 필요한 경우가 아니라면 기본 모드 스냅숏을 사용합니다.  
  
     문자 모드 스냅숏이 필요한[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외의 구독자와 [!INCLUDE[ssEW](../../../includes/ssew-md.md)]를 실행하는 구독자를 제외하고 모든 구독자에 대해 기본값인 기본 모드 스냅숏을 사용합니다.  
  
-   게시에 대해 단일 스냅숏 폴더를 사용합니다.  
  
     스냅숏 위치와 관련된 게시 속성을 지정하는 경우 기본 스냅숏 폴더, 대체 스냅숏 폴더 또는 두 폴더 모두에 스냅숏 파일을 생성하도록 선택할 수 있습니다. 두 위치 모두에 스냅숏 파일을 생성하려면 스냅숏 에이전트 실행 시 추가 디스크 공간 및 추가 처리가 필요합니다.  
  
-   데이터베이스 또는 로그 파일 저장에 사용되지 않는 배포자의 로컬 드라이브에 스냅숏 폴더를 둡니다.  
  
     스냅숏 에이전트는 스냅숏 폴더에 데이터를 순차적으로 씁니다. 다른 데이터베이스나 로그 파일과 분리된 별도의 드라이브에 스냅숏 폴더를 두면 디스크 간 경합을 줄이고 스냅숏 과정을 좀 더 빠르게 완료할 수 있습니다.  
  
-   구독자에서 구독 데이터베이스를 만들 때는 단순 또는 대량 로그 복구 모델을 지정합니다. 이렇게 하면 구독자에서 스냅숏을 적용하는 동안 수행된 대량 삽입의 로깅이 최소화됩니다. 스냅숏이 구독 데이터베이스에 적용된 후 필요에 따라 다른 복구 모델로 변경할 수 있습니다. 복제된 데이터베이스는 모든 복구 모델을 사용할 수 있습니다. 복구 모델을 선택하는 방법은 [복원 및 복구 개요&#40;SQL Server&#41;](../../backup-restore/restore-and-recovery-overview-sql-server.md)를 참조하세요.  
  
-   느린 대역폭 네트워크의 경우 이동식 미디어에서 대체 스냅숏 폴더와 압축 스냅숏을 사용해 봅니다.  
  
     대체 스냅숏 폴더의 스냅숏 파일을 압축하면 스냅숏에 필요한 디스크 스토리지를 줄일 수 있으며 이동식 미디어에서 스냅숏 파일을 보다 간단하게 전송할 수 있습니다.  
  
     스냅숏을 압축하면 네트워크에서의 스냅숏 파일 전송 성능이 향상되는 경우도 있습니다. 그러나 스냅숏 에이전트에서 스냅숏 파일을 생성하는 경우와 배포 에이전트 또는 병합 에이전트에서 스냅숏 파일을 적용하는 경우에 스냅숏 파일을 압축하려면 추가 처리 작업이 필요합니다. 이 경우 스냅숏 생성 속도가 느려지거나 스냅숏 적용 시간이 늘어날 수 있습니다. 또한 네트워크 오류가 발생하면 압축 스냅숏은 재개할 수 없으므로 불안정한 네트워크에서는 압축 스냅숏이 적합하지 않습니다. 네트워크에서 압축 스냅숏을 사용하는 경우 이러한 장단점을 신중하게 고려하여 균형을 맞추는 것이 좋습니다. 자세한 내용은 [Alternate Snapshot Folder Locations](../alternate-snapshot-folder-locations.md) 및 [Compressed Snapshots](../compressed-snapshots.md)를 참조하세요.  
  
-   구독을 수동으로 초기화해 봅니다.  
  
     큰 초기 데이터 세트와 관련된 일부 시나리오에서는 스냅숏 대신 다른 방법을 사용하여 구독을 초기화하는 것이 좋습니다. 자세한 내용은 [스냅숏 없이 트랜잭션 구독 초기화](../initialize-a-transactional-subscription-without-a-snapshot.md)에서 수동으로 구독을 초기화하는 방법에 대해 설명합니다.  
  
## <a name="agent-parameters"></a>에이전트 매개 변수  
  
-   초기 테스트, 모니터링 또는 디버깅 도중을 제외하고 복제 에이전트의 정보 표시 수준을 줄입니다.  
  
     배포 에이전트 및 병합 에이전트의 **–HistoryVerboseLevel** 매개 변수 및 **–OutputVerboseLevel** 매개 변수를 줄입니다. 이렇게 하면 추적 에이전트 기록 및 출력에 삽입되는 새 행의 수가 줄어듭니다. 대신 상태가 같은 이전 기록 메시지는 새 기록 정보로 업데이트됩니다. 에이전트 작업에 대한 정보를 최대한 많이 가질 수 있도록 테스트, 모니터링 및 디버깅의 정보 표시 수준을 늘립니다.  
  
-   스냅숏 에이전트, 병합 에이전트 및 배포 에이전트의 **–MaxBCPThreads** 매개 변수를 사용합니다(지정된 스레드 수는 컴퓨터의 프로세서 수를 초과할 수 없습니다). 이 매개 변수는 스냅숏이 생성되어 적용될 때 병렬로 수행할 수 있는 대량 복사 작업 수를 지정합니다.  
  
-   배포 에이전트와 병합 에이전트의 **–UseInprocLoader** 매개 변수를 사용합니다(게시된 테이블에 XML 열이 포함된 경우 이 매개 변수를 사용할 수 없습니다). 이 매개 변수를 사용할 경우 스냅숏이 적용되면 에이전트가 BULK INSERT 명령을 사용할 수 있습니다.  
  
 에이전트 프로필 및 명령줄에서 에이전트 매개 변수를 지정할 수 있습니다. 참조 항목:  
  
-   [복제 에이전트 프로필 작업](../agents/work-with-replication-agent-profiles.md)  
  
-   [복제 에이전트의 명령 프롬프트 매개 변수 보기 및 수정&#40;SQL Server Management Studio&#41;](../agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
-   [Replication Agent Executables Concepts](../concepts/replication-agent-executables-concepts.md)에 할당될 최소 및 최대 메모리 양을 설정합니다.  
  
  
