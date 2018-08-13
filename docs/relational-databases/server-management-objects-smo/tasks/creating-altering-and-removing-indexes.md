---
title: 만들기, 변경, 및 인덱스 제거 | Microsoft 문서
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
- indexes [SMO]
ms.assetid: ad1befa5-46e0-4895-b9d3-42852e07607b
caps.latest.revision: 50
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 382f5750bbb10271579455f3e430b26e7afdf44d
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39560253"
---
# <a name="creating-altering-and-removing-indexes"></a>인덱스 생성, 변경 및 제거
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects(SMO) 계층 구조에서 인덱스는 <xref:Microsoft.SqlServer.Management.Smo.Index> 개체로 표시됩니다. 인덱싱된 열은 <xref:Microsoft.SqlServer.Management.Smo.IndexedColumn> 속성으로 표현된 <xref:Microsoft.SqlServer.Management.Smo.Index.IndexedColumns%2A> 개체 모음으로 표시됩니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.Index.IsXmlIndex%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Index> 속성을 지정하여 XML 열에 인덱스를 만들 수 있습니다.  
  
## <a name="examples"></a>예  
 제공된 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="creating-a-non-clustered-composite-index-in-visual-basic"></a>Visual Basic에서 비클러스터형 복합 인덱스 만들기  
 이 코드 예제는 복합 비클러스터형 인덱스를 만드는 방법을 보여 줍니다. 복합 인덱스를 위해 두 개 이상의 열을 인덱스에 추가합니다. 설정 된 <xref:Microsoft.SqlServer.Management.Smo.Index.IsClustered%2A> 속성을 **False** 비클러스터형 인덱스에 대 한 합니다.  
  
```  
' /r:Microsoft.SqlServer.Smo.dll  
' /r:Microsoft.SqlServer.ConnectionInfo.dll  
' /r:Microsoft.SqlServer.SqlEnum.dll  
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
Imports Microsoft.SqlServer.Management.Smo  
Public Class A  
    Public Shared Sub Main()  
        ' Connect to the local, default instance of SQL Server.   
        Dim srv As Server  
        srv = New Server()  
  
        ' Reference the AdventureWorks2012 database.   
        Dim db As Database  
        db = srv.Databases("AdventureWorks2012")  
  
        ' Declare a Table object and reference the HumanResources table.   
        Dim tb As Table  
        tb = db.Tables("Employee", "HumanResources")  
  
        ' Define an Index object variable by providing the parent table and index name in the constructor.   
        Dim idx As Index  
        idx = New Index(tb, "TestIndex")  
  
        ' Add indexed columns to the index.   
        Dim icol1 As IndexedColumn  
        icol1 = New IndexedColumn(idx, "BusinessEntityID", True)  
        idx.IndexedColumns.Add(icol1)  
        Dim icol2 As IndexedColumn  
        icol2 = New IndexedColumn(idx, "HireDate", True)  
        idx.IndexedColumns.Add(icol2)  
  
        ' Set the index properties.   
        idx.IndexKeyType = IndexKeyType.DriUniqueKey  
        idx.IsClustered = False  
        idx.FillFactor = 50  
  
        ' Create the index on the instance of SQL Server.   
        idx.Create()  
  
        ' Modify the page locks property.   
        idx.DisallowPageLocks = True  
  
        ' Run the Alter method to make the change on the instance of SQL Server.   
        idx.Alter()  
  
        ' Remove the index from the table.   
        idx.Drop()  
    End Sub  
End Class  
  
```  
  
## <a name="creating-a-non-clustered-composite-index-in-visual-c"></a>Visual C#에서 비클러스터형 복합 인덱스 만들기  
 이 코드 예제는 복합 비클러스터형 인덱스를 만드는 방법을 보여 줍니다. 복합 인덱스를 위해 두 개 이상의 열을 인덱스에 추가합니다. 설정 된 <xref:Microsoft.SqlServer.Management.Smo.Index.IsClustered%2A> 속성을 **False** 비클러스터형 인덱스에 대 한 합니다.  
  
