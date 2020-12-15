---
description: 메서드 호출
title: 호출 메서드 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- methods [SMO]
- calling methods
- SQL Server Management Objects, method calling
- SMO [SQL Server], method calling
ms.assetid: c88d5c5f-9ff0-4f84-b2b6-24c6b90fa15e
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b07761711e38e1a8446550408a73e4b1f239b3d7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97416741"
---
# <a name="calling-methods"></a>메서드 호출
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  메서드는 데이터베이스에서 **검사점** 을 실행 하거나 인스턴스에 대해 열거 된 로그온 목록을 요청 하는 등 개체와 관련 된 특정 태스크를 수행 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 합니다.  
  
 메서드는 개체에 대해 작업을 수행하며 매개 변수를 사용할 수 있고 반환 값을 갖는 경우도 있습니다. 반환 값은 단순한 데이터 형식, 복잡한 개체 또는 여러 멤버가 포함된 구조일 수 있습니다.  
  
 메서드가 성공적으로 실행되었는지 여부를 확인하려면 예외 처리를 사용합니다. 자세한 내용은 [Handling SMO Exceptions](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-exceptions.md)을 참조하세요.  
  
## <a name="examples"></a>예  
제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은  [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
 
  
## <a name="using-a-simple-smo-method-in-visual-basic"></a>Visual Basic에서 간단한 SMO 메서드 사용  
 이 예에서 <xref:Microsoft.SqlServer.Management.Smo.Database.Create%2A> 메서드는 매개 변수를 사용하지 않고 반환 값도 가지지 않습니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Define a Database object variable by supplying the parent server and the database name arguments in the constructor.
Dim db As Database
db = New Database(srv, "Test_SMO_Database")
'Call the Create method to create the database on the instance of SQL Server. 
db.Create()
```
  
## <a name="using-a-simple-smo-method-in-visual-c"></a>Visual C#에서 간단한 SMO 메서드 사용  
 이 예에서 <xref:Microsoft.SqlServer.Management.Smo.Database.Create%2A> 메서드는 매개 변수를 사용하지 않고 반환 값도 가지지 않습니다.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Define a Database object variable by supplying the parent server and the database name arguments in the constructor.   
Database db;   
db = new Database(srv, "Test_SMO_Database");   
//Call the Create method to create the database on the instance of SQL Server.   
db.Create();   
```  
  
 }  
  
## <a name="using-an-smo-method-with-a-parameter-in-visual-basic"></a>Visual Basic에서 매개 변수가 있는 SMO 메서드 사용  
 <xref:Microsoft.SqlServer.Management.Smo.Table> 개체에는 <xref:Microsoft.SqlServer.Management.Smo.Table.RebuildIndexes%2A>라는 메서드가 있습니다. 이 메서드에는 **FillFactor** 를 지정하는 숫자 매개 변수가 필요합니다.  
  
```VBNET
Dim srv As Server  
srv = New Server  
Dim tb As Table  
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources")  
tb.RebuildIndexes(70)  
```  
  
## <a name="using-an-smo-method-with-a-parameter-in-visual-c"></a>Visual C#에서 매개 변수가 있는 SMO 메서드 사용  
 <xref:Microsoft.SqlServer.Management.Smo.Table> 개체에는 <xref:Microsoft.SqlServer.Management.Smo.Table.RebuildIndexes%2A>라는 메서드가 있습니다. 이 메서드에는 `FillFactor`를 지정하는 숫자 매개 변수가 필요합니다.  
  
```csharp  
{   
Server srv = default(Server);   
srv = new Server();   
Table tb = default(Table);   
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources");   
tb.RebuildIndexes(70);   
}   
```  
  
## <a name="using-an-enumeration-method-that-returns-a-datatable-object-in-visual-basic"></a>Visual Basic에서 DataTable 개체를 반환하는 열거형 메서드 사용  
 이 섹션에서는 열거형 메서드를 호출하는 방법 및 반환된 <xref:System.Data.DataTable> 개체의 데이터를 처리하는 방법에 대해 설명합니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.Server.EnumCollations%2A> 메서드는 <xref:System.Data.DataTable> 개체를 반환하며, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 모든 데이터 정렬 정보에 액세스하려면 이 개체를 추가적으로 탐색해야 합니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.  
