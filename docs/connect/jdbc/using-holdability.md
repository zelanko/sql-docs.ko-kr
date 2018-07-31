---
title: 유지 기능을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: aa48306c-e7a0-4dcb-af21-9ebb6898e45a
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0bf10226926d3c5df21d546de042095defbbe812
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37982095"
---
# <a name="using-holdability"></a>유지 기능 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  기본적으로 트랜잭션 내에 만들어진 결과 집합은 트랜잭션이 데이터베이스에 커밋되거나 롤백된 후 열린 상태로 남아 있습니다. 그러나 트랜잭션이 커밋된 후 결과 집합을 닫으면 유용한 경우가 있습니다. 이를 위해 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 결과 집합 유지 기능을 사용할 수 있도록 지원합니다.  
  
 결과 집합 유지 기능은 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [setHoldability](../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 메서드를 사용하여 설정할 수 있습니다. 결과 집합 유지 기능 상수를 ResultSet.HOLD_CURSORS_OVER_COMMIT setHoldability 메서드를 사용 하 여 유지 기능을 설정 하는 경우 또는 ResultSet.CLOSE_CURSORS_AT_COMMIT를 사용할 수 있습니다.  
  
 또한 JDBC 드라이버는 Statement 개체를 만들 때 유지 기능을 설정할 수 있도록 지원합니다. 결과 집합 유지 기능 매개 변수의 오버로드가 있는 Statement 개체를 만들 때 statement 개체의 유지 기능은 연결의 유지 기능과 일치해야 합니다. 일치하지 않으면 예외가 발생합니다. 이렇게 되는 이유는 SQL Server가 연결 수준에서만 유지 기능을 지원하기 때문입니다.  
  
 결과 집합의 유지 기능이란 서버측 커서에 대해서만 결과 집합을 만들 때 해당 결과 집합에 연결되는 SQLServerConnection 개체의 유지 기능입니다. 클라이언트 쪽 커서에는 적용되지 않습니다. 클라이언트 쪽 커서를 사용 하 여 모든 결과 집합 유지 기능 값은 ResultSet.HOLD_CURSORS_OVER_COMMIT의 경우 항상 됩니다.  
  
 서버 커서의 경우 SQL Server 2005 이상과 연결되어 있을 때 유지 기능을 설정하면 해당 연결에서 만들어질 새 결과 집합의 유지 기능만 영향을 받게 됩니다. 즉 유지 기능을 설정해도 이미 만들어졌거나 해당 연결에서 이미 열려 있는 결과 집합은 영향을 받지 않습니다. 그러나 SQL Server 2000의 경우에는 유지 기능을 설정하면 기존 결과 집합과 해당 연결에서 만들어질 새 결과 집합의 유지 기능이 모두 영향을 받습니다.  
  
 다음 예제에서는 `try` 블록에서 두 개의 별도 명령문으로 구성된 로컬 트랜잭션을 수행하면서 결과 집합 유지 기능을 설정합니다. 이들 명령문은 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스의 Production.ScrapReason 테이블에 대해 실행됩니다. 먼저 이 예에서는 자동 커밋을 **false**로 설정하여 수동 트랜잭션 모드로 전환합니다. 자동 커밋 모드가 해제되면 응용 프로그램이 명시적으로 [commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) 메서드를 호출할 때까지 SQL 문이 커밋되지 않습니다. 예외가 발생하면 catch 블록의 코드에서 트랜잭션을 롤백합니다.  
  
 [!code[JDBC#UsingHoldability1](../../connect/jdbc/codesnippet/Java/using-holdability_1.java)]  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버로 트랜잭션 수행](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