```  
// /r:Microsoft.SqlServer.Smo.dll  
// /r:Microsoft.SqlServer.ConnectionInfo.dll  
// /r:Microsoft.SqlServer.SqlEnum.dll  
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
using Microsoft.SqlServer.Management.Smo;  
  
public class A {  
   public static void Main() {  
      // Connect to the local, default instance of SQL Server.   
      Server srv;  
      srv = new Server();  
  
      // Reference the AdventureWorks2012 database.   
      Database db;  
      db = srv.Databases["AdventureWorks2012"];  
  
      // Declare a Table object and reference the HumanResources table.   
      Table tb;  
      tb = db.Tables["Employee", "HumanResources"];  
  
      // Define an Index object variable by providing the parent table and index name in the constructor.   
      Index idx;  
      idx = new Index(tb, "TestIndex");  
  
      // Add indexed columns to the index.   
      IndexedColumn icol1;  
      icol1 = new IndexedColumn(idx, "BusinessEntityID", true);  
      idx.IndexedColumns.Add(icol1);  
      IndexedColumn icol2;  
      icol2 = new IndexedColumn(idx, "HireDate", true);  
      idx.IndexedColumns.Add(icol2);  
  
      // Set the index properties.   
      idx.IndexKeyType = IndexKeyType.DriUniqueKey;  
      idx.IsClustered = false;  
      idx.FillFactor = 50;  
  
      // Create the index on the instance of SQL Server.   
      idx.Create();  
  
      // Modify the page locks property.   
      idx.DisallowPageLocks = true;  
  
      // Run the Alter method to make the change on the instance of SQL Server.   
      idx.Alter();  
  
      // Remove the index from the table.   
      idx.Drop();  
   }  
}  
  
```  
  
## <a name="creating-a-non-clustered-composite-index-in-powershell"></a>PowerShell에서 비클러스터형 복합 인덱스 만들기  
 이 코드 예제는 복합 비클러스터형 인덱스를 만드는 방법을 보여 줍니다. 복합 인덱스를 위해 두 개 이상의 열을 인덱스에 추가합니다. 설정 된 <xref:Microsoft.SqlServer.Management.Smo.Index.IsClustered%2A> 속성을 **False** 비클러스터형 인덱스에 대 한 합니다.  
  
```  
# Set the path context to the local, default instance of SQL Server and to the  
#database tables in Adventureworks2012  
CD \sql\localhost\default\databases\AdventureWorks2012\Tables\  
  
#Get a reference to the table  
$tb = get-item HumanResources.Employee  
  
#Define an Index object variable by providing the parent table and index name in the constructor.   
$idx = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Index -argumentlist $tb, "TestIndex"  
  
#Add indexed columns to the index.   
$icol1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.IndexedColumn `  
-argumentlist $idx, "BusinessEntityId", $true  
$idx.IndexedColumns.Add($icol1)  
  
$icol2 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.IndexedColumn `  
-argumentlist $idx, "HireDate", $true  
$idx.IndexedColumns.Add($icol2)  
  
#Set the index properties.   
$idx.IndexKeyType = [Microsoft.SqlServer.Management.SMO.IndexKeyType]::DriUniqueKey   
$idx.IsClustered = $false  
$idx.FillFactor = 50  
  
#Create the index on the instance of SQL Server.   
$idx.Create()  
  
#Modify the page locks property.   
$idx.DisallowPageLocks = $true  
  
#Run the Alter method to make the change on the instance of SQL Server.   
$idx.Alter()  
  
#Remove the index from the table.   
$idx.Drop();  
```  
  
## <a name="creating-an-xml-index-in-visual-basic"></a>Visual Basic에서 XML 인덱스 만들기  
 이 코드 예제는 XML 데이터 형식에 XML 인덱스를 만드는 방법을 보여 줍니다. XML 데이터 형식은 XML 스키마 컬렉션에서 만들어진 MySampleCollection 라는 [XML 스키마를 사용 하 여](../../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md). XML 인덱스에는 몇 가지 제한 사항이 있는데, 그 중 하나는 이미 클러스터형 기본 키를 가지고 있는 테이블에 XML 인덱스를 만들어야 한다는 것입니다.  
  
