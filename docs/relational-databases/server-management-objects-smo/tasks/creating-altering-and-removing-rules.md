---
title: "생성, 변경 및 제거 하는 규칙 | Microsoft Docs"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: rules [SMO]
ms.assetid: 16981459-524e-4b39-a899-4370eaf763cc
caps.latest.revision: "46"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b4e0a96280d38f7447a10decb6c99187b925f646
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/12/2018
---
# <a name="creating-altering-and-removing-rules"></a>규칙 생성, 변경 및 제거
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO에서 규칙은 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체로 표시됩니다. 규칙은 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 속성, 즉 IN, LIKE, BETWEEN과 같은 연산자나 조건자를 사용하는 조건식이 포함된 텍스트 문자열로 정의됩니다. 규칙은 열 또는 기타 데이터베이스 개체를 참조할 수 없습니다. 데이터베이스 개체를 참조하지 않는 기본 제공 함수는 포함할 수 있습니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 속성 정의에는 입력한 데이터 값을 참조하는 변수가 포함되어야 합니다. 규칙을 만들 때는 모든 이름 또는 기호를 사용하여 값을 나타낼 수 있으나 첫 번째 문자는 반드시 @ 기호를 사용해야 합니다.  
  
## <a name="example"></a>예제  
 제공된 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 참조 [만들기 Visual C &#35; Visual Studio.NET에서에서 SMO 프로젝트](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-basic"></a>Visual Basic에서 규칙 생성, 변경 및 제거  
 이 코드 예제는 규칙을 만들고, 규칙을 열에 연결하고, <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체의 속성을 수정하고, 열에서 규칙을 분리하고, 규칙을 삭제하는 방법을 보여 줍니다.  
  
 **Dim** 문에 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체와 혼동을 피하기 전체 어셈블리 경로로 지정 됩니다는 <xref:Microsoft.SqlServer.Management.Smo.Rule> System.Data 어셈블리의 개체입니다.  
  
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
  
 **Dim** 문에 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체와 혼동을 피하기 전체 어셈블리 경로로 지정 됩니다는 <xref:Microsoft.SqlServer.Management.Smo.Rule> System.Data 어셈블리의 개체입니다.  
  
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
  
 **Dim** 문에 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체와 혼동을 피하기 전체 어셈블리 경로로 지정 됩니다는 <xref:Microsoft.SqlServer.Management.Smo.Rule> System.Data 어셈블리의 개체입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.SqlServer.Management.Smo.Rule>  
  
  
