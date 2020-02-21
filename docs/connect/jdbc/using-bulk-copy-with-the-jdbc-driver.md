---
title: JDBC 드라이버에서 대량 복사 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 21e19635-340d-49bb-b39d-4867102fb5df
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 75ee40e0b7ca753efd32e0ab057340f61824acef
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026408"
---
# <a name="using-bulk-copy-with-the-jdbc-driver"></a>JDBC 드라이버에서 대량 복사 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft SQL Server에는 **bcp**라는 많이 사용되는 명령줄 유틸리티가 있어 SQL Server 데이터베이스의 테이블이나 뷰로 큰 파일을 신속하게 대량 복사할 수 있습니다. SQLServerBulkCopy 클래스를 사용하면 비슷한 기능을 제공하는 코드 솔루션을 Java로 작성할 수 있습니다. INSERT 문과 같은 다른 방법을 사용하여 데이터를 SQL Server 테이블에 로드할 수 있지만 SQLServerBulkCopy는 훨씬 더 향상된 성능을 제공합니다.  
  
SQLServerBulkCopy 클래스를 사용하면 SQL Server 테이블에만 데이터를 작성할 수 있습니다. 그러나 데이터 원본은 SQL Server로 제한되지 않습니다. ResultSet, RowSet 또는 ISQLServerBulkRecord 구현으로 데이터를 읽을 수 있는 한 모든 데이터 원본을 사용할 수 있습니다.  
  
SQLServerBulkCopy 클래스를 사용하여 다음을 수행할 수 있습니다.  
  
- 단일 대량 복사 작업  
  
- 여러 대량 복사 작업  
  
- 트랜잭션이 있는 대량 복사 작업  
  
> [!NOTE]  
> SQLServerBulkCopy 클래스를 지원하지 않는 SQL Server용 Microsoft JDBC Driver 4.1 이전 버전을 사용하는 경우 SQL Server Transact-SQL BULK INSERT 문을 대신 실행할 수 있습니다.  
  
## <a name="bulk-copy-example-setup"></a>대량 복사 예제 설정  

SQLServerBulkCopy 클래스를 사용하면 SQL Server 테이블에만 데이터를 작성할 수 있습니다. 이 문서에 표시된 코드 샘플에서는 SQL Server 샘플 데이터베이스 AdventureWorks를 사용합니다. 기존 테이블 코드 샘플이 변경되지 않도록 하려면 먼저 만들어야 하는 테이블에 데이터를 씁니다.  
  
BulkCopyDemoMatchingColumns 및 BulkCopyDemoDifferentColumns 테이블은 모두 AdventureWorks Production.Products 테이블을 기반으로 합니다. 이러한 테이블을 사용하는 코드 샘플에서 데이터는 Production.Products 테이블에서 이러한 샘플 테이블 중 하나에 추가됩니다. BulkCopyDemoDifferentColumns 테이블은 샘플에서 원본 데이터의 열을 대상 테이블에 매핑하는 방법을 보여 주는 경우에 사용되고, BulkCopyDemoMatchingColumns는 대부분의 다른 샘플에서 사용됩니다.  
  
일부 코드 샘플에서는 하나의 SQLServerBulkCopy 클래스를 사용하여 여러 테이블에 쓰는 방법을 보여 줍니다. 이러한 샘플에서는 BulkCopyDemoOrderHeader 및 BulkCopyDemoOrderDetail 테이블이 대상 테이블로 사용됩니다. 이러한 테이블은 AdventureWorks의 Sales.SalesOrderHeader 및 Sales.SalesOrderDetail 테이블을 기반으로 합니다.  
  
> [!NOTE]  
> SQLServerBulkCopy 코드 샘플은 SQLServerBulkCopy를 사용하는 구문을  보여 주기 위해서만 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있는 경우에는 Transact-SQL INSERT … SELECT 문을 사용하여 데이터를 복사합니다.  

### <a name="table-setup"></a>테이블 설정  

코드 샘플을 올바르게 실행하는 데 필요한 테이블을 만들려면 SQL Server 데이터베이스에서 다음 TRANSACT-SQL 문을 실행해야 합니다.  

```sql
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobject
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
```

## <a name="single-bulk-copy-operations"></a>단일 대량 복사 작업

SQL Server 대량 복사 작업을 수행하는 가장 간단한 방법은 데이터베이스에 대해 단일 작업을 수행하는 것입니다. 기본적으로 대량 복사 작업은 격리된 작업으로 수행됩니다. 복사 작업은 트랜잭션되지 않은 방식으로 수행되어 롤백할 수 없습니다.  
  
