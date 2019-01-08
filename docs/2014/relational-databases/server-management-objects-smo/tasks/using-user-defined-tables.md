---
title: 사용자 정의 테이블을 사용 하 여 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- user-defined tables [SQL Server]
ms.assetid: 620a4e1f-9678-4711-ae09-bcf7c9cae724
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 04bc89c22ab2c49b047ed00b20b37f8abecf97c7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52758285"
---
# <a name="using-user-defined-tables"></a>사용자 정의 테이블 사용
  사용자 정의 테이블은 테이블 형식의 정보를 나타냅니다. 이들은 테이블 형식 데이터를 저장 프로시저나 사용자 정의 함수로 전달할 때 매개 변수로 사용할 수 있습니다. 데이터베이스 테이블의 열 표시에는 사용자 정의 테이블을 사용할 수 없습니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.Database> 개체에는 <xref:Microsoft.SqlServer.Management.Smo.Database.UserDefinedTableTypes%2A> 개체를 참조하는 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedTableTypeCollection> 속성이 있습니다. 각 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedTableType> 컬렉션에는 개체를 **열** 속성의 컬렉션을 나타내는 <xref:Microsoft.SqlServer.Management.Smo.Column> 개체는 사용자 정의 테이블의 열을 나열 합니다. 사용자 정의 테이블에 열을 추가하려면 Add 메서드를 사용합니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedTableType> 개체를 사용하여 새 사용자 정의 테이블을 정의할 때 여러 열과 이 열들 중 하나를 기반으로 하는 기본 키를 제공해야 합니다.  
  
 사용자 정의 테이블 형식은 한번 만든 후 변경할 수 없습니다. <xref:Microsoft.SqlServer.Management.Smo.UserDefinedTableType>은 Alter 메서드를 지원하지 않습니다. 사용자 정의 테이블 형식은 CHECK 제약 조건을 갖지만 형식을 수정할 수 없으므로 일부 확인 작업에서 예외가 발생합니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.DataType> 클래스는 열 및 매개 변수와 연관된 데이터 형식을 지정하는 데 사용됩니다. 사용자 정의 테이블 형식을 사용자 정의 함수 및 저장 프로시저에 대한 매개 변수로 지정하려면 이 형식을 사용하십시오.  
  
## <a name="examples"></a>예  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="creating-a-user-defined-table-in-visual-basic"></a>Visual Basic에서 사용자 정의 테이블 만들기  
 이 예에서는 `StringCollection` 형식을 포함하는 클래스 라이브러리에 대해 imports 문을 추가해야 합니다.  
  
 `Imports System.Collections.Specialized`  
  
 이 예는 사용자 정의 테이블을 만들어 사용자 정의 함수의 매개 변수로 사용하는 방법을 보여 줍니다.  
  
```  
'Connect to the local, default instance of SQL Server  
        Dim srv As Server  
        srv = New Server  
        'Reference the AdventureWorks2012 database.  
        Dim db As Database  
        db = srv.Databases("AdventureWorks2012")  
        'Define a UserDefinedTableType object variable by supplying the 'database and name in the constructor.  
        Dim udtt As UserDefinedTableType  
        udtt = New UserDefinedTableType(db, "My_User_Defined_Table")  
        'Add three columns of different types to the  
        'UserDefinedTableType object.  
        udtt.Columns.Add(New Column(udtt, "Col1", DataType.Int))  
        udtt.Columns.Add(New Column(udtt, "Col2", DataType.VarCharMax))  
        udtt.Columns.Add(New Column(udtt, "Col3", DataType.Money))  
        'Define an Index object variable by supplying the user-defined  
        'table variable and name in the constructor.  
        Dim idx As Index  
        idx = New Index(udtt, "PK_UddtTable")  
        'Add the first column in the user-defined table as  
        'the indexed column.  
        idx.IndexedColumns.Add(New IndexedColumn(idx, "Col1"))  
        'Specify that the index is a clustered, unique, primary key.  
        idx.IsClustered = True  
        idx.IsUnique = True  
        idx.IndexKeyType = IndexKeyType.DriPrimaryKey  
        udtt.Indexes.Add(idx)  
        'Add the index and create the user-defined table.  
        udtt.Create()  
        'Display the Transact-SQL creation script for the  
        'user-defined table.  
        Dim sc As StringCollection  
        sc = udtt.Script()  
        For Each c As String In sc  
            Console.WriteLine(c)  
        Next  
  
        'Define a new user-defined function with a single parameter.  
        Dim udf As UserDefinedFunction  
        udf = New UserDefinedFunction(db, "My_User_Defined_Function")  
        udf.TextMode = False  
        udf.FunctionType = UserDefinedFunctionType.Scalar  
        udf.ImplementationType = ImplementationType.TransactSql  
        udf.DataType = DataType.DateTime  
        'Specify the parameter as a UserDefinedTableTable object.  
        Dim udfp As UserDefinedFunctionParameter  
        udfp = New UserDefinedFunctionParameter(udf, "@param")  
        udfp.DataType = New DataType(udtt)  
        udfp.IsReadOnly = True  
        udf.Parameters.Add(udfp)  
        'Specify the TextBody property to the Transact-SQL definition of the  
        'user-defined function.  
        udf.TextBody = "BEGIN RETURN (GETDATE());end"  
        'Create the user-defined function.  
        udf.Create()  
```  
  
## <a name="creating-a-user-defined-table-in-visual-c"></a>Visual C#에서 사용자 정의 테이블 만들기  
 이 예에서는 `StringCollection` 형식을 포함하는 클래스 라이브러리에 대해 imports 문을 추가해야 합니다.  
  
 `using System.Collections.Specialized;`  
  
 이 예는 사용자 정의 테이블을 만들어 사용자 정의 함수의 매개 변수로 사용하는 방법을 보여 줍니다.  
  
