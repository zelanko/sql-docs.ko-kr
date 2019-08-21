---
title: 결과 집합 데이터 샘플 캐싱 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 13a95ebb-996c-4713-a1bd-5834fe22a334
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f59c7010875824b65d6b7d12129056f02537e908
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028419"
---
# <a name="caching-result-set-data-sample"></a>결과 집합 데이터 캐싱 샘플

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 샘플 애플리케이션에서는 데이터베이스에서 대량의 데이터 집합을 검색한 후 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) 메서드를 사용하여 클라이언트에서 캐시할 데이터 행의 수를 제어하는 방법을 보여 줍니다.

> [!NOTE]  
> 클라이언트에서 캐시된 행의 수를 제한하는 것은 결과 집합에 포함된 전체 행 수를 제한한다는 의미가 아닙니다. 결과 집합에 포함된 전체 행 수를 제어하려면 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 개체와 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 개체에서 상속된 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 [setMaxRows](../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) 메서드를 사용합니다.

클라이언트에서 캐시되는 행 수에 제한을 설정하려면 우선 Statement 개체를 만들 때 사용할 커서 유형을 구체적으로 지정하여 Statement 개체 중 하나를 만들 때 서버측 커서를 제일 먼저 사용해야 합니다. 예를 들어 JDBC 드라이버에서 제공하는 커서 유형인 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 사용되는 빨리 감기 및 읽기 전용 서버측 커서입니다.

> [!NOTE]  
> 이 대신에 SQL Server 전용 커서 유형을 사용하려면 selectMethod 연결 문자열 속성 값을 "cursor"로 설정하여 사용하면 됩니다. JDBC 드라이버에서 지 원하는 커서 유형에 대 한 자세한 내용은 [커서 유형 이해](../../connect/jdbc/understanding-cursor-types.md)를 참조 하세요.

Statement 개체에 포함된 쿼리를 실행하고 해당 데이터가 결과 집합으로 클라이언트에 반환된 후에는 setFetchSize 메서드를 호출하여 한 번에 데이터베이스에서 검색할 수 있는 데이터 양을 제어할 수 있습니다. 예를 들어 하나의 테이블에 데이터 행이 100개가 있으며 반입 크기를 10으로 설정한 경우, 클라이언트에서는 항상 10개의 데이터 행만 캐시됩니다. 이와 같은 경우 데이터 처리 속도가 저하되기는 하지만 클라이언트의 메모리를 적게 사용한다는 이점이 있으므로 대량의 데이터를 처리해야 하는 경우 특히 유용합니다.

이 샘플의 코드 파일 이름은 CacheResultSet.java이며 다음과 같은 위치에 있습니다.

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\resultsets
```

## <a name="requirements"></a>요구 사항

이 샘플 애플리케이션을 실행하려면 mssql-jdbc jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 또한 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대한 액세스 권한이 필요합니다. 클래스 경로를 설정 하는 방법에 대 한 자세한 내용은 [JDBC 드라이버 사용](../../connect/jdbc/using-the-jdbc-driver.md)을 참조 하세요.

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 기본 설정된 JRE(Java Runtime Environment)에 따라 사용할 수 있는 mssql-jdbc 클래스 라이브러리 파일을 제공합니다. 선택할 JAR 파일에 대한 자세한 내용은 [System Requirements for the JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)(JDBC Driver 시스템 요구 사항)를 참조하세요.

## <a name="example"></a>예제

다음 예제에서는 샘플 코드가 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 연결됩니다. 그런 다음, [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 개체가 있는 SQL 문을 사용하고 서버측 커서 유형을 지정한 후, SQL 문을 실행하여 반환하는 데이터를 SQLServerResultSet 개체로 지정합니다.

다음으로, 샘플 코드에서는 사용할 페치 크기 및 결과 집합을 인수로 전달하여 사용자 지정 timerTest 메서드를 호출합니다. 그런 다음, timerTest 메서드는 setFetchSize 메서드를 사용하여 결과 집합의 페치 크기를 설정하고 테스트 시작 시간을 설정한 후, `While` 루프를 사용하여 결과 집합을 반복합니다. `While` 루프가 종료됨과 동시에 예제 코드는 테스트 중지 시간을 설정한 다음, 페치 크기, 처리된 행의 수, 테스트 실행에 소요된 시간 등 테스트 결과를 표시합니다.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;

import com.microsoft.sqlserver.jdbc.SQLServerResultSet;

public class CacheResultSet {

    @SuppressWarnings("serial")
    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement(SQLServerResultSet.TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, SQLServerResultSet.CONCUR_READ_ONLY);) {

            String SQL = "SELECT * FROM Sales.SalesOrderDetail;";

            for (int n : new ArrayList<Integer>() {
                {
                    add(1);
                    add(10);
                    add(100);
                    add(1000);
                    add(0);
                }
            }) {
                // Perform a fetch for every nth row in the result set.
                try (ResultSet rs = stmt.executeQuery(SQL)) {
                    timerTest(n, rs);
                }
            }
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void timerTest(int fetchSize,
            ResultSet rs) throws SQLException {

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
    }
}

```

## <a name="see-also"></a>관련 항목:

[결과 집합 작업](../../connect/jdbc/working-with-result-sets.md)
