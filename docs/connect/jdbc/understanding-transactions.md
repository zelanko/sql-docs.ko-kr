---
title: 트랜잭션 이해 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d3e0414c-6809-4bb1-93b1-4960507faecc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d5a6caa9c9bf1766b59aa813719d1461b6ef1aa
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027340"
---
# <a name="understanding-transactions"></a>트랜잭션 이해

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

트랜잭션은 논리적 작업 단위로 결합되는 작업 그룹입니다. 트랜잭션은 시스템에서 발생할 수 있는 오류에 관계없이 트랜잭션의 각 동작에 대해 일관성과 무결성을 제어하고 유지 관리하는 데 사용됩니다.

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]의 트랜잭션은 로컬 또는 분산 중 하나일 수 있습니다. 또한 트랜잭션은 격리 수준을 사용합니다. JDBC 드라이버에서 지 원하는 격리 수준에 대 한 자세한 내용은 [격리 수준 이해](../../connect/jdbc/understanding-isolation-levels.md)를 참조 하세요.

애플리케이션은 Transact-SQL 문 또는 JDBC 드라이버에서 제공하는 메서드 중 하나만을 사용하여 트랜잭션을 제어해야 합니다. 동일한 트랜잭션에서 Transact-SQL 문과 JDBC API 메서드를 둘 다 사용하면 트랜잭션을 정상적으로 커밋할 수 없거나, 트랜잭션이 커밋 또는 롤백되고 예상치 않은 새로운 트랜잭션이 시작되거나, "트랜잭션 다시 시작 실패" 예외 등의 문제가 발생할 수 있습니다.

## <a name="using-local-transactions"></a>로컬 트랜잭션 사용

트랜잭션이 1단계 트랜잭션이면 로컬 트랜잭션으로 간주하고 데이터베이스에서 직접 처리합니다. JDBC 드라이버는 [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md), [commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) 및 [rollback](../../connect/jdbc/reference/rollback-method.md) 같은 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 다양한 메서드를 사용하여 로컬 트랜잭션을 지원합니다. 일반적으로 로컬 트랜잭션은 애플리케이션에서 명시적으로 관리하거나 Java Platform, Enterprise Edition(Java EE) 애플리케이션 서버에서 자동으로 관리합니다.

다음 예제에서는`try` 블록에서 두 개의 개별 문으로 구성된 로컬 트랜잭션을 수행합니다. 이들 문은 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스의 Production.ScrapReason 테이블에 대해 실행되고 예외가 발생하지 않을 경우 커밋됩니다. 예외가 발생하면 `catch` 블록의 코드에서 트랜잭션을 롤백합니다.

[!code[JDBC#UnderstandingTransactions1](../../connect/jdbc/codesnippet/Java/understanding-transactions_1.java)]

## <a name="using-distributed-transactions"></a>분산 트랜잭션 사용

분산 트랜잭션은 ACID(원자성, 일관성, 격리성, 영속성)라는 중요한 트랜잭션 처리 속성을 유지하면서 둘 이상의 네트워크 데이터베이스에서 데이터를 업데이트합니다. 분산 트랜잭션 지원은 JDBC 2.0 옵션 API 사양의 JDBC API에 추가되었습니다. 일반적으로 분산 트랜잭션 관리는 Java EE 애플리케이션 서버 환경에서 JTS(Java Transaction Service) 트랜잭션 관리자가 자동으로 수행합니다. 그러나 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서는 임의의 JTA(Java Transaction API) 규격 트랜잭션 관리자 하에서 분산 트랜잭션을 지원합니다.

JDBC 드라이버는 MS DTC([!INCLUDE[msCoName](../../includes/msconame_md.md)] Distributed Transaction Coordinator)와 원활하게 통합되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 진정한 분산 트랜잭션을 지원합니다. MS DTC는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 시스템용으로 [!INCLUDE[msCoName](../../includes/msconame_md.md)]에서 제공하는 분산 트랜잭션 기능입니다. MS DTC는 [!INCLUDE[msCoName](../../includes/msconame_md.md)]의 검증된 트랜잭션 처리 기술을 사용하여 완전한 2단계 분산 커밋 프로토콜 및 분산 트랜잭션 복구와 같은 XA 기능을 지원합니다.

분산 트랜잭션을 사용 하는 방법에 대 한 자세한 내용은 [XA 트랜잭션 이해](../../connect/jdbc/understanding-xa-transactions.md)를 참조 하세요.

## <a name="see-also"></a>관련 항목:

[JDBC 드라이버로 트랜잭션 수행](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