```  
{  
            //Connect to the local, default instance of SQL Server   
               Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database db = srv.Databases["AdventureWorks2012"];  
            //Define a UserDefinedTableType object variable by supplying the  
            //database and name in the constructor.   
         UserDefinedTableType udtt = new UserDefinedTableType(db, "My_User_Defined_Table");  
  
            //Add three columns of different types to the   
            //UserDefinedTableType object.   
         udtt.Columns.Add(new Column(udtt, "Col1", DataType.Int));  
         udtt.Columns.Add(new Column(udtt, "Col2", DataType.VarCharMax));  
         udtt.Columns.Add(new Column(udtt, "Col3", DataType.Money));  
  
            //Define an Index object variable by supplying the user-defined   
            //table variable and name in the constructor.   
  
            Index idx = new Index(udtt, "PK_UddtTable");  
  
            //Add the first column in the user-defined table as   
            //the indexed column.   
            idx.IndexedColumns.Add(new IndexedColumn(idx, "Col1"));  
            //Specify that the index is a clustered, unique, primary key.   
            idx.IsClustered = true;  
            idx.IsUnique = true;  
            idx.IndexKeyType = IndexKeyType.DriPrimaryKey;  
            udtt.Indexes.Add(idx);  
            //Add the index and create the user-defined table.   
            udtt.Create();  
  
            //Display the Transact-SQL creation script for the   
            //user-defined table.   
            System.Collections.Specialized.StringCollection sc;  
            sc = udtt.Script();  
            foreach (string s in sc)  
            {  
                Console.WriteLine(s);  
            }  
  
            //Define a new user-defined function with a single parameter.  
            UserDefinedFunction udf = new UserDefinedFunction(db, "My_User_Defined_Function");  
            udf.TextMode = false;  
            udf.FunctionType = UserDefinedFunctionType.Scalar;  
            udf.ImplementationType = ImplementationType.TransactSql;  
            udf.DataType = DataType.DateTime;  
  
            //Specify the parameter as a UserDefinedTableTable object.  
             UserDefinedFunctionParameter udfp = new UserDefinedFunctionParameter(udf, "@param");  
            udfp.DataType = new DataType(udtt);  
            udfp.IsReadOnly = true;  
            udf.Parameters.Add(udfp);  
  
            //Specify the TextBody property to the Transact-SQL definition of the   
            //user-defined function.   
            udf.TextBody = "BEGIN RETURN (GETDATE());end";  
            //Create the user-defined function.   
            udf.Create();  
        }  
```  
  
## <a name="creating-a-user-defined-table-in-powershell"></a>PowerShell에서 사용자 정의 테이블 만들기  
 이 예에서는 `StringCollection` 형식을 포함하는 클래스 라이브러리에 대해 imports 문을 추가해야 합니다.  
  
 `using System.Collections.Specialized;`  
  
 이 예는 사용자 정의 테이블을 만들어 사용자 정의 함수의 매개 변수로 사용하는 방법을 보여 줍니다.  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
#Define a UserDefinedTableType object variable by supplying the  
#database and name in the constructor.   
$udtt = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedTableType `  
-argumentlist $db, "My_User_Defined_Table"  
  
#Add three columns of different types to the UserDefinedTableType object.  
  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::Int  
$col = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column `  
-argumentlist $udtt, "col1",$type  
$udtt.Columns.Add($col)  
  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::VarCharMax  
$col = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column `  
-argumentlist $udtt, "col2",$type  
$udtt.Columns.Add($col)  
  
 $type = [Microsoft.SqlServer.Management.SMO.DataType]::Money  
$col = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column `  
-argumentlist $udtt, "col3",$type  
$udtt.Columns.Add($col)          
  
#Define an Index object variable by supplying the user-defined   
#table variable and name in the constructor.   
$idx = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Index `  
-argumentlist $udtt, "PK_UddtTable"  
  
#Add the first column in the user-defined table as   
#the indexed column.   
$idxcol = New-Object -TypeName Microsoft.SqlServer.Management.SMO.IndexedColumn `  
-argumentlist $idx, "Col1"  
$idx.IndexedColumns.Add($idxcol)  
  
#Specify that the index is a clustered, unique, primary key.   
$idx.IsClustered = $true  
$idx.IsUnique = $true  
$idx.IndexKeyType = [Microsoft.SqlServer.Management.SMO.IndexKeyType]::DriPrimaryKey;  
  
#Add the index and create the user-defined table.   
$udtt.Indexes.Add($idx)  
$udtt.Create();  
  
# Display the Transact-SQL creation script for the   
# user-defined table.   
$sc = $udtt.Script()  
$sc  
  
# Define a new user-defined function with a single parameter.   
$udf = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunction `  
-argumentlist $db, "My_User_Defined_Function"  
$udf.TextMode = $false  
$udf.FunctionType = [Microsoft.SqlServer.Management.SMO.UserDefinedFunctionType]::Scalar  
$udf.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
$udf.DataType = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
  
# Specify the parameter as a UserDefinedTableTable object.  
$udfp = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunctionParameter `  
-argumentlist $udf, "@param"  
$type    =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.DataType `  
-argumentlist $udtt  
$udfp.DataType = $type  
$udfp.IsReadOnly = $true  
$udf.Parameters.Add($udfp)  
  
# Specify the TextBody property to the Transact-SQL definition of the   
# user-defined function.   
$udf.TextBody = "BEGIN RETURN (GETDATE());end"  
  
# Create the user-defined function.   
$udf.Create()           
```  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.SqlServer.Management.Smo.FileGroup>   
 [데이터베이스 파일 및 파일 그룹](../../databases/database-files-and-filegroups.md)  
  
  
