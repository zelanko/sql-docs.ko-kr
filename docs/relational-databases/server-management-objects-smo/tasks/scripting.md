---
description: 스크립팅
title: 스크립팅 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- dependencies [SMO]
- scripts [SMO]
ms.assetid: 13a35511-3987-426b-a3b7-3b2e83900dc7
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0f59d526c2b238eb5bed080087cfbc453dabee8b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475444"
---
# <a name="scripting"></a>스크립팅
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  SMO의 스크립팅은 <xref:Microsoft.SqlServer.Management.Smo.Scripter> 개체와 자식 개체 또는 개별 개체의 **스크립트** 메서드를 통해 제어 됩니다. <xref:Microsoft.SqlServer.Management.Smo.Scripter>개체는 인스턴스의 개체에 대 한 종속성 관계의 매핑을 제어 합니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 <xref:Microsoft.SqlServer.Management.Smo.Scripter> 개체와 자식 개체를 사용한 고급 스크립팅은 다음 3단계 프로세스를 거칩니다.  
  
1.  검색  
  
2.  목록 생성  
  
3.  스크립트 생성  

 검색 단계에서는 <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker> 개체를 사용합니다. 개체의 URN 목록을 제공하면 <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker.DiscoverDependencies%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker> 메서드가 URN 목록의 개체에 대해 <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> 개체를 반환합니다. 부울 *Fparents* 매개 변수는 지정 된 개체의 부모 또는 자식을 검색할지 여부를 선택 하는 데 사용 됩니다. 이 단계에서 종속성 트리를 수정할 수 있습니다.  
  
 목록 생성 단계에서는 트리가 전달되고 결과 목록이 반환됩니다. 이 개체 목록은 스크립팅 순서로 나열되며 조작할 수 있습니다.  
  
 목록 생성 단계에서는 <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker.WalkDependencies%2A> 메서드를 사용하여 <xref:Microsoft.SqlServer.Management.Smo.DependencyTree>를 반환합니다. 이 단계에서 <xref:Microsoft.SqlServer.Management.Smo.DependencyTree>를 수정할 수 있습니다.  
  
 마지막 세 번째 단계에서는 지정된 목록 및 스크립팅 옵션으로 스크립트가 생성됩니다. 결과가 <xref:System.Collections.Specialized.StringCollection> 시스템 개체로 반환됩니다. 이 단계에서는 <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> 개체의 항목 컬렉션과 <xref:Microsoft.SqlServer.Management.Smo.DependencyTree.NumberOfSiblings%2A> 및 <xref:Microsoft.SqlServer.Management.Smo.DependencyTree.FirstChild%2A>와 같은 속성으로부터 종속 개체 이름이 추출됩니다.  
  
## <a name="example"></a>예  
 제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
  
 이 코드 예제에는 System.object 네임 스페이스에 대 한 **Imports** 문이 필요 합니다. 애플리케이션의 선언 앞에 다른 Imports 문과 함께 삽입하십시오.  
  
```  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
Imports System.Collections.Specialized  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-visual-basic"></a>Visual Basic에서 데이터베이스의 종속성 스크립팅  
 이 코드 예제는 종속성을 검색하고 목록 전체를 반복하여 결과를 표시하는 방법을 보여 줍니다.  
  
```  
' compile with:   
' /r:Microsoft.SqlServer.Smo.dll   
' /r:Microsoft.SqlServer.ConnectionInfo.dll   
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Sdk.Sfc  
  
Public Class A  
   Public Shared Sub Main()  
      ' database name  
      Dim dbName As [String] = "AdventureWorksLT2012"   ' database name  
  
      ' Connect to the local, default instance of SQL Server.   
      Dim srv As New Server()  
  
      ' Reference the database.    
      Dim db As Database = srv.Databases(dbName)  
  
      ' Define a Scripter object and set the required scripting options.   
      Dim scrp As New Scripter(srv)  
      scrp.Options.ScriptDrops = False  
      scrp.Options.WithDependencies = True  
      scrp.Options.Indexes = True   ' To include indexes  
      scrp.Options.DriAllConstraints = True   ' to include referential constraints in the script  
  
      ' Iterate through the tables in database and script each one. Display the script.  
      For Each tb As Table In db.Tables  
         ' check if the table is not a system table  
         If tb.IsSystemObject = False Then  
            Console.WriteLine("-- Scripting for table " + tb.Name)  
  
            ' Generating script for table tb  
            Dim sc As System.Collections.Specialized.StringCollection = scrp.Script(New Urn() {tb.Urn})  
            For Each st As String In sc  
               Console.WriteLine(st)  
            Next  
            Console.WriteLine("--")  
         End If  
      Next  
   End Sub  
End Class  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-visual-c"></a>Visual C#에서 데이터베이스의 종속성 스크립팅  
 이 코드 예제는 종속성을 검색하고 목록 전체를 반복하여 결과를 표시하는 방법을 보여 줍니다.  
  
```  
// compile with:   
// /r:Microsoft.SqlServer.Smo.dll   
// /r:Microsoft.SqlServer.ConnectionInfo.dll   
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using System;  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Sdk.Sfc;  
  
public class A {  
   public static void Main() {   
      String dbName = "AdventureWorksLT2012"; // database name  
  
      // Connect to the local, default instance of SQL Server.   
      Server srv = new Server();  
  
      // Reference the database.    
      Database db = srv.Databases[dbName];  
  
      // Define a Scripter object and set the required scripting options.   
      Scripter scrp = new Scripter(srv);  
      scrp.Options.ScriptDrops = false;  
      scrp.Options.WithDependencies = true;  
      scrp.Options.Indexes = true;   // To include indexes  
      scrp.Options.DriAllConstraints = true;   // to include referential constraints in the script  
  
      // Iterate through the tables in database and script each one. Display the script.     
      foreach (Table tb in db.Tables) {   
         // check if the table is not a system table  
         if (tb.IsSystemObject == false) {  
            Console.WriteLine("-- Scripting for table " + tb.Name);  
  
            // Generating script for table tb  
            System.Collections.Specialized.StringCollection sc = scrp.Script(new Urn[]{tb.Urn});  
            foreach (string st in sc) {  
               Console.WriteLine(st);  
            }  
            Console.WriteLine("--");  
         }  
      }   
   }  
}  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-powershell"></a>PowerShell에서 데이터베이스의 종속성 스크립팅  
 이 코드 예제는 종속성을 검색하고 목록 전체를 반복하여 결과를 표시하는 방법을 보여 줍니다.  
  
```  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default  
  
# Create a Scripter object and set the required scripting options.  
$scrp = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Scripter -ArgumentList (Get-Item .)  
$scrp.Options.ScriptDrops = $false  
$scrp.Options.WithDependencies = $true  
$scrp.Options.IncludeIfNotExists = $true  
  
# Set the path context to the tables in AdventureWorks2012.  
  
CD Databases\AdventureWorks2012\Tables  
  
foreach ($Item in Get-ChildItem)  
 {    
 $scrp.Script($Item)  
 }  
```  
  
  