Dim srv As Server  
srv = New Server  
'Call the EnumCollations method and return collation information to DataTable variable.  
Dim d As DataTable  
'Select the returned data into an array of DataRow.  
d = srv.EnumCollations  
'Iterate through the rows and display collation details for the instance of SQL Server.  
Dim r As DataRow  
Dim c As DataColumn  
For Each r In d.Rows  
    Console.WriteLine("==")  
    For Each c In r.Table.Columns  
        Console.WriteLine(c.ColumnName + " = " + r(c).ToString)  
    Next  
Next  
```  
  
## <a name="using-an-enumeration-method-that-returns-a-datatable-object-in-visual-c"></a>Visual C#에서 DataTable 개체를 반환하는 열거형 메서드 사용  
 이 섹션에서는 열거형 메서드를 호출하는 방법 및 반환된 <xref:System.Data.DataTable> 개체의 데이터를 처리하는 방법에 대해 설명합니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.Server.EnumCollations%2A> 메서드는 시스템 <xref:System.Data.DataTable> 개체를 반환합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 모든 데이터 정렬 정보에 액세스하려면 <xref:System.Data.DataTable> 개체를 추가적으로 탐색해야 합니다.  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
//Call the EnumCollations method and return collation information to DataTable variable.   
DataTable d = default(DataTable);   
//Select the returned data into an array of DataRow.   
d = srv.EnumCollations;   
//Iterate through the rows and display collation details for the instance of SQL Server.   
DataRow r = default(DataRow);   
DataColumn c = default(DataColumn);   
foreach ( r in d.Rows) {   
  Console.WriteLine("=========");   
  foreach ( c in r.Table.Columns) {   
    Console.WriteLine(c.ColumnName + " = " + r(c).ToString);   
  }   
}   
}   
```  
  
## <a name="constructing-an-object-in-visual-basic"></a>Visual Basic에서 개체 생성  
 **New** 연산자를 사용하여 모든 개체의 생성자를 호출할 수 있습니다. <xref:Microsoft.SqlServer.Management.Smo.Database> 개체 생성자는 오버로드되며 예제에 사용된 <xref:Microsoft.SqlServer.Management.Smo.Database> 개체 생성자의 버전은 매개 변수 두 개, 즉 데이터베이스가 속해 있는 부모 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체와 새 데이터베이스의 이름을 나타내는 문자열을 사용합니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Declare and define a Database object by supplying the parent server and the database name arguments in the constructor.
