---
title: 생성, 변경 및 뷰를 제거 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- views [SMO]
ms.assetid: 7d445c0e-77ef-4734-993b-e022de31df23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1f19027d4707220306accfe451314f52a22cfe35
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52805315"
---
# <a name="creating-altering-and-removing-views"></a>뷰 생성, 변경 및 제거
  SMO([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects)에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 뷰는 <xref:Microsoft.SqlServer.Management.Smo.View> 개체로 표시됩니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.View.TextBody%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.View> 속성이 뷰를 정의합니다. 이 속성은 뷰를 만드는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] SELECT 문에 해당합니다.  
  
## <a name="example"></a>예제  
 제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio.NET에서 Visual Basic SMO 프로젝트 만들기](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) 또는 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="creating-altering-and-removing-a-view-in-visual-basic"></a>Visual Basic에서 뷰 생성, 변경 및 제거  
 이 코드 예제는 내부 조인을 사용하여 두 테이블을 조인한 뷰를 만드는 방법을 보여 줍니다. 텍스트 모드를 사용하여 뷰를 작성하므로 <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> 속성을 설정해야 합니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBViews1](SMO How to#SMO_VBViews1)]  -->  
  
## <a name="creating-altering-and-removing-a-view-in-visual-c"></a>Visual C#에서 뷰 생성, 변경 및 제거  
 이 코드 예제는 내부 조인을 사용하여 두 테이블을 조인한 뷰를 만드는 방법을 보여 줍니다. 텍스트 모드를 사용하여 뷰를 작성하므로 <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> 속성을 설정해야 합니다.  
  
```  
{  
        //Connect to the local, default instance of SQL Server.   
        Server srv;   
        srv = new Server();   
        //Reference the AdventureWorks2012 database.   
        Database db;   
        db = srv.Databases["AdventureWorks2012"];   
        //Define a View object variable by supplying the parent database, view name and schema in the constructor.   
        View myview;   
        myview = new View(db, "Test_View", "Sales");   
        //Set the TextHeader and TextBody property to define the view.   
        myview.TextHeader = "CREATE VIEW [Sales].[Test_View] AS";   
        myview.TextBody = "SELECT h.SalesOrderID, d.OrderQty FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID";   
        //Create the view on the instance of SQL Server.   
        myview.Create();   
        //Remove the view.   
        myview.Drop();   
        }  
```  
  
## <a name="creating-altering-and-removing-a-view-in-powershell"></a>PowerShell에서 뷰 생성, 변경 및 제거  
 이 코드 예제는 내부 조인을 사용하여 두 테이블을 조인한 뷰를 만드는 방법을 보여 줍니다. 텍스트 모드를 사용하여 뷰를 작성하므로 <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> 속성을 설정해야 합니다.  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a View object variable by supplying the parent database, view name and schema in the constructor.   
$myview  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.View `  
-argumentlist $db, "Test_View", "Sales"  
  
# Set the TextHeader and TextBody property to define the view.   
$myview.TextHeader = "CREATE VIEW [Sales].[Test_View] AS"  
$myview.TextBody ="SELECT h.SalesOrderID, d.OrderQty FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID"  
  
# Create the view on the instance of SQL Server.   
$myview.Create()  
  
# Remove the view.   
$myview.Drop();  
```  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.SqlServer.Management.Smo.View>  
  
  