```  
' /r:Microsoft.SqlServer.Smo.dll  
' /r:Microsoft.SqlServer.ConnectionInfo.dll  
' /r:Microsoft.SqlServer.SqlEnum.dll  
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
Imports Microsoft.SqlServer.Management.Smo  
  
Public Class A  
    Public Shared Sub Main()  
        ' Connect to the local, default instance of SQL Server.   
        Dim srv As Server  
        srv = New Server()  
        Dim db1 As Database = srv.Databases("TESTDB")  
        ' Define a Table object variable and add an XML type column.   
        Dim tb As New Table(db1, "XmlTable3")  
  
        Dim mySample As New XmlSchemaCollection(db1, "Sample4", "dbo")  
        mySample.Text = "<xsd:schema xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" targetNamespace=""NS2""> <xsd:element name=""elem1"" type=""xsd:integer""/></xsd:schema>"  
        mySample.Create()  
  
        Dim col11 As Column  
  
        ' This sample requires that an XML schema type called MySampleCollection exists on the database.   
        col11 = New Column(tb, "XMLValue", DataType.Xml("Sample4"))  
  
        ' Add another integer column that can be made into a unique, primary key.   
        tb.Columns.Add(col11)  
        Dim col21 As Column  
        col21 = New Column(tb, "Number", DataType.Int)  
        col21.Nullable = False  
        tb.Columns.Add(col21)  
  
        ' Create the table of the instance of SQL Server.   
        tb.Create()  
  
        ' Create a unique, clustered, primary key index on the integer column. This is required for an XML index.   
        Dim cp As Index  
        cp = New Index(tb, "clusprimindex3")  
        cp.IsClustered = True  
        cp.IndexKeyType = IndexKeyType.DriPrimaryKey  
        Dim cpcol As IndexedColumn  
        cpcol = New IndexedColumn(cp, "Number", True)  
        cp.IndexedColumns.Add(cpcol)  
        cp.Create()  
  
        ' Define and XML Index object variable by supplying the parent table and the XML index name arguments in the constructor.   
        Dim i As Index  
        i = New Index(tb, "xmlindex")  
        Dim ic As IndexedColumn  
        ic = New IndexedColumn(i, "XMLValue", True)  
        i.IndexedColumns.Add(ic)  
  
        ' Create the XML index on the instance of SQL Server.   
        i.Create()  
    End Sub  
End Class  
  
```  
  
## <a name="creating-an-xml-index-in-visual-c"></a>Visual C#에서 XML 인덱스 만들기  
 이 코드 예제는 XML 데이터 형식에 XML 인덱스를 만드는 방법을 보여 줍니다. XML 데이터 형식은 XML 스키마 컬렉션에서 만들어진 MySampleCollection 라는 [XML 스키마를 사용 하 여](../../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md). XML 인덱스에는 몇 가지 제한 사항이 있는데, 그 중 하나는 이미 클러스터형 기본 키를 가지고 있는 테이블에 XML 인덱스를 만들어야 한다는 것입니다.  
  
