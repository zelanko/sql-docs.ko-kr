---
title: 설정 속성-SMO | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SMO [SQL Server], properties
- SQL Server Management Objects, properties
- properties [SMO]
ms.assetid: 342569ba-d2f7-44d2-8f3f-ae9c701c7f0f
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cf121a37bf0229ba3366e18c149530f316fcdc56
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098280"
---
# <a name="setting-properties---smo"></a>속성 설정 - SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  속성은 개체에 대한 설명 정보를 저장하는 값입니다. 예를 들어 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 옵션으로 표시 됩니다는 <xref:Microsoft.SqlServer.Management.Smo.Server.Configuration%2A> 개체의 속성입니다. 속성 컬렉션을 사용하여 직접 또는 간접적으로 속성에 액세스할 수 있습니다. 속성에 직접 액세스하는 경우 다음 구문을 사용합니다.  
  
 `objInstance.PropertyName`  
  
 속성에 읽기/쓰기 권한 또는 읽기 전용 권한이 있는지에 따라 속성 값을 수정하거나 검색할 수 있습니다. 또한 특정 속성을 설정해야 개체를 만들 수 있습니다. 자세한 내용은 특정 개체에 대한 SMO 참조를 참조하십시오.  
  
> [!NOTE]  
>  자식 개체의 컬렉션은 개체의 속성으로 나타납니다. 예를 들어 **Tables** 컬렉션은 **Server** 개체의 속성입니다. 자세한 내용은 [Using Collections](../../../relational-databases/server-management-objects-smo/create-program/using-collections.md)을 참조하세요.  
  
 개체의 속성은 속성 컬렉션의 멤버입니다. 속성 컬렉션을 사용하여 개체의 모든 속성을 반복할 수 있습니다.  
  
 다음과 같은 이유로 속성을 사용할 수 없는 경우도 있습니다.  
  
-   이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 새로운 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능을 나타내는 속성에 액세스하려는 경우와 같이 서버 버전에서 속성을 지원하지 않습니다.  
  
-   설치되지 않은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 요소를 나타내는 속성에 액세스하려는 경우와 같이 서버에서 속성 데이터를 제공하지 않습니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.UnknownPropertyException> 및 <xref:Microsoft.SqlServer.Management.Smo.PropertyCannotBeRetrievedException> SMO 실행을 catch하여 이러한 문제를 처리할 수 있습니다.  
  
## <a name="setting-default-initialization-fields"></a>기본 초기화 필드 설정  
 SMO는 개체를 검색할 때 최적화를 수행합니다. 최적화는 다음과 같은 상태를 자동으로 조정하여 로드되는 속성 수를 최소화합니다.  
  
1.  부분적으로 로드됨. 개체를 처음 참조하는 경우 이름 및 스키마와 같은 최소한의 속성만 사용할 수 있습니다.  
  
2.  전체 로드됨. 아무 속성이나 참조하면 나머지 속성이 신속하게 로드되어 초기화되고 사용할 수 있게 됩니다.  
  
3.  많은 메모리를 사용하는 속성. 사용할 수 없는 나머지 속성은 많은 메모리를 사용하며 <xref:Microsoft.SqlServer.Management.Smo.Property.Expensive%2A> 속성 값이 true입니다(예: <xref:Microsoft.SqlServer.Management.Smo.Database.DataSpaceUsage%2A>). 이러한 속성은 구체적으로 참조될 때만 로드됩니다.  
  
 애플리케이션이 부분적으로 로드됨 상태에서 제공되는 속성 이외의 추가 속성을 인출하는 경우 쿼리를 제출하여 이러한 추가 속성을 검색하고 전체 로드됨 상태로 확장됩니다. 이로 인해 클라이언트와 서버 간에 불필요한 트래픽이 발생할 수 있습니다. <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A> 메서드를 호출하여 보다 최적화할 수 있습니다. <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A> 메서드를 사용하면 개체를 초기화할 때 로드되는 속성을 지정할 수 있습니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.Server.SetDefaultInitFields%2A> 메서드는 다시 설정될 때까지 또는 나머지 응용 프로그램에 대해 속성 로드 동작을 설정합니다. <xref:Microsoft.SqlServer.Management.Smo.Server.GetDefaultInitFields%2A> 메서드를 사용하여 원래 동작을 저장하고 필요한 경우 복원할 수 있습니다.  
  
