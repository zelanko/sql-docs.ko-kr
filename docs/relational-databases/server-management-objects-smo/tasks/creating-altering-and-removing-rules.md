---
title: 규칙 생성, 변경 및 제거
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- rules [SMO]
ms.assetid: 16981459-524e-4b39-a899-4370eaf763cc
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b2f918e611a4bc88c1a77ad7d539a9101f3f8dac
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74095521"
---
# <a name="creating-altering-and-removing-rules"></a>규칙 생성, 변경 및 제거
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO에서 규칙은 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체로 표시됩니다. 규칙은 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 속성, 즉 IN, LIKE, BETWEEN과 같은 연산자나 조건자를 사용하는 조건식이 포함된 텍스트 문자열로 정의됩니다. 규칙은 열 또는 기타 데이터베이스 개체를 참조할 수 없습니다. 데이터베이스 개체를 참조하지 않는 기본 제공 함수는 포함할 수 있습니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 속성 정의에는 입력한 데이터 값을 참조하는 변수가 포함되어야 합니다. 규칙을 만들 때 모든 이름 또는 기호를 사용 하 여 값을 나타낼 수 있지만 첫 번째 문자는 \@ 기호 여야 합니다.  
  
## <a name="example"></a>예제  
 제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-basic"></a>Visual Basic에서 규칙 생성, 변경 및 제거  
 이 코드 예제는 규칙을 만들고, 규칙을 열에 연결하고, <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체의 속성을 수정하고, 열에서 규칙을 분리하고, 규칙을 삭제하는 방법을 보여 줍니다.  
  
 System.object의 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체에 대 <xref:Microsoft.SqlServer.Management.Smo.Rule> 한 모호성을 방지 하기 위해 개체에 대 한 **Dim** 문은 전체 어셈블리 경로로 지정 됩니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Product table.
Dim tb As Table
tb = db.Tables("Product", "Production")
'Define a Rule object variable by supplying the parent database, name and schema in the constructor. 
'Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.
Dim ru As Microsoft.SqlServer.Management.Smo.Rule
ru = New Rule(db, "TestRule", "Production")
'Set the TextHeader and TextBody properties to define the rule.
ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"
ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"
'Create the rule on the instance of SQL Server.
ru.Create()
'Bind the rule to a column in the Product table by supplying the table, schema, and 
'column as arguments in the BindToColumn method.
ru.BindToColumn("Product", "SellEndDate", "Production")
'Unbind from the column before removing the rule from the database.
ru.UnbindFromColumn("Product", "SellEndDate", "Production")
ru.Drop()
```
  
## <a name="creating-altering-and-removing-a-rule-in-visual-c"></a>Visual C#에서 규칙 생성, 변경 및 제거  
 이 코드 예제는 규칙을 만들고, 규칙을 열에 연결하고, <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체의 속성을 수정하고, 열에서 규칙을 분리하고, 규칙을 삭제하는 방법을 보여 줍니다.  
  
 System.object의 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체에 대 <xref:Microsoft.SqlServer.Management.Smo.Rule> 한 모호성을 방지 하기 위해 개체에 대 한 **Dim** 문은 전체 어셈블리 경로로 지정 됩니다.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
            //Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.   
            Microsoft.SqlServer.Management.Smo.Rule ru;  
            ru = new Rule(db, "TestRule", "Production");  
            //Set the TextHeader and TextBody properties to define the rule.   
            ru.TextHeader = "CREATE RULE [Production].[TestRule] AS";  
            ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())";  
            //Create the rule on the instance of SQL Server.   
            ru.Create();  
            //Bind the rule to a column in the Product table by supplying the table, schema, and   
            //column as arguments in the BindToColumn method.   
            ru.BindToColumn("Product", "SellEndDate", "Production");  
            //Unbind from the column before removing the rule from the database.   
            ru.UnbindFromColumn("Product", "SellEndDate", "Production");  
            ru.Drop();  
  
        }  
```  
  
## <a name="creating-altering-and-removing-a-rule-in-powershell"></a>PowerShell에서 규칙 생성, 변경 및 제거  
 이 코드 예제는 규칙을 만들고, 규칙을 열에 연결하고, <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체의 속성을 수정하고, 열에서 규칙을 분리하고, 규칙을 삭제하는 방법을 보여 줍니다.  
  
 System.object의 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체에 대 <xref:Microsoft.SqlServer.Management.Smo.Rule> 한 모호성을 방지 하기 위해 개체에 대 한 **Dim** 문은 전체 어셈블리 경로로 지정 됩니다.  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
$ru = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Rule `  
-argumentlist $db, "TestRule", "Production"  
  
#Set the TextHeader and TextBody properties to define the rule.   
$ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"  
$ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"  
  
#Create the rule on the instance of SQL Server.   
$ru.Create()  
  
# Bind the rule to a column in the Product table by supplying the table, schema, and   
# column as arguments in the BindToColumn method.   
$ru.BindToColumn("Product", "SellEndDate", "Production")  
  
#Unbind from the column before removing the rule from the database.   
$ru.UnbindFromColumn("Product", "SellEndDate", "Production")  
$ru.Drop()  
```  
  
## <a name="see-also"></a>참고 항목  
 <xref:Microsoft.SqlServer.Management.Smo.Rule>  
  
  
