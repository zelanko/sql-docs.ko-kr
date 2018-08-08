---
title: 결과 집합 데이터 샘플 수정 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b5ae54dc-2a79-4664-bb21-cacdb7d745e1
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f43960439d015bb9c23598d1182c13ced74347d2
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39454347"
---
# <a name="modifying-result-set-data-sample"></a>결과 집합 데이터 샘플 수정

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

이 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 응용 프로그램 예제에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터베이스에서 업데이트 가능한 데이터 집합을 검색하는 방법을 보여 줍니다. 그런 다음, [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 메서드를 사용하여 데이터 행을 데이터 집합에 삽입하고 수정한 후, 마지막에는 데이터 집합에서 삭제합니다.

이 샘플의 코드 파일 이름은 UpdateResultSet.java이며 다음과 같은 위치에 있습니다.

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\resultsets
```

## <a name="requirements"></a>요구 사항

이 샘플 응용 프로그램을 실행하려면 mssql-jdbc jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 또한 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대한 액세스 권한이 필요합니다. 클래스 경로 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. [JDBC 드라이버를 사용 하 여](../../../connect/jdbc/using-the-jdbc-driver.md)입니다.

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]는 기본 설정된 JRE(Java Runtime Environment)에 따라 사용할 수 있는 mssql-jdbc 클래스 라이브러리 파일을 제공합니다. JAR 파일을 선택 하는 방법에 대 한 자세한 내용은 참조 하세요. [JDBC 드라이버 시스템 요구 사항](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)합니다.

## <a name="example"></a>예제

다음 예제에서는 샘플 코드가 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 연결됩니다. 그런 다음, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체를 포함하는 SQL 문을 사용하여 SQL 문을 실행하고 반환되는 데이터를 업데이트 가능한 SQLServerResultSet 개체로 지정합니다.

그런 다음, [moveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) 메서드를 사용하여 결과 집합 커서를 삽입 행으로 이동하고, 일련의 [updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) 메서드를 사용하여 데이터를 새로운 행에 삽입한 후, [insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) 메서드를 호출하여 새로운 데이터 행을 데이터베이스에 다시 보관합니다.

새로운 데이터 행을 삽입한 후 샘플 코드는 SQL 문을 사용하여 이전에 삽입한 행을 검색한 다음, updateString 및 [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 메서드 조합을 사용하여 데이터 행을 업데이트하고 데이터베이스에 다시 보관합니다.

마지막으로 앞서 업데이트한 데이터 행을 검색한 다음, [deleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md) 메서드를 사용하여 이 데이터 행을 데이터베이스에서 삭제합니다.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class UpdateResultSet {

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);) {

            // Create and execute an SQL statement, retrieving an updateable result set.
            String SQL = "SELECT * FROM HumanResources.Department;";
            ResultSet rs = stmt.executeQuery(SQL);

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
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void displayRow(String title,
            ResultSet rs) throws SQLException {
        System.out.println(title);
        while (rs.next()) {
            System.out.println(rs.getString("Name") + " : " + rs.getString("GroupName"));
            System.out.println();
        }
    }
}

```

## <a name="see-also"></a>참고 항목

[결과 집합 작업](../../../connect/jdbc/code-samples/working-with-result-sets.md)
