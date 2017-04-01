---
title: "메모리 내 OLTP에 대해 지원되지 않는 SQL Server 기능 | Microsoft Docs"
ms.custom: ""
ms.date: "10/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
caps.latest.revision: 55
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 55
---
# 메모리 내 OLTP에 대해 지원되지 않는 SQL Server 기능
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 항목에서는 메모리 액세스에 최적화된 개체와 함께 사용할 수 없는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능에 대해 설명합니다.  
  
## [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 내 OLTP에 지원되지 않는 기능  
 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능은 메모리 액세스에 최적화된 데이터 파일 그룹과 같은 메모리 액세스에 최적화된 개체가 포함된 데이터베이스에서 지원되지 않습니다.  
  
|지원되지 않는 기능|기능 설명|  
|-------------------------|-------------------------|  
|메모리 액세스에 최적화된 테이블에 대한 데이터 압축|데이터 압축 기능을 사용하여 데이터베이스 내의 데이터를 압축하고 데이터베이스의 크기를 줄일 수 있습니다. 자세한 내용은 [Data Compression](../../relational-databases/data-compression/data-compression.md)을 참조하세요.|  
|메모리 액세스에 최적화된 테이블 및 HASH 인덱스와 비클러스터형 인덱스의 분할|분할 테이블 및 인덱스의 데이터는 데이터베이스에서 두 개 이상의 파일 그룹으로 분할될 수 있는 단위로 나뉩니다. 자세한 내용은 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)을 참조하세요.|  
|복제|구독자에서 메모리 액세스에 최적화된 테이블에 대한 트랜잭션 복제 이외의 복제 구성은 메모리 액세스에 최적화된 테이블을 참조하는 탭 또는 뷰와 호환되지 않습니다. 메모리 액세스에 최적화된 파일 그룹이 있는 경우 sync_mode=’database snapshot’을 사용한 복제는 지원되지 않습니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블 구독자로 복제](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)를 참조하세요.|  
|미러링|MEMORY_OPTIMIZED_DATA 파일 그룹이 포함된 데이터베이스에는 데이터베이스 미러링이 지원되지 않습니다. 미러링에 대한 자세한 내용은 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 참조하세요.|  
|로그를 다시 작성|MEMORY_OPTIMIZED_DATA 파일 그룹이 포함된 데이터베이스에는 연결 또는 ALTER DATABASE를 통한 로그 다시 작성이 지원되지 않습니다.|  
|연결된 서버|메모리 액세스에 최적화된 테이블과 같은 쿼리 또는 트랜잭션에서는 연결된 서버에 액세스할 수 없습니다. 자세한 내용은 [연결된 서버&#40;데이터베이스 엔진&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)를 참조하세요.|  
|대량 로깅|데이터베이스의 복구 모델에 관계없이 메모리 액세스에 최적화된 영구 테이블에 대한 모든 작업은 항상 모두 기록됩니다.|  
|최소 로깅|최소 로깅은 메모리 액세스에 최적화된 테이블에 대해 지원되지 않습니다. 최소 로깅에 대한 자세한 내용은 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md) 및 [대량 가져오기의 최소 로깅을 위한 선행 조건](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)을 참조하세요.|  
|변경 내용 추적|변경 내용 추적은 메모리 내 OLTP 개체가 포함된 데이터베이스에서 사용할 수 있습니다. 그러나 메모리 액세스에 최적화된 테이블의 변경 내용은 추적되지 않습니다.|  
|DDL 트리거|메모리 내 OLTP 테이블과 고유하게 컴파일된 모듈에서는 데이터베이스 수준 및 서버 수준 DDL 트리거가 모두 지원되지 않습니다.|  
|CDC(변경 데이터 캡처)|CDC는 실행되는 DROP TABLE에 대해 DDL 트리거를 사용하므로 메모리 액세스에 최적화된 테이블을 포함하는 데이터베이스에 사용할 수 없습니다.|  
|파이버 모드|메모리 액세스에 최적화된 테이블에서는 파이버 모드가 지원되지 않습니다.<br /><br /> 파이버 모드가 활성인 경우 메모리 액세스에 최적화된 파일 그룹이 포함된 데이터베이스를 만들거나 메모리 액세스에 최적화된 파일 그룹을 기존 데이터베이스에 추가할 수 없습니다.<br /><br /> 메모리 액세스에 최적화된 파일 그룹이 포함된 데이터베이스가 있는 경우 파이버 모드를 활성화할 수 있습니다. 하지만 파이버 모드를 사용하려면 서버를 다시 시작해야 합니다. 이러한 상황에서는 메모리 액세스에 최적화된 파일 그룹이 포함된 데이터베이스가 복구에 실패하며 메모리 액세스에 최적화된 파일 그룹이 포함된 데이터베이스를 사용하려면 파이버 모드를 비활성화할 것을 제안하는 오류 메시지가 나타납니다.<br /><br /> 파이버 모드가 활성이면 메모리 액세스에 최적화된 파일 그룹이 포함된 데이터베이스를 첨부하거나 복원하는 작업이 실패합니다. 데이터베이스는 주의 대상으로 표시됩니다.<br /><br /> <br /><br /> 자세한 내용은 [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)을 참조하세요.|  
|Service Broker 제한|고유하게 컴파일된 저장 프로시저에서 큐에 액세스할 수 없습니다.<br /><br /> 메모리 액세스에 최적화된 테이블에 액세스하는 트랜잭션에서 원격 데이터베이스에 있는 큐에 액세스할 수 없습니다.|  
|구독자에서 복제|구독자에서는 메모리 액세스에 최적화된 테이블에 대한 트랜잭션 복제가 지원되지만 몇 가지 제한 사항이 있습니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블 구독자로 복제](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)를 참조하세요.|  
  
 몇 가지 예외를 제외하고 데이터베이스간 트랜잭션은 지원되지 않습니다. 다음 테이블에서는 지원되는 경우 및 해당 제한 사항에 대해 설명합니다. (참고 항목: [데이터베이스 간 쿼리](../../relational-databases/in-memory-oltp/cross-database-queries.md))  
  