## <a name="examples"></a>예  
제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  

  
## <a name="getting-and-setting-a-property-in-visual-basic"></a>Visual Basic에서 속성 가져오기 및 설정  
 이 코드 예제에서는 가져오는 방법을 보여 줍니다는 <xref:Microsoft.SqlServer.Management.Smo.Information.Edition%2A> 의 속성을 <xref:Microsoft.SqlServer.Management.Smo.Information> 개체 및 설정 하는 방법을 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.SqlExecutionModes%2A> 의 속성을 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 속성을는 **ExecuteSql** 의 멤버는 <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> 열거 형식입니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Get a property.
Console.WriteLine(srv.Information.Version)
'Set a property.
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql
```
  
## <a name="getting-and-setting-a-property-in-visual-c"></a>Visual C#에서 속성 가져오기 및 설정  
 이 코드 예제에서는 가져오는 방법을 보여 줍니다는 <xref:Microsoft.SqlServer.Management.Smo.Information.Edition%2A> 의 속성을 <xref:Microsoft.SqlServer.Management.Smo.Information> 개체 및 설정 하는 방법을 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.SqlExecutionModes%2A> 의 속성을 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 속성을는 **ExecuteSql** 의 멤버는 <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> 열거 형식입니다.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Get a property.   
Console.WriteLine(srv.Information.Version);   
//Set a property.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql;   
}  
```  
  
## <a name="setting-various-properties-before-an-object-is-created-in-visual-basic"></a>Visual Basic에서 개체를 만들기 전에 다양한 속성 설정  
 이 코드 예제에서는 <xref:Microsoft.SqlServer.Management.Smo.Table.AnsiNullsStatus%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Table> 속성을 직접 설정하는 방법과 <xref:Microsoft.SqlServer.Management.Smo.Table> 개체를 만들기 전에 열을 만들고 추가하는 방법을 보여 줍니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Create a new table in the AdventureWorks2012 database. 
Dim db As Database
db = srv.Databases("AdventureWorks2012")
Dim tb As Table
'Specify the parent database, table schema and the table name in the constructor.
tb = New Table(db, "Test_Table", "HumanResources")
'Add columns because the table requires columns before it can be created. 
Dim c1 As Column
'Specify the parent table, the column name and data type in the constructor.
c1 = New Column(tb, "ID", DataType.Int)
tb.Columns.Add(c1)
c1.Nullable = False
c1.Identity = True
c1.IdentityIncrement = 1
c1.IdentitySeed = 0
Dim c2 As Column
c2 = New Column(tb, "Name", DataType.NVarChar(100))
c2.Nullable = False
tb.Columns.Add(c2)
tb.AnsiNullsStatus = True
'Create the table on the instance of SQL Server.
tb.Create()
```
  
## <a name="setting-various-properties-before-an-object-is-created-in-visual-c"></a>Visual C#에서 개체를 만들기 전에 다양한 속성 설정  
 이 코드 예제에서는 <xref:Microsoft.SqlServer.Management.Smo.Table.AnsiNullsStatus%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Table> 속성을 직접 설정하는 방법과 <xref:Microsoft.SqlServer.Management.Smo.Table> 개체를 만들기 전에 열을 만들고 추가하는 방법을 보여 줍니다.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Create a new table in the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
Table tb;   
//Specify the parent database, table schema, and the table name in the constructor.   
tb = new Table(db, "Test_Table", "HumanResources");   
//Add columns because the table requires columns before it can be created.   
Column c1;   
//Specify the parent table, the column name, and data type in the constructor.   
c1 = new Column(tb, "ID", DataType.Int);   
tb.Columns.Add(c1);   
c1.Nullable = false;   
c1.Identity = true;   
c1.IdentityIncrement = 1;   
c1.IdentitySeed = 0;   
Column c2;   
c2 = new Column(tb, "Name", DataType.NVarChar(100));   
c2.Nullable = false;   
tb.Columns.Add(c2);   
tb.AnsiNullsStatus = true;   
//Create the table on the instance of SQL Server.   
tb.Create();   
}  
```  
  
