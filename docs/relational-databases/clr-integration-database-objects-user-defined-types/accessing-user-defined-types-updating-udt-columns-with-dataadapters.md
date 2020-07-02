---
title: Dataadapter를 사용 하 여 UDT 열 업데이트 | Microsoft Docs
description: SQL Server 데이터베이스의 Udt는 데이터를 검색 및 수정 하기 위해 SqlDataAdapter 및를 사용 하 여 지원 됩니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- ADO.NET [CLR integration]
- updating data [CLR integration]
- populating DataSet
- datasets [CLR integration]
- UDTs [CLR integration], ADO.NET
- updating UDT columns
- user-defined types [CLR integration], ADO.NET
- data adapters [CLR integration]
ms.assetid: 4489c938-ba03-4fdb-b533-cc3f5975ae50
author: rothja
ms.author: jroth
ms.openlocfilehash: 07b1dc9d3f7beca9f048ec0e367c33922e388f32
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727832"
---
# <a name="accessing-user-defined-types---updating-udt-columns-with-dataadapters"></a>사용자 정의 형식 액세스 - DataAdapters로 UDT 열 업데이트
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Udt (사용자 정의 형식)는 데이터를 검색 및 수정 **하는** **SqlDataAdapter** 및 데이터를 사용 하 여 지원 됩니다.  
  
## <a name="populating-a-dataset"></a>데이터 세트 채우기  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 문을 사용하여 UDT 열 값을 선택하면 데이터 어댑터를 사용하여 데이터 세트을 채울 수 있습니다. 다음 예에서는 다음 구조와 일부 샘플 데이터를 사용 하 여 정의 된 **Points** 테이블이 있다고 가정 합니다. 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 **Points** 테이블을 만들고 몇 개의 행을 삽입 합니다.  
  
```  
CREATE TABLE dbo.Points (id int PRIMARY Key, p Point);  
  
INSERT INTO dbo.Points VALUES (1, CONVERT(Point, '1,3'));  
INSERT INTO dbo.Points VALUES (2, CONVERT(Point, '2,4'));  
INSERT INTO dbo.Points VALUES (3, CONVERT(Point, '3,5'));  
INSERT INTO dbo.Points VALUES (4, CONVERT(Point, '4,6'));  
GO  
```  
  
 다음 ADO.NET 코드 조각에서는 유효한 연결 문자열을 검색 하 고, 새 **SqlDataAdapter**를 만든 다음, **Points** 테이블의 데이터 **행으로 system.xml을 채웁니다** .  
  
```vb  
Dim da As New SqlDataAdapter( _  
    "SELECT id, p FROM dbo.Points", connectionString)  
Dim datTable As New DataTable("Points")  
da.Fill(datTable)  
```  
  
```csharp  
SqlDataAdapter da = new SqlDataAdapter(  
   "SELECT id, p FROM dbo.Points", connectionString);  
DataTable datTable = new DataTable("Points");  
da.Fill(datTable);  
```  
  
## <a name="updating-udt-data-in-a-dataset"></a>데이터 세트의 UDT 데이터 업데이트  
 다음 두 가지 방법을 사용 하 여 **데이터 집합**의 UDT 열을 업데이트할 수 있습니다.  
  
-   **SqlDataAdapter** 개체에 대 한 사용자 지정 **InsertCommand**, **UpdateCommand** 및 **DeleteCommand** 개체를 제공 합니다.  
  
-   명령 작성기 (**SqlCommandBuilder**)를 사용 하 여 자동으로 INSERT, UPDATE 및 DELETE 명령을 만듭니다. 충돌 감지를 위해 UDT가 포함 된 테이블에 **timestamp** 열 (alias **rowversion**)을 추가 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **Timestamp** 데이터 형식을 사용 하 여 테이블의 행을 버전 스탬프로 만들고 데이터베이스 내에서 고유 하 게 보장할 수 있습니다. 테이블의 값이 변경되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 자동으로 변경이 적용되는 행의 8바이트 이진 숫자를 업데이트합니다.  
  
 기본 테이블에 **timestamp** 열이 없는 경우 **SqlCommandBuilder** 는 충돌 검색에 UDT를 고려 하지 않습니다. UDT는 비교가 가능할 수도 있고 불가능할 수도 있으므로 "원래 값 비교" 옵션을 사용하여 명령을 생성하는 경우 WHERE 절에 포함되지 않습니다.  
  