Dim d As Database
d = New Database(srv, "Test_SMO_Database")
'Create the database on the instance of SQL Server.
d.Create()
Console.WriteLine(d.Name)
```
  
## <a name="constructing-an-object-in-visual-c"></a>Visual C#에서 개체 생성  
 **New** 연산자를 사용하여 모든 개체의 생성자를 호출할 수 있습니다. <xref:Microsoft.SqlServer.Management.Smo.Database> 개체 생성자는 오버로드되며 예제에 사용된 <xref:Microsoft.SqlServer.Management.Smo.Database> 개체 생성자의 버전은 매개 변수 두 개, 즉 데이터베이스가 속해 있는 부모 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체와 새 데이터베이스의 이름을 나타내는 문자열을 사용합니다.  
  
```csharp  
{   
Server srv;   
srv = new Server();   
Table tb;   
tb = srv.Databases("AdventureWorks2012").Tables("Employee", "HumanResources");   
tb.RebuildIndexes(70);   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Declare and define a Database object by supplying the parent server and the database name arguments in the constructor.   
Database d;   
d = new Database(srv, "Test_SMO_Database");   
//Create the database on the instance of SQL Server.   
d.Create();   
Console.WriteLine(d.Name);   
}  
```  
  
## <a name="copying-an-smo-object-in-visual-basic"></a>Visual Basic에서 SMO 개체 복사  
 이 코드 예에서는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> 메서드를 사용하여 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체의 복사본을 만듭니다. <xref:Microsoft.SqlServer.Management.Smo.Server> 개체는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결을 나타냅니다.  
  
```VBNET  
'Connect to the local, default instance of SQL Server.
Dim srv1 As Server
srv1 = New Server()
'Modify the default database and the timeout period for the connection.
srv1.ConnectionContext.DatabaseName = "AdventureWorks2012"
srv1.ConnectionContext.ConnectTimeout = 30
'Make a second connection using a copy of the ConnectionContext property and verify settings.
Dim srv2 As Server
srv2 = New Server(srv1.ConnectionContext.Copy)
Console.WriteLine(srv2.ConnectionContext.ConnectTimeout.ToString)
```
  
## <a name="copying-an-smo-object-in-visual-c"></a>Visual C#에서 SMO 개체 복사  
 이 코드 예에서는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> 메서드를 사용하여 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체의 복사본을 만듭니다. <xref:Microsoft.SqlServer.Management.Smo.Server> 개체는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결을 나타냅니다.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv1;   
srv1 = new Server();   
//Modify the default database and the timeout period for the connection.   
srv1.ConnectionContext.DatabaseName = "AdventureWorks2012";   
srv1.ConnectionContext.ConnectTimeout = 30;   
//Make a second connection using a copy of the ConnectionContext property and verify settings.   
Server srv2;   
srv2 = new Server(srv1.ConnectionContext.Copy);   
Console.WriteLine(srv2.ConnectionContext.ConnectTimeout.ToString);   
}  
```  
  
## <a name="monitoring-server-processes-in-visual-basic"></a>Visual Basic에서 서버 프로세스 모니터링  
 열거형 메서드를 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스에 대한 현재 상태 형식 정보를 얻을 수 있습니다. 코드 예에서는 <xref:Microsoft.SqlServer.Management.Smo.Server.EnumProcesses%2A> 메서드를 사용하여 현재 프로세스에 대한 정보를 확인합니다. 또한 이 예에서는 반환된 <xref:System.Data.DataTable> 개체의 열과 행으로 작업하는 방법도 보여 줍니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Call the EnumCollations method and return collation information to DataTable variable.
Dim d As DataTable
'Select the returned data into an array of DataRow.
d = srv.EnumProcesses
'Iterate through the rows and display collation details for the instance of SQL Server.
Dim r As DataRow
Dim c As DataColumn
For Each r In d.Rows
    Console.WriteLine("============================================")
    For Each c In r.Table.Columns
        Console.WriteLine(c.ColumnName + " = " + r(c).ToString)
    Next
Next
```
  
## <a name="monitoring-server-processes-in-visual-c"></a>Visual C#에서 서버 프로세스 모니터링  
 열거형 메서드를 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스에 대한 현재 상태 형식 정보를 얻을 수 있습니다. 코드 예에서는 <xref:Microsoft.SqlServer.Management.Smo.Server.EnumProcesses%2A> 메서드를 사용하여 현재 프로세스에 대한 정보를 확인합니다. 또한 이 예에서는 반환된 <xref:System.Data.DataTable> 개체의 열과 행으로 작업하는 방법도 보여 줍니다.  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
//Call the EnumCollations method and return collation information to DataTable variable.   
DataTable d = default(DataTable);   
//Select the returned data into an array of DataRow.   
d = srv.EnumProcesses;   
//Iterate through the rows and display collation details for the instance of SQL Server.   
DataRow r = default(DataRow);   
DataColumn c = default(DataColumn);   
foreach ( r in d.Rows) {   
  Console.WriteLine("=====");   
  foreach ( c in r.Table.Columns) {   
    Console.WriteLine(c.ColumnName + " = " + r(c).ToString);   
  }   
}   
}   
```  
  
## <a name="see-also"></a>참고 항목  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
