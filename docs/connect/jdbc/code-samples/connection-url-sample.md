---
title: 연결 URL 샘플 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 96fabc42-59d1-4cc0-93c5-db00cbe55e95
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e6d42e7743e7fba02992e641c18609371b2d1e5a
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028355"
---
# <a name="connection-url-sample"></a>연결 URL 샘플

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

이 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 샘플 애플리케이션에서는 연결 URL을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 방법을 보여 줍니다. 또한 SQL 문을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터를 검색하는 방법도 보여 줍니다.

이 샘플의 코드 파일 이름은 ConnectURL.java이며 다음과 같은 위치에 있습니다.

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\connections
```

## <a name="requirements"></a>요구 사항

이 샘플 애플리케이션을 실행하려면 mssql-jdbc jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 또한 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대한 액세스 권한이 필요합니다. 클래스 경로를 설정 하는 방법에 대 한 자세한 내용은 [JDBC 드라이버 사용](../../../connect/jdbc/using-the-jdbc-driver.md)을 참조 하세요.

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]는 기본 설정된 JRE(Java Runtime Environment)에 따라 사용할 수 있는 mssql-jdbc 클래스 라이브러리 파일을 제공합니다. 선택할 JAR 파일에 대한 자세한 내용은 [JDBC 드라이버 시스템 요구 사항](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)를 참조하세요.

## <a name="example"></a>예제

다음 예제에서 샘플 코드는 연결 URL의 다양한 연결 속성을 설정한 다음, DriverManager 클래스의 getConnection 메서드를 호출하여 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체를 반환합니다.

그런 다음, 샘플 코드에서는 SQLServerConnection 개체의 [createStatement](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 메서드를 사용하여 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체를 만든 후, [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 메서드를 호출하여 SQL 문을 실행합니다.

마지막으로 executeQuery 메서드에서 반환된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 사용하여 SQL 문이 반환한 결과를 반복합니다.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class ConnectURL {
    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();) {
            String SQL = "SELECT TOP 10 * FROM Person.Contact";
            ResultSet rs = stmt.executeQuery(SQL);

            // Iterate through the data in the result set and display it.
            while (rs.next()) {
                System.out.println(rs.getString("FirstName") + " " + rs.getString("LastName"));
            }
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## <a name="see-also"></a>관련 항목:

[데이터 연결 및 검색](../../../connect/jdbc/code-samples/connecting-and-retrieving-data.md)
