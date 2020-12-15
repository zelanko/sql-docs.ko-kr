---
description: 테이블 생성, 변경 및 제거
title: 테이블 생성, 변경 및 제거
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- tables [SMO]
ms.assetid: ff0bcfff-812f-4999-b0c7-736a97804c2b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 337ecf0eb01787dcc3f9d82ee5e872fea5edeff9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97431638"
---
# <a name="creating-altering-and-removing-tables"></a>테이블 생성, 변경 및 제거
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects(SMO)에서 테이블은 <xref:Microsoft.SqlServer.Management.Smo.Table> 개체로 표시됩니다. SMO 개체 계층 구조에서 <xref:Microsoft.SqlServer.Management.Smo.Table> 개체는 <xref:Microsoft.SqlServer.Management.Smo.Database> 개체 아래에 있습니다.  
  
## <a name="example"></a>예  
 제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 템플릿 및 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
  
## <a name="creating-altering-and-removing-a-table-in-visual-basic"></a>Visual Basic에서 테이블 생성, 변경 및 제거  
 이 코드 예제는 서로 다른 유형과 용도의 여러 열이 있는 테이블을 만듭니다. 또한 ID 필드를 만드는 방법, 기본 키를 만드는 방법, 테이블 속성을 변경하는 방법에 대한 예를 제공합니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a Table object variable by supplying the parent database and table name in the constructor. 
Dim tb As Table
tb = New Table(db, "Test_Table")
'Add various columns to the table.
Dim col1 As Column
col1 = New Column(tb, "Name", DataType.NChar(50))
col1.Collation = "Latin1_General_CI_AS"
col1.Nullable = True
tb.Columns.Add(col1)
Dim col2 As Column
col2 = New Column(tb, "ID", DataType.Int)
col2.Identity = True
col2.IdentitySeed = 1
col2.IdentityIncrement = 1
tb.Columns.Add(col2)
Dim col3 As Column
col3 = New Column(tb, "Value", DataType.Real)
tb.Columns.Add(col3)
Dim col4 As Column
col4 = New Column(tb, "Date", DataType.DateTime)
col4.Nullable = False
tb.Columns.Add(col4)
'Create the table on the instance of SQL Server.
tb.Create()
'Add another column.
Dim col5 As Column
col5 = New Column(tb, "ExpiryDate", DataType.DateTime)
col5.Nullable = False
tb.Columns.Add(col5)
'Run the Alter method to make the change on the instance of SQL Server.
tb.Alter()
'Remove the table from the database.

tb.Drop()
``` 
  
## <a name="creating-altering-and-removing-a-table-in-visual-c"></a>Visual C#에서 테이블 생성, 변경 및 제거  
 이 코드 예제는 서로 다른 유형과 용도의 여러 열이 있는 테이블을 만듭니다. 또한 ID 필드를 만드는 방법, 기본 키를 만드는 방법, 테이블 속성을 변경하는 방법에 대한 예를 제공합니다.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
        Server srv;   
        srv = new Server();   
        //Reference the AdventureWorks2012 database.   
        Database db;   
        db = srv.Databases["AdventureWorks2012"];   
        //Define a Table object variable by supplying the parent database and table name in the constructor.   
        Table tb;   
        tb = new Table(db, "Test_Table");   
        //Add various columns to the table.   
        Column col1;   
        col1 = new Column(tb, "Name", DataType.NChar(50));   
        col1.Collation = "Latin1_General_CI_AS";   
        col1.Nullable = true;   
        tb.Columns.Add(col1);   
        Column col2;   
        col2 = new Column(tb, "ID", DataType.Int);   
        col2.Identity = true;   
        col2.IdentitySeed = 1;   
        col2.IdentityIncrement = 1;   
        tb.Columns.Add(col2);   
        Column col3;   
        col3 = new Column(tb, "Value", DataType.Real);   
        tb.Columns.Add(col3);   
        Column col4;   
        col4 = new Column(tb, "Date", DataType.DateTime);   
        col4.Nullable = false;   
        tb.Columns.Add(col4);   
        //Create the table on the instance of SQL Server.   
        tb.Create();   
        //Add another column.   
        Column col5;   
        col5 = new Column(tb, "ExpiryDate", DataType.DateTime);   
        col5.Nullable = false;   
        tb.Columns.Add(col5);   
        //Run the Alter method to make the change on the instance of SQL Server.   
        tb.Alter();   
        //Remove the table from the database.   
        tb.Drop();   
        }  
```  
  
## <a name="creating-altering-and-removing-a-table-in-powershell"></a>PowerShell에서 테이블 생성, 변경 및 제거  
 이 코드 예제는 서로 다른 유형과 용도의 여러 열이 있는 테이블을 만듭니다. 또한 ID 필드를 만드는 방법, 기본 키를 만드는 방법, 테이블 속성을 변경하는 방법에 대한 예를 제공합니다.  
  
```powershell  
#Load the assembly containing the objects used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.Types")  
  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012.  
$db = get-item AdventureWorks2012  
  
#Create a SMO Table  
$tb = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Table -argumentlist $db, "Test_Table"  
  
#Add various columns to the table.   
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::NChar(50)  
$col1 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Name", $Type  
$col1.Collation = "Latin1_General_CI_AS"  
$col1.Nullable = $true  
$tb.Columns.Add($col1)  
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::Int  
$col2 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"ID", $Type  
$col2.Identity = $true  
$col2.IdentitySeed = 1  
$col2.IdentityIncrement = 1  
$tb.Columns.Add($col2)   
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::Real  
$col3 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Value", $Type  
$tb.Columns.Add($col3)   
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$col4 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Date", $Type  
$col4.Nullable = $false  
$tb.Columns.Add($col4)   
  
#Create the table  
$tb.Create()  
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$col5 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"ExpiryDate", $Type  
$col5.Nullable = $false  
$tb.Columns.Add($col5)   
  
#Run the Alter method to make the change on the instance of SQL Server.   
$tb.Alter()  
  
#Remove the table from the database.   
$tb.Drop()  
  
```  
  
## <a name="see-also"></a>참고 항목  
 <xref:Microsoft.SqlServer.Management.Smo.Table>  
  
  
