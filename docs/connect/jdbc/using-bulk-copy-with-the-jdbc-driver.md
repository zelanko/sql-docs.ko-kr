---
title: JDBC 드라이버와 함께 대량 복사를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 21e19635-340d-49bb-b39d-4867102fb5df
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6daf0ae2773d8a99e4f9264c05024a86fcd79926
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853108"
---
# <a name="using-bulk-copy-with-the-jdbc-driver"></a>JDBC 드라이버에서 대량 복사 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Microsoft SQL Server 라는 명령줄 유틸리티가 포함 되어 **bcp** 에 대 한 신속 하 게 대량으로 테이블이 나 SQL Server 데이터베이스의 뷰로 큰 파일을 복사 합니다. SQLServerBulkCopy 클래스를 사용하면 비슷한 기능을 제공하는 코드 솔루션을 Java로 작성할 수 있습니다. INSERT 문과 같은 다른 방법을 사용하여 데이터를 SQL Server 테이블에 로드할 수 있지만 SQLServerBulkCopy는 훨씬 더 향상된 성능을 제공합니다.  
  
 SQLServerBulkCopy 클래스를 사용하면 SQL Server 테이블에만 데이터를 작성할 수 있습니다. 그러나 데이터 원본은 SQL Server로 제한되지 않습니다. ResultSet, RowSet 또는 ISQLServerBulkRecord 구현으로 데이터를 읽을 수 있는 한 모든 데이터 원본을 사용할 수 있습니다.  
  
 SQLServerBulkCopy 클래스를 사용하여 다음을 수행할 수 있습니다.  
  
-   단일 대량 복사 작업  
  
-   여러 대량 복사 작업  
  
-   트랜잭션이 있는 대량 복사 작업  
  
> [!NOTE]  
>  SQLServerBulkCopy 클래스를 지원하지 않는 SQL Server용 Microsoft JDBC Driver 4.1 이전 버전을 사용하는 경우 SQL Server Transact-SQL BULK INSERT 문을 대신 실행할 수 있습니다.  
  
## <a name="bulk-copy-example-setup"></a>대량 복사 예제 설정  
 SQLServerBulkCopy 클래스를 사용하면 SQL Server 테이블에만 데이터를 작성할 수 있습니다. 이 항목에 표시된 코드 샘플에서는 SQL Server 샘플 데이터베이스 AdventureWorks를 사용합니다. 기존 테이블 코드 샘플이 변경되지 않도록 하려면 먼저 만들어야 하는 테이블에 데이터를 씁니다.  
  
 BulkCopyDemoMatchingColumns 및 BulkCopyDemoDifferentColumns 테이블은 모두 AdventureWorks Production.Products 테이블을 기반으로 합니다. 이러한 테이블을 사용하는 코드 샘플에서 데이터는 Production.Products 테이블에서 이러한 샘플 테이블 중 하나에 추가됩니다. BulkCopyDemoDifferentColumns 테이블은 샘플에서 원본 데이터의 열을 대상 테이블에 매핑하는 방법을 보여 주는 경우에 사용되고, BulkCopyDemoMatchingColumns는 대부분의 다른 샘플에서 사용됩니다.  
  
 일부 코드 샘플에서는 하나의 SQLServerBulkCopy 클래스를 사용하여 여러 테이블에 쓰는 방법을 보여 줍니다. 이러한 샘플에서는 BulkCopyDemoOrderHeader 및 BulkCopyDemoOrderDetail 테이블이 대상 테이블로 사용됩니다. 이러한 테이블은 AdventureWorks의 Sales.SalesOrderHeader 및 Sales.SalesOrderDetail 테이블을 기반으로 합니다.  
  
> [!NOTE]  
>  SQLServerBulkCopy 코드 샘플은 SQLServerBulkCopy를 사용하는 구문을  보여 주기 위해서만 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있는 경우에는 Transact-SQL INSERT … SELECT 문을 사용하면 더 쉽고 더 빠르게 데이터를 복사할 수 있습니다.  
  
###  <a name="BKMK_TableSetup"></a> 테이블 설정  
 코드 샘플을 올바르게 실행하는 데 필요한 테이블을 만들려면 SQL Server 데이터베이스에서 다음 TRANSACT-SQL 문을 실행해야 합니다.  
  
```  
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
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
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
>  오류가 발생하여 대량 복사의 일부 또는 전체를 롤백해야 하는 경우 SQLServerBulkCopy 관리 트랜잭션을 사용하거나 기존 트랜잭션 내에서 대량 복사 작업을 수행할 수 있습니다.  
>   
>  자세한 내용은 참조 [트랜잭션 및 대량 복사 작업](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TransactionBulk)  
  
 대량 복사 작업을 수행하는 일반적인 단계는 다음과 같습니다.  
  
1.  원본 서버에 연결하고 복사할 데이터를 가져옵니다. 데이터는 ResultSet 개체 또는 ISQLServerBulkRecord 구현에서 검색할 수 있는 경우에 다른 원본에서 가져올 수도 있습니다.  
  
2.  대상 서버에 연결 (사용 하려는 경우가 아니면 **SQLServerBulkCopy** 있습니다에 대 한 연결을 설정 하).  
  
3.  통해 필요한 속성을 설정 하 여 SQLServerBulkCopy 개체를 만든 **setBulkCopyOptions**합니다.  
  
4.  호출 된 **setDestinationTableName** 메서드를 나타내는 대상 테이블에 대량 삽입 작업입니다.  
  
5.  하나를 호출 하는 **writeToServer** 메서드.  
  
6.  필요에 따라 속성을 통해 업데이트 **setBulkCopyOptions** 호출 **writeToServer** 필요에 따라 다시 합니다.  
  
7.  호출 **닫습니다**, 또는 리소스와 try 문 내에서 대량 복사 작업을 래핑합니다.  
  
> [!CAUTION]  
>  원본 열과 대상 열의 데이터 형식은 일치하는 것이 좋습니다. 데이터 형식이 일치하지 않으면 SQLServerBulkCopy에서 각 원본 값을 대상 데이터 형식으로 변환하려고 합니다. 변환은 성능에 영향을 줄 수 있으며 예기치 않은 오류가 발생할 수도 있습니다. 예를 들어 double 데이터 형식은 대부분의 경우 decimal 데이터 형식으로 변환할 수 있지만 항상 그렇지는 않습니다.  
  
### <a name="example"></a>예제  
 다음 응용 프로그램에서는 SQLServerBulkCopy 클래스를 사용하여 데이터를 로드하는 방법을 보여 줍니다. 이 예제에서 ResultSet은 SQL Server AdventureWorks 데이터베이스 Production.Product 테이블의 데이터를 동일한 데이터베이스의 유사한 테이블에 복사하는 데 사용됩니다.  
  
> [!IMPORTANT]  
>  이 샘플을 만들지 않은 경우 작업 테이블에 설명 된 대로 실행 되지 것입니다 [테이블 설정](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup)합니다. 이 코드는 SQLServerBulkCopy를 사용하는 구문을 보여 주기 위해서만 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있는 경우에는 Transact-SQL INSERT … SELECT 문을 사용하면 더 쉽고 더 빠르게 데이터를 복사할 수 있습니다.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    // Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
                        // Open the destination connection. In the real world you would    
                        // not use SQLServerBulkCopy to move data from one table to the other    
                        // in the same database. This is for demonstration purposes only.   
                        try (Connection destinationConnection =   
                                DriverManager.getConnection(connectionString))  
                        {  
                            // Set up the bulk copy object.    
                            // Note that the column positions in the source   
                            // table match the column positions in    
                            // the destination table so there is no need to   
                            // map columns.   
                            try (SQLServerBulkCopy bulkCopy =  
                                       new SQLServerBulkCopy(destinationConnection))  
                            {  
                                bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                                try  
                                {  
                                    // Write from the source to the destination.  
                                    bulkCopy.writeToServer(rsSourceData);  
                                }  
                                catch (Exception e)  
                                {  
                                    // Handle any errors that may have occurred.  
                                    e.printStackTrace();  
                                }  
                            }  
  
                            // Perform a final count on the destination    
                            // table to see how many rows were added.  
                            try (ResultSet rsRowCount = stmt.executeQuery(  
                                    "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                            {  
                                rsRowCount.next();  
                                long countEnd = rsRowCount.getInt(1);  
                                System.out.println("Ending row count = " + countEnd);  
                                System.out.println((countEnd - countStart) + " rows were added.");  
                            }  
                        }  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
           "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
```  
  
