---
title: SQL Server 기능 지원 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
caps.latest.revision: 48
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 5233c8ab4eaa9926fe8c058c3f6d410d536306da
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183301"
---
# <a name="supported-sql-server-features"></a>지원되는 SQL Server 기능
  이 항목에서는 메모리 최적화 개체와 함께 사용할 수 있거나 사용할 수 없는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능에 대해 설명합니다.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-features-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 내 OLTP에 대 한 지원 되는 기능  
 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능은 메모리 최적화 파일 그룹을 비롯해서 메모리 최적화 개체가 포함된 데이터베이스에서 지원됩니다.  
  
 지원되는 데이터 형식에 대한 자세한 내용은 [Supported Data Types](supported-data-types-for-in-memory-oltp.md)을 참조하세요.  
  
-   메모리 최적화 테이블에서 지원되는 옵션 및 작업. 자세한 내용은 [CREATE TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)을 참조하세요.  
  
-   고유하게 컴파일된 저장 프로시저에서 지원되는 옵션 및 작업. 자세한 내용은 [CREATE PROCEDURE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)를 참조하세요.  
  
-   해석된 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하여 메모리 최적화 테이블에 액세스할 수 있는 기능. 해석된 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 은 [!INCLUDE[tsql](../../../includes/tsql-md.md)]과 고유하게 컴파일되지 않은 저장 프로시저를 사용하여 메모리 액세스에 최적화되지 않은 테이블에 액세스하는 것과 동일한 노출 영역을 제공합니다. 자세한 내용은 [해석된 Transact-SQL을 사용하여 메모리 액세스에 최적화된 테이블에 액세스](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)를 참조하세요.  
  
-   다중 버전 관리 및 낙관적 동시성 제어. 자세한 내용은 [Transaction Isolation Levels](../../database-engine/transaction-isolation-levels.md)을 참조하세요.  
  
-   메모리 최적화 데이터 파일 그룹이 포함된 데이터베이스의 백업 및 복원. 자세한 내용은 [Back Up and Restore of SQL Server Databases](../backup-restore/back-up-and-restore-of-sql-server-databases.md)을 참조하세요.  
  
-   지원 가능성을 위해 제공되는 카탈로그 뷰, 동적 관리 뷰 및 확장 이벤트. 자세한 내용은 [메모리 내 OLTP에 대한 시스템 뷰, 저장 프로시저, DMV 및 대기 유형](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)을 참조하세요.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 개체. 자세한 내용은 [메모리 내 OLTP에 대한 SQL Server 관리 개체 지원](sql-server-management-objects-support-for-in-memory-oltp.md)을 참조하세요.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]을 참조하세요. 자세한 내용은 [메모리 내 OLTP에 대한 SQL Server Management Studio 지원](sql-server-management-studio-support-for-in-memory-oltp.md)을 참조하세요.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. 자세한 내용은 [SQL Server PowerShell 개요](http://msdn.microsoft.com/library/cc281954\(SQL.105\).aspx)를 참조하세요.  
  
-   bcp 유틸리티를 사용하여 대량 데이터 가져오기 및 내보내기. 자세한 내용은 [bcp 유틸리티를 사용하여 대량 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](../import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)를 참조하세요.  
  
-   충돌 복구  
  
-   메모리 최적화 데이터 파일 그룹에서 메모리 내 OLTP 개체를 저장하고 RTO(복구 시간 목표)를 줄이기 위한 컨테이너 여러 개  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 트랜잭션 로그 블록 체크섬을 계산 하 고 유효성을 검사 합니다.  
  
-   새 SNAPSHOT 테이블 힌트. 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)를 참조하세요.  
  
-   DB COMPAT 수준  
  
-   부분적으로 포함된 데이터베이스. 포함된 데이터베이스 인증이 지원됩니다. 그러나 모든 메모리 내 OLTP 개체는 DMV dm_db_uncontained_entities에 포함 위반으로 표시됩니다.  
  
-   제한 사항이 있는 Service Broker. 고유하게 컴파일된 저장 프로시저에서 큐에 액세스할 수 없습니다. 메모리 최적화 테이블에 액세스하는 트랜잭션에서 원격 데이터베이스에 있는 큐에 액세스할 수 없습니다.  
  
-   장애 조치(failover) 클러스터링: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] AlwaysOn 제공의 일부로 AlwaysOn 장애 조치(Failover) 클러스터 인스턴스는 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 기능을 활용하여 FCI(장애 조치(failover) 클러스터 인스턴스)라는 서버 인스턴스 수준의 중복성을 통해 로컬 고가용성을 제공합니다. 자세한 내용은 [Always On 장애 조치(failover) 클러스터 인스턴스(SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)를 참조하세요.  
  
-   AlwaysOn과 통합: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 AlwaysOn을 비롯하여 서버 또는 데이터베이스의 고가용성 유지를 위한 여러 가지 옵션을 제공합니다. 자세한 내용은 [고가용성 솔루션&#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)을 참조하세요.  
  
-   로그 전달: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 전달을 사용하면 주 서버 인스턴스의 주 데이터베이스에서 별도의 보조 서버 인스턴스에 있는 하나 이상의 보조 데이터베이스로 트랜잭션 로그 백업을 자동으로 보낼 수 있습니다. 자세한 내용은 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)를 참조하세요.  
  
-   구독자에서 메모리 최적화 테이블에 대한 트랜잭션 복제가 지원되지만 몇 가지 제한 사항이 있습니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블 구독자로 복제](../replication/replication-to-memory-optimized-table-subscribers.md)를 참조하세요.  
  
