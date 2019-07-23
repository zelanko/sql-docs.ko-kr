---
title: 저장점 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3b48eb13-32ef-4fb3-8e95-dbc9468c9a44
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9212e2de7a093b92c51489bb17623a2120e5ce35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916227"
---
# <a name="using-savepoints"></a>저장점 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

저장점은 트랜잭션의 일부를 롤백하는 메커니즘을 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 SAVE TRANSACTION savepoint_name 문을 사용하여 저장점을 만듭니다. 나중에 트랜잭션의 시작 지점으로 롤백하는 대신 저장점으로 롤백하려면 ROLLBACK TRANSACTION savepoint_name 문을 실행합니다.

저장점은 오류가 발생할 가능성이 거의 없는 경우에 유용합니다. 오류가 자주 발생하지 않는 경우 업데이트 전에 각 트랜잭션을 테스트하여 업데이트가 유효한지 확인하는 것보다 저장점을 사용하여 트랜잭션의 일부를 롤백하는 것이 더 효율적입니다. 업데이트와 롤백은 비용이 많이 드는 작업이므로 저장점은 오류가 발생할 가능성이 적고 업데이트 전에 미리 유효성을 검사하는 데 비교적 비용이 많이 드는 경우에만 효과적입니다.

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [setSavepoint](../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md) 메서드를 통해 저장점을 사용할 수 있도록 지원합니다. setSavepoint 메서드를 사용하면 현재 트랜잭션 내에 명명되거나 명명되지 않은 저장점을 만들 수 있으며, 그러면 이 메서드가 [SQLServerSavepoint](../../connect/jdbc/reference/sqlserversavepoint-class.md) 개체를 반환합니다. 또한 한 트랜잭션에 여러 개의 저장점을 만들 수 있습니다. 트랜잭션을 지정한 저장점으로 롤백하려면 SQLServerSavepoint 개체를 [rollback (java.sql.Savepoint)](../../connect/jdbc/reference/rollback-method-java-sql-savepoint.md) 메서드로 전달합니다.

다음 예제에서는 `try` 블록에서 두 개의 개별 명령문으로 구성된 로컬 트랜잭션을 수행하는 과정에 저장점을 사용합니다. 이들 명령문은 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 있는 Production.ScrapReason 테이블에 대해 실행되며 저장점은 두 번째 명령문을 롤백하는 데 사용됩니다. 이렇게 하면 첫 번째 문만 데이터베이스에 커밋됩니다.

[!code[JDBC#UsingSavepoints1](../../connect/jdbc/codesnippet/Java/using-savepoints_1.java)]

## <a name="see-also"></a>참고 항목

[JDBC 드라이버로 트랜잭션 수행](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
