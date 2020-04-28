---
title: SMO 이벤트 처리 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- events [SMO]
- SQL Server Management Objects, events
- SMO [SQL Server], events
- events [SMO], about events
ms.assetid: b4f120dd-ba78-46ff-99c5-e47effac8544
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 893fb08f2d32c7ae9d80321c1d849010660cc308
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70148722"
---
# <a name="handling-smo-events"></a>SMO 이벤트 처리
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  이벤트 처리기 및 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 사용하여 구독할 수 있는 서버 이벤트 유형이 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects(SMO)의 인스턴스 클래스 대부분은 서버에서 특정 동작이 발생할 때 이벤트를 트리거할 수 있습니다.  
  
 이러한 이벤트는 이벤트 처리기를 설정하고 연관된 이벤트를 구독하여 프로그래밍 방식으로 처리할 수 있습니다. 모든 구독은 SMO 클라이언트 프로그램이 종료될 때 제거되므로 이런 유형의 이벤트 처리는 일시적입니다.  
  
## <a name="connectioncontext-event-handling"></a>ConnectionContext 이벤트 처리  
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체는 여러 이벤트 유형을 지원합니다. 이벤트 속성을 적절한 이벤트 처리기 인스턴스로 설정한 다음, 이벤트 처리기 개체를 이벤트를 처리하는 보호된 함수로 정의해야 합니다.  
  
## <a name="event-subscription"></a>이벤트 구독  
 이벤트 처리기 클래스를 작성하고, 해당 인스턴스를 만들고, 이벤트 처리기를 부모 개체에 할당하고, 이벤트를 구독하는 방법으로 이벤트를 처리합니다.  
  
 이벤트를 처리하려면 이벤트 처리기 클래스를 작성해야 합니다. 이벤트 처리기 클래스는 여러 개의 이벤트 처리기 함수를 포함할 수 있고, 이벤트를 처리하려면 이 클래스를 설치해야 합니다. 이벤트 처리기 함수는 이벤트에 대 한 정보를 보고 하는 데 사용할 수 있는 이벤트에 대 한 정보를 *ServerEventNotificatificationArgs* 매개 변수에서 받습니다.  
  
 처리할 수 있는 데이터베이스 및 서버 이벤트의 유형은 <xref:Microsoft.SqlServer.Management.Smo.DatabaseEventSet> 클래스 및 <xref:Microsoft.SqlServer.Management.Smo.ServerEventSet>클래스에 나열 됩니다.  
  
## <a name="example"></a>예제  
제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  

  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-basic"></a>Visual Basic에서 이벤트 처리기 등록 및 이벤트 처리 구독  
 이 코드 예제는 이벤트 처리기를 설정하는 방법과 데이터베이스 이벤트를 구독하는 방법을 보여 줍니다.  
  
```VBNET
'Create an event handler subroutine that runs when a table is created.
Private Sub MyCreateEventHandler(ByVal sender As Object, ByVal e As ServerEventArgs)
    Console.WriteLine("A table has just been added to the AdventureWorks2012 2008 database.")
End Sub
'Create an event handler subroutine that runs when a table is deleted.
Private Sub MyDropEventHandler(ByVal sender As Object, ByVal e As ServerEventArgs)
    Console.WriteLine("A table has just been dropped from the AdventureWorks2012 2008 database.")
End Sub
Sub Main()
    'Connect to the local, default instance of SQL Server.
    Dim srv As Server
    srv = New Server
    'Reference the AdventureWorks2012 database.
    Dim db As Database
    db = srv.Databases("AdventureWorks2012")
    'Create a database event set that contains the CreateTable event only.
    Dim databaseCreateEventSet As New DatabaseEventSet
    databaseCreateEventSet.CreateTable = True
    'Create a server event handler and set it to the first event handler subroutine.
    Dim serverCreateEventHandler As ServerEventHandler
    serverCreateEventHandler = New ServerEventHandler(AddressOf MyCreateEventHandler)
    'Subscribe to the first server event handler when a CreateTable event occurs.
    db.Events.SubscribeToEvents(databaseCreateEventSet, serverCreateEventHandler)
    'Create a database event set that contains the DropTable event only.
    Dim databaseDropEventSet As New DatabaseEventSet
    databaseDropEventSet.DropTable = True
    'Create a server event handler and set it to the second event handler subroutine.
    Dim serverDropEventHandler As ServerEventHandler
    serverDropEventHandler = New ServerEventHandler(AddressOf MyDropEventHandler)
    'Subscribe to the second server event handler when a DropTable event occurs.
    db.Events.SubscribeToEvents(databaseDropEventSet, serverDropEventHandler)
    'Start event handling.
    db.Events.StartEvents()
    'Create a table on the database.
    Dim tb As Table
    tb = New Table(db, "Test_Table")
    Dim mycol1 As Column
    mycol1 = New Column(tb, "Name", DataType.NChar(50))
    mycol1.Collation = "Latin1_General_CI_AS"
    mycol1.Nullable = True
    tb.Columns.Add(mycol1)
    tb.Create()
    'Remove the table.
    tb.Drop()
    'Wait until the events have occured.
    Dim x As Integer
    Dim y As Integer
    For x = 1 To 1000000000
        y = x * 2
    Next
    'Stop event handling.
    db.Events.StopEvents()

End Sub
``` 
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-c"></a>Visual C#에서 이벤트 처리기 등록 및 이벤트 처리 구독  
 이 코드 예제는 이벤트 처리기를 설정하는 방법과 데이터베이스 이벤트를 구독하는 방법을 보여 줍니다.  
  
```csharp  
//Create an event handler subroutine that runs when a table is created.   
private void MyCreateEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been added to the AdventureWorks2012 database.");   
}   
//Create an event handler subroutine that runs when a table is deleted.   
private void MyDropEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been dropped from the AdventureWorks2012 database.");   
}   
public void Main()   
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Create a database event set that contains the CreateTable event only.   
DatabaseEventSet databaseCreateEventSet = new DatabaseEventSet();   
databaseCreateEventSet.CreateTable = true;   
//Create a server event handler and set it to the first event handler subroutine.   
ServerEventHandler serverCreateEventHandler;   
serverCreateEventHandler = new ServerEventHandler(MyCreateEventHandler);   
//Subscribe to the first server event handler when a CreateTable event occurs.   
db.Events.SubscribeToEvents(databaseCreateEventSet, serverCreateEventHandler);   
    //Create a database event set that contains the DropTable event only.   
DatabaseEventSet databaseDropEventSet = new DatabaseEventSet();   
databaseDropEventSet.DropTable = true;   
//Create a server event handler and set it to the second event handler subroutine.   
ServerEventHandler serverDropEventHandler;   
serverDropEventHandler = new ServerEventHandler(MyDropEventHandler);   
//Subscribe to the second server event handler when a DropTable event occurs.   
db.Events.SubscribeToEvents(databaseDropEventSet, serverDropEventHandler);   
//Start event handling.   
db.Events.StartEvents();   
//Create a table on the database.   
Table tb;   
tb = new Table(db, "Test_Table");   
Column mycol1;   
mycol1 = new Column(tb, "Name", DataType.NChar(50));   
mycol1.Collation = "Latin1_General_CI_AS";   
mycol1.Nullable = true;   
tb.Columns.Add(mycol1);   
tb.Create();   
//Remove the table.   
tb.Drop();   
//Wait until the events have occured.   
int x;   
int y;   
for (x = 1; x <= 1000000000; x++) {   
    y = x * 2;   
}   
//Stop event handling.   
db.Events.StopEvents();   
}  
```  
  
  