```  
// /r:Microsoft.SqlServer.Smo.dll  
// /r:Microsoft.SqlServer.ConnectionInfo.dll  
// /r:Microsoft.SqlServer.SqlEnum.dll  
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
using Microsoft.SqlServer.Management.Smo;  
  
public class A {  
   public static void Main() {  
      // Connect to the local, default instance of SQL Server.   
      Server srv;  
      srv = new Server();  
      Database db1 = srv.Databases["TESTDB"];  
      // Define a Table object variable and add an XML type column.   
      Table tb = new Table(db1, "XmlTable3");  
  
      XmlSchemaCollection mySample = new XmlSchemaCollection(db1, "Sample4", "dbo");  
      mySample.Text = "<xsd:schema xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\" targetNamespace=\"NS2\"> <xsd:element name=\"elem1\" type=\"xsd:integer\"/></xsd:schema>";  
      mySample.Create();  
  
      Column col11;  
  
      // This sample requires that an XML schema type called MySampleCollection exists on the database.   
      col11 = new Column(tb, "XMLValue", DataType.Xml("Sample4"));  
  
      // Add another integer column that can be made into a unique, primary key.   
      tb.Columns.Add(col11);  
      Column col21;  
      col21 = new Column(tb, "Number", DataType.Int);  
      col21.Nullable = false;  
      tb.Columns.Add(col21);  
  
      // Create the table of the instance of SQL Server.   
      tb.Create();  
  
      // Create a unique, clustered, primary key index on the integer column. This is required for an XML index.   
      Index cp;  
      cp = new Index(tb, "clusprimindex3");  
      cp.IsClustered = true;  
      cp.IndexKeyType = IndexKeyType.DriPrimaryKey;  
      IndexedColumn cpcol;  
      cpcol = new IndexedColumn(cp, "Number", true);  
      cp.IndexedColumns.Add(cpcol);  
      cp.Create();  
  
      // Define and XML Index object variable by supplying the parent table and the XML index name arguments in the constructor.   
      Index i;  
      i = new Index(tb, "xmlindex");  
      IndexedColumn ic;  
      ic = new IndexedColumn(i, "XMLValue", true);  
      i.IndexedColumns.Add(ic);  
  
      // Create the XML index on the instance of SQL Server.   
      i.Create();  
   }  
}  
  
```  
  
## <a name="creating-an-xml-index-in-powershell"></a>PowerShell에서 XML 인덱스 만들기  
 이 코드 예제는 XML 데이터 형식에 XML 인덱스를 만드는 방법을 보여 줍니다. XML 데이터 형식은 XML 스키마 컬렉션에서 만들어진 MySampleCollection 라는 [XML 스키마를 사용 하 여](../../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md). XML 인덱스에는 몇 가지 제한 사항이 있는데, 그 중 하나는 이미 클러스터형 기본 키를 가지고 있는 테이블에 XML 인덱스를 만들어야 한다는 것입니다.  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to adventureworks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
#Define a Table object variable and add an XML type column.   
#This sample requires that an XML schema type called MySampleCollection exists on the database.   
#See sample on Creating an XML schema to do this  
$tb = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Table -argumentlist $db, "XmlTable"  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::Xml("MySampleCollection")  
$col1 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"XMLValue", $Type  
$tb.Columns.Add($col1)  
  
#Add another integer column that can be made into a unique, primary key.   
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::Int  
$col2 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Number", $Type  
$col2.Nullable = $false  
$tb.Columns.Add($col2)  
  
#Create the table of the instance of SQL Server.   
$tb.Create()  
  
#Create a unique, clustered, primary key index on the integer column. This is required for an XML index.   
#Define an Index object variable by providing the parent table and index name in the constructor.   
$cp = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Index -argumentlist $tb, "clusprimindex"          
$cp.IsClustered = $true;  
$cp.IndexKeyType = [Microsoft.SqlServer.Management.SMO.IndexKeyType]::DriPrimaryKey;  
  
#Create and add an indexed column to the index.   
$cpcol = New-Object -TypeName Microsoft.SqlServer.Management.SMO.IndexedColumn `  
-argumentlist $cp, "Number", $true  
$cp.IndexedColumns.Add($cpcol)  
$cp.Create()  
  
#Define and XML Index object variable by supplying the parent table and  
# the XML index name arguments in the constructor.   
$i = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Index -argumentlist $tb, "xmlindex"   
  
#Create and add an indexed column to the index.   
$ic = New-Object -TypeName Microsoft.SqlServer.Management.SMO.IndexedColumn `  
-argumentlist $i, "XMLValue", $true    
$i.IndexedColumns.Add($ic)  
  
#Create the XML index on the instance of SQL Server  
$i.Create()  
```  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.SqlServer.Management.Smo.Index>  
  
  