|데이터베이스|허용함|설명|  
|---------------|-------------|-----------------|  
|사용자 데이터베이스, 모델 및 msdb|아니요|데이터베이스 간 쿼리 및 트랜잭션은 지원되지 않습니다.<br /><br /> 메모리 액세스에 최적화된 테이블이나 고유하게 컴파일된 저장 프로시저에 액세스하는 쿼리와 트랜잭션은 시스템 데이터베이스 master(읽기 전용 액세스) 및 tempdb를 제외하고 다른 데이터베이스에 액세스할 수 없습니다.|  
|리소스 데이터베이스, tempdb|예|단일 사용자 데이터베이스를 제외하고 리소스 데이터베이스 및 tempdb를 사용하는 데이터베이스 간 트랜잭션에는 제한 사항이 없습니다.|  
|master|읽기 전용|메모리 내 OLTP 및 master 데이터베이스와 관련된 데이터베이스 간 트랜잭션은 master 데이터베이스에 대한 쓰기가 포함된 경우 커밋에 실패합니다. master 데이터베이스에서 읽기만 하고 하나의 사용자 데이터베이스만 사용하는 데이터베이스 간 트랜잭션은 허용됩니다.|  
  
## 지원되지 않는 시나리오  
  
-   메모리 내 OLTP에서는 데이터베이스 포함([포함된 데이터베이스](../../relational-databases/databases/contained-databases.md))이 지원되지 않습니다. 포함된 데이터베이스 인증이 지원됩니다. 그러나 모든 메모리 내 OLTP 개체는 DMV dm_db_uncontained_entities에 포함 위반으로 표시됩니다.  
  
-   CLR 저장 프로시저 내부에서 컨텍스트 연결을 사용하여 메모리 액세스에 최적화된 테이블에 액세스  
  
-   메모리 액세스에 최적화된 테이블에 액세스하는 쿼리의 키 집합 및 동적 커서. 이러한 커서는 정적 및 읽기 전용으로 성능이 저하됩니다.  
  
-   *target*과 함께 **MERGE INTO***target*을 사용하면 메모리 액세스에 최적화된 테이블입니다. **MERGE USING***source*는 메모리 액세스에 최적화된 테이블에 대해 지원됩니다.  
  
-   ROWVERSION(TIMESTAMP) 데이터 형식은 지원되지 않습니다. 자세한 내용은 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)을 참조하세요.  
  
-   자동 닫기는 MEMORY_OPTIMIZED_DATA 파일 그룹이 포함된 데이터베이스에서 지원되지 않습니다.  
  
-   데이터베이스 스냅숏은 MEMORY_OPTIMIZED_DATA 파일 그룹이 있는 데이터베이스에 대해 지원되지 않습니다.  
  
-   트랜잭션 DDL. 사용자 트랜잭션 내에서는 메모리 내 OLTP 개체에 대한 CREATE/ALTER/DROP 작업이 지원되지 않습니다.  
  
-   이벤트 알림  
  
-   PBM(정책 기반 관리). PBM의 방지 및 로그 전용 모드는 지원되지 않습니다. 서버에 이러한 정책이 있으면 메모리 내 OLTP DDL이 성공적으로 실행되지 않을 수 있습니다. 요청 시 및 예약 시 모드는 지원됩니다.  
  
## 참고 항목  
 [메모리 내 OLTP에 대한 SQL Server 지원](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)  
  
  