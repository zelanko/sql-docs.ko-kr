---
description: 데이터베이스 생성, 변경 및 제거
title: 데이터베이스 생성, 변경 및 제거
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- databases [SMO]
- databases [SMO], creating
- databases [SMO], modifying
- databases [SMO], deleting
ms.assetid: fcfb3ec2-7556-4f72-971a-501295892cb0
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 67d1650eb19e2a0f7f06f27a280458fff661e424
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439734"
---
# <a name="creating-altering-and-removing-databases"></a>데이터베이스 생성, 변경 및 제거
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  SMO에서 데이터베이스는 <xref:Microsoft.SqlServer.Management.Smo.Database> 개체로 표시됩니다.  
  
 데이터베이스를 수정하거나 참조하기 위해 <xref:Microsoft.SqlServer.Management.Smo.Database> 개체를 만들 필요는 없습니다. 데이터베이스는 컬렉션을 사용하여 참조할 수 있습니다.  
  
## <a name="example"></a>예  
 제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
  
## <a name="creating-altering-and-removing-a-database-in-visual-basic"></a>Visual Basic에서 데이터베이스 생성, 변경 및 제거  
 이 코드 예제는 새 데이터베이스를 만듭니다. 파일 및 파일 그룹은 데이터베이스를 위해 자동으로 만들어집니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Define a Database object variable by supplying the server and the database name arguments in the constructor.
Dim db As Database
db = New Database(srv, "Test_SMO_Database")
'Create the database on the instance of SQL Server.
db.Create()
'Reference the database and display the date when it was created.
db = srv.Databases("Test_SMO_Database")
Console.WriteLine(db.CreateDate)
'Remove the database.
db.Drop()
```
  
## <a name="creating-altering-and-removing-a-database-in-visual-c"></a>Visual C#에서 데이터베이스 생성, 변경 및 제거  
 이 코드 예제는 새 데이터베이스를 만듭니다. 파일 및 파일 그룹은 데이터베이스를 위해 자동으로 만들어집니다.  
  
```csharp  
{  
                //Connect to the local, default instance of SQL Server.   
                Server srv;  
                srv = new Server();  
                //Define a Database object variable by supplying the server and the database name arguments in the constructor.   
                Database db;  
                db = new Database(srv, "Test_SMO_Database");  
                //Create the database on the instance of SQL Server.   
                db.Create();  
                //Reference the database and display the date when it was created.   
                db = srv.Databases["Test_SMO_Database"];  
                Console.WriteLine(db.CreateDate);  
                //Remove the database.   
                db.Drop();  
            }  
```  
  
## <a name="creating-altering-and-removing-a-database-in-powershell"></a>PowerShell에서 데이터베이스 생성, 변경 및 제거  
 이 코드 예제는 새 데이터베이스를 만듭니다. 파일 및 파일 그룹은 데이터베이스를 위해 자동으로 만들어집니다.  
  
```powershell  
#Get a server object which corresponds to the default instance  
cd \sql\localhost\  
$srv = get-item default  
  
#Create a new database  
$db = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Database -argumentlist $srv, "Test_SMO_Database"  
$db.Create()  
  
#Reference the database and display the date when it was created.   
$db = $srv.Databases["Test_SMO_Database"]  
$db.CreateDate  
  
#Drop the database  
$db.Drop()  
```  
  
## <a name="see-also"></a>참고 항목  
 <xref:Microsoft.SqlServer.Management.Smo.Database>  
  
  
