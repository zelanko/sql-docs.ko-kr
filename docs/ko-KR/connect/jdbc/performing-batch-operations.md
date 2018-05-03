---
title: 일괄 처리 작업 수행 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1a576d95-7da6-4b7b-8b32-59e5b4d354c4
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1cc71b8b547be9a8b5e62e213d1da4cb8b261837
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="performing-batch-operations"></a>일괄 작업 수행
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  여러 번 업데이트할 때 성능을 향상 시키기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 라고도 하는 일괄 처리 작업의 단일 단위로 여러 업데이트를 전송 하는 기능을 제공 합니다.  
  
 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), 및 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스를 모두 사용 일괄 처리 업데이트를 제출할 수 있습니다. [addBatch](../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md) 메서드는 명령을 추가 하는 데 사용 됩니다. [clearBatch](../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md) 메서드 명령 목록을 지우는 데 사용 됩니다. [executeBatch](../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md) 메서드는 처리할 모든 명령을 전송 하는 데 사용 됩니다. 단순 업데이트 횟수를 반환하는 DDL(데이터 정의 언어) 및 DML(데이터 조작 언어) 문만 일괄 처리의 일부로 실행할 수 있습니다.  
  
 ExecuteBatch 메서드 배열을 반환 **int** 각 명령의 업데이트 횟수에 해당 하는 값입니다. 명령 중 하나가 실패 하면는 BatchUpdateException throw 되지 않으며 업데이트 횟수 배열을 검색 BatchUpdateException 클래스의 getUpdateCounts 메서드를 사용 해야 합니다. 명령 하나가 실패하더라도 드라이버는 계속해서 나머지 명령을 처리합니다. 그러나 명령에 구문 오류가 있으면 일괄 처리에 있는 문이 실패합니다.  
  
> [!NOTE]  
>  업데이트 횟수를 사용 해야 하는 경우에 SET NOCOUNT ON 문을 먼저 발급할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 이렇게 하면 네트워크 트래픽이 감소하고 응용 프로그램의 성능도 향상됩니다.  
  
 예를 들어에 다음 테이블을 만듭니다는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
```  
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
```  
  
 다음 예에서는 열린 연결에에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] addBatch 메서드는 실행 될 문을 작성 하는 데 되며 데이터베이스에 일괄 처리를 제출 하려면 executeBatch 메서드는 예제 데이터베이스 함수에 전달 됩니다.  
  
```  
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
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버에서 문 사용](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
