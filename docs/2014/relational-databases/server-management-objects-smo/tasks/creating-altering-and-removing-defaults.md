---
title: 생성, 변경 및 기본값을 제거 | Microsoft Docs
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
- defaults [SMO]
ms.assetid: c30ac3b9-8150-4264-ba4c-c549f44261ab
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d7daddec0a7c96776938f2824635b719341ecbe4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081311"
---
# <a name="creating-altering-and-removing-defaults"></a>기본값 생성, 변경 및 제거
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects(SMO)에서 기본 제약 조건은 <xref:Microsoft.SqlServer.Management.Smo.Default> 개체로 표시됩니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Default> 속성은 삽입할 값을 설정하는 데 사용되며, 상수 또는 상수 값을 반환하는 GETDATE()와 같은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문일 수 있습니다. <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 속성은 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 메서드로 수정할 수 없습니다. 대신 <xref:Microsoft.SqlServer.Management.Smo.Default> 개체를 삭제하고 다시 만들어야 합니다.  
  
## <a name="example"></a>예제  
 제공된 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 참조 [Visual Studio.NET에서 Visual Basic SMO 프로젝트 만들기](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) 또는 [Visual C를 만들&#35; Visual Studio.NET에서 SMO 프로젝트](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="creating-altering-and-removing-a-default-in-visual-basic"></a>Visual Basic에서 기본값 생성, 변경 및 제거  
 이 코드 예제는 기본값을 하나는 단순 텍스트로 만들고 다른 하나는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문으로 만드는 방법을 보여 줍니다. 기본값은 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> 메서드를 사용하여 열에 연결하고 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A> 메서드를 사용하여 분리해야 합니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDefaults1](SMO How to#SMO_VBDefaults1)]  -->  
  
## <a name="creating-altering-and-removing-a-default-in-visual-c"></a>Visual C#에서 기본값 생성, 변경 및 제거  
 이 코드 예제는 기본값을 하나는 단순 텍스트로 만들고 다른 하나는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문으로 만드는 방법을 보여 줍니다. 기본값은 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> 메서드를 사용하여 열에 연결하고 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A> 메서드를 사용하여 분리해야 합니다.  
  
```  
{  
  
          Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database  db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Default object variable by supplying the parent database and the default name   
            //in the constructor.   
            Default def = new Default(db, "Test_Default2");  
  
            //Set the TextHeader and TextBody properties that define the default.   
            def.TextHeader = "CREATE DEFAULT [Test_Default2] AS";  
            def.TextBody = "GetDate()";  
  
            //Create the default on the instance of SQL Server.   
            def.Create();  
  
            //Bind the default to a column in a table in AdventureWorks2012  
            def.BindToColumn("SpecialOffer", "StartDate", "Sales");  
  
            //Unbind the default from the column and remove it from the database.   
            def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales");  
            def.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-default-in-powershell"></a>PowerShell에서 기본값 생성, 변경 및 제거  
 이 코드 예제는 기본값을 하나는 단순 텍스트로 만들고 다른 하나는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문으로 만드는 방법을 보여 줍니다. 기본값은 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> 메서드를 사용하여 열에 연결하고 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A> 메서드를 사용하여 분리해야 합니다.  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
#Define a Default object variable by supplying the parent database and the default name in the constructor.  
$def = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Default `  
-argumentlist $db, "Test_Default2"  
  
#Set the TextHeader and TextBody properties that define the default.   
$def.TextHeader = "CREATE DEFAULT [Test_Default2] AS"  
$def.TextBody = "GetDate()"  
  
#Create the default on the instance of SQL Server.   
$def.Create()  
  
#Bind the default to the column.   
$def.BindToColumn("SpecialOffer", "StartDate", "Sales")  
  
#Unbind the default from the column and remove it from the database.   
$def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales")  
$def.Drop()  
```  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.SqlServer.Management.Smo.Default>  
  
  