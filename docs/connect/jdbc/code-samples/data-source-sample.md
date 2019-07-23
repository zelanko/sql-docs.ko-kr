---
title: 데이터 원본 샘플 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b4a933ee-f2c6-4e0d-a96d-6dd061abf759
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 61ad7ad7a2de372d4b223986d141fee76882d512
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957214"
---
# <a name="data-source-sample"></a>데이터 원본 샘플

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

이 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 샘플 애플리케이션에서는 데이터 원본 개체를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 방법을 보여 줍니다. 또한 저장 프로시저를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터를 검색하는 방법도 보여 줍니다.

이 샘플의 코드 파일 이름은 ConnectDataSource.java이며 다음과 같은 위치에 있습니다.

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\connections
```

## <a name="requirements"></a>요구 사항

이 샘플 애플리케이션을 실행하려면 mssql-jdbc jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 또한 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대한 액세스 권한이 필요합니다. 클래스 경로를 설정 하는 방법에 대 한 자세한 내용은 [JDBC 드라이버 사용](../../../connect/jdbc/using-the-jdbc-driver.md)을 참조 하세요.

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]는 기본 설정된 JRE(Java Runtime Environment)에 따라 사용할 수 있는 mssql-jdbc 클래스 라이브러리 파일을 제공합니다. 선택할 JAR 파일에 대한 자세한 내용은 [System Requirements for the JDBC Driver](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)(JDBC Driver 시스템 요구 사항)를 참조하세요.

## <a name="example"></a>예제

다음 예제의 샘플 코드에서는 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체의 setter 메서드를 사용하여 다양한 연결 속성을 설정한 다음, SQLServerDataSource 개체의 [getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) 메서드를 호출하여 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체를 반환합니다.

그런 다음, SQLServerConnection 개체의 [prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 메서드를 사용하여 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 개체를 만든 후, [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) 메서드를 호출하여 저장 프로시저를 실행합니다.

마지막으로 executeQuery 메서드에서 반환된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 사용하여 저장 프로시저가 반환한 결과를 반복합니다.

```java
import java.sql.CallableStatement;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class ConnectDataSource {

    public static void main(String[] args) {

        // Create datasource.
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setUser("<user>");
        ds.setPassword("<password>");
        ds.setServerName("<server>");
        ds.setPortNumber(Integer.parseInt("<port>"));
        ds.setDatabaseName("AdventureWorks");

        try (Connection con = ds.getConnection();
                CallableStatement cstmt = con.prepareCall("{call dbo.uspGetEmployeeManagers(?)}");) {
            // Execute a stored procedure that returns some data.
            cstmt.setInt(1, 50);
            ResultSet rs = cstmt.executeQuery();

            // Iterate through the data in the result set and display it.
            while (rs.next()) {
                System.out.println("EMPLOYEE: " + rs.getString("LastName") + ", " + rs.getString("FirstName"));
                System.out.println("MANAGER: " + rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));
                System.out.println();
            }
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## <a name="see-also"></a>참고 항목

[데이터 연결 및 검색](../../../connect/jdbc/code-samples/connecting-and-retrieving-data.md)