### <a name="performing-a-bulk-copy-operation-using-transact-sql"></a>Transact-SQL을 사용하여 대량 복사 작업 수행  
 다음 예제에서는 executeUpdate 메서드를 사용하여 BULK INSERT 문을 실행하는 방법을 보여 줍니다.  
  
> [!NOTE]  
>  데이터 원본의 파일 경로는 서버에 상대적입니다. 대량 복사 작업이 성공하려면 서버 프로세스에서 해당 경로에 액세스할 수 있어야 합니다.  
  
```  
try (Connection con = DriverManager.getConnection(connectionString))  
{  
    try (Statement stmt = con.createStatement())  
    {  
        // Perform the BULK INSERT  
        stmt.executeUpdate(  
                "BULK INSERT Northwind.dbo.[Order Details] " +  
                        "FROM 'f:\\mydata\\data.tbl' " +  
                        "WITH ( FORMATFILE='f:\\mydata\\data.fmt' )");  
    }  
}  
```  
  
## <a name="multiple-bulk-copy-operations"></a>여러 대량 복사 작업  
 SQLServerBulkCopy 클래스의 단일 인스턴스를 사용하여 여러 대량 복사 작업을 수행할 수 있습니다. 복사본 간에 작업 매개 변수(예: 대상 테이블의 이름)가 변경되는 경우 다음 예제에 설명된 대로 writeToServer 메서드에 대한 후속 호출 전에 업데이트해야 합니다. 명시적으로 변경한 경우가 아니라면 모든 속성 값이 지정된 인스턴스에 대한 이전 대량 복사 작업 시와 동일하게 유지됩니다.  
  
> [!NOTE]  
>  SQLServerBulkCopy의 동일한 인스턴스를 사용하여 여러 대량 복사 작업을 수행하면 일반적으로 각 작업에 대해 별도의 인스턴스를 사용하는 경우보다 더 효율적입니다.  
  
 동일한 SQLServerBulkCopy 개체를 사용하여 여러 대량 복사 작업을 수행하는 경우 원본 또는 대상 정보가 각 작업에서 동일한지 다른지에 대한 제한이 없습니다. 그러나 서버에 쓸 때마다 열 연결 정보가 제대로 설정되어 있는지 확인해야 합니다.  
  
