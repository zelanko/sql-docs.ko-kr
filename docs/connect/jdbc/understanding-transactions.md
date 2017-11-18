---
title: "트랜잭션 이해 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d3e0414c-6809-4bb1-93b1-4960507faecc
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 64a9539296531bc0d07d79da3613eb953fefa917
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-transactions"></a>트랜잭션 이해
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  트랜잭션은 논리적 작업 단위로 결합되는 작업 그룹입니다. 트랜잭션은 시스템에서 발생할 수 있는 오류에 관계없이 트랜잭션의 각 동작에 대해 일관성과 무결성을 제어하고 유지 관리하는 데 사용됩니다.  
  
 와 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], 로컬 또는 분산 트랜잭션이 될 수 있습니다. 또한 트랜잭션은 격리 수준을 사용합니다. JDBC 드라이버에서 지 원하는 격리 수준에 대 한 자세한 내용은 참조 [격리 수준 이해](../../connect/jdbc/understanding-isolation-levels.md)합니다.  
  
 응용 프로그램은 Transact-SQL 문 또는 JDBC 드라이버에서 제공하는 메서드 중 하나만을 사용하여 트랜잭션을 제어해야 합니다. 동일한 트랜잭션에서 Transact-SQL 문과 JDBC API 메서드를 둘 다 사용하면 트랜잭션을 정상적으로 커밋할 수 없거나, 트랜잭션이 커밋 또는 롤백되고 예상치 않은 새로운 트랜잭션이 시작되거나, "트랜잭션 다시 시작 실패" 예외 등의 문제가 발생할 수 있습니다.  
  
## <a name="using-local-transactions"></a>로컬 트랜잭션 사용  
 트랜잭션이 1단계 트랜잭션이면 로컬 트랜잭션으로 간주하고 데이터베이스에서 직접 처리합니다. JDBC 드라이버의 다양 한 메서드를 사용 하 여 로컬 트랜잭션을 지원는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스를 포함 하 여 [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md), [커밋](../../connect/jdbc/reference/commit-method-sqlserverconnection.md), 및 [롤백](../../connect/jdbc/reference/rollback-method.md)합니다. 일반적으로 로컬 트랜잭션은 응용 프로그램에서 명시적으로 관리하거나 Java Platform, Enterprise Edition(Java EE) 응용 프로그램 서버에서 자동으로 관리합니다.  
  
 다음 예제에서는에서 두 개의 별도 문으로 구성 된 로컬 트랜잭션을 수행 하는 `try` 블록입니다. 문은 Production.ScrapReason 테이블에 대해 실행 되는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스 되며 커밋된 예외가 throw 되지 않을 경우. 코드는 `catch` 블록에서 트랜잭션을 롤백할 경우 예외가 throw 됩니다.  
  
 [!code[JDBC#UnderstandingTransactions1](../../connect/jdbc/codesnippet/Java/understanding-transactions_1.java)]  
  
## <a name="using-distributed-transactions"></a>분산 트랜잭션 사용  
 분산 트랜잭션은 ACID(원자성, 일관성, 격리성, 영속성)라는 중요한 트랜잭션 처리 속성을 유지하면서 둘 이상의 네트워크 데이터베이스에서 데이터를 업데이트합니다. 분산 트랜잭션 지원은 JDBC 2.0 옵션 API 사양의 JDBC API에 추가되었습니다. 일반적으로 분산 트랜잭션 관리는 Java EE 응용 프로그램 서버 환경에서 JTS(Java Transaction Service) 트랜잭션 관리자가 자동으로 수행합니다. 그러나는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 임의의 API JTA (Java Transaction) 규격 트랜잭션 관리자 하에서 분산된 트랜잭션을 지원 합니다.  
  
 JDBC 드라이버와 원활 하 게 통합 되어 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 진정한에 Distributed Transaction Coordinator (MS DTC) 분산 된 트랜잭션 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. MS DTC는에서 제공 하는 분산된 트랜잭션 기능 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 에 대 한 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 시스템. MS DTC에서 검증 된 트랜잭션 처리 기술을 사용 하 여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 완전 한 2 단계 분산된 커밋 프로토콜 및 분산된 트랜잭션 복구와 같은 XA 기능을 지원 합니다.  
  
 분산된 트랜잭션을 사용 하는 방법에 대 한 자세한 내용은 참조 [XA 트랜잭션 이해](../../connect/jdbc/understanding-xa-transactions.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 트랜잭션 수행](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  