> [!NOTE]  
> 오류가 발생하여 대량 복사의 일부 또는 전체를 롤백해야 하는 경우 SQLServerBulkCopy 관리 트랜잭션을 사용하거나 기존 트랜잭션 내에서 대량 복사 작업을 수행할 수 있습니다.  
> 자세한 내용은 [트랜잭션 및 대량 복사 작업](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#transaction-and-bulk-copy-operations)을 참조하세요.  
  
 대량 복사 작업을 수행하는 일반적인 단계는 다음과 같습니다.  
  
1. 원본 서버에 연결하고 복사할 데이터를 가져옵니다. 데이터는 ResultSet 개체 또는 ISQLServerBulkRecord 구현에서 검색할 수 있는 경우에 다른 원본에서 가져올 수도 있습니다.  
  
2. 대상 서버에 연결합니다(**SQLServerBulkCopy**에서 연결을 설정하도록 하지 않으려는 경우).  
  
3. SQLServerBulkCopy 개체를 만들고 **setBulkCopyOptions**를 통해 필요한 속성을 설정합니다.  
  
4. **setDestinationTableName** 메서드를 호출하여 대량 삽입 작업의 대상 테이블을 나타냅니다.  
  
5. **writeToServer** 메서드 중 하나를 호출합니다.  
  
6. 필요에 따라 **setBulkCopyOptions**를 통해 속성을 업데이트하고 필요에 따라 **writeToServer**를 다시 호출합니다.  
  
7. **close**를 호출하거나 try-with-resources 문 내에서 대량 복사 작업을 래핑합니다.  
  
> [!CAUTION]  
> 원본 열과 대상 열의 데이터 형식은 일치하는 것이 좋습니다. 데이터 형식이 일치하지 않으면 SQLServerBulkCopy에서 각 원본 값을 대상 데이터 형식으로 변환하려고 합니다. 변환은 성능에 영향을 줄 수 있으며 예기치 않은 오류가 발생할 수도 있습니다. 예를 들어 double 데이터 형식은 대부분의 경우 decimal 데이터 형식으로 변환할 수 있지만 항상 그렇지는 않습니다.  
  
### <a name="example"></a>예제

다음 애플리케이션에서는 SQLServerBulkCopy 클래스를 사용하여 데이터를 로드하는 방법을 보여 줍니다. 이 예제에서 ResultSet은 SQL Server AdventureWorks 데이터베이스 Production.Product 테이블의 데이터를 동일한 데이터베이스의 유사한 테이블에 복사하는 데 사용됩니다.  
  
> [!IMPORTANT]  
> 이 샘플은 [테이블 설정](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#table-setup)에 설명된 대로 작업 테이블을 만들지 않은 경우 실행되지 않습니다. 이 코드는 SQLServerBulkCopy를 사용하는 구문을 보여 주기 위해서만 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있는 경우에는 Transact-SQL INSERT … SELECT 문을 사용하여 데이터를 복사합니다.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;

public class BulkCopySingle {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection)) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // In real world applications you would
            // not use SQLServerBulkCopy to move data from one table to the other
            // in the same database. This is for demonstration purposes only.

            // Set up the bulk copy object.
            // Note that the column positions in the source
            // table match the column positions in
            // the destination table so there is no need to
            // map columns.
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            bulkCopy.writeToServer(rsSourceData);

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="performing-a-bulk-copy-operation-using-transact-sql"></a>Transact-SQL을 사용하여 대량 복사 작업 수행

다음 예제에서는 executeUpdate 메서드를 사용하여 BULK INSERT 문을 실행하는 방법을 보여 줍니다.  
  
> [!NOTE]  
> 데이터 원본의 파일 경로는 서버에 상대적입니다. 대량 복사 작업이 성공하려면 서버 프로세스에서 해당 경로에 액세스할 수 있어야 합니다.  

```java
try (Connection con = DriverManager.getConnection(connectionUrl);
        Statement stmt = con.createStatement()) {
    // Perform the BULK INSERT
    stmt.executeUpdate(
            "BULK INSERT Northwind.dbo.[Order Details] " + "FROM 'f:\\mydata\\data.tbl' " + "WITH ( FORMATFILE='f:\\mydata\\data.fmt' )");
}
```  

## <a name="multiple-bulk-copy-operations"></a>여러 대량 복사 작업  

SQLServerBulkCopy 클래스의 단일 인스턴스를 사용하여 여러 대량 복사 작업을 수행할 수 있습니다. 복사본 간에 작업 매개 변수(예: 대상 테이블의 이름)가 변경되는 경우 다음 예제에 설명된 대로 writeToServer 메서드에 대한 후속 호출 전에 업데이트해야 합니다. 명시적으로 변경한 경우가 아니라면 모든 속성 값이 지정된 인스턴스에 대한 이전 대량 복사 작업 시와 동일하게 유지됩니다.  

> [!NOTE]  
> SQLServerBulkCopy의 동일한 인스턴스를 사용하여 여러 대량 복사 작업을 수행하면 일반적으로 각 작업에 대해 별도의 인스턴스를 사용하는 경우보다 더 효율적입니다.  
  
동일한 SQLServerBulkCopy 개체를 사용하여 여러 대량 복사 작업을 수행하는 경우 원본 또는 대상 정보가 각 작업에서 동일한지 다른지에 대한 제한이 없습니다. 그러나 서버에 쓸 때마다 열 연결 정보가 제대로 설정되어 있는지 확인해야 합니다.  
  
> [!IMPORTANT]  
> 이 샘플은 [테이블 설정](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#table-setup)에 설명된 대로 작업 테이블을 만들지 않은 경우 실행되지 않습니다. 이 코드는 SQLServerBulkCopy를 사용하는 구문을 보여 주기 위해서만 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있는 경우에는 Transact-SQL INSERT … SELECT 문을 사용하여 데이터를 복사합니다.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyMultiple {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationHeaderTable = "dbo.BulkCopyDemoOrderHeader";
        String destinationDetailTable = "dbo.BulkCopyDemoOrderDetail";
        int countHeaderBefore, countDetailBefore, countHeaderAfter, countDetailAfter;
        ResultSet rsHeader, rsDetail;

        try (Connection sourceConnection1 = DriverManager.getConnection(connectionUrl);
                Connection sourceConnection2 = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection1.createStatement();
                PreparedStatement preparedStmt1 = sourceConnection1.prepareStatement(
                        "SELECT [SalesOrderID], [OrderDate], [AccountNumber] FROM [Sales].[SalesOrderHeader] WHERE [AccountNumber] = ?;");
                PreparedStatement preparedStmt2 = sourceConnection2.prepareStatement(
                        "SELECT [Sales].[SalesOrderDetail].[SalesOrderID], [SalesOrderDetailID], [OrderQty], [ProductID], [UnitPrice] FROM "
                                + "[Sales].[SalesOrderDetail] INNER JOIN [Sales].[SalesOrderHeader] ON "
                                + "[Sales].[SalesOrderDetail].[SalesOrderID] = [Sales].[SalesOrderHeader].[SalesOrderID] WHERE [AccountNumber] = ?;");
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(connectionUrl);) {

            // Empty the destination tables.
            stmt.executeUpdate("DELETE FROM " + destinationHeaderTable);
            stmt.executeUpdate("DELETE FROM " + destinationDetailTable);

            // Perform an initial count on the destination
            // table with matching columns.
            countHeaderBefore = getRowCount(stmt, destinationHeaderTable);

            // Perform an initial count on the destination
            // table with different column positions.
            countDetailBefore = getRowCount(stmt, destinationDetailTable);

            // Get data from the source table as a ResultSet.
            // The Sales.SalesOrderHeader and Sales.SalesOrderDetail
            // tables are quite large and could easily cause a timeout
            // if all data from the tables is added to the destination.
            // To keep the example simple and quick, a parameter is
            // used to select only orders for a particular account
            // as the source for the bulk insert.
            preparedStmt1.setString(1, "10-4020-000034");
            rsHeader = preparedStmt1.executeQuery();

            // Get the Detail data in a separate connection.
            preparedStmt2.setString(1, "10-4020-000034");
            rsDetail = preparedStmt2.executeQuery();

            // Create the SQLServerBulkCopySQLServerBulkCopy object.
            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setBulkCopyTimeout(100);
            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationHeaderTable);

            // Guarantee that columns are mapped correctly by
            // defining the column mappings for the order.
            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");
            bulkCopy.addColumnMapping("OrderDate", "OrderDate");
            bulkCopy.addColumnMapping("AccountNumber", "AccountNumber");

            // Write rsHeader to the destination.
            bulkCopy.writeToServer(rsHeader);

            // Set up the order details destination.
            bulkCopy.setDestinationTableName(destinationDetailTable);

            // Clear the existing column mappings
            bulkCopy.clearColumnMappings();

            // Add order detail column mappings.
            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");
            bulkCopy.addColumnMapping("SalesOrderDetailID", "SalesOrderDetailID");
            bulkCopy.addColumnMapping("OrderQty", "OrderQty");
            bulkCopy.addColumnMapping("ProductID", "ProductID");
            bulkCopy.addColumnMapping("UnitPrice", "UnitPrice");

            // Write rsDetail to the destination.
            bulkCopy.writeToServer(rsDetail);

            // Perform a final count on the destination
            // tables to see how many rows were added.
            countHeaderAfter = getRowCount(stmt, destinationHeaderTable);
            countDetailAfter = getRowCount(stmt, destinationDetailTable);

            System.out.println((countHeaderAfter - countHeaderBefore) + " rows were added to the Header table.");
            System.out.println((countDetailAfter - countDetailBefore) + " rows were added to the Detail table.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

## <a name="transaction-and-bulk-copy-operations"></a>트랜잭션 및 대량 복사 작업

 대량 복사 작업은 격리된 작업이나 여러 단계 트랜잭션의 일부로 수행할 수 있습니다. 후자 옵션을 사용하면 동일한 트랜잭션 내에서 둘 이상의 대량 복사 작업을 수행할 뿐만 아니라 전체 트랜잭션을 커밋하거나 롤백하면서 다른 데이터베이스 작업(예: 삽입, 업데이트 및 삭제)을 수행할 수 있습니다.  
  
 기본적으로 대량 복사 작업은 격리된 작업으로 수행됩니다. 대량 복사 작업은 트랜잭션되지 않은 방식으로 수행되어 롤백할 수 없습니다. 오류가 발생하여 대량 복사의 일부 또는 전체를 롤백해야 하는 경우 SQLServerBulkCopy 관리 트랜잭션을 사용하거나 기존 트랜잭션 내에서 대량 복사 작업을 수행할 수 있습니다.  
  
### <a name="performing-a-non-transacted-bulk-copy-operation"></a>트랜잭션되지 않은 대량 복사 작업 수행

다음 애플리케이션에서는 트랜잭션되지 않은 대량 복사 작업 중 오류가 발생할 경우 어떻게 되는지를 보여 줍니다.  
  
예제에서 원본 테이블과 대상 테이블에는 각각 **ProductID**라는 ID 열이 있습니다. 먼저 코드는 모든 행을 삭제한 다음, **ProductID**가 원본 테이블에 있는 것으로 알려진 단일 행을 삽입하여 대상 테이블을 준비합니다. 기본적으로 ID 열에 대한 새 값은 추가된 각 행에 대한 대상 테이블에 생성됩니다. 이 예제에서 옵션은 대량 로드 프로세스에서 원본 테이블의 ID 값을 대신 강제로 사용하도록 하는 연결을 열 때 설정됩니다.  
  
대량 복사 작업은 **BatchSize** 속성을 10으로 설정하여 실행됩니다. 작업에서 잘못된 행이 발견되는 경우 예외가 throw됩니다. 이 첫 번째 예제에서는 대량 복사 작업이 트랜잭션되지 않습니다. 오류 지점까지 복사된 모든 일괄 처리가 커밋됩니다. 중복 키가 포함된 일괄 처리는 롤백되고 대량 복사 작업은 다른 모든 일괄 처리를 처리하기 전에 중지됩니다.  
  
> [!NOTE]  
> 이 샘플은 [테이블 설정](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#table-setup)에 설명된 대로 작업 테이블을 만들지 않은 경우 실행되지 않습니다. 이 코드는 SQLServerBulkCopy를 사용하는 구문을 보여 주기 위해서만 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있는 경우에는 Transact-SQL INSERT … SELECT 문을 사용하여 데이터를 복사합니다.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyNonTransacted {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(connectionUrl)) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Add a single row that will result in duplicate key
            // when all rows from source are bulk copied.
            // Note that this technique will only be successful in
            // illustrating the point if a row with ProductID = 446
            // exists in the AdventureWorks Production.Products table.
            // If you have made changes to the data in this table, change
            // the SQL statement in the code to add a ProductID that
            // does exist in your version of the Production.Products
            // table. Choose any ProductID in the middle of the table
            // (not first or last row) to best illustrate the result.
            stmt.executeUpdate("SET IDENTITY_INSERT " + destinationTable + " ON;" + "INSERT INTO " + destinationTable
                    + "([ProductID], [Name] ,[ProductNumber]) VALUES(446, 'Lock Nut 23','LN-3416'); SET IDENTITY_INSERT " + destinationTable
                    + " OFF");

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // Set up the bulk copy object using the KeepIdentity option and BatchSize = 10.
            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setKeepIdentity(true);
            copyOptions.setBatchSize(10);

            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            // This should fail with a duplicate key error
            // after some of the batches have been copied.
            try {
                bulkCopy.writeToServer(rsSourceData);
            }
            catch (SQLException e) {
                e.printStackTrace();
            }

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="performing-a-dedicated-build-copy-operation-in-a-transaction"></a>트랜잭션에서 전용 빌드 복사 작업 수행 

기본적으로 대량 복사 작업은 고유한 트랜잭션입니다. 전용 대량 복사 작업을 수행하려면 연결 문자열이 있는 SQLServerBulkCopy의 새 인스턴스를 만듭니다. 이 시나리오에서는 대량 복사 작업에서 트랜잭션을 만든 다음 커밋하거나 롤백합니다. **SQLServerBulkCopyOptions**에서 **UseInternalTransaction** 옵션을 명시적으로 지정하여 명시적으로 대량 복사 작업이 고유한 트랜잭션을 실행하도록 함으로써 대량 복사 작업의 각 일괄 처리가 별도의 트랜잭션 내에서 실행되도록 할 수 있습니다.  
  
> [!NOTE]  
> 다른 일괄 처리는 다른 트랜잭션에서 실행되므로 대량 복사 작업 중 오류가 발생하는 경우 현재 일괄 처리의 모든 행이 롤백되지만 이전 일괄 처리의 행은 데이터베이스에 유지됩니다.  
  
**BulkCopyNonTransacted**에서 **UseInternalTransaction** 옵션을 지정하는 경우 대량 복사 작업은 더 큰 외부 트랜잭션에 포함됩니다. 기본 키 위반 오류가 발생하면 전체 트랜잭션이 롤백되고 행이 대상 테이블에 추가되지 않습니다.

```java
SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
copyOptions.setKeepIdentity(true);
copyOptions.setBatchSize(10);
copyOptions.setUseInternalTransaction(true);
```

### <a name="using-existing-transactions"></a>기존 트랜잭션 사용

트랜잭션이 SQLServerBulkCopy 생성자의 매개 변수로 설정된 연결 개체를 전달할 수 있습니다. 이 상황에서는 대량 복사 작업이 기존 트랜잭션에서 수행되며 트랜잭션 상태가 변경되지 않습니다. 즉, 커밋되거나 중단되지 않습니다. 따라서 애플리케이션이 다른 데이터베이스 작업과 함께 대량 복사 작업을 트랜잭션에 포함할 수 있습니다. 오류가 발생하여 전체 대량 복사 작업을 롤백해야 하는 경우 또는 롤백할 수 있는 더 큰 프로세스의 일부로 대량 복사를 실행해야 하는 경우 대량 복사 작업 후 임의 지점에서 연결 개체에 대한 롤백을 수행할 수 있습니다.  
  
다음 애플리케이션은 한 가지 예외를 제외하고 **BulkCopyNonTransacted**와 유사합니다. 이 예제에서는 대량 복사 작업이 더 큰 외부 트랜잭션에 포함됩니다. 기본 키 위반 오류가 발생하면 전체 트랜잭션이 롤백되고 행이 대상 테이블에 추가되지 않습니다.

> [!NOTE]  
> 이 샘플은 [테이블 설정](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#table-setup)에 설명된 대로 작업 테이블을 만들지 않은 경우 실행되지 않습니다. 이 코드는 SQLServerBulkCopy를 사용하는 구문을 보여 주기 위해서만 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있는 경우에는 Transact-SQL INSERT … SELECT 문을 사용하여 데이터를 복사합니다.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyExistingTransactions {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;
        SQLServerBulkCopyOptions copyOptions;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection);) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Add a single row that will result in duplicate key
            // when all rows from source are bulk copied.
            // Note that this technique will only be successful in
            // illustrating the point if a row with ProductID = 446
            // exists in the AdventureWorks Production.Products table.
            // If you have made changes to the data in this table, change
            // the SQL statement in the code to add a ProductID that
            // does exist in your version of the Production.Products
            // table. Choose any ProductID in the middle of the table
            // (not first or last row) to best illustrate the result.
            stmt.executeUpdate("SET IDENTITY_INSERT " + destinationTable + " ON;" + "INSERT INTO " + destinationTable
                    + "([ProductID], [Name] ,[ProductNumber]) VALUES(446, 'Lock Nut 23','LN-3416'); SET IDENTITY_INSERT " + destinationTable
                    + " OFF");

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // Set up the bulk copy object inside the transaction.
            destinationConnection.setAutoCommit(false);

            copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setKeepIdentity(true);
            copyOptions.setBatchSize(10);

            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            // This should fail with a duplicate key error.
            try {
                bulkCopy.writeToServer(rsSourceData);
                destinationConnection.commit();
            }
            catch (SQLException e) {
                e.printStackTrace();
            }

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        catch (Exception e) {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="bulk-copy-from-a-csv-file"></a>CSV 파일에서 대량 복사  

 다음 애플리케이션에서는 SQLServerBulkCopy 클래스를 사용하여 데이터를 로드하는 방법을 보여 줍니다. 이 예제에서 CSV 파일은 SQL Server AdventureWorks 데이터베이스의 Production.Product 테이블에서 내보낸 데이터를 데이터베이스의 유사한 테이블에 복사하는 데 사용됩니다.  
  
> [!IMPORTANT]  
> 이 샘플은 가져올 [테이블 설정](../../ssms/download-sql-server-management-studio-ssms.md)에 설명된 대로 작업 테이블을 만들지 않은 경우 실행되지 않습니다.  
  
1. **SQL Server Management Studio**를 열고 AdventureWorks 데이터베이스가 있는 SQL Server에 연결합니다.  
  
2. 데이터베이스를 확장하고 AdventureWorks 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음, **작업** 및 **데이터 내보내기**를 선택합니다.  
  
3. 데이터 원본에서 SQL Server(예: SQL Server Native Client 11.0)에 연결할 수 있는 **데이터 원본**을 선택하고 구성을 확인한 후, **다음**을 선택합니다.  
  
4. 대상에서 **플랫 파일 대상**을 선택하고 대상이 있는 **파일 이름**(예: C:\Test\TestBulkCSVExample.csv)을 입력합니다. **형식**이 구분 기호로 분리됨이고 **텍스트 한정자**가 없음인지 확인하고 **첫 번째 데이터 행의 열 이름**을 사용하도록 설정한 후, **다음**을 선택합니다.  
  
5. **전송 데이터를 지정할 쿼리 작성** 및 **다음**을 선택합니다.  **SQL 문** SELECT ProductID, Name, ProductNumber FROM Production.Product를 입력하고 **다음**을 선택합니다.  
  
6. 구성을 확인합니다. 행 구분 기호는 {CR}{LF}로, 열 구분 기호는 쉼표({,})로 유지할 수 있습니다.  **Edit Mappings**(매핑 편집)를 선택하고 각 열에 대해 데이터 **형식**이 올바른지 확인합니다(예: ProductID의 경우 정수, 그 외의 경우 유니코드 문자열).  
  
7. **마침**으로 건너뛰고 내보내기를 실행합니다.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCSVFileRecord;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;

public class BulkCopyCSV {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;

        // Get data from the source file by loading it into a class that implements ISQLServerBulkRecord.
        // Here we are using the SQLServerBulkCSVFileRecord implementation to import the example CSV file.
        try (Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = destinationConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection);
                SQLServerBulkCSVFileRecord fileRecord = new SQLServerBulkCSVFileRecord("C:\\Test\\TestBulkCSVExample.csv", true);) {

            // Set the metadata for each column to be copied.
            fileRecord.addColumnMetadata(1, null, java.sql.Types.INTEGER, 0, 0);
            fileRecord.addColumnMetadata(2, null, java.sql.Types.NVARCHAR, 50, 0);
            fileRecord.addColumnMetadata(3, null, java.sql.Types.NVARCHAR, 25, 0);

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Set up the bulk copy object.
            // Note that the column positions in the source
            // data reader match the column positions in
            // the destination table so there is no need to
            // map columns.
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            bulkCopy.writeToServer(fileRecord);

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```  

### <a name="bulk-copy-with-always-encrypted-columns"></a>Always Encrypted 열을 포함하는 대량 복사  

SQL Server용 Microsoft JDBC Driver 6.0부터 Always Encrypted 열을 포함하는 대량 복사가 지원됩니다.  
  
대량 복사 옵션 및 원본와 대상 테이블의 암호화 유형에 따라 JDBC 드라이버에서 데이터를 투명하게 해독한 다음, 암호화하거나 암호화된 데이터를 그대로 보낼 수 있습니다. 예를 들어 데이터를 암호화된 열에서 암호화되지 않은 열로 대량 복사하는 경우 드라이버에서 데이터를 SQL Server로 보내기 전에 투명하게 해독합니다. 마찬가지로 데이터를 암호화되지 않은 열에서(또는 CSV 파일에서) 암호화된 열로 대량 복사하는 경우 드라이버에서 데이터를 SQL Server로 보내기 전에 투명하게 암호화합니다. 소스와 대상이 모두 암호화된 경우 **allowEncryptedValueModifications** 대량 복사 옵션에 따라 드라이버에서 데이터를 그대로 보내거나 SQL Server로 보내기 전에 다시 해독 및 암호화합니다.  
  
자세한 내용은 아래의 **allowEncryptedValueModifications** 대량 복사 옵션 및 [JDBC 드라이버에서 Always Encrypted 사용](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)을 참조하세요.  
  
> [!IMPORTANT]  
> 데이터를 CSV 파일에서 암호화된 열로 대량 복사하는 경우 SQL Server용 Microsoft JDBC Driver 6.0의 제한 사항:  
>
> 날짜 및 시간 형식의 경우 Transact-SQL 기본 문자열 리터럴 형식만 지원됩니다.  
>
> DATETIME 및 SMALLDATETIME 데이터 형식은 지원되지 않습니다.  
  
## <a name="bulk-copy-api-for-jdbc-driver"></a>JDBC 드라이버용 대량 복사 API  
  
### <a name="sqlserverbulkcopy"></a>SQLServerBulkCopy 

다른 원본의 데이터를 사용하여 SQL Server 테이블을 효율적으로 대량 로드할 수 있습니다.  
  
Microsoft SQL Server에는 많이 사용되는 bcp라는 명령 프롬프트 유틸리티가 있어 단일 서버인지 서버 간인지에 관계없이 테이블 간에 데이터를 이동할 수 있습니다. SQLServerBulkCopy 클래스를 사용하면 비슷한 기능을 제공하는 코드 솔루션을 Java로 작성할 수 있습니다. INSERT 문과 같은 다른 방법을 사용하여 데이터를 SQL Server 테이블에 로드할 수 있지만 SQLServerBulkCopy는 훨씬 더 향상된 성능을 제공합니다.  
  
SQLServerBulkCopy 클래스를 사용하면 SQL Server 테이블에만 데이터를 작성할 수 있습니다. 그러나 데이터 원본은 SQL Server로 제한되지 않습니다. ResultSet 인스턴스나 ISQLServerBulkRecord 구현으로 데이터를 읽을 수 있는 한 모든 데이터 원본을 사용할 수 있습니다.  
  
| 생성자                             | Description                                                                                                                                                                                                                    |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| SQLServerBulkCopy(Connection)           | SQLServerConnection의 지정된 열린 인스턴스를 사용하여 SQLServerBulkCopy 클래스의 새 인스턴스를 초기화합니다. 연결에 사용하도록 설정된 트랜잭션이 있으면 해당 트랜잭션 내에서 복사 작업이 수행됩니다. |
| SQLServerBulkCopy(String connectionURL) | 제공된 connectionURL에 따라 SQLServerConnection의 새 인스턴스를 초기화하고 엽니다. 생성자는 SQLServerConnection을 사용하여 SQLServerBulkCopy 클래스의 새 인스턴스를 초기화합니다.                     |
  
| 속성                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| String DestinationTableName | 서버에 있는 대상 테이블의 이름입니다.<br /><br /> writeToServer가 호출될 때 DestinationTableName이 설정되지 않은 경우 SQLServerException이 throw됩니다.<br /><br /> DestinationTableName은 (\<database>.\<owningschema>.\<name>)의 세 부분으로 구성된 이름입니다. 원하는 경우 데이터베이스 및 소유 스키마로 테이블 이름을 한정할 수 있습니다. 그러나 테이블 이름에서 밑줄("_")이나 다른 특수 문자를 사용하는 경우 주변 대괄호를 사용하여 이름을 이스케이프해야 합니다. 자세한 내용은 SQL Server 온라인 설명서의 “Identifiers”를 참조하세요. |
| ColumnMappings              | 열 매핑에서는 데이터 원본의 열과 대상의 열 간 관계를 정의합니다.<br /><br /> 매핑이 정의되지 않은 경우 열은 서수 위치에 따라 암시적으로 매핑됩니다. 이렇게 하려면 원본 및 대상 스키마가 일치해야 합니다. 일치하지 않으면 예외가 throw됩니다.<br /><br /> 매핑이 비어 있지 않을 경우 데이터 원본에 있는 일부 열을 지정할 수 없으며, 매핑되지 않은 열은 무시됩니다.<br /><br /> 원본 및 대상 열은 이름이나 서수로 나타낼 수 있습니다.               |
  
| 방법                                                                | Description                                                                                                                                                                |
| --------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Void addColumnMapping((int sourceColumn, int destinationColumn)       | 서수를 사용하여 원본 및 대상 열을 지정하는 새로운 열 매핑을 추가합니다.                                                                                  |
| Void addColumnMapping ((int sourceColumn, String destinationColumn)   | 원본 열에는 서수를, 대상 열에는 열 이름을 사용하는 새로운 열 매핑을 추가합니다.                                                            |
| Void addColumnMapping ((String sourceColumn, int destinationColumn)   | 열 이름을 사용하여 원본 열을 설명하고 서수를 사용하여 대상 열을 지정하는 새로운 열 매핑을 추가합니다.                                             |
| Void addColumnMapping (String sourceColumn, String destinationColumn) | 열 이름을 사용하여 원본 및 대상 열을 모두 지정하는 새로운 열 매핑을 추가합니다.                                                                              |
| Void clearColumnMappings()                                            | 열 매핑의 내용을 지웁니다.                                                                                                                                |
| Void close()                                                          | SQLServerBulkCopy 인스턴스를 닫습니다.                                                                                                                                     |
| SQLServerBulkCopyOptions getBulkCopyOptions()                         | SQLServerBulkCopyOptions의 현재 집합을 검색합니다.                                                                                                                     |
| 문자열 getDestinationTableName()                                      | 현재 대상 테이블 이름을 검색합니다.                                                                                                                               |
| Void setBulkCopyOptions(SQLServerBulkCopyOptions copyOptions)         | 제공된 옵션에 따라 SQLServerBulkCopy 인스턴스의 동작을 업데이트합니다.                                                                                  |
| Void setDestinationTableName(String tableName)                        | 대상 테이블의 이름을 설정합니다.                                                                                                                                    |
| Void writeToServer(ResultSet sourceData)                              | 제공된 ResultSet의 모든 행을 SQLServerBulkCopy 개체의 DestinationTableName 속성으로 지정된 대상 테이블에 복사합니다.                           |
| Void writeToServer(RowSet sourceData)                                 | 제공된 RowSet의 모든 행을 SQLServerBulkCopy 개체의 DestinationTableName 속성으로 지정된 대상 테이블에 복사합니다.                              |
| Void writeToServer(ISQLServerBulkRecord sourceData)                   | 제공된 ISQLServerBulkRecord 구현의 모든 행을 SQLServerBulkCopy 개체의 DestinationTableName 속성으로 지정된 대상 테이블에 복사합니다. |
  
### <a name="sqlserverbulkcopyoptions"></a>SQLServerBulkCopyOptions  

 WriteToServer 메서드가 SQLServerBulkCopy의 인스턴스에서 작동하는 방식을 제어하는 설정의 컬렉션입니다.  
  
| 생성자                | Description                                                                                              |
| -------------------------- | -------------------------------------------------------------------------------------------------------- |
| SQLServerBulkCopyOptions() | 모든 설정에 기본값을 사용하여 SQLServerBulkCopyOptions 클래스의 새 인스턴스를 초기화합니다. |
  
 다음 옵션에 대한 Getter 및 setter가 있습니다.  
  
| 옵션                                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | 기본값                                                              |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Boolean CheckConstraints                 | 데이터가 삽입되는 동안 제약 조건을 확인합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | False - 제약 조건을 확인하지 않습니다.                                   |
| Boolean FireTriggers                     | 지정한 경우 서버에서 데이터베이스에 삽입할 행에 대해 삽입 트리거를 발생하도록 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | False - 트리거가 발생하지 않습니다.                                        |
| Boolean KeepIdentity                     | 원본 ID 값을 유지합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | False - ID 값이 대상에 의해 할당됩니다.              |
| Boolean KeepNulls                        | 기본값에 대한 설정에 관계없이 대상 테이블에서 null 값을 유지합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | False - 해당되는 경우 null 값이 기본값으로 대체됩니다. |
| Boolean TableLock                        | 대량 복사 작업의 기간 동안 대량 업데이트 잠금을 획득합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | False - 행 잠금이 사용됩니다.                                          |
| Boolean UseInternalTransaction           | 지정한 경우 대량 복사 작업의 각 일괄 처리가 트랜잭션 내에서 발생됩니다. SQLServerBulkCopy가 생성자에 지정된 대로 기존 연결을 사용하는 경우 SQLServerException이 발생합니다.  SQLServerBulkCopy에서 전용 연결을 만든 경우 트랜잭션이  전용된 연결을 만든 경우 트랜잭션이 활성화됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | False - 트랜잭션이 없습니다.                                               |
| Int BatchSize                            | 각 일괄 처리의 행 수입니다. 각 일괄 처리가 끝나면 일괄 처리의 행이 서버로 보내집니다.<br /><br /> 일괄 처리는 BatchSize 행이 처리되었거나 대상 데이터 원본으로 보낼 행이 더 이상 없는 경우 완료됩니다.  SQLServerBulkCopy 인스턴스가 UseInternalTransaction 옵션을 적용하지 않고 선언된 경우 행은 한 번에 서버 BatchSize 행으로 보내지지만 트랜잭션 관련 작업이 수행되지 않습니다. UseInternalTransaction이 적용된 경우 행의 각 일괄 처리가 별도의 트랜잭션으로 삽입됩니다.                                                                                                                                                                                                                                                                                                                                                                                                                                           | 0 - 각 writeToServer 작업이 단일 일괄 처리임을 나타냅니다.    |
| Int BulkCopyTimeout                      | 제한 시간이 초과되기 전에 작업이 완료되는 시간(초)입니다. 0 값은 제한이 없음을 나타내며 대량 복사가 무기한 대기합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | 60초입니다.                                                          |
| Boolean allowEncryptedValueModifications | 이 옵션은 SQL Server용 Microsoft JDBC Driver 6.0 이상에서 사용할 수 있습니다.<br /><br /> **allowEncryptedValueModifications**을 지정하면 데이터를 해독하지 않고 테이블 또는 데이터베이스 간에 암호화된 데이터를 대량 복사할 수 있습니다. 일반적으로 애플리케이션은 데이터를 해독하지 않고 한 테이블에서 암호화된 열을 선택한(앱은 열 암호화 설정 키워드가 사용하지 않도록 설정된 상태에서 데이터베이스에 연결함) 다음, 이 옵션을 사용하여 여전히 암호돠된 데이터를 대량 복사합니다. 자세한 내용은 [상시 암호화와 JDBC 드라이버 사용](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)을 참조하세요.<br /><br /> **allowEncryptedValueModifications**를 지정하면 드라이버에서 데이터가 실제로 암호화되었는지 여부 또는 동일한 암호화 형식, 알고리즘 및 키를 대상 열로 사용하여 올바르게 암호화되었는지 확인하지 않아 데이터베이스가 손상될 수 있으므로 주의하여 사용합니다. |
  
 Getter 및 setter:  
  
| 메서드                                                                            | Description                                                                                                                                                                               |
| ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Boolean isCheckConstraints()                                                       | 데이터를 삽입하는 동안 제약 조건을 확인하는지 여부를 나타냅니다.                                                                                                      |
| Void setCheckConstraints(Boolean checkConstraints)                                 | 데이터를 삽입하는 동안 제약 조건을 확인하는지 여부를 설정합니다.                                                                                                           |
| Boolean isFireTriggers()                                                           | 서버에서 데이터베이스에 삽입할 행에 대해 삽입 트리거를 발생해야 하는지 여부를 나타냅니다.                                                                                    |
| Void setFireTriggers(Boolean fireTriggers)                                         | 서버에서 데이터베이스에 삽입할 행에 대해 트리거를 발생하도록 설정해야 하는지 여부를 설정합니다.                                                                                     |
| Boolean isKeepIdentity()                                                           | 모든 원본 ID 값을 유지하는지 여부를 나타냅니다.                                                                                                                          |
| Void setKeepIdentity(Boolean keepIdentity)                                         | ID 값을 유지하는지 여부를 설정합니다.                                                                                                                                          |
| Boolean isKeepNulls()                                                              | 기본값에 대한 설정과 관계 없이 대상 테이블의 Null 값을 유지하는지 여부 또는 해당 값을 기본값으로 바꾸어야 하는지(해당하는 경우) 여부를 나타냅니다. |
| Void setKeepNulls(Boolean keepNulls)                                               | 기본값에 대한 설정과 관계 없이 대상 테이블의 Null 값을 유지하는지 여부 또는 해당 값을 기본값으로 바꾸어야 하는지(해당하는 경우) 여부를 설정합니다.      |
| Boolean isTableLock()                                                              | SQLServerBulkCopy가 대량 복사 작업의 기간 동안 대량 업데이트 잠금을 획득하는지 여부를 나타냅니다.                                                                         |
| Void setTableLock(Boolean tableLock)                                               | SQLServerBulkCopy에서 대량 복사 작업의 기간 동안 대량 업데이트 잠금을 획득하는지 여부를 설정합니다.                                                                              |
| Boolean isUseInternalTransaction()                                                 | 대량 복사 작업의 각 일괄 처리가 트랜잭션 내에서 발생하는지 여부를 나타냅니다.                                                                                                  |
| Void setUseInternalTranscation(Boolean useInternalTransaction)                     | 대량 복사 작업의 각 일괄 처리가 트랜잭션 내에서 발생하는지 여부를 설정합니다.                                                                                               |
| Int getBatchSize()                                                                 | 각 일괄 처리의 행 수를 가져옵니다. 각 일괄 처리가 끝나면 일괄 처리의 행이 서버로 보내집니다.                                                                             |
| Void setBatchSize(int batchSize)                                                   | 각 일괄 처리의 행 수를 설정합니다. 각 일괄 처리가 끝나면 일괄 처리의 행이 서버로 보내집니다.                                                                            |
| Int getBulkCopyTimeout()                                                           | 제한 시간이 초과되기 전에 작업을 완료할 시간(초)를 가져옵니다.                                                                                                             |
| Void  setBulkCopyTimeout(int timeout)                                              | 제한 시간이 초과되기 전에 작업을 완료할 시간(초)를 설정합니다.                                                                                                             |
| boolean isAllowEncryptedValueModifications()                                       | allowEncryptedValueModifications 설정이 활성화되었는지 여부를 나타냅니다.                                                                                                        |
| void setAllowEncryptedValueModifications(boolean allowEncryptedValueModifications) | Always Encrypted 열을 포함하는 대량 복사에 사용되는 allowEncryptedValueModifications 설정을 구성합니다.                                                                         |
  
### <a name="isqlserverbulkrecord"></a>ISQLServerBulkRecord  

 ISQLServerBulkRecord 인터페이스는 원본(예: 파일)에서 데이터를 읽고 SQLServerBulkCopy 인스턴스에서 해당 데이터로 SQL Server 테이블을 대량 로드할 수 있도록 하는 클래스를 만드는 데 사용할 수 있습니다.  
  
| 인터페이스 메서드                   | Description                                                                                                                                                                                                                                                                                            |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 설정\<정수> getColumnOrdinals()   | 이 데이터 레코드에 표시된 각 열에 대한 서수를 가져옵니다.                                                                                                                                                                                                                              |
| String getColumnName(int 열)    | 지정된 열의 이름을 가져옵니다.                                                                                                                                                                                                                                                                      |
| Int getColumnType(int 열)       | 지정된 열의 JDBC 데이터 형식을 가져옵니다.                                                                                                                                                                                                                                                            |
| Int getPrecision(int 열)        | 지정된 열의 전체 자릿수를 가져옵니다.                                                                                                                                                                                                                                                                |
| Object[] getRowData()               | 현재 행에 대한 데이터를 개체의 배열로 가져옵니다.<br /><br /> 각 개체는 지정된 열에 대해 표시된 JDBC 데이터 형식을 나타내는 데 사용되는 Java 언어 형식과 일치해야 합니다.  자세한 내용은 ‘JDBC 드라이버 데이터 형식 이해’에서 적절한 매핑을 참조하세요. |
| Int getScale(int 열)            | 지정된 열에 대한 소수 자릿수를 가져옵니다.                                                                                                                                                                                                                                                                    |
| Boolean isAutoIncrement(int 열) | 열이 ID 열을 나타내는지 여부를 나타냅니다.                                                                                                                                                                                                                                            |
| Boolean next()                      | 다음 데이터 행으로 이동합니다.                                                                                                                                                                                                                                                                         |
  
### <a name="sqlserverbulkcsvfilerecord"></a>SQLServerBulkCSVFileRecord  

각 줄이 데이터 행을 나타내는 구분 기호로 분리된 파일에서 기본 Java 데이터 형식을 읽는 데 사용할 수 있는 ISQLServerBulkRecord 인터페이스의 간단한 구현입니다.  
  
구현 참고 사항 및 제한 사항:  
  
1. 한 번에 한 줄씩 데이터를 읽으므로 지정된 모든 행에서 허용되는 최대 데이터 크기는 사용 가능한 메모리에 의해 제한됩니다.  
  
2. varchar(max), varbinary(max), nvarchar(max), sqlxml, ntext 등 큰 데이터 형식의 스트리밍은 지원되지 않습니다.  
  
3. CSV 파일에 대해 지정된 구분 기호는 데이터의 임의 위치에 표시되지 않아야 하며 Java 정규식에서 제한된 문자인 경우 올바르게 이스케이프되어야 합니다.  
  
4. CSV 파일 구현에서 큰따옴표는 데이터의 일부로 처리됩니다. 예를 들어 hello,“world”,“hello,world” 줄은 구분 기호가 쉼표인 경우 hello, “world”, “hello 및 world” 값을 갖는 네 개의 열이 있는 것으로 처리됩니다.  
  
5. 줄 바꿈 문자는 행 종결자로 사용되며, 데이터의 어떤 위치에서도 허용되지 않습니다.  
  
| 생성자                                                                                                                                                                 | Description                                                                                                                                                                                                                                                                                                                        |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SQLServerBulkCSVFileRecord(String fileToParse, String encoding, String delimiter, Boolean firstLineIsColumnNamesSQLServerBulkCSVFileRecord(String, String, String, boolean) | 제공된 구분 기호 및 인코딩으로 fileToParse의 각 줄을 구분 분석하는 SQLServerBulkCSVFileRecord 클래스의 새 인스턴스를 초기화합니다. FirstLineIsColumnNames가 True로 설정된 경우 파일의 첫 줄은 열 이름으로 구문 분석됩니다.  인코딩이 NULL인 경우에는 기본 인코딩이 사용됩니다.            |
| SQLServerBulkCSVFileRecord(String fileToParse, String encoding, Boolean firstLineIsColumnNamesSQLServerBulkCSVFileRecord(String, String, boolean)                           | 구분 기호 및 제공된 인코딩으로 fileToParse의 각 줄을 구분 분석하는 SQLServerBulkCSVFileRecord 클래스의 새 인스턴스를 초기화합니다. FirstLineIsColumnNames가 True로 설정된 경우 파일의 첫 줄은 열 이름으로 구문 분석됩니다.  인코딩이 NULL인 경우에는 기본 인코딩이 사용됩니다. |
| SQLServerBulkCSVFileRecord(String fileToParse, Boolean firstLineIsColumnNamesSQLServerBulkCSVFileRecord(String, boolean)                                                    | 쉼표 구분 기호 및 기본 인코딩으로 fileToParse의 각 줄을 구분 분석하는 SQLServerBulkCSVFileRecord 클래스의 새 인스턴스를 초기화합니다. FirstLineIsColumnNames가 True로 설정된 경우 파일의 첫 줄은 열 이름으로 구문 분석됩니다.                                                           |
  
| 방법                                                                                                 | Description                                                                                         |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| Void addColumnMetadata(int positionInFile, String columnName, int jdbcType, int precision, int scale)  | 파일의 지정된 열에 대한 메타데이터를 추가합니다.                                                     |
| Void close()                                                                                           | 파일 판독기와 관련된 모든 리소스를 해제합니다.                                             |
| Void setTimestampWithTimezoneFormat(DateTim eFormatter dateTimeFormatter                               | 파일의 타임스탬프 데이터를 java.sql.Types.TIMESTAMP_WITH_TIMEZONE으로 구문 분석하는 형식을 설정합니다. |
| Void setTimestampWithTimezoneFormat(String dateTimeFormat)setTimeWithTimezoneFormat(DateTimeFormatter) | 파일의 시간 데이터를 java.sql.Types.TIME_WITH_TIMEZONE으로 구문 분석하는 형식을 설정합니다.           |
| Void setTimeWithTimezoneFormat(DateTimeForm atter dateTimeFormatter)                                   | 파일의 시간 데이터를 java.sql.Types.TIME_WITH_TIMEZONE으로 구문 분석하는 형식을 설정합니다.           |
| Void setTimeWithTimezoneFormat(String timeFormat)                                                      | 파일의 시간 데이터를 java.sql.Types.TIME_WITH_TIMEZONE으로 구문 분석하는 형식을 설정합니다.           |
  
## <a name="see-also"></a>참고 항목  

[JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