### <a name="example"></a>예제  
 다음 예에서는 **Point** UDT 열 뿐만 아니라 **timestamp** 열을 포함 하는 두 번째 테이블을 만들어야 합니다. 두 테이블은 데이터를 업데이트 하는 사용자 지정 명령 개체를 만드는 방법과 **타임 스탬프** 열을 사용 하 여 업데이트 하는 방법을 설명 하는 데 사용 됩니다. 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하여 두 번째 테이블을 만들고 예제 데이터를 채웁니다.  
  
```  
CREATE TABLE dbo.Points_ts (id int PRIMARY KEY, p Point, ts timestamp);  
  
INSERT INTO dbo.Points_ts (id, p) VALUES (1, CONVERT(Point, '1,3'));  
INSERT INTO dbo.Points_ts (id, p) VALUES (2, CONVERT(Point, '2,4'));  
INSERT INTO dbo.Points_ts (id, p) VALUES (3, CONVERT(Point, '3,5'));  
INSERT INTO dbo.Points_ts (id, p) VALUES (4, CONVERT(Point, '4,6'));  
```  
  
 다음 ADO.NET 예에는 두 개의 메서드가 있습니다.  
  
-   **InsertCommand**, **UpdateCommand**및 **DeleteCommand** 개체를 제공 하 여 **Points** 테이블 ( **타임 스탬프** 열이 포함 되지 않음)의 **Point** UDT를 업데이트 하는 방법을 보여 주는 **user제공**되는 명령입니다.  
  
