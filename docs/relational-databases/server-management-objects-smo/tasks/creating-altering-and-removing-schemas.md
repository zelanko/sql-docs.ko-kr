---
title: 생성, 변경 및 스키마를 제거 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- schemas [SMO]
ms.assetid: 3e3619de-c6a2-4280-b2be-4ec9924608fb
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e2990ccbfd28e16d71aba887e814805e9af50bca
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38060261"
---
# <a name="creating-altering-and-removing-schemas"></a>스키마 생성, 변경 및 제거
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  <xref:Microsoft.SqlServer.Management.Smo.Schema> 개체는 데이터베이스 개체에 대한 소유권 컨텍스트를 나타냅니다. <xref:Microsoft.SqlServer.Management.Smo.Database.Schemas%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Database> 속성은 <xref:Microsoft.SqlServer.Management.Smo.Schema> 개체 모음을 나타냅니다.  
  
## <a name="example"></a>예제  
 제공된 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="creating-altering-and-removing-a-schema-in-visual-basic"></a>Visual Basic에서 스키마 생성, 변경 및 제거  
 이 코드 예제는 스키마를 만들어 데이터베이스 개체에 할당하는 방법을 보여 줍니다. 그러면 프로그램이 사용자에게 권한을 부여하고 스키마에 새 테이블을 만듭니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a Schema object variable by supplying the parent database and name arguments in the constructor.
Dim sch As Schema
sch = New Schema(db, "MySchema1")
sch.Owner = "dbo"
'Create the schema on the instance of SQL Server.
sch.Create()
'Define an ObjectPermissionSet that contains the Update and Select object permissions.
Dim obperset As ObjectPermissionSet
obperset = New ObjectPermissionSet()
obperset.Add(ObjectPermission.Select)
obperset.Add(ObjectPermission.Update)
'Grant the set of permissions on the schema to the guest account.
sch.Grant(obperset, "guest")
'Define a Table object variable by supplying the parent database, name and schema arguments in the constructor.
Dim tb As Table
tb = New Table(db, "MyTable", "MySchema1")
Dim mycol As Column
mycol = New Column(tb, "Date", DataType.DateTime)
tb.Columns.Add(mycol)
tb.Create()
'Modify the owner of the schema and run the Alter method to make the change on the instance of SQL Server.
sch.Owner = "guest"
sch.Alter()
'Run the Drop method for the table and the schema to remove them.
tb.Drop()
sch.Drop()
``` 
  
## <a name="creating-altering-and-removing-a-schema-in-visual-c"></a>Visual C#에서 스키마 생성, 변경 및 제거  
 이 코드 예제는 스키마를 만들어 데이터베이스 개체에 할당하는 방법을 보여 줍니다. 그러면 프로그램이 사용자에게 권한을 부여하고 스키마에 새 테이블을 만듭니다.  
  
```csharp  
{  
         //Connect to the local, default instance of SQL Server.   
         Server srv = new Server();   
        //Reference the AdventureWorks2012 database.   
        Database db = srv.Databases["AdventureWorks2012"];   
        //Define a Schema object variable by supplying the parent database and name arguments in the constructor.   
        Schema sch = new Schema(db, "MySchema1");   
        sch.Owner = "dbo";   
  
        //Create the schema on the instance of SQL Server.   
        sch.Create();   
  
        //Define an ObjectPermissionSet that contains the Update and Select object permissions.   
        ObjectPermissionSet obperset = new ObjectPermissionSet();   
        obperset.Add(ObjectPermission.Select);   
        obperset.Add(ObjectPermission.Update);   
  
        //Grant the set of permissions on the schema to the guest account.   
        sch.Grant(obperset, "guest");   
  
        //Define a Table object variable by supplying the parent database, name and schema arguments in the constructor.   
        Table tb = new Table(db, "MyTable", "MySchema1");   
       Column mycol = new Column(tb, "Date", DataType.DateTime);   
        tb.Columns.Add(mycol);   
        tb.Create();   
  
        //Modify the owner of the schema and run the Alter method to make the change on the instance of SQL Server.   
        sch.Owner = "guest";   
        sch.Alter();   
  
        //Run the Drop method for the table and the schema to remove them.   
        tb.Drop();   
        sch.Drop();   
}  
```  
  
## <a name="creating-altering-and-removing-a-schema-in-powershell"></a>PowerShell에서 스키마 생성, 변경 및 제거  
 이 코드 예제는 스키마를 만들어 데이터베이스 개체에 할당하는 방법을 보여 줍니다. 그러면 프로그램이 사용자에게 권한을 부여하고 스키마에 새 테이블을 만듭니다.  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a schema object variable by supplying the parent database and name arguments in the constructor.   
$sch  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Schema `  
-argumentlist $db, "MySchema1"  
  
# Set schema owner  
$sch.Owner = "dbo"   
  
# Create the schema on the instance of SQL Server.   
$sch.Create()  
  
# Define an ObjectPermissionSet that contains the Update and Select object permissions.   
$obperset  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.ObjectPermissionSet  
$obperset.Add([Microsoft.SqlServer.Management.SMO.ObjectPermission]::Select)  
$obperset.Add([Microsoft.SqlServer.Management.SMO.ObjectPermission]::Update)  
  
# Grant the set of permissions on the schema to the guest account.   
$sch.Grant($obperset, "guest")  
  
#Create a SMO Table with one column and add it to the database  
$tb = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Table -argumentlist $db, "MyTable", "MySchema1"  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$mycol =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Date", $Type  
$tb.Columns.Add($mycol)  
$tb.Create()   
  
# Modify the owner of the schema and run the Alter method to make the change on the instance of SQL Server.   
$sch.Owner = "guest"  
$sch.Alter()  
  
# Run the Drop method for the table and the schema to remove them.   
$tb.Drop()  
$sch.Drop()  
```  
  
  
