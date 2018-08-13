---
title: 파일 그룹 및 데이터를 저장할 파일을 사용 하 여 | Microsoft Docs
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
- filegroups [SMO]
- storing data [SMO]
- files [SMO]
- files [SMO], about files
- storage [SMO]
ms.assetid: 7e2327ce-e1a6-4904-83d1-0944b24a7b43
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 6c4c28d9b485745865ea2a8d1878a97b4e9cee5c
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39537813"
---
# <a name="using-filegroups-and-files-to-store-data"></a>파일 그룹 및 파일을 사용하여 데이터 저장
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  데이터 파일은 데이터베이스 파일을 저장하는 데 사용됩니다. 데이터 파일은 파일 그룹으로 다시 세분됩니다. <xref:Microsoft.SqlServer.Management.Smo.Database> 개체에는 <xref:Microsoft.SqlServer.Management.Smo.Database.FileGroups%2A> 개체를 참조하는 <xref:Microsoft.SqlServer.Management.Smo.FileGroupCollection> 속성이 있습니다. 해당 컬렉션의 각 <xref:Microsoft.SqlServer.Management.Smo.FileGroup> 개체에는 <xref:Microsoft.SqlServer.Management.Smo.FileGroup.Files%2A> 속성이 있습니다. 이 속성은 데이터베이스에 속하는 모든 데이터 파일을 포함하는 <xref:Microsoft.SqlServer.Management.Smo.DataFileCollection> 컬렉션을 참조합니다. 파일 그룹은 주로 데이터베이스 개체 저장에 사용되는 파일을 그룹화하는 데 사용됩니다. 데이터베이스 개체를 여러 파일에 분산시키는 한 가지 이유는 성능을 높일 수 있다는 점입니다. 특히 파일이 서로 다른 디스크 드라이브에 저장된 경우 매우 유용합니다.  
  
 자동으로 생성된 모든 데이터베이스에는 "Primary"라는 파일 그룹과 데이터베이스와 같은 이름의 데이터 파일이 있습니다. 추가 파일과 그룹을 컬렉션에 추가할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-basic"></a>Visual Basic에서 데이터베이스에 파일 그룹 및 데이터 파일 추가  
 주 파일 그룹 및 데이터 파일이 기본 속성 값으로 자동으로 생성됩니다. 코드 예제는 사용자가 사용할 수 있는 몇 가지 속성 값을 지정합니다. 그렇지 않으면 기본 속성 값이 사용됩니다.  
  
```vbnet  
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a FileGroup object called SECONDARY on the database.
Dim fg1 As FileGroup
fg1 = New FileGroup(db, "SECONDARY")
'Call the Create method to create the file group on the instance of SQL Server.
fg1.Create()
'Define a DataFile object on the file group and set the FileName property.
Dim df1 As DataFile
df1 = New DataFile(fg1, "datafile1")
df1.FileName = "c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data\datafile2.ndf"
'Call the Create method to create the data file on the instance of SQL Server.
df1.Create()
```
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-c"></a>Visual C#에서 데이터베이스에 파일 그룹 및 데이터 파일 추가  
 주 파일 그룹 및 데이터 파일이 기본 속성 값으로 자동으로 생성됩니다. 코드 예제는 사용자가 사용할 수 있는 몇 가지 속성 값을 지정합니다. 그렇지 않으면 기본 속성 값이 사용됩니다.  
  
```  
{  
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a FileGroup object called SECONDARY on the database.   
            FileGroup fg1 = default(FileGroup);  
            fg1 = new FileGroup(db, "SECONDARY");  
            //Call the Create method to create the file group on the instance of SQL Server.   
            fg1.Create();  
            //Define a DataFile object on the file group and set the FileName property.   
            DataFile df1 = default(DataFile);  
            df1 = new DataFile(fg1, "datafile1");  
            df1.FileName = "c:\\Program Files\\Microsoft SQL Server\\MSSQL.1\\MSSQL\\Data\\datafile2.ndf";  
            //Call the Create method to create the data file on the instance of SQL Server.   
            df1.Create();  
        }  
```  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-powershell"></a>PowerShell에서 데이터베이스에 파일 그룹 및 데이터 파일 추가  
 주 파일 그룹 및 데이터 파일이 기본 속성 값으로 자동으로 생성됩니다. 코드 예제는 사용자가 사용할 수 있는 몇 가지 속성 값을 지정합니다. 그렇지 않으면 기본 속성 값이 사용됩니다.  
  
```powershell   
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012.  
$db = get-item AdventureWorks2012  
  
#Create a new filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "SECONDARY"  
$fg1.Create()  
  
#Define a DataFile object on the file group and set the FileName property.   
$df1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.DataFile -argumentlist $fg1, "datafile1"  
  
#Make sure to have a directory created to hold the designated data file  
$df1.FileName = "c:\\TestData\\datafile2.ndf"  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$df1.Create()  
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-basic"></a>Visual Basic에서 로그 파일 생성, 변경 및 제거  
 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.LogFile> 개체를 만들고 속성 중 하나를 변경한 다음 데이터베이스에서 제거합니다.  
  
```vbnet  
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a LogFile object and set the database, name, and file name properties in the constructor.
Dim lf1 As LogFile
lf1 = New LogFile(db, "logfile1", "c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data\logfile1.ldf")
'Set the file growth to 6%.
lf1.GrowthType = FileGrowthType.Percent
lf1.Growth = 6
'Run the Create method to create the log file on the instance of SQL Server.
lf1.Create()
'Alter the growth percentage.
lf1.Growth = 7
lf1.Alter()
'Remove the log file.
lf1.Drop()
```
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-c"></a>Visual C#에서 로그 파일 생성, 변경 및 제거  
 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.LogFile> 개체를 만들고 속성 중 하나를 변경한 다음 데이터베이스에서 제거합니다.  
  
```  
//Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a LogFile object and set the database, name, and file name properties in the constructor.   
            LogFile lf1 = default(LogFile);  
            lf1 = new LogFile(db, "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf");  
            //Set the file growth to 6%.   
            lf1.GrowthType = FileGrowthType.Percent;  
            lf1.Growth = 6;  
            //Run the Create method to create the log file on the instance of SQL Server.   
            lf1.Create();  
            //Alter the growth percentage.   
            lf1.Growth = 7;  
            lf1.Alter();  
            //Remove the log file.   
            lf1.Drop();  
  
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-powershell"></a>PowerShell에서 로그 파일 생성, 변경 및 제거  
 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.LogFile> 개체를 만들고 속성 중 하나를 변경한 다음 데이터베이스에서 제거합니다.  
  
```powershell  
#Load the assembly containing the enums used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.SqlEnum")  
  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012  
$db = get-item AdventureWorks2012  
  
#Create a filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Secondary"  
  
#Call the Create method to create the file group on the instance of SQL Server.   
$fg1.Create()  
  
#Define a LogFile object on the file group and set the FileName property.   
$lf1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LogFile -argumentlist $db, "LogFile2"  
  
#Set a location for it - make sure the directory exists  
$lf1.FileName = "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf"  
  
#Set file growth to 6%  
$lf1.GrowthType = [Microsoft.SqlServer.Management.Smo.FileGrowthType]::Percent  
$lf1.Growth = 6.0  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$lf1.Create()  
  
#Alter a value and drop the log file  
$lf1.Growth = 7.0  
$lf1.Alter()  
$lf1.Drop()  
  
```  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.SqlServer.Management.Smo.FileGroup>   
 [데이터베이스 파일 및 파일 그룹](../../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