-   **CommandBuilder**는 **타임 스탬프** 열이 포함 된 **Points_ts** 테이블에서 **SqlCommandBuilder** 를 사용 하는 방법을 보여 줍니다.  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
    ' Retrieves the connection string  
    Private connString As String = GetConnectionString()  
  
    Sub Main()  
        UserProvidedCommands()  
        CommandBuilder()  
    End Sub  
  
    Private Sub UserProvidedCommands()  
        ' Create a new SqlDataAdapter  
        Dim da As New SqlDataAdapter( _  
          "SELECT id, p FROM dbo.Points", connString)  
  
        ' Setup the INSERT/UPDATE/DELETE commands  
        Dim idParam As SqlParameter  
        Dim pointParam As SqlParameter  
  
        da.InsertCommand = New SqlCommand( _  
          "INSERT INTO dbo.Points (id, p) VALUES (@id, @p)", _  
          da.SelectCommand.Connection)  
        idParam = da.InsertCommand.Parameters.Add( _  
          "@id", SqlDbType.Int)  
        idParam.SourceColumn = "id"  
        pointParam = da.InsertCommand.Parameters.Add( _  
          "@p", SqlDbType.Udt)  
        pointParam.SourceColumn = "p"  
        pointParam.UdtTypeName = "dbo.Point"  
  
        da.UpdateCommand = New SqlCommand( _  
          "UPDATE dbo.Points SET p = @p WHERE id = @id", _  
          da.SelectCommand.Connection)  
        idParam = _  
           da.UpdateCommand.Parameters.Add("@id", SqlDbType.Int)  
        idParam.SourceColumn = "id"  
        pointParam = da.UpdateCommand.Parameters.Add( _  
          "@p", SqlDbType.Udt)  
        pointParam.SourceColumn = "p"  
        pointParam.UdtTypeName = "dbo.Point"  
  
        da.DeleteCommand = New SqlCommand( _  
          "DELETE dbo.Points WHERE id = @id", _  
          da.SelectCommand.Connection)  
        idParam = da.DeleteCommand.Parameters.Add( _  
          "@id", SqlDbType.Int)  
        idParam.SourceColumn = "id"  
  
        ' Fill the DataTable with UDT rows  
        Dim datTable As New DataTable("Points")  
        da.Fill(datTable)  
  
        ' Display the contents of the p (Point) column  
        Dim r As DataRow  
        For Each r In datTable.Rows  
            Dim p As Point = CType(r(1), Point)  
            Console.WriteLine( _  
              "ID: {0}, x={1}, y={1}", r(0), p.X, p.Y)  
        Next r  
  
        ' Update a row if the DataTable has at least 1 row  
        If datTable.Rows.Count > 0 Then  
            Dim oldPoint As Point = _  
              CType(datTable.Rows(0)(1), Point)  
            datTable.Rows(0)(1) = _  
              New Point(oldPoint.X + 1, oldPoint.Y + 1)  
        End If  
  
        ' Delete the last row  
        If datTable.Rows.Count > 0 Then  
            ' If we have at least 1 row  
            datTable.Rows(1).Delete()  
        End If  
  
        ' Insert a row. This will fail if run twice  
        ' because 100 is a primary key value.  
        datTable.Rows.Add(100, New Point(100, 200))  
  
        ' Send the changes back to the database  
        da.Update(datTable)  
    End Sub  
  
    Private Sub CommandBuilder()  
        ' Create a new SqlDataAdapter  
        Dim da As New SqlDataAdapter( _  
          "SELECT id, ts, p FROM dbo.Points_ts", connString)  
  
        ' Select a few rows with UDTs from the database  
        Dim datTable As New DataTable("Points")  
        da.Fill(datTable)  
  
        ' Display the contents of the p (Point) column  
        Dim r As DataRow  
        For Each r In datTable.Rows  
            Dim p As Point = CType(r(2), Point)  
            Console.WriteLine( _  
              "ID: {0}, x={1}, y={1}", r(0), p.X, p.Y)  
        Next r  
  
        ' Update a row if DataTable has at least 1 row  
        If datTable.Rows.Count > 0 Then  
            Dim oldPoint As Point = _  
              CType(datTable.Rows(0)(2), Point)  
            datTable.Rows(0)(2) = _  
              New Point(oldPoint.X + 1, oldPoint.Y + 1)  
        End If  
  
        ' Delete the last row  
        If datTable.Rows.Count > 0 Then  
            ' if we have at least 1 row  
            datTable.Rows(1).Delete()  
        End If  
  
        ' Insert a row. This will fail if run twice  
        ' because 100 is a primary key value  
        datTable.Rows.Add(100, Nothing, New Point(100, 200))  
  
        ' Use the CommandBuilder to generate DML statements  
        Dim bld As New SqlCommandBuilder(da)  
        bld.ConflictDetection = ConflictOptions.CompareRowVersion  
  
        ' Send the changes back to the database  
        da.Update(datTable)  
    End Sub  
  
  Private Function GetConnectionString() As String  
      ' To avoid storing the connection string in your code,   
      ' you can retrieve it from a configuration file.  
     Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
       & "Integrated Security=SSPI"  
   End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
  
