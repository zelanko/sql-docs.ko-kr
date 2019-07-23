---
title: 일괄 작업 수행 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1a576d95-7da6-4b7b-8b32-59e5b4d354c4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 244c20b2fb7721d117557581068791e1a2d99d14
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956220"
---
# <a name="performing-batch-operations"></a>일괄 작업 수행
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 여러 번 업데이트할 때 성능을 향상시키기 위해 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 여러 업데이트를 하나의 작업으로 전송하는 기능을 지원하며, 이를 일괄 처리(batch)라고 합니다.  
  
 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 및 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스는 모두 일괄 처리 업데이트를 전송하는 데 사용할 수 있습니다. [addBatch](../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md) 메서드는 명령을 추가하는 데 사용됩니다. [clearBatch](../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md) 메서드는 명령 목록을 지우는 데 사용됩니다. [executeBatch](../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md) 메서드는 처리할 모든 명령을 전송하는 데 사용됩니다. 단순 업데이트 횟수를 반환하는 DDL(데이터 정의 언어) 및 DML(데이터 조작 언어) 문만 일괄 처리의 일부로 실행할 수 있습니다.  
  
 executeBatch 메서드는 각 명령의 업데이트 횟수에 해당하는 **int** 값 배열을 반환합니다. 명령 중 하나가 실패 하면 BatchUpdateException이 throw 되며, BatchUpdateException 클래스의 getUpdateCounts 메서드를 사용 하 여 업데이트 횟수 배열을 검색 해야 합니다. 명령 하나가 실패하더라도 드라이버는 계속해서 나머지 명령을 처리합니다. 그러나 명령에 구문 오류가 있으면 일괄 처리에 있는 문이 실패합니다.  
  
> [!NOTE]  
>  업데이트 횟수를 사용할 필요가 없다면 SET NOCOUNT ON 문을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 먼저 발급할 수 있습니다. 이렇게 하면 네트워크 트래픽이 감소하고 응용 프로그램의 성능도 향상됩니다.  
  
 예를 들어 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 다음과 같은 테이블을 만듭니다.  
  
```sql
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
```  
  
 다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대해 열린 연결을 함수로 전달하며, addBatch 메서드를 사용하여 실행할 명령문을 만들고, executeBatch 메서드를 호출하여 일괄 처리를 데이터베이스로 전송합니다.  
  
```java
public static void executeBatchUpdate(Connection con) {  
   try {  
      Statement stmt = con.createStatement();  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('X', 100)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Y', 200)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Z', 300)");  
      int[] updateCounts = stmt.executeBatch();  
      stmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버에서 문 사용](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
