---
title: 데이터 원본 샘플 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b4a933ee-f2c6-4e0d-a96d-6dd061abf759
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a67bfc72422962f8510fc6486dc37451bfd7224
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-sample"></a>데이터 원본 샘플
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 샘플 응용 프로그램에 연결 하는 방법을 보여 줍니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터 원본 개체를 사용 하 여 데이터베이스입니다. 데이터를 검색 하는 방법을 보여 줍니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 저장된 프로시저를 사용 하 여 데이터베이스입니다.  
  
 이 샘플의 코드 파일 이름은 connectDS.java이며 다음과 같은 위치에 있습니다.  
  
 \<*설치 디렉터리*> \sqljdbc_\<*버전*>\\<*언어*> \samples\connections  
  
## <a name="requirements"></a>요구 사항  
 이 샘플 응용 프로그램을 실행하려면 sqljdbc.jar 파일 또는 sqljdbc4.jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 클래스 경로에 sqljdbc.jar 또는 sqljdbc4.jar에 대한 항목이 없으면 샘플 응용 프로그램에서 일반적인 "클래스를 찾을 수 없습니다." 예외가 발생합니다. 에 대 한 액세스를 해야 합니다는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 예제 데이터베이스. 클래스 경로 설정 하는 방법에 대 한 자세한 내용은 참조 [JDBC 드라이버를 사용 하 여](../../../connect/jdbc/using-the-jdbc-driver.md)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] sqljdbc.jar 및 sqljdbc4.jar 클래스 라이브러리 파일을 기본 Java Runtime Environment (JRE) 설정에 따라 사용 수를 제공 합니다. JAR 파일 선택에 대 한 자세한 내용은 참조 하십시오. [JDBC 드라이버에 대 한 시스템 요구 사항](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)합니다.  
  
## <a name="example"></a>예제  
 다음 예제의 샘플 코드의 setter 메서드를 사용 하 여 다양 한 연결 속성을 설정는 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체를 차례로 호출은 [getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) 의 메서드는 반환할 SQLServerDataSource 개체는 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.  
  
 예제 코드에서는 사용 하는 다음으로 [prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 만들 SQLServerConnection 개체의 메서드는 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 개체, 한 다음은 [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) 저장된 프로시저를 실행 하는 메서드 호출 됩니다.  
  
 마지막으로,이 샘플에서는 사용 된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) executeQuery 메서드는 저장된 프로시저에서 반환 된 결과 반복 하에서 반환 된 개체입니다.  
  
```java
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  
  
public class connectDS {  
  
   public static void main(String[] args) {  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      CallableStatement cstmt = null;  
      ResultSet rs = null;  
  
      try {  
         // Establish the connection.   
         SQLServerDataSource ds = new SQLServerDataSource();  
         ds.setUser("UserName");  
         ds.setPassword("*****");  
         ds.setServerName("localhost");  
         ds.setPortNumber(1433);   
         ds.setDatabaseName("AdventureWorks");  
         con = ds.getConnection();  
  
         // Execute a stored procedure that returns some data.  
         cstmt = con.prepareCall("{call dbo.uspGetEmployeeManagers(?)}");  
         cstmt.setInt(1, 50);  
         rs = cstmt.executeQuery();  
  
         // Iterate through the data in the result set and display it.  
         while (rs.next()) {  
            System.out.println("EMPLOYEE: " + rs.getString("LastName") +   
               ", " + rs.getString("FirstName"));  
            System.out.println("MANAGER: " + rs.getString("ManagerLastName") +   
               ", " + rs.getString("ManagerFirstName"));  
            System.out.println();  
         }  
      }  
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
      finally {  
         if (rs != null) try { rs.close(); } catch(Exception e) {}  
         if (cstmt != null) try { cstmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
         System.exit(1);  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 연결 및 검색](../../../connect/jdbc/connecting-and-retrieving-data.md)  
  
  
