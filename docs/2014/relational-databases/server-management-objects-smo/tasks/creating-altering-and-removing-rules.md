---
title: 생성, 변경 및 규칙을 제거 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rules [SMO]
ms.assetid: 16981459-524e-4b39-a899-4370eaf763cc
caps.latest.revision: 44
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d68aa2d625de762ad1bf503c9c79fdbbeaa3875d
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39082815"
---
# <a name="creating-altering-and-removing-rules"></a>규칙 생성, 변경 및 제거
  SMO에서 규칙은 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체로 표시됩니다. 규칙은 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 속성, 즉 IN, LIKE, BETWEEN과 같은 연산자나 조건자를 사용하는 조건식이 포함된 텍스트 문자열로 정의됩니다. 규칙은 열 또는 기타 데이터베이스 개체를 참조할 수 없습니다. 데이터베이스 개체를 참조하지 않는 기본 제공 함수는 포함할 수 있습니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 속성 정의에는 입력한 데이터 값을 참조하는 변수가 포함되어야 합니다. 모든 이름 또는 기호 규칙을 만들 때 값을 나타내는 데 사용할 수 있지만 첫 번째 문자 여야 합니다 \@ 기호입니다.  
  
## <a name="example"></a>예제  
 제공된 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio.NET에서 Visual Basic SMO 프로젝트 만들기](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) 또는 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-basic"></a>Visual Basic에서 규칙 생성, 변경 및 제거  
 이 코드 예제는 규칙을 만들고, 규칙을 열에 연결하고, <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체의 속성을 수정하고, 열에서 규칙을 분리하고, 규칙을 삭제하는 방법을 보여 줍니다.  
  
 System.Data 어셈블리의 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체와 혼동을 피하기 위해 이 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체의 `Dim` 문은 전체 어셈블리 경로로 지정됩니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBRules1](SMO How to#SMO_VBRules1)]  -->  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-c"></a>Visual C#에서 규칙 생성, 변경 및 제거  
 이 코드 예제는 규칙을 만들고, 규칙을 열에 연결하고, <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체의 속성을 수정하고, 열에서 규칙을 분리하고, 규칙을 삭제하는 방법을 보여 줍니다.  
  
 System.Data 어셈블리의 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체와 혼동을 피하기 위해 이 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체의 `Dim` 문은 전체 어셈블리 경로로 지정됩니다.  
  
```  
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
  
 System.Data 어셈블리의 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체와 혼동을 피하기 위해 이 <xref:Microsoft.SqlServer.Management.Smo.Rule> 개체의 `Dim` 문은 전체 어셈블리 경로로 지정됩니다.  
  
```  
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
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.SqlServer.Management.Smo.Rule>  
  
  
