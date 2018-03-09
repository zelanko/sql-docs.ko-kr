---
title: "결과 집합 데이터 샘플 캐싱 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13a95ebb-996c-4713-a1bd-5834fe22a334
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 131bf443f88c0071dcb158fb67c997d6b0c57de2
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="caching-result-set-data-sample"></a>결과 집합 데이터 샘플 캐싱
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  이 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 샘플 응용 프로그램에는 데이터베이스에서 큰 데이터 집합을 검색 한 후 사용 하 여 클라이언트에서 캐시할 데이터 행의 수를 제어 하는 방법을 보여 줍니다는 [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) 의 메서드는 [ SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
> [!NOTE]  
>  클라이언트에서 캐시된 행의 수를 제한하는 것은 결과 집합에 포함된 전체 행 수를 제한한다는 의미가 아닙니다. 사용 하 여 결과 집합에 포함 된 행의 총 수를 제어 하려면는 [setMaxRows](../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) 의 메서드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 둘 다에서 상속 된 개체는 [ SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 및 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 개체입니다.  
  
 클라이언트에 캐시 행의 수에 제한을 설정 하려면 먼저 사용 해야 서버 쪽 커서 문 개체를 만들 때 사용할 커서 유형을 구체적으로 지정 하 여 문 개체 중 하나를 만들 때. JDBC 드라이버는 빠른 정방향 전용 인 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY 커서 유형을 제공 하는 예를 들어 읽기 전용 서버측 커서와 함께 사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스.  
  
> [!NOTE]  
>  이 대신에 SQL Server 전용 커서 유형을 사용하려면 selectMethod 연결 문자열 속성 값을 "cursor"로 설정하여 사용하면 됩니다. JDBC 드라이버에서 지 원하는 커서 유형에 대 한 자세한 내용은 참조 하십시오. [커서 종류 이해](../../connect/jdbc/understanding-cursor-types.md)합니다.  
  
 문 개체에 포함 된 쿼리를 실행 한 후 데이터는 클라이언트에는 결과 집합으로 반환에 한 번에 데이터베이스에서 검색 된 데이터의 양을 제어 하려면 setFetchSize 메서드를 호출할 수 있습니다. 예를 들어 하나의 테이블에 데이터 행이 100개가 있으며 반입 크기를 10으로 설정한 경우, 클라이언트에서는 항상 10개의 데이터 행만 캐시됩니다. 이와 같은 경우 데이터 처리 속도가 저하되기는 하지만 클라이언트의 메모리를 적게 사용한다는 이점이 있으므로 대량의 데이터를 처리해야 하는 경우 특히 유용합니다.  
  
 이 샘플의 코드 파일 이름은 cacheRS.java이며 다음과 같은 위치에 있습니다.  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \samples\resultsets  
  
## <a name="requirements"></a>요구 사항  
 이 샘플 응용 프로그램을 실행하려면 sqljdbc.jar 파일 또는 sqljdbc4.jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 클래스 경로에 sqljdbc.jar 또는 sqljdbc4.jar에 대한 항목이 없으면 샘플 응용 프로그램에서 일반적인 "클래스를 찾을 수 없습니다." 예외가 발생합니다. 에 대 한 액세스를 해야 합니다는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스. 클래스 경로 설정 하는 방법에 대 한 자세한 내용은 참조 [JDBC 드라이버를 사용 하 여](../../connect/jdbc/using-the-jdbc-driver.md)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] sqljdbc.jar 및 sqljdbc4.jar 클래스 라이브러리 파일을 기본 Java Runtime Environment (JRE) 설정에 따라 사용 수를 제공 합니다. JAR 파일 선택에 대 한 자세한 내용은 참조 하십시오. [JDBC 드라이버에 대 한 시스템 요구 사항](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 샘플 코드에서는 연결에는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스. 포함 하는 SQL 문을 사용 하 여 다음의 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 개체, 서버 쪽 커서 유형을 지정 다음 SQL 문을 실행 하 고 SQLServerResultSet 개체에 반환 하는 데이터입니다.  
  
 다음으로, 예제 코드 및 사용 하 여 결과 집합의 반입 크기를 인수로 전달 timerTest 사용자 지정 메서드를 호출 합니다. TimerTest 메서드 setFetchSize 메서드를 사용 하 여 결과 집합의 반입 크기를 설정는 테스트의 시작 시간을 설정 하 고 다음 결과 집합을 반복는 `While` 루프입니다. 즉시는 `While` 루프가 종료 됨, 코드, 테스트 중지 시간을 설정 하 고 다음 반입 크기, 처리 된 행의 수를 포함 하 여 테스트의 결과 표시 하 고 테스트 실행에 걸린 시간입니다.  
  
```java
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.SQLServerResultSet;  
  
public class cacheRS {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
            "databaseName=AdventureWorks;integratedSecurity=true;";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
  
         // Create and execute an SQL statement that returns a large  
         // set of data and then display it.  
         String SQL = "SELECT * FROM Sales.SalesOrderDetail;";  
         stmt = con.createStatement(SQLServerResultSet.TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, +  
               SQLServerResultSet.CONCUR_READ_ONLY);  
  
         // Perform a fetch for every row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(1, rs);  
         rs.close();  
  
         // Perform a fetch for every tenth row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(10, rs);  
         rs.close();  
  
         // Perform a fetch for every 100th row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(100, rs);  
         rs.close();  
  
         // Perform a fetch for every 1000th row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(1000, rs);  
         rs.close();  
  
         // Perform a fetch for every 128th row (the default) in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(0, rs);  
         rs.close();  
      }  
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
  
      finally {  
         if (rs != null) try { rs.close(); } catch(Exception e) {}  
         if (stmt != null) try { stmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
      }  
   }  
  
   private static void timerTest(int fetchSize, ResultSet rs) {  
      try {  
  
         // Declare the variables for tracking the row count and elapsed time.  
         int rowCount = 0;  
         long startTime = 0;  
         long stopTime = 0;  
         long runTime = 0;  
  
         // Set the fetch size then iterate through the result set to  
         // cache the data locally.  
         rs.setFetchSize(fetchSize);  
         startTime = System.currentTimeMillis();  
         while (rs.next()) {  
            rowCount++;  
         }  
         stopTime = System.currentTimeMillis();  
         runTime = stopTime - startTime;  
  
         // Display the results of the timer test.  
         System.out.println("FETCH SIZE: " + rs.getFetchSize());  
         System.out.println("ROWS PROCESSED: " + rowCount);  
         System.out.println("TIME TO EXECUTE: " + runTime);  
         System.out.println();  
  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [결과 집합 작업](../../connect/jdbc/working-with-result-sets.md)  
  
  