-   리소스 관리자: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업 및 시스템 리소스 소비량을 관리하는 데 사용할 수 있는 기능입니다. 리소스 관리자를 사용하면 들어오는 응용 프로그램 요청이 사용할 수 있는 CPU, 물리적 IO 및 메모리 양을 제한할 수 있습니다. 자세한 내용은 [Managing Memory for In-Memory OLTP](../../database-engine/managing-memory-for-in-memory-oltp.md) 및 [Resource Governor](../resource-governor/resource-governor.md)를 참조하세요.  
  
-   메모리 내 OLTP는 메모리 최적화 테이블의 (var)char 열에 대해 지원되는 코드 페이지와 인덱스 및 고유하게 컴파일된 저장 프로시저에 사용되는 지원되는 데이터 정렬에 대한 제한 사항이 있습니다. 자세한 내용은 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)를 참조하세요.  
  
-   BACPAC 지원.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-features-not-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 내 OLTP에 지원되지 않는 기능  
 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능은 메모리 최적화 데이터 파일 그룹과 같은 메모리 최적화 개체가 포함된 데이터베이스에서 지원되지 않습니다.  
  
|지원되지 않는 기능|기능 설명|  
|-------------------------|-------------------------|  
|메모리 최적화 테이블에 대한 데이터 압축|데이터 압축 기능을 사용하여 데이터베이스 내의 데이터를 압축하고 데이터베이스의 크기를 줄일 수 있습니다. 자세한 내용은 [Data Compression](../data-compression/data-compression.md)을 참조하세요.|  
|메모리 최적화 테이블 및 HASH 인덱스의 분할|분할 테이블 및 인덱스의 데이터는 데이터베이스에서 두 개 이상의 파일 그룹으로 분할될 수 있는 단위로 나뉩니다. 자세한 내용은 [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md)을 참조하세요.|  
|데이터베이스의 메모리 최적화 데이터 파일 그룹에 대한 TDE(투명한 데이터 암호화)|TDE(투명한 데이터 암호화)를 통해 데이터 및 로그 파일의 실시간 I/O 암호화 및 암호 해독을 수행합니다. 자세한 내용은 [TDE&#40;투명한 데이터 암호화&#41;](../security/encryption/transparent-data-encryption.md)를 참조하세요.<br /><br /> TDE는 메모리 내 OLTP 개체가 포함된 데이터베이스에서 사용할 수 있습니다. TDE가 사용하도록 설정된 경우에는 메모리 내 OLTP 로그 레코드가 암호화됩니다. 영구 테이블에 대한 검사점 파일은 데이터베이스에서 TDE가 사용하도록 설정된 경우에도 암호화되지 않습니다.|  
|복제|구독자에서 메모리 최적화 테이블에 대한 트랜잭션 복제 이외의 복제 구성은 메모리 최적화 테이블을 참조하는 탭 또는 뷰와 호환되지 않습니다. 메모리 최적화 파일 그룹이 있는 경우 sync_mode=’database snapshot’을 사용한 복제는 지원되지 않습니다. 자세한 내용은 [Replication to Memory-Optimized Table Subscribers](../replication/replication-to-memory-optimized-table-subscribers.md)를 참조하세요.|  
|MARS(Multiple Active Result Sets)|MARS(Multiple Active Result Set)는 메모리 최적화 테이블에 지원되지 않습니다. 이 오류는 연결된 서버 사용을 나타낼 수도 있습니다. 연결된 서버는 MARS를 사용할 수 있습니다. 연결된 서버는 메모리 최적화 테이블에 지원되지 않습니다. 그 대신 메모리 최적화 테이블을 호스팅하는 서버와 데이터베이스에 직접 연결합니다.|  
|미러링|데이터베이스 미러링은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 가용성을 높이기 위한 솔루션입니다. 자세한 내용은 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 참조하세요.|  
|로그를 다시 작성|연결을 통해 로그를 다시 작성 하거나 ALTER DATABASE 데이터베이스는 MEMORY_OPTIMIZED_DATA 파일 그룹에 대해 지원 되지 않습니다.|  
|연결된 서버|자세한 내용은 [연결된 서버&#40;데이터베이스 엔진&#41;](../linked-servers/linked-servers-database-engine.md)를 참조하세요.|  
|대량 로깅|데이터베이스의 복구 모델에 관계없이 메모리 최적화 영구 테이블에 대한 모든 작업은 항상 모두 기록됩니다.|  
|최소 로깅|최소 로깅은 메모리 최적화 테이블에 대해 지원되지 않습니다. 최소 로깅에 대한 자세한 내용은 [트랜잭션 로그&#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md) 및 [대량 가져오기의 최소 로깅을 위한 선행 조건](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)을 참조하세요.|  
|변경 내용 추적|변경 내용 추적은 메모리 내 OLTP 개체가 포함된 데이터베이스에서 사용할 수 있습니다. 그러나 메모리 최적화 테이블의 변경 내용은 추적되지 않습니다.|  
|DDL 트리거|데이터베이스 수준 및 서버 수준 DDL 트리거는 둘 다 메모리 내 OLTP 테이블과 고유하게 컴파일된 저장 프로시저에서 지원되지 않습니다.|  
|CDC(변경 데이터 캡처)|CDC는 DROP과 같은 특정 작업을 수행할 수 없도록 하므로 메모리 내 OLTP 개체가 포함된 데이터베이스에서 사용하도록 설정하면 안 됩니다.|  
|데이터베이스 포함|데이터베이스 포함은 고유하게 컴파일된 저장 프로시저와 메모리 최적화 테이블이 포함된 데이터베이스에서 지원되지 않습니다. 자세한 내용은 [Contained Databases](../databases/contained-databases.md)를 참조하세요.|  
|컨텍스트 연결|CLR 저장 프로시저 내부에서 컨텍스트 연결을 사용하여 메모리 최적화 테이블에 액세스는 지원되지 않습니다.|  
|커서|메모리 최적화 테이블에 액세스하는 쿼리의 키 집합 및 동적 커서. 이러한 쿼리는 정적 쿼리로 강등되어 읽기 전용이 됩니다.|  
|TABLESTAMP|TABLESTAMP는 지원되지 않습니다. 자세한 내용은 [FROM&#40;Transact-SQL&#41;](/sql/t-sql/queries/from-transact-sql)을 참조하세요.|  
|AUTO_CLOSE|AUTO_CLOSE는 지원되지 않습니다. 자세한 내용은 [Set the AUTO_CLOSE Database Option to OFF](../policy-based-management/set-the-auto-close-database-option-to-off.md)을 참조하세요.|  
|데이터베이스 스냅숏|데이터베이스 스냅숏은 지원되지 않습니다. 자세한 내용은 [데이터베이스 스냅숏&#40;SQL Server&#41;](../databases/database-snapshots-sql-server.md)을 참조하세요.|  
|트랜잭션 DDL|트랜잭션 DDL은 메모리 내 OLTP에서 지원되지 않습니다.|  
|이벤트 알림|이벤트 알림은 지원되지 않습니다. 자세한 내용은 [Event Notifications](../service-broker/event-notifications.md)을 참조하세요.|  
|파이버 모드|파이버 모드는 메모리 내 OLTP에서 지원되지 않습니다.|  
|PBM(정책 기반 관리).|PBM의 방지 및 로그 전용 모드는 지원되지 않습니다. 서버에 이러한 정책이 있으면 메모리 내 OLTP DDL이 성공적으로 실행되지 않을 수 있습니다. 요청 시 및 예약 시 모드는 지원됩니다.|  
|DACFX 배포/추출|DAC Framework 배포/추출은 메모리 내 OLTP에서 지원되지 않습니다.|  
  
 몇 가지 예외를 제외하고 데이터베이스간 트랜잭션은 지원되지 않습니다. 다음 테이블에서는 지원되는 경우 및 해당 제한 사항에 대해 설명합니다. (참고 항목: [데이터베이스 간 쿼리](cross-database-queries.md))  
  
|데이터베이스|허용함|Description|  
|---------------|-------------|-----------------|  
|사용자 데이터베이스, 모델 및 msdb|아니요|데이터베이스 간 쿼리 및 트랜잭션은 지원되지 않습니다.<br /><br /> 메모리 최적화 테이블이나 고유하게 컴파일된 저장 프로시저에 액세스하는 쿼리와 트랜잭션은 시스템 데이터베이스 master(읽기 전용 액세스) 및 tempdb를 제외하고 다른 데이터베이스에 액세스할 수 없습니다.|  
|리소스 데이터베이스 및 tempdb|예|단일 사용자 데이터베이스를 제외하고 리소스 데이터베이스 및 tempdb를 사용하는 데이터베이스 간 트랜잭션에는 제한 사항이 없습니다.|  
|master|읽기 전용|메모리 내 OLTP 및 master 데이터베이스와 관련된 데이터베이스 간 트랜잭션은 master 데이터베이스에 대한 쓰기가 포함된 경우 커밋에 실패합니다. master 데이터베이스에서 읽기만 하고 하나의 사용자 데이터베이스만 사용하는 데이터베이스 간 트랜잭션은 허용됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP에 대한 SQL Server 지원](sql-server-support-for-in-memory-oltp.md)  
  
  