## <a name="iterating-through-all-properties-of-an-object-in-visual-basic"></a>Visual Basic에서 개체의 모든 속성 반복  
 이 코드 예제에서는 반복를 **속성** 의 컬렉션을 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> 개체 및에 표시 합니다는 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 출력 화면.  
  
 이 예에서 <xref:Microsoft.SqlServer.Management.Smo.Property> 개체는 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 키워드이기도 하기 때문에 대괄호 안에 있습니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Set properties on the uspGetEmployeeManagers stored procedure on the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
Dim sp As StoredProcedure
sp = db.StoredProcedures("uspGetEmployeeManagers")
sp.AnsiNullsStatus = False
sp.QuotedIdentifierStatus = False
'Iterate through the properties of the stored procedure and display.
'Note the Property object requires [] parentheses to distinguish it from the Visual Basic key word.
Dim p As [Property]
For Each p In sp.Properties
    Console.WriteLine(p.Name & p.Value)
Next
```
  
## <a name="iterating-through-all-properties-of-an-object-in-visual-c"></a>Visual C#에서 개체의 모든 속성 반복  
 이 코드 예제에서는 반복를 **속성** 의 컬렉션을 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> 개체 및에 표시 합니다는 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 출력 화면.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Set properties on the uspGetEmployeedManagers stored procedure on the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
StoredProcedure sp;   
sp = db.StoredProcedures("uspGetEmployeeManagers");   
sp.AnsiNullsStatus = false;   
sp.QuotedIdentifierStatus = false;   
//Iterate through the properties of the stored procedure and display.   
  Property p;   
  foreach ( p in sp.Properties) {   
    Console.WriteLine(p.Name + p.Value);   
  }   
}  
```  
  
## <a name="setting-default-initialization-fields-in-visual-basic"></a>Visual Basic에서 기본 초기화 필드 설정  
 이 코드 예제에서는 SMO 프로그램에서 초기화되는 개체 속성 수를 최소화하는 방법을 보여 줍니다. <xref:System.Collections.Specialized.StringCollection> 개체를 사용하려면 `using System.Collections.Specialized` 문을 포함해야 합니다.  
  
 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스로 전송되는 문 수와 이 최적화를 비교할 수 있습니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Assign the Table object type to a System.Type object variable.
Dim tb As Table
Dim typ As Type
tb = New Table
typ = tb.GetType
'Assign the current default initialization fields for the Table object type to a 
'StringCollection object variable.
Dim sc As StringCollection
sc = srv.GetDefaultInitFields(typ)
'Set the default initialization fields for the Table object type to the CreateDate property.
srv.SetDefaultInitFields(typ, "CreateDate")
'Retrieve the Schema, Name, and CreateDate properties for every table in AdventureWorks2012.
'Note that the improvement in performance can be viewed in SQL Profiler.
For Each tb In db.Tables
    Console.WriteLine(tb.Schema + "." + tb.Name + " " + tb.CreateDate)
Next
'Set the default initialization fields for the Table object type back to the original settings.
srv.SetDefaultInitFields(typ, sc)
```
  
## <a name="setting-default-initialization-fields-in-visual-c"></a>Visual C#에서 기본 초기화 필드 설정  
 이 코드 예제에서는 SMO 프로그램에서 초기화되는 개체 속성 수를 최소화하는 방법을 보여 줍니다. <xref:System.Collections.Specialized.StringCollection> 개체를 사용하려면 `using System.Collections.Specialized` 문을 포함해야 합니다.  
  
 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스로 전송되는 문 수와 이 최적화를 비교할 수 있습니다.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Assign the Table object type to a System.Type object variable.   
Table tb;   
Type typ;   
tb = new Table();   
typ = tb.GetType;   
//Assign the current default initialization fields for the Table object type to a   
//StringCollection object variable.   
StringCollection sc;   
sc = srv.GetDefaultInitFields(typ);   
//Set the default initialization fields for the Table object type to the CreateDate property.   
srv.SetDefaultInitFields(typ, "CreateDate");   
//Retrieve the Schema, Name, and CreateDate properties for every table in AdventureWorks2012.   
   //Note that the improvement in performance can be viewed in SQL Server Profiler.   
foreach ( tb in db.Tables) {   
   Console.WriteLine(tb.Schema + "." + tb.Name + " " + tb.CreateDate);   
}   
//Set the default initialization fields for the Table object type back to the original settings.   
srv.SetDefaultInitFields(typ, sc);   
}  
```  
  
  
