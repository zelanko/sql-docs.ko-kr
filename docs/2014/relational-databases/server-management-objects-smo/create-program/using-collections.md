---
title: 컬렉션을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQL Server Management Objects, collections
- SMO [SQL Server], collections
- collections [SMO]
ms.assetid: 209eb175-2514-4de1-bc32-b2e6a469d945
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0be31e67be0b80de13a9239b221ca73436a8d6e7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52813925"
---
# <a name="using-collections"></a>컬렉션 사용
  컬렉션은 동일한 개체 클래스에서 구성되고 동일한 부모 개체를 공유하는 개체 목록입니다. 컬렉션 개체에는 항상 Collection 접미사가 있는 개체 유형의 이름이 포함됩니다. 예를 들어 지정한 테이블의 열에 액세스하려면 <xref:Microsoft.SqlServer.Management.Smo.ColumnCollection> 개체 유형을 사용합니다. 이 개체 유형에는 동일한 <xref:Microsoft.SqlServer.Management.Smo.Column> 개체에 속하는 모든 <xref:Microsoft.SqlServer.Management.Smo.Table> 개체가 포함됩니다.  
  
 합니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] `For...Each` 문 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] `foreach` 문은 컬렉션의 각 멤버를 반복할 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-basic"></a>Visual Basic에서 컬렉션을 사용하여 개체 참조  
 이 코드 예제에서는 <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> 및 <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A> 속성을 사용하여 열 속성을 설정하는 방법을 보여 줍니다. 이러한 속성은 개체의 이름을 지정하는 매개 변수와 함께 사용될 때 특정 개체를 식별하는 데 사용할 수 있는 컬렉션을 나타냅니다. <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> 컬렉션 개체 속성에는 이름과 스키마가 필요합니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections1](SMO How to#SMO_VBCollections1)]  -->  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-c"></a>Visual C#에서 컬렉션을 사용하여 개체 참조  
 이 코드 예제에서는 <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> 및 <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A> 속성을 사용하여 열 속성을 설정하는 방법을 보여 줍니다. 이러한 속성은 개체의 이름을 지정하는 매개 변수와 함께 사용될 때 특정 개체를 식별하는 데 사용할 수 있는 컬렉션을 나타냅니다. <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> 컬렉션 개체 속성에는 이름과 스키마가 필요합니다.  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Modify a property using the Databases, Tables, and Columns collections to reference a column.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Nullable = true;   
//Call the Alter method to make the change on the instance of SQL Server.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Alter();   
}  
```  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-basic"></a>Visual Basic에서 컬렉션의 멤버 전체 반복  
 이 코드 예제에서는 <xref:Microsoft.AnalysisServices.Server.Databases%2A> 컬렉션 속성 전체를 반복하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 모든 데이터베이스 연결을 표시합니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections2](SMO How to#SMO_VBCollections2)]  -->  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-c"></a>Visual C#에서 컬렉션의 멤버 전체 반복  
 이 코드 예제에서는 <xref:Microsoft.AnalysisServices.Server.Databases%2A> 컬렉션 속성 전체를 반복하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 모든 데이터베이스 연결을 표시합니다.  
  
```  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
int count = 0;   
int total = 0;   
//Iterate through the databases and call the GetActiveDBConnectionCount method.   
Database db = default(Database);   
foreach ( db in srv.Databases) {   
  count = srv.GetActiveDBConnectionCount(db.Name);   
  total = total + count;   
  //Display the number of connections for each database.   
  Console.WriteLine(count + " connections on " + db.Name);   
}   
//Display the total number of connections on the instance of SQL Server.   
Console.WriteLine("Total connections =" + total);   
}   
```  
  
  
