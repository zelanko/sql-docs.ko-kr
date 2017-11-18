---
title: "저장점 사용 | Microsoft Docs"
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
ms.assetid: 3b48eb13-32ef-4fb3-8e95-dbc9468c9a44
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f11dd8f60ae5d284b9a2035f3eedafb37ce304e5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-savepoints"></a>저장점 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  저장점은 트랜잭션의 일부를 롤백하는 메커니즘을 제공합니다. 내에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SAVE TRANSACTION savepoint_name 문을 사용 하 여 저장 점을 만들 수 있습니다. 나중에 트랜잭션의 시작 지점으로 롤백하는 대신 저장점으로 롤백하려면 ROLLBACK TRANSACTION savepoint_name 문을 실행합니다.  
  
 저장점은 오류가 발생할 가능성이 거의 없는 경우에 유용합니다. 오류가 자주 발생하지 않는 경우 업데이트 전에 각 트랜잭션을 테스트하여 업데이트가 유효한지 확인하는 것보다 저장점을 사용하여 트랜잭션의 일부를 롤백하는 것이 더 효율적입니다. 업데이트와 롤백은 비용이 많이 드는 작업이므로 저장점은 오류가 발생할 가능성이 적고 업데이트 전에 미리 유효성을 검사하는 데 비교적 비용이 많이 드는 경우에만 효과적입니다.  
  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 통해 저장 점을 사용할 수 있도록 지원는 [setSavepoint](../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스입니다. SetSavepoint 메서드를 사용 하 여 현재 트랜잭션 내에서 명명 되거나 명명 되지 않은 저장 점을 만들 수 있습니다 및 메서드는 반환 된 [SQLServerSavepoint](../../connect/jdbc/reference/sqlserversavepoint-class.md) 개체입니다. 또한 한 트랜잭션에 여러 개의 저장점을 만들 수 있습니다. 트랜잭션을 지정한 저장 점으로 롤백하려면, SQLServerSavepoint 개체를 전달할 수 있습니다는 [rollback (java.sql.Savepoint)](../../connect/jdbc/reference/rollback-method-java-sql-savepoint.md) 메서드.  
  
 다음 예제에서는 저장 점을에 두 개의 개별 문으로 구성 된 로컬 트랜잭션을 수행 하는 동안 사용 되는 `try` 블록입니다. 문은 Production.ScrapReason 테이블에 대해 실행 되는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스와 저장 점을 두 번째 문을 롤백하는 데 사용 합니다. 이렇게 하면 첫 번째 문만 데이터베이스에 커밋됩니다.  
  
 [!code[JDBC#UsingSavepoints1](../../connect/jdbc/codesnippet/Java/using-savepoints_1.java)]  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 트랜잭션 수행](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  

