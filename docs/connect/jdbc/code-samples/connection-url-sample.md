---
title: "연결 URL 샘플 | Microsoft Docs"
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
ms.assetid: 96fabc42-59d1-4cc0-93c5-db00cbe55e95
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bbb062925c0c0ee1c14c0f2190101c8967d0c65
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="connection-url-sample"></a>연결 URL 샘플
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 샘플 응용 프로그램에 연결 하는 방법을 보여 줍니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 연결 URL을 사용 하 여 데이터베이스입니다. 데이터를 검색 하는 방법을 보여 줍니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SQL 문을 사용 하 여 데이터베이스입니다.  
  
 이 샘플의 코드 파일 이름은 connectURL.java이며 다음과 같은 위치에 있습니다.  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \samples\connections  
  
## <a name="requirements"></a>요구 사항  
 이 샘플 응용 프로그램을 실행하려면 sqljdbc.jar 파일 또는 sqljdbc4.jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 클래스 경로에 sqljdbc.jar 또는 sqljdbc4.jar에 대한 항목이 없으면 샘플 응용 프로그램에서 일반적인 "클래스를 찾을 수 없습니다." 예외가 발생합니다. 에 대 한 액세스를 해야 합니다는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 예제 데이터베이스. 클래스 경로 설정 하는 방법에 대 한 자세한 내용은 참조 [JDBC 드라이버를 사용 하 여](../../../connect/jdbc/using-the-jdbc-driver.md)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] sqljdbc.jar 및 sqljdbc4.jar 클래스 라이브러리 파일을 기본 Java Runtime Environment (JRE) 설정에 따라 사용 수를 제공 합니다. JAR 파일 선택에 대 한 자세한 내용은 참조 하십시오. [JDBC 드라이버에 대 한 시스템 요구 사항](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)합니다.  
  
## <a name="example"></a>예제  
 다음 예제의 샘플 코드 연결 URL에 다양 한 연결 속성을 설정 하 고 반환할 DriverManager 클래스의 getConnection 메서드를 호출 하는 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.  
  
 예제 코드에서는 사용 하는 다음으로 [createStatement](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 만들 SQLServerConnection 개체의 메서드는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체, 한 다음은 [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 메서드 SQL 문을 실행 하 라고 합니다.  
  
 마지막으로,이 샘플에서는 사용 된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) SQL 문에 의해 반환 된 결과 반복 하는 executeQuery 메서드에서 반환 된 개체입니다.  
  
```java  
import java.sql.*;  
  
public class connectURL {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
         "databaseName=AdventureWorks;user=UserName;password=*****";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
  
         // Create and execute an SQL statement that returns some data.  
         String SQL = "SELECT TOP 10 * FROM Person.Contact";  
         stmt = con.createStatement();  
         rs = stmt.executeQuery(SQL);  
  
         // Iterate through the data in the result set and display it.  
         while (rs.next()) {  
            System.out.println(rs.getString(4) + " " + rs.getString(6));  
         }  
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
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 연결 및 검색](../../../connect/jdbc/connecting-and-retrieving-data.md)  
  
  