class Class1  
  {  
// Retrieves the connection string  
private string connString = GetConnectionString();  
  
static void Main()  
{  
        UserProvidedCommands();  
        CommandBuilder();  
 }  
    static void UserProvidedCommands()  
    {  
        // Create a new SqlDataAdapter  
        SqlDataAdapter da = new SqlDataAdapter(  
          "SELECT id, p FROM dbo.Points", connString);  
  
        // Setup the INSERT/UPDATE/DELETE commands  
        SqlParameter idParam;  
        SqlParameter pointParam;  
  
        da.InsertCommand = new SqlCommand(  
            "INSERT INTO dbo.Points (id, p) VALUES (@id, @p)",   
             da.SelectCommand.Connection);  
        idParam =   
            da.InsertCommand.Parameters.Add("@id", SqlDbType.Int);  
        idParam.SourceColumn = "id";  
        pointParam =   
            da.InsertCommand.Parameters.Add("@p", SqlDbType.Udt);  
        pointParam.SourceColumn = "p";  
        pointParam.UdtTypeName = "dbo.Point";  
  
        da.UpdateCommand = new SqlCommand(  
            "UPDATE dbo.Points SET p = @p WHERE id = @id",   
            da.SelectCommand.Connection);  
        idParam =   
            da.UpdateCommand.Parameters.Add("@id", SqlDbType.Int);  
        idParam.SourceColumn = "id";  
        pointParam =   
            da.UpdateCommand.Parameters.Add("@p", SqlDbType.Udt);  
        pointParam.SourceColumn = "p";  
        pointParam.UdtTypeName = "dbo.Point";   
  
        da.DeleteCommand = new SqlCommand(  
            "DELETE dbo.Points WHERE id = @id",   
            da.SelectCommand.Connection);  
        idParam =   
            da.DeleteCommand.Parameters.Add("@id", SqlDbType.Int);  
        idParam.SourceColumn = "id";  
  
        // Fill the DataTable with UDT rows  
        DataTable datTable = new DataTable("Points");  
        da.Fill(datTable);  
  
        // Display the contents of the p (Point) column  
        foreach(DataRow r in datTable.Rows)   
        {  
            Point p = (Point)r[1];  
            Console.WriteLine(  
                "ID: {0}, x={1}, y={1}", r[0], p.X, p.Y);  
        }  
  
        // Update a row if the DataTable has at least 1 row  
        if(datTable.Rows.Count > 0 )   
        {   
            Point oldPoint = (Point)datTable.Rows[0][1];  
            datTable.Rows[0][1] =   
                new Point(oldPoint.X+1, oldPoint.Y+1);  
        }  
  
        // Delete the last row  
        if(datTable.Rows.Count > 0 )   
        { // If we have at least 1 row  
            datTable.Rows[1].Delete();  
        }  
  
        // Insert a row. This will fail if run twice  
        // because 100 is a primary key value.  
        datTable.Rows.Add(100, new Point(100, 200));   
  
        // Send the changes back to the database  
        da.Update(datTable);  
    }  
  
    static void CommandBuilder()  
    {  
        // Create a new SqlDataAdapter  
        SqlDataAdapter da = new SqlDataAdapter(  
            "SELECT id, ts, p FROM dbo.Points_ts", connString);  
  
        // Select a few rows with UDTs from the database  
        DataTable datTable = new DataTable("Points");  
        da.Fill(datTable);  
  
        // Display the contents of the p (Point) column  
        foreach (DataRow r in datTable.Rows)  
        {  
            Point p = (Point)r[2];  
            Console.WriteLine(  
                "ID: {0}, x={1}, y={1}", r[0], p.X, p.Y);  
        }  
  
        // Update a row if DataTable has at least 1 row  
        if (datTable.Rows.Count > 0)  
        {   
            Point oldPoint = (Point)datTable.Rows[0][2];  
            datTable.Rows[0][2] =   
                new Point(oldPoint.X + 1, oldPoint.Y + 1);  
        }  
  
        // Delete the last row  
        if (datTable.Rows.Count > 0)  
        { // if we have at least 1 row  
            datTable.Rows[1].Delete();  
        }  
  
        // Insert a row. This will fail if run twice  
        // because 100 is a primary key value  
        datTable.Rows.Add(100, null, new Point(100, 200));   
  
        // Use the CommandBuilder to generate DML statements  
        SqlCommandBuilder bld = new SqlCommandBuilder(da);  
        bld.ConflictDetection = ConflictOptions.CompareRowVersion;  
  
        // Send the changes back to the database  
        da.Update(datTable);  
    }  
  
 static private string GetConnectionString()  
 {  
 // To avoid storing the connection string in your code,   
 // you can retrieve it from a configuration file.  
    return "Data Source=localhost;Initial Catalog=AdventureWorks;"  
        + "Integrated Security=SSPI";  
  }  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [ADO.NET의 사용자 정의 형식 액세스](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-in-ado-net.md)  
  
  
