---
title: "결과 집합 데이터 샘플 수정 | Microsoft Docs"
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
ms.assetid: b5ae54dc-2a79-4664-bb21-cacdb7d745e1
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f8f0cc4e1a8758557a84c065f9143b7c8753e1e4
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="modifying-result-set-data-sample"></a>결과 집합 데이터 샘플 수정
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  이 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 샘플 응용 프로그램에서 데이터의 업데이트 가능한 집합을 검색 하는 방법을 보여 줍니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다. 그런 다음 메서드를 사용 하 여 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 삽입, 수정 및 다음 데이터 집합에서 마지막으로 데이터의 행을 삭제 합니다.  
  
 이 샘플의 코드 파일 이름은 updateRS.java이며 다음과 같은 위치에 있습니다.  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \samples\resultsets  
  
## <a name="requirements"></a>요구 사항  
 이 샘플 응용 프로그램을 실행하려면 sqljdbc.jar 파일 또는 sqljdbc4.jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 클래스 경로에 sqljdbc.jar 또는 sqljdbc4.jar에 대한 항목이 없으면 샘플 응용 프로그램에서 일반적인 "클래스를 찾을 수 없습니다." 예외가 발생합니다. 에 대 한 액세스를 해야 합니다는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스. 클래스 경로 설정 하는 방법에 대 한 자세한 내용은 참조 [JDBC 드라이버를 사용 하 여](../../connect/jdbc/using-the-jdbc-driver.md)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] sqljdbc.jar 및 sqljdbc4.jar 클래스 라이브러리 파일을 기본 Java Runtime Environment (JRE) 설정에 따라 사용 수를 제공 합니다. JAR 파일 선택에 대 한 자세한 내용은 참조 하십시오. [JDBC 드라이버에 대 한 시스템 요구 사항](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 샘플 코드에서는 연결에는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스. 다음을 포함 하는 SQL 문을 사용 하는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) SQL 문을 실행 하 고는 업데이트 가능한 SQLServerResultSet 개체에 반환 하는 데이터 개체입니다.  
  
 다음으로, 예제 코드를 사용는 [moveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) 결과 집합 커서를 삽입 행으로 이동 하는 방법은 일련의를 사용 하 여 [updateString](../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) 새 행에 데이터를 삽입 하는 메서드를 호출 하 여 [insertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) 메서드를 다시 데이터베이스에 데이터의 새 행을 유지 합니다.  
  
 데이터의 새 행을 삽입 한 후 샘플 코드 SQL 문을 사용 하 여 앞서 삽입된 한 행을 검색 하 고 다음 updateString 조합을 사용 하 여 및 [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 로 다시 데이터의 행을 업데이트 하 고 보관 하는 메서드 데이터베이스입니다.  
  
 마지막으로 샘플 코드는 데이터의 이전에 업데이트 된 행을 검색 하 고 다음을 사용 하 여 데이터베이스에서 삭제 된 [deleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md) 메서드.  
  
```java
import java.sql.*;  
  
public class updateRS {  
  
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
  
         // Create and execute an SQL statement, retrieving an updateable result set.  
         String SQL = "SELECT * FROM HumanResources.Department;";  
         stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);  
         rs = stmt.executeQuery(SQL);  
  
         // Insert a row of data.  
         rs.moveToInsertRow();  
         rs.updateString("Name", "Accounting");  
         rs.updateString("GroupName", "Executive General and Administration");  
         rs.updateString("ModifiedDate", "08/01/2006");  
         rs.insertRow();  
  
         // Retrieve the inserted row of data and display it.  
         SQL = "SELECT * FROM HumanResources.Department WHERE Name = 'Accounting';";  
         rs = stmt.executeQuery(SQL);  
         displayRow("ADDED ROW", rs);  
  
         // Update the row of data.  
         rs.first();  
         rs.updateString("GroupName", "Finance");  
         rs.updateRow();  
  
         // Retrieve the updated row of data and display it.  
         rs = stmt.executeQuery(SQL);  
         displayRow("UPDATED ROW", rs);  
  
         // Delete the row of data.  
         rs.first();  
         rs.deleteRow();  
         System.out.println("ROW DELETED");  
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
  
   private static void displayRow(String title, ResultSet rs) {  
      try {  
         System.out.println(title);  
         while (rs.next()) {  
            System.out.println(rs.getString("Name") + " : " + rs.getString("GroupName"));  
            System.out.println();  
         }  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [결과 집합 작업](../../connect/jdbc/working-with-result-sets.md)  
  
  
