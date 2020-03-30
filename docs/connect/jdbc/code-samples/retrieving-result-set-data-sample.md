---
title: 결과 집합 데이터 검색 샘플 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1b190c36-3d38-49a2-8599-612329675851
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2cca84ebc59bdefb43e2aa1a5f8b62bbf6301d51
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69028368"
---
# <a name="retrieving-result-set-data-sample"></a>결과 집합 데이터 검색 샘플

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

이 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 샘플 애플리케이션에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터 집합을 검색한 다음, 해당 데이터를 표시하는 방법을 보여 줍니다.

이 샘플의 코드 파일 이름은 RetrieveResultSet.java이며 다음과 같은 위치에 있습니다.

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\resultsets  
```

## <a name="requirements"></a>요구 사항

이 샘플 애플리케이션을 실행하려면 mssql-jdbc jar 파일을 포함하도록 클래스 경로를 설정해야 합니다. 또한 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대한 액세스 권한이 필요합니다. 클래스 경로를 설정하는 방법에 대한 자세한 내용은 [JDBC 드라이버 사용](../../../connect/jdbc/using-the-jdbc-driver.md)을 참조하세요.

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]는 기본 설정된 JRE(Java Runtime Environment)에 따라 사용할 수 있는 mssql-jdbc 클래스 라이브러리 파일을 제공합니다. 선택할 JAR 파일에 대한 자세한 내용은 [JDBC 드라이버 시스템 요구 사항](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)을 참조하세요.

## <a name="example"></a>예제

다음 예제에서는 샘플 코드가 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 연결됩니다. 그런 다음, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체를 포함하는 SQL 문을 사용하여 SQL 문을 실행하고 반환되는 데이터를 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 지정합니다.

그런 다음, 샘플 코드에서는 사용자 지정 displayRow 메서드를 호출하여 결과 집합에 있는 데이터 행을 반복하고 [getString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) 메서드를 사용하여 데이터를 표시합니다.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class RetrieveRS {

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();) {
            createTable(stmt);
        String SQL = "SELECT * FROM Production.Product;";
            ResultSet rs = stmt.executeQuery(SQL);
            displayRow("PRODUCTS", rs);
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
            System.out.println(rs.getString("ProductNumber") + " : " + rs.getString("Name"));
        }
    }

    private static void createTable(Statement stmt) throws SQLException {
        stmt.execute("if exists (select * from sys.objects where name = 'Product_JDBC_Sample')"
                + "drop table Product_JDBC_Sample");

        String sql = "CREATE TABLE [Product_JDBC_Sample](" + "[ProductID] [int] IDENTITY(1,1) NOT NULL,"
                + "[Name] [varchar](30) NOT NULL," + "[ProductNumber] [nvarchar](25) NOT NULL,"
                + "[MakeFlag] [bit] NOT NULL," + "[FinishedGoodsFlag] [bit] NOT NULL," + "[Color] [nvarchar](15) NULL,"
                + "[SafetyStockLevel] [smallint] NOT NULL," + "[ReorderPoint] [smallint] NOT NULL,"
                + "[StandardCost] [money] NOT NULL," + "[ListPrice] [money] NOT NULL," + "[Size] [nvarchar](5) NULL,"
                + "[SizeUnitMeasureCode] [nchar](3) NULL," + "[WeightUnitMeasureCode] [nchar](3) NULL,"
                + "[Weight] [decimal](8, 2) NULL," + "[DaysToManufacture] [int] NOT NULL,"
                + "[ProductLine] [nchar](2) NULL," + "[Class] [nchar](2) NULL," + "[Style] [nchar](2) NULL,"
                + "[ProductSubcategoryID] [int] NULL," + "[ProductModelID] [int] NULL,"
                + "[SellStartDate] [datetime] NOT NULL," + "[SellEndDate] [datetime] NULL,"
                + "[DiscontinuedDate] [datetime] NULL," + "[rowguid] [uniqueidentifier] ROWGUIDCOL  NOT NULL,"
                + "[ModifiedDate] [datetime] NOT NULL,)";

        stmt.execute(sql);

        sql = "INSERT Product_JDBC_Sample VALUES ('Adjustable Time','AR-5381','0','0',NULL,'1000','750','0.00','0.00',NULL,NULL,NULL,NULL,'0',NULL,NULL,NULL,NULL,NULL,'2008-04-30 00:00:00.000',NULL,NULL,'694215B7-08F7-4C0D-ACB1-D734BA44C0C8','2014-02-08 10:01:36.827') ";
        stmt.execute(sql);

        sql = "INSERT Product_JDBC_Sample VALUES ('ML Bottom Bracket','BB-8107','0','0',NULL,'1000','750','0.00','0.00',NULL,NULL,NULL,NULL,'0',NULL,NULL,NULL,NULL,NULL,'2008-04-30 00:00:00.000',NULL,NULL,'694215B7-08F7-4C0D-ACB1-D734BA44C0C8','2014-02-08 10:01:36.827') ";
        stmt.execute(sql);

        sql = "INSERT Product_JDBC_Sample VALUES ('Mountain-500 Black, 44','BK-M18B-44','0','0',NULL,'1000','750','0.00','0.00',NULL,NULL,NULL,NULL,'0',NULL,NULL,NULL,NULL,NULL,'2008-04-30 00:00:00.000',NULL,NULL,'694215B7-08F7-4C0D-ACB1-D734BA44C0C8','2014-02-08 10:01:36.827') ";
        stmt.execute(sql);
    }

    private static void displayRow(String title, ResultSet rs) {
        try {
            System.out.println(title);
            while (rs.next()) {
                System.out.println(rs.getString("ProductNumber") + " : " + rs.getString("Name"));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

## <a name="see-also"></a>참고 항목

[결과 집합 작업](../../../connect/jdbc/code-samples/working-with-result-sets.md)
