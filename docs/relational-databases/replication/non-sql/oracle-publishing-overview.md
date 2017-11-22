---
title: "Oracle 게시 개요 | Microsoft 문서"
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publishing [SQL Server replication], Oracle publishing
- snapshot replication [SQL Server], Oracle publishing
- Oracle publishing [SQL Server replication]
- transactional replication, Oracle publishing
- Oracle publishing [SQL Server replication], about Oracle publishing
ms.assetid: 2e013259-0022-4897-a08d-5f8deb880fa8
caps.latest.revision: "40"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 888fdaaa1943e3b8e31010b9f6f695abf0cd2180
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="oracle-publishing-overview"></a>Oracle 게시 개요  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]부터는 복제 토폴로지에 Oracle 버전 9i 이상의 Oracle 게시자를 추가할 수 있습니다. 게시 서버는 모든 Oracle 지원 하드웨어 및 운영 체제에 배포할 수 있습니다. 이 기능은 잘 설정된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 스냅숏 복제 및 트랜잭션 복제의 토대 위에 구축되었으므로 비슷한 성능과 유용성을 제공합니다.  
  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 트랜잭션 및 스냅숏 복제에 대해 다음과 같이 다른 유형의 시나리오를 지원합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 구독자로 데이터 게시  

-   Oracle에서 데이터를 게시할 때 다음과 같은 제한 사항이 있습니다.  
  | |2016 또는 이전 버전 |2017 이상 |
  |-------|-------|--------|
  |Oracle에서 복제 |Oracle 10g 또는 이전 버전만 지원 |Oracle 10g 또는 이전 버전만 지원 |
  |Oracle로 복제 |Oracle 12c까지 |지원되지 않음 |


 SQL Server 이외의 구독자에 대한 다른 유형의 복제는 지원되지 않습니다. Oracle 게시는 지원되지 않습니다. 데이터를 이동하려면 변경 데이터 캡처 및 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]를 사용하여 솔루션을 만듭니다.  

  
## <a name="snapshot-replication-for-oracle"></a>Oracle의 스냅숏 복제  
 Oracle 스냅숏 게시는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 스냅숏 게시와 비슷한 방식으로 구현됩니다. Oracle 게시에 대해 스냅숏 에이전트가 실행되면 해당 에이전트는 Oracle 게시자에 연결한 다음 게시의 각 테이블을 처리합니다. 이 에이전트는 각 테이블을 처리할 때 테이블 행을 검색하고 스키마 스크립트를 만듭니다. 이 스크립트는 게시의 스냅숏 공유에 저장됩니다. 스냅숏 에이전트가 실행될 때마다 전체 데이터 집합이 생성되므로 트랜잭션 복제의 경우처럼 Oracle 테이블에 변경 내용 추적 트리거가 추가되지 않습니다. 스냅숏 복제를 사용하면 게시 시스템에 미치는 영향을 최소화하면서 데이터를 편리하게 마이그레이션할 수 있습니다.  
  
## <a name="transactional-replication-for-oracle"></a>Oracle의 트랜잭션 복제  
 Oracle 트랜잭션 게시는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 트랜잭션 게시 아키텍처를 사용하여 구현되지만 변경 내용은 Oracle 데이터베이스에 대한 데이터베이스 트리거와 로그 판독기 에이전트를 함께 사용하여 추적합니다. Oracle 트랜잭션 게시에 대한 구독자는 스냅숏 복제를 사용하여 자동으로 초기화됩니다. 후속 변경 내용이 발생하면 로그 판독기 에이전트를 통해 추적된 후 구독자로 배달됩니다.  
  
 Oracle 게시가 생성되면 Oracle 데이터베이스 내의 게시된 각 테이블에 대해 트리거 및 추적 테이블이 생성됩니다. 게시된 테이블의 데이터가 변경되면 테이블에 대해 데이터베이스 트리거가 발생되고 수정된 각 행에 대한 정보가 복제 추적 테이블에 삽입됩니다. 그런 후 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에 대한 로그 판독기 에이전트가 추적 테이블의 데이터 변경 정보를 배포자의 배포 데이터베이스로 옮깁니다. 마지막으로 표준 트랜잭션 복제의 경우처럼 배포 에이전트가 배포자에서 구독자로 변경 내용을 옮깁니다.  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle 게시를 위한 용어 설명](../../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [다른 유형의 데이터베이스 복제](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  