> [!IMPORTANT]  
>  이 샘플을 만들지 않은 경우 작업 테이블에 설명 된 대로 실행 되지 것입니다 [테이블 설정](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup)합니다. 이 코드는 SQLServerBulkCopy를 사용하는 구문을 보여 주기 위해서만 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있는 경우에는 Transact-SQL INSERT … SELECT 문을 사용하면 더 쉽고 더 빠르게 데이터를 복사할 수 있습니다.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection1 = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection1.createStatement())  
                {  
  
                    // Empty the destination tables.   
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoOrderHeader;");  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoOrderDetail;");  
  
                    // Perform an initial count on the destination   
                    //  table with matching columns.  
                    long countStartHeader = 0;  
                    try (ResultSet rsRowCountHeader = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderHeader;"))  
                    {  
                        rsRowCountHeader.next();  
                        countStartHeader = rsRowCountHeader.getInt(1);  
                        System.out.println("Starting row count for Header table = " + countStartHeader);  
                    }  
  
                    // Perform an initial count on the destination   
                    // table with different column positions.  
                    long countStartDetail = 0;  
                    try (ResultSet rsRowCountDetail = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderDetail;"))  
                    {  
                        rsRowCountDetail.next();  
                        countStartDetail = rsRowCountDetail.getInt(1);  
                        System.out.println("Starting row count for Detail table = " + countStartDetail);  
                    }  
  
                    // Get data from the source table as a ResultSet.   
                    // The Sales.SalesOrderHeader and Sales.SalesOrderDetail   
                    // tables are quite large and could easily cause a timeout   
                    // if all data from the tables is added to the destination.    
                    // To keep the example simple and quick, a parameter is     
                    // used to select only orders for a particular account    
                    // as the source for the bulk insert.  
                    try (PreparedStatement preparedStmt1 = sourceConnection1.prepareStatement(  
                            "SELECT [SalesOrderID], [OrderDate], " +  
                            "[AccountNumber] FROM [Sales].[SalesOrderHeader] " +  
                            "WHERE [AccountNumber] = ?;"))  
                    {  
                        preparedStmt1.setString(1, "10-4020-000034");  
  
                        try (ResultSet rsHeader = preparedStmt1.executeQuery())  
                        {  
                            // Get the Detail data in a separate connection.   
                            try (Connection sourceConnection2 = DriverManager.getConnection(connectionString))  
                            {  
                                try (PreparedStatement preparedStmt2 = sourceConnection2.prepareStatement(  
                                        "SELECT [Sales].[SalesOrderDetail].[SalesOrderID], " +  
                                                "[SalesOrderDetailID], [OrderQty], [ProductID], " +  
                                                "[UnitPrice] FROM [Sales].[SalesOrderDetail] " +  
                                                "INNER JOIN [Sales].[SalesOrderHeader] " +  
                                                "ON [Sales].[SalesOrderDetail].[SalesOrderID] " +  
                                                "= [Sales].[SalesOrderHeader].[SalesOrderID] " +  
                                                "WHERE [AccountNumber] = ?;"))  
                                {  
                                    preparedStmt2.setString(1, "10-4020-000034");  
  
                                    try (ResultSet rsDetail = preparedStmt2.executeQuery())  
                                    {  
                                        // Create the SQLServerBulkCopySQLServerBulkCopy object.    
                                        try (SQLServerBulkCopy bulkCopy =  
                                                   new SQLServerBulkCopy(connectionString))  
                                        {  
                                            bulkCopy.setBulkCopyOptions(copyOptions);  
                                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoOrderHeader");  
  
                                            // Guarantee that columns are mapped correctly by   
                                            // defining the column mappings for the order.  
                                            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");  
                                            bulkCopy.addColumnMapping("OrderDate", "OrderDate");  
                                            bulkCopy.addColumnMapping("AccountNumber", "AccountNumber");  
  
                                            // Write rsHeader to the destination.   
                                            try  
                                            {  
                                                bulkCopy.writeToServer(rsHeader);  
                                            }  
                                            catch (Exception e)  
                                            {  
                                                // Handle any errors that may have occurred.  
                                                e.printStackTrace();  
                                            }  
  
                                            // Set up the order details destination.   
                                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoOrderDetail");  
  
                                            // Clear the existing column mappings  
                                            bulkCopy.clearColumnMappings();  
  
                                            // Add order detail column mappings.  
                                            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");  
                                            bulkCopy.addColumnMapping(  
                                                    "SalesOrderDetailID",   
                                                    "SalesOrderDetailID");  
                                            bulkCopy.addColumnMapping("OrderQty", "OrderQty");  
                                            bulkCopy.addColumnMapping("ProductID", "ProductID");  
                                            bulkCopy.addColumnMapping("UnitPrice", "UnitPrice");  
  
                                            // Write rsDetail to the destination.   
                                            try  
                                            {  
                                                bulkCopy.writeToServer(rsDetail);  
                                            }  
                                            catch (Exception e)  
                                            {  
                                                // Handle any errors that may have occurred.  
                                                e.printStackTrace();  
                                            }  
                                        }  
                                    }  
                                }  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination   
                    // tables to see how many rows were added.  
                    try (ResultSet rsRowCountHeader = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderHeader;"))  
                    {  
                        rsRowCountHeader.next();  
                        long countEndHeader =  rsRowCountHeader.getInt(1);  
                        System.out.println(  
                                (countEndHeader - countStartHeader) +   
                                " rows were added to the Header table.");  
                    }  
  
                    try (ResultSet rsRowCountDetail = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderDetail;"))  
                    {  
                        rsRowCountDetail.next();  
                        long countEndDetail = rsRowCountDetail.getInt(1);  
                        System.out.println(  
                                (countEndDetail - countStartDetail) +   
                                " rows were added to the Detail table.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;"  
                + "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
  
```  
  
##  <a name="BKMK_TransactionBulk"></a> 트랜잭션 및 대량 복사 작업  
 대량 복사 작업은 격리된 작업이나 여러 단계 트랜잭션의 일부로 수행할 수 있습니다. 후자 옵션을 사용하면 동일한 트랜잭션 내에서 둘 이상의 대량 복사 작업을 수행할 뿐만 아니라 전체 트랜잭션을 커밋하거나 롤백하면서 다른 데이터베이스 작업(예: 삽입, 업데이트 및 삭제)을 수행할 수 있습니다.  
  
 기본적으로 대량 복사 작업은 격리된 작업으로 수행됩니다. 대량 복사 작업은 트랜잭션되지 않은 방식으로 수행되어 롤백할 수 없습니다. 오류가 발생하여 대량 복사의 일부 또는 전체를 롤백해야 하는 경우 SQLServerBulkCopy 관리 트랜잭션을 사용하거나 기존 트랜잭션 내에서 대량 복사 작업을 수행할 수 있습니다.  
  
### <a name="performing-a-non-transacted-bulk-copy-operation"></a>트랜잭션되지 않은 대량 복사 작업 수행  
 다음 응용 프로그램에서는 트랜잭션되지 않은 대량 복사 작업 중 오류가 발생할 경우 어떻게 되는지를 보여 줍니다.  
  
 예제에서는 원본 테이블과 대상 테이블 각 라는 Id 열 포함 됩니다. **ProductID**합니다. 먼저 코드는 모든 행을 삭제 하 여 대상 테이블을 준비 하 고 행을 단일을 삽입 한 다음 **ProductID** 원본 테이블에 없는 것으로 알려져 있습니다. 기본적으로 ID 열에 대한 새 값은 추가된 각 행에 대한 대상 테이블에 생성됩니다. 이 예제에서 옵션은 대량 로드 프로세스에서 원본 테이블의 ID 값을 대신 강제로 사용하도록 하는 연결을 열 때 설정됩니다.  
  
 로 대량 복사 작업이 실행 되는 **BatchSize** 속성이 10로 설정 합니다. 작업에서 잘못된 행이 발견되는 경우 예외가 throw됩니다. 이 첫 번째 예제에서는 대량 복사 작업이 트랜잭션되지 않습니다. 오류 지점까지 복사된 모든 일괄 처리가 커밋됩니다. 중복 키가 포함된 일괄 처리는 롤백되고 대량 복사 작업은 다른 모든 일괄 처리를 처리하기 전에 중지됩니다.  
  
> [!NOTE]  
>  이 샘플을 만들지 않은 경우 작업 테이블에 설명 된 대로 실행 되지 것입니다 [테이블 설정](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup)합니다. 이 코드는 SQLServerBulkCopy를 사용하는 구문을 보여 주기 위해서만 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있는 경우에는 Transact-SQL INSERT … SELECT 문을 사용하면 더 쉽고 더 빠르게 데이터를 복사할 수 있습니다.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    //  Delete all from the destination table.  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoMatchingColumns");  
  
                    //  Add a single row that will result in duplicate key            
                    //  when all rows from source are bulk copied.            
                    //  Note that this technique will only be successful in             
                    //  illustrating the point if a row with ProductID = 446              
                    //  exists in the AdventureWorks Production.Products table.             
                    //  If you have made changes to the data in this table, change            
                    //  the SQL statement in the code to add a ProductID that            
                    //  does exist in your version of the Production.Products            
                    //  table. Choose any ProductID in the middle of the table            
                    //  (not first or last row) to best illustrate the result.  
                    stmt.executeUpdate("SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns ON;" +  
                            "INSERT INTO " + "dbo.BulkCopyDemoMatchingColumns " +  
                            "([ProductID], [Name] ,[ProductNumber]) " +  
                            "VALUES(446, 'Lock Nut 23','LN-3416');" +  
                            "SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns OFF");  
  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    //  Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
  
                        // Set up the bulk copy object using the KeepIdentity option and BatchSize = 10.  
                        SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();  
                        copyOptions.setKeepIdentity(true);  
                        copyOptions.setBatchSize(10);  
  
                        try (SQLServerBulkCopy bulkCopy =   
                                new SQLServerBulkCopy(connectionString))  
                        {  
                            bulkCopy.setBulkCopyOptions(copyOptions);  
                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                            // Write from the source to the destination.   
                            // This should fail with a duplicate key error   
                            // after some of the batches have been copied.   
                            try  
                            {  
                                bulkCopy.writeToServer(rsSourceData);  
                            }  
                            catch (Exception e)  
                            {  
                                // Handle any errors that may have occurred.  
                                e.printStackTrace();  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection String.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
              "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
```  
  
### <a name="performing-a-dedicated-build-copy-operation-in-a-transaction"></a>트랜잭션에서 전용 빌드 복사 작업 수행  
 기본적으로 대량 복사 작업은 고유한 트랜잭션입니다. 전용 대량 복사 작업을 수행하려면 연결 문자열이 있는 SQLServerBulkCopy의 새 인스턴스를 만듭니다. 이 시나리오에서는 대량 복사 작업에서 트랜잭션을 만든 다음 커밋하거나 롤백합니다. 명시적으로 지정할 수는 **UseInternalTransaction** 옵션 **SQLServerBulkCopyOptions** 대량의 각 배치가 자체 트랜잭션에서 실행 되도록 대량 복사 작업을 별도 트랜잭션 내에서 실행할 작업을 복사 합니다.  
  
> [!NOTE]  
>  다른 일괄 처리는 다른 트랜잭션에서 실행되므로 대량 복사 작업 중 오류가 발생하는 경우 현재 일괄 처리의 모든 행이 롤백되지만 이전 일괄 처리의 행은 데이터베이스에 유지됩니다.  
  
 다음 응용 프로그램은 한 가지를 제외하고 이전 예제와 유사합니다. 이 예제에서 대량 복사 작업은 고유 트랜잭션을 관리 합니다. 오류 지점까지 복사된 모든 일괄 처리가 커밋됩니다. 중복 키가 포함된 일괄 처리는 롤백되고 대량 복사 작업은 다른 모든 일괄 처리를 처리하기 전에 중지됩니다.  
  
> [!NOTE]  
>  이 샘플을 만들지 않은 경우 작업 테이블에 설명 된 대로 실행 되지 것입니다 [테이블 설정](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup)합니다. 이 코드는 SQLServerBulkCopy를 사용하는 구문을 보여 주기 위해서만 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있는 경우에는 Transact-SQL INSERT … SELECT 문을 사용하면 더 쉽고 더 빠르게 데이터를 복사할 수 있습니다.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    //  Delete all from the destination table.  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoMatchingColumns");  
  
                    //  Add a single row that will result in duplicate key            
                    //  when all rows from source are bulk copied.            
                    //  Note that this technique will only be successful in             
                    //  illustrating the point if a row with ProductID = 446              
                    //  exists in the AdventureWorks Production.Products table.             
                    //  If you have made changes to the data in this table, change            
                    //  the SQL statement in the code to add a ProductID that            
                    //  does exist in your version of the Production.Products            
                    //  table. Choose any ProductID in the middle of the table            
                    //  (not first or last row) to best illustrate the result.  
                    stmt.executeUpdate("SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns ON;" +  
                            "INSERT INTO " + "dbo.BulkCopyDemoMatchingColumns " +  
                            "([ProductID], [Name] ,[ProductNumber]) " +  
                            "VALUES(446, 'Lock Nut 23','LN-3416');" +  
                            "SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns OFF");  
  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    //  Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
  
                        // Set up the bulk copy object.  
                        // Note that when specifying the UseInternalTransaction   
                        // option, you cannot also use an external transaction.   
                        // Therefore, you must use the SQLServerBulkCopy construct that   
                        // requires a string for the connection, rather than an   
                        // existing Connection object.   
                        SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();  
                        copyOptions.setKeepIdentity(true);  
                        copyOptions.setBatchSize(10);  
                        copyOptions.setUseInternalTransaction(true);  
  
                        try (SQLServerBulkCopy bulkCopy =   
                                new SQLServerBulkCopy(connectionString))  
                        {  
                            bulkCopy.setBulkCopyOptions(copyOptions);  
                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                            // Write from the source to the destination.   
                            // This should fail with a duplicate key error   
                            // after some of the batches have been copied.   
                            try  
                            {  
                                bulkCopy.writeToServer(rsSourceData);  
                            }  
                            catch (Exception e)  
                            {  
                                // Handle any errors that may have occurred.  
                                e.printStackTrace();  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;"  
                + "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
```  
  
### <a name="using-existing-transactions"></a>기존 트랜잭션 사용  
 트랜잭션이 SQLServerBulkCopy 생성자의 매개 변수로 설정된 연결 개체를 전달할 수 있습니다. 이 상황에서는 대량 복사 작업이 기존 트랜잭션에서 수행되며 트랜잭션 상태가 변경되지 않습니다. 즉, 커밋되거나 중단되지 않습니다. 따라서 응용 프로그램이 다른 데이터베이스 작업과 함께 대량 복사 작업을 트랜잭션에 포함할 수 있습니다. 오류가 발생하여 전체 대량 복사 작업을 롤백해야 하는 경우 또는 롤백할 수 있는 더 큰 프로세스의 일부로 대량 복사를 실행해야 하는 경우 대량 복사 작업 후 임의 지점에서 연결 개체에 대한 롤백을 수행할 수 있습니다.  
  
 다음 응용 프로그램은 한 가지 예외를 제외하고 트랜잭션되지 않은 첫 번째 예제와 유사합니다. 이 예제에서는 대량 복사 작업이 더 큰 외부 트랜잭션에 포함됩니다. 기본 키 위반 오류가 발생하면 전체 트랜잭션이 롤백되고 행이 대상 테이블에 추가되지 않습니다.  
  
> [!NOTE]  
>  이 샘플을 만들지 않은 경우 작업 테이블에 설명 된 대로 실행 되지 것입니다 [테이블 설정](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup)합니다. 이 코드는 SQLServerBulkCopy를 사용하는 구문을 보여 주기 위해서만 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있는 경우에는 Transact-SQL INSERT … SELECT 문을 사용하면 더 쉽고 더 빠르게 데이터를 복사할 수 있습니다.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    //  Delete all from the destination table.  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoMatchingColumns");  
  
                    //  Add a single row that will result in duplicate key            
                    //  when all rows from source are bulk copied.            
                    //  Note that this technique will only be successful in             
                    //  illustrating the point if a row with ProductID = 446              
                    //  exists in the AdventureWorks Production.Products table.             
                    //  If you have made changes to the data in this table, change            
                    //  the SQL statement in the code to add a ProductID that            
                    //  does exist in your version of the Production.Products            
                    //  table. Choose any ProductID in the middle of the table            
                    //  (not first or last row) to best illustrate the result.  
                    stmt.executeUpdate("SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns ON;" +  
                            "INSERT INTO " + "dbo.BulkCopyDemoMatchingColumns " +  
                            "([ProductID], [Name] ,[ProductNumber]) " +  
                            "VALUES(446, 'Lock Nut 23','LN-3416');" +  
                            "SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns OFF");  
  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    //  Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
  
                        // Set up the bulk copy object inside the transaction.  
                        try (Connection destinationConnection =   
                                DriverManager.getConnection(connectionString))  
                        {  
                            destinationConnection.setAutoCommit(false);  
  
                            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();  
                            copyOptions.setKeepIdentity(true);  
                            copyOptions.setBatchSize(10);  
  
                            try (SQLServerBulkCopy bulkCopy =   
                                    new SQLServerBulkCopy(destinationConnection))  
                            {  
                                bulkCopy.setBulkCopyOptions(copyOptions);  
                                bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                                // Write from the source to the destination.   
                                // This should fail with a duplicate key error.   
                                try  
                                {  
                                    bulkCopy.writeToServer(rsSourceData);  
                                    destinationConnection.commit();  
                                }  
                                catch (Exception e)  
                                {  
                                    // Handle any errors that may have occurred.  
                                    e.printStackTrace();  
                                    destinationConnection.rollback();  
                                }  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;"  
                + "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
  
```  
  
### <a name="bulk-copy-from-a-csv-file"></a>CSV 파일에서 대량 복사  
 다음 응용 프로그램에서는 SQLServerBulkCopy 클래스를 사용하여 데이터를 로드하는 방법을 보여 줍니다. 이 예제에서 CSV 파일은 SQL Server AdventureWorks 데이터베이스의 Production.Product 테이블에서 내보낸 데이터를 데이터베이스의 유사한 테이블에 복사하는 데 사용됩니다.  
  
> [!IMPORTANT]  
>  이 샘플을 만들지 않은 경우 작업 테이블에 설명 된 대로 실행 되지 것입니다 [테이블 설정](../../ssms/download-sql-server-management-studio-ssms.md) 를 가져오려고 합니다.  
  
1.  열기 **SQL Server Management Studio** 및 AdventureWorks 데이터베이스가 있는 SQL Server에 연결 합니다.  
  
2.  데이터베이스를 확장, AdventureWorks 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고, 선택 **작업** 및 **데이터 내보내기**...  
  
3.  데이터 원본에 대 한 선택은 **데이터 소스** 되는 구성을 확인 합니다 (예: SQL Server Native Client 11.0) SQL Server에 연결할 수 있습니다 및 **다음**  
  
4.  대상으로 선택 된 **플랫 파일 대상** 입력는 **파일 이름** C:\Test\TestBulkCSVExample.csv 예. 있는지 여부를 확인는 **형식** 구분 됩니다는 **텍스트 한정자** none, 이며 사용 **첫 번째 데이터 행의 열 이름**를 선택한 후 **다음**  
  
5.  선택 **전송 데이터를 지정 하는 쿼리를 작성할** 및 **다음**합니다.  입력 프로그램 **SQL 문을** 선택 ProductID, Name, ProductNumber FROM Production.Product 및 **다음**  
  
6.  구성을 확인 하십시오: {CR} {LF}로 행 구분 기호 및 열 구분 기호는 쉼표 그대로 두면 {,}합니다.  선택 **매핑 편집**... 있는지 여부를 확인 하 고 데이터 **형식** 은 각 열 (예: 다른 항목에 대 한 ProductID 및 유니코드 문자열에 대 한 정수)에 적합 합니다.  
  
7.  로 건너뛰십시오 **마침** 내보내기를 실행 합니다.  
  
```  
  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCSVFileRecord;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        SQLServerBulkCSVFileRecord fileRecord = null;  
        try  
        {              
            // Get data from the source file by loading it into a class that implements ISQLServerBulkRecord.  
            // Here we are using the SQLServerBulkCSVFileRecord implementation to import the example CSV file.  
            fileRecord = new SQLServerBulkCSVFileRecord("C:\\Test\\TestBulkCSVExample.csv", true);      
  
            // Set the metadata for each column to be copied.  
            fileRecord.addColumnMetadata(1, null, java.sql.Types.INTEGER, 0, 0);  
            fileRecord.addColumnMetadata(2, null, java.sql.Types.NVARCHAR, 50, 0);  
            fileRecord.addColumnMetadata(3, null, java.sql.Types.NVARCHAR, 25, 0);  
  
            // Open a destinationConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection destinationConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = destinationConnection.createStatement())  
                {  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    // Set up the bulk copy object.    
                    // Note that the column positions in the source   
                    // data reader match the column positions in    
                    // the destination table so there is no need to   
                    // map columns.   
                    try (SQLServerBulkCopy bulkCopy =  
                               new SQLServerBulkCopy(destinationConnection))  
                    {  
                        bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                        try  
                        {  
                            // Write from the source to the destination.  
                            bulkCopy.writeToServer(fileRecord);  
                        }  
                        catch (Exception e)  
                        {  
                            // Handle any errors that may have occurred.  
                            e.printStackTrace();  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
        finally  
        {  
            if (fileRecord != null) try { fileRecord.close(); } catch(Exception e) {}  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
           "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
  
```  
  
### <a name="bulk-copy-with-always-encrypted-columns"></a>상시 암호화 열을 사용 하 여 대량 복사  
 SQL Server 용 Microsoft JDBC Driver 6.0부터, 상시 암호화 열이 있는 대량 복사는 지원 합니다.  
  
 대량 복사 옵션 및 암호화에 따라 JDBC 드라이버 수 투명 하 게 해독 한 다음 암호화 또는 데이터 원본 및 대상 테이블의 형식을 그대로 암호화 된 데이터를 보낼 수 있습니다. 예를 들어 대량 암호화 된 열에서 암호화 되지 않은 열 데이터를 복사 하는 경우 드라이버 데이터 SQL Server로 보내기 전에 투명 하 게 해독 합니다. 마찬가지로 대량 암호화 되지 않은 열 (또는 CSV 파일) 암호화 된 열에 데이터를 복사 하는 경우 드라이버 데이터 SQL Server로 보내기 전에 투명 하 게 암호화 합니다. 원본 모두 대상 암호화 하는 경우 다음에 따라는 **allowEncryptedValueModifications** 대량 복사 옵션 또는 데이터를 암호 해독이 고 SQL Server로 보내기 전에 다시 암호화 드라이버에서 데이터를 보내는 것과 합니다.  
  
 자세한 내용은 참조는 **allowEncryptedValueModifications** 대량 복사 옵션 아래 및 [상시 암호화와 JDBC 드라이버를 사용 하 여](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)합니다.  
  
> [!IMPORTANT]  
>  대량 암호화 된 열에는 CSV 파일에서 데이터를 복사 하는 경우 SQL Server 용 Microsoft JDBC Driver 6.0의 제한 사항:  
>   
>  날짜 및 시간 형식 Transact SQL 기본 문자열 리터럴 형식에만 사용할 수  
>   
>  DATETIME 및 SMALLDATETIME 데이터 형식 지원 되지 않습니다.  
  
## <a name="bulk-copy-api-for-jdbc-driver"></a>JDBC 드라이버용 대량 복사 API  
  
### <a name="sqlserverbulkcopy"></a>SQLServerBulkCopy  
 다른 원본의 데이터를 사용하여 SQL Server 테이블을 효율적으로 대량 로드할 수 있습니다.  
  
 Microsoft SQL Server에는 많이 사용되는 bcp라는 명령 프롬프트 유틸리티가 있어 단일 서버인지 서버 간인지에 관계없이 테이블 간에 데이터를 이동할 수 있습니다. SQLServerBulkCopy 클래스를 사용하면 비슷한 기능을 제공하는 코드 솔루션을 Java로 작성할 수 있습니다. INSERT 문과 같은 다른 방법을 사용하여 데이터를 SQL Server 테이블에 로드할 수 있지만 SQLServerBulkCopy는 훨씬 더 향상된 성능을 제공합니다.  
  
 SQLServerBulkCopy 클래스를 사용하면 SQL Server 테이블에만 데이터를 작성할 수 있습니다. 그러나 데이터 원본은 SQL Server로 제한되지 않습니다. ResultSet 인스턴스나 ISQLServerBulkRecord 구현으로 데이터를 읽을 수 있는 한 모든 데이터 원본을 사용할 수 있습니다.  
  
|생성자|Description|  
|-----------------|-----------------|  
|SQLServerBulkCopy(Connection)|SQLServerConnection의 지정된 된 열린 인스턴스를 사용 하 여 SQLServerBulkCopy 클래스의 새 인스턴스를 초기화 합니다. 연결에 사용하도록 설정된 트랜잭션이 있으면 해당 트랜잭션 내에서 복사 작업이 수행됩니다.|  
|SQLServerBulkCopy (문자열 connectionURL)|초기화 하 고 제공된 된 connectionURL에 따라 SQLServerConnection의 새 인스턴스를 엽니다. 생성자는 SQLServerConnection을 사용 하 여 SQLServerBulkCopy 클래스의 새 인스턴스를 초기화 합니다.|  
  
|속성|Description|  
|--------------|-----------------|  
|문자열 DestinationTableName|서버에 있는 대상 테이블의 이름입니다.<br /><br /> writeToServer가 호출될 때 DestinationTableName 이 설정되지 않은 경우 SQLServerException이 throw됩니다.<br /><br /> DestinationTableName은 세 부분으로 이루어진 이름 (\<데이터베이스 >.\< m a >. \<이름 >). 원하는 경우 데이터베이스 및 소유 스키마로 테이블 이름을 한정할 수 있습니다. 그러나 테이블 이름에서 밑줄("_")이나 다른 특수 문자를 사용하는 경우 주변 대괄호를 사용하여 이름을 이스케이프해야 합니다. 자세한 내용은 SQL Server 온라인 설명서의 “Identifiers”를 참조하세요.|  
|ColumnMappings|열 매핑에서는 데이터 원본의 열과 대상의 열 간 관계를 정의합니다.<br /><br /> 매핑이 정의되지 않은 경우 열은 서수 위치에 따라 암시적으로 매핑됩니다. 이렇게 하려면 원본 및 대상 스키마가 일치해야 합니다. 그렇지 않으면 예외가 throw됩니다.<br /><br /> 매핑이 비어 있지 않을 경우 데이터 원본에 있는 일부 열을 지정할 수 없으며, 매핑되지 않은 열은 무시됩니다.<br /><br /> 원본 및 대상 열은 이름이나 서수로 나타낼 수 있습니다.|  
  
|메서드|Description|  
|------------|-----------------|  
|Void addColumnMapping ((sourceColumn int, int destinationColumn)|서수를 사용하여 원본 및 대상 열을 지정하는 새로운 열 매핑을 추가합니다.|  
|Void addColumnMapping ((int sourceColumn, 문자열 destinationColumn)|원본 열에는 서수를, 대상 열에는 열 이름을 사용하는 새로운 열 매핑을 추가합니다.|  
|Void addColumnMapping ((문자열 sourceColumn, int destinationColumn)|열 이름을 사용하여 원본 열을 설명하고 서수를 사용하여 대상 열을 지정하는 새로운 열 매핑을 추가합니다.|  
|Void addColumnMapping (문자열 sourceColumn, 문자열 destinationColumn)|열 이름을 사용하여 원본 및 대상 열을 모두 지정하는 새로운 열 매핑을 추가합니다.|  
|Void clearColumnMappings()|열 매핑의 내용을 지웁니다.|  
|Void close)|SQLServerBulkCopy 인스턴스를 닫습니다.|  
|SQLServerBulkCopyOptions getBulkCopyOptions()|SQLServerBulkCopyOptions의 현재 집합을 검색합니다.|  
|문자열 getDestinationTableName()|현재 대상 테이블 이름을 검색합니다.|  
|Void setBulkCopyOptions(SQLServerBulkCopyOptions copyOptions)|제공된 옵션에 따라 SQLServerBulkCopy 인스턴스의 동작을 업데이트합니다.|  
|Void setDestinationTableName(String tableName)|대상 테이블의 이름을 설정합니다.|  
|Void writeToServer(ResultSet sourceData)|제공된 된 ResultSet의 모든 행을 SQLServerBulkCopy 개체의 DestinationTableName 속성으로 지정 된 대상 테이블에 복사 합니다.|  
|Void writeToServer(RowSet sourceData)|제공된 RowSet의 모든 행을 SQLServerBulkCopy 개체의 DestinationTableName 속성으로 지정된 대상 테이블에 복사합니다.|  
|Void writeToServer(ISQLServerBulkRecord sourceData)|복사의 대상 테이블에 제공된 된 ISQLServerBulkRecord 구현의 모든 행 SQLServerBulkCopy 개체의 DestinationTableName 속성으로 지정 합니다.|  
  
### <a name="sqlserverbulkcopyoptions"></a>SQLServerBulkCopyOptions  
 WriteToServer 메서드가 SQLServerBulkCopy의 인스턴스에서 작동하는 방식을 제어하는 설정의 컬렉션입니다.  
  
|생성자|Description|  
|-----------------|-----------------|  
|SQLServerBulkCopyOptions()|모든 설정에 대 한 기본값을 사용 하 여 SQLServerBulkCopyOptions 클래스의 새 인스턴스를 초기화 합니다.|  
  
 다음 옵션에 대한 Getter 및 setter가 있습니다.  
  
|옵션|Description|기본값|  
|------------|-----------------|-------------|  
|부울 CheckConstraints|데이터가 삽입되는 동안 제약 조건을 확인합니다.|False - 제약 조건을 확인하지 않습니다.|  
|부울 FireTriggers|지정한 경우 서버에서 데이터베이스에 삽입할 행에 대해 삽입 트리거를 발생하도록 합니다.|False - 트리거가 발생하지 않습니다.|  
|부울 KeepIdentity|원본 ID 값을 유지합니다.|False - ID 값이 대상에 의해 할당됩니다.|  
|부울 KeepNulls|기본값에 대한 설정에 관계없이 대상 테이블에서 null 값을 유지합니다.|False - 해당되는 경우 null 값이 기본값으로 대체됩니다.|  
|부울 TableLock|대량 복사 작업의 기간 동안 대량 업데이트 잠금을 획득합니다.|False - 행 잠금이 사용됩니다.|  
|부울 UseInternalTransaction|지정한 경우 대량 복사 작업의 각 일괄 처리가 트랜잭션 내에서 발생됩니다. SQLServerBulkCopy가 생성자에 지정된 대로 기존 연결을 사용하는 경우 SQLServerException이 발생합니다.  SQLServerBulkCopy에서 전용 연결을 만든 경우 트랜잭션이  전용된 연결을 만든 경우 트랜잭션이 활성화됩니다.|False - 트랜잭션이 없습니다.|  
|Int BatchSize|각 일괄 처리의 행 수입니다. 각 일괄 처리가 끝나면 일괄 처리의 행이 서버로 보내집니다.<br /><br /> 일괄 처리는 BatchSize 행이 처리되었거나 대상 데이터 원본으로 보낼 행이 더 이상 없는 경우 완료됩니다.  SQLServerBulkCopy 인스턴스가 UseInternalTransaction 옵션을 적용하지 않고 선언된 경우 행은 한 번에 서버 BatchSize 행으로 보내지지만 트랜잭션 관련 작업이 수행되지 않습니다. UseInternalTransaction이 적용된 경우 행의 각 일괄 처리가 별도의 트랜잭션으로 삽입됩니다.|0 - 각 writeToServer 작업이 단일 일괄 처리임을 나타냅니다.|  
|Int BulkCopyTimeout|제한 시간이 초과되기 전에 작업이 완료되는 시간(초)입니다. 0 값은 제한이 없음을 나타내며 대량 복사가 무기한 대기합니다.|60초입니다.|  
|부울 allowEncryptedValueModifications|이 옵션을 사용할 수 있는 Microsoft JDBC Driver 6.0 (또는 그 이상) for SQL Server.<br /><br /> 을 지정 하면 **allowEncryptedValueModifications** 데이터를 해독 하지 않고 테이블 또는 데이터베이스 간에 암호화 된 데이터의 대량 복사할 수 있습니다. 응용 프로그램 (응용 프로그램은 데이터베이스에 연결 사용 안 함으로 설정 하는 열 암호화 설정 키워드와 함께) 데이터를 해독 하지 않고 한 테이블에서 암호화 된 열에서 데이터를 선택 합니다 하 고 데이터를 대량 복사 하려면이 옵션을 사용 하는 일반적으로, 여전히 암호화 됩니다. 자세한 내용은 참조 [상시 암호화와 JDBC 드라이버를 사용 하 여](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)합니다.<br /><br /> 지정할 때는 주의 **allowEncryptedValueModifications** 드라이버 경우 데이터가 암호화 되었는지 검사 하지 않기 때문에 데이터베이스를 손상 될 수 또는 동일한 암호화를 사용 하 여 올바르게 암호화 된 경우 형식, 알고리즘 및 키에 대상 열으로 합니다.||  
  
 Getter 및 setter:  
  
|메서드|Description|  
|-------------|-----------------|  
|부울 isCheckConstraints()|제약 조건 확인 여부 데이터가 삽입 되는 동안 확인 되는지 여부를 나타냅니다.|  
|Void setCheckConstraints(Boolean checkConstraints)|제약 조건 확인 여부 데이터가 삽입 되는 동안 확인 여부를 설정 합니다.|  
|부울 isFireTriggers()|서버 데이터베이스에 삽입 되는 행에 대 한 insert 트리거를 발생 시켜야 하는 경우를 나타냅니다.|  
|Void setFireTriggers(Boolean fireTriggers)|데이터베이스에 삽입 되는 행에 대 한 트리거를 실행 하려면 서버를 설정 해야 하는지 여부를 설정 합니다.|  
|부울 isKeepIdentity()|모든 소스 id 값을 유지할지 여부를 나타냅니다.|  
|Void setKeepIdentity(Boolean keepIdentity)|Id 값을 유지 여부를 설정 합니다.|  
|부울 isKeepNulls()|이러한 교체 해야 기본값 (있는 경우) 또는 기본 값에 대 한 설정에 관계 없이 대상 테이블에서 null 값을 유지할지 여부를 나타냅니다.|  
|Void setKeepNulls(Boolean keepNulls)|이러한 교체 해야 기본값 (있는 경우) 또는 기본 값에 대 한 설정에 관계 없이 대상 테이블에서 null 값을 유지할지 여부를 설정 합니다.|  
|부울 isTableLock()|SQLServerBulkCopy 대량 복사 작업의 기간에 대 한 한 대량 업데이트 잠금을 획득 해야 있는지 여부를 나타냅니다.|  
|Void setTableLock(Boolean tableLock)|SQLServerBulkCopy 대량 복사 작업의 기간에 대 한 한 대량 업데이트 잠금을 획득 해야 하는지 여부를 설정 합니다.|  
|부울 isUseInternalTransaction()|트랜잭션 내에서 대량 복사 작업의 각 일괄 처리가 발생 여부를 나타냅니다.|  
|Void setUseInternalTranscation(Boolean useInternalTransaction)|여부는 대량 복사 작업의 각 일괄 처리가 트랜잭션 내에서 발생 합니다 있는지 여부를 설정 합니다.|  
|Int getBatchSize()|각 일괄 처리의 행 수를 가져옵니다. 서버로 전송 되는 일괄 처리의 행 각 일괄 처리의 끝|  
|Void setBatchSize(int batchSize)|각 일괄 처리의 행 수를 설정합니다. 각 일괄 처리가 끝나면 일괄 처리의 행이 서버로 보내집니다.|  
|Int getBulkCopyTimeout()|시간 (초) 작업에 대 한 제한 시간이 초과 되기 전에 완료할 수를 가져옵니다.|  
|Void setBulkCopyTimeout(int timeout)|제한 시간이 초과 되기 전에 완료할 작업에 대 한 시간을 초 단위로 설정 합니다.|  
|부울 isAllowEncryptedValueModifications()|AllowEncryptedValueModifications 설정이 사용 되는지 여부를 나타냅니다.|  
|void setAllowEncryptedValueModifications(boolean allowEncryptedValueModifications)|상시 암호화 열을 사용 하 여 대량 복사에 사용 되는 allowEncryptedValueModifications 설정을 구성 합니다.|  
  
### <a name="isqlserverbulkrecord"></a>ISQLServerBulkRecord  
 ISQLServerBulkRecord 인터페이스는 원본(예: 파일)에서 데이터를 읽고 SQLServerBulkCopy 인스턴스에서 해당 데이터로 SQL Server 테이블을 대량 로드할 수 있도록 하는 클래스를 만드는 데 사용할 수 있습니다.  
  
|인터페이스 메서드|Description|  
|-----------------------|-----------------|  
|설정\<정수 > getColumnOrdinals()|이 데이터 레코드에 표시된 각 열에 대한 서수를 가져옵니다.|  
|문자열 getColumnName(int column)|지정된 열의 이름을 가져옵니다.|  
|Int getColumnType (int 열)|지정된 열의 JDBC 데이터 형식을 가져옵니다.|  
|Int getPrecision (int 열)|지정된 열의 전체 자릿수를 가져옵니다.|  
|개체 getRowData()|현재 행에 대한 데이터를 개체의 배열로 가져옵니다.<br /><br /> 각 개체는 지정된 열에 대해 표시된 JDBC 데이터 형식을 나타내는 데 사용되는 Java 언어 형식과 일치해야 합니다.  자세한 내용은 'JDBC 드라이버 데이터 형식 이해’에서 적절한 매핑을 참조하세요.|  
|Int getScale (int 열)|지정된 열에 대한 소수 자릿수를 가져옵니다.|  
|부울 isAutoIncrement (int 열)|열이 ID 열을 나타내는지 여부를 나타냅니다.|  
|부울 next)|다음 데이터 행으로 이동합니다.|  
  
### <a name="sqlserverbulkcsvfilerecord"></a>SQLServerBulkCSVFileRecord  
 각 줄이 데이터 행을 나타내는 구분 기호로 분리된 파일에서 기본 Java 데이터 형식을 읽는 데 사용할 수 있는 ISQLServerBulkRecord 인터페이스의 간단한 구현입니다.  
  
 구현 참고 사항 및 제한 사항:  
  
1.  한 번에 한 줄씩 데이터를 읽으므로 지정된 모든 행에서 허용되는 최대 데이터 크기는 사용 가능한 메모리에 의해 제한됩니다.  
  
2.  varchar(max), varbinary(max), nvarchar(max), sqlxml, ntext 등 큰 데이터 형식의 스트리밍은 지원되지 않습니다.  
  
3.  CSV 파일에 대해 지정된 구분 기호는 데이터의 임의 위치에 표시되지 않아야 하며 Java 정규식에서 제한된 문자인 경우 올바르게 이스케이프되어야 합니다.  
  
4.  CSV 파일 구현에서 큰따옴표는 데이터의 일부로 처리됩니다. 예를 들어 hello,”world”,”hello,world” 줄은 구분 기호가 쉼표인 경우 hello, “world”, “hello 및 world” 값을 갖는 네 개의 열이 있는 것으로 처리됩니다.  
  
5.  줄 바꿈 문자는 행 종결자로 사용되며 데이터의 임의 위치에서 허용되지 않습니다.  
  
|생성자|Description|  
|-----------------|-----------------|  
|SQLServerBulkCSVFileRecord (문자열 fileToParse, 문자열 인코딩, 문자열 구분 기호, 부울 firstLineIsColumnNamesSQLServerBulkCSVFileRecord (문자열, String, String, boolean)|제공된 구분 기호 및 인코딩으로 fileToParse의 각 줄을 구분 분석하는 SQLServerBulkCSVFileRecord 클래스의 새 인스턴스를 초기화합니다. FirstLineIsColumnNames가 True로 설정된 경우 파일의 첫 줄은 열 이름으로 구문 분석됩니다.  인코딩이 NULL인 경우에는 기본 인코딩이 사용됩니다.|  
|SQLServerBulkCSVFileRecord (문자열 fileToParse, 문자열 인코딩, 부울 firstLineIsColumnNamesSQLServerBulkCSVFileRecord (String, String, boolean)|구분 기호 및 제공된 인코딩으로 fileToParse의 각 줄을 구분 분석하는 SQLServerBulkCSVFileRecord 클래스의 새 인스턴스를 초기화합니다. FirstLineIsColumnNames가 True로 설정된 경우 파일의 첫 줄은 열 이름으로 구문 분석됩니다.  인코딩이 NULL인 경우에는 기본 인코딩이 사용됩니다.|  
|SQLServerBulkCSVFileRecord (문자열 fileToParse, 부울 firstLineIsColumnNamesSQLServerBulkCSVFileRecord (String, boolean)|쉼표 구분 기호 및 기본 인코딩으로 fileToParse의 각 줄을 구분 분석하는 SQLServerBulkCSVFileRecord 클래스의 새 인스턴스를 초기화합니다. FirstLineIsColumnNames가 True로 설정에 파일의 첫 번째 줄에는 됩니다 열 이름으로 구문 분석할 수 있습니다.|  
  
|메서드|Description|  
|------------|-----------------|  
|Void addColumnMetadata (int positionInFile, 문자열 열 이름, int jdbcType, int 정밀도, 배율 int)|파일의 지정된 열에 대한 메타데이터를 추가합니다.|  
|Void close)|파일 판독기와 관련된 모든 리소스를 해제합니다.|  
|Void setTimestampWithTimezoneFormat (DateTim eFormatter dateTimeFormatter|파일의 타임스탬프 데이터를 java.sql.Types.TIMESTAMP_WITH_TIMEZONE으로 구문 분석하는 형식을 설정합니다.|  
|Void setTimestampWithTimezoneFormat(String dateTimeFormat)setTimeWithTimezoneFormat(DateTimeFormatter)|파일의 시간 데이터를 java.sql.Types.TIME_WITH_TIMEZONE으로 구문 분석하는 형식을 설정합니다.|  
|Void setTimeWithTimezoneFormat (DateTimeForm atter dateTimeFormatter)|파일의 시간 데이터를 java.sql.Types.TIME_WITH_TIMEZONE으로 구문 분석하는 형식을 설정합니다.|  
|Void setTimeWithTimezoneFormat(String timeFormat)|파일의 시간 데이터를 java.sql.Types.TIME_WITH_TIMEZONE으로 구문 분석하는 형식을 설정합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
