---
title: 프로그래밍 방식으로 이벤트 처리 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Integration Services packages, events
- SQL Server Integration Services packages, events
- SSIS events, programmatically handling
- packages [Integration Services], events
- DtsEventHandler object
- SSIS packages, events
- SSIS events
- events [Integration Services], programmatically
- tasks [Integration Services], events
- IDTSEvents interface
ms.assetid: 0f00bd66-efd5-4f12-9e1c-36195f739332
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c54c3fe00842122b4b2fdeb4eb6c7bcbb38cf0a4
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84924824"
---
# <a name="handling-events-programmatically"></a>프로그래밍 방식으로 이벤트 처리
  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 런타임에서는 패키지의 유효성 검사 및 실행 전후와 도중에 발생하는 이벤트 컬렉션을 제공합니다. 이러한 이벤트는 두 가지 방법으로 캡처할 수 있습니다. 첫 번째 방법은 클래스에 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> 인터페이스를 구현하고 해당 클래스를 패키지의 `Execute` 및 `Validate` 메서드에 대한 매개 변수로 지정하는 것입니다. 두 번째 방법은 태스크 및 루프와 같이 다른 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 개체를 포함할 수 있으며 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>에서 이벤트가 발생할 때 실행되는 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> 개체를 만드는 것입니다. 이 섹션에서는 이러한 두 가지 방법에 대해 설명하고 각 사용 방법을 보여 주는 코드 예를 제공합니다.  
  
## <a name="receiving-idtsevents-callbacks"></a>IDTSEvents 콜백 받기  
 프로그래밍 방식으로 패키지를 만들고 실행하는 개발자는 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> 인터페이스를 사용하여 유효성 검사 및 실행 중에 이벤트 알림을 받을 수 있습니다. 이렇게 하려면 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> 인터페이스를 구현하는 클래스를 만들고 이 클래스를 패키지의 `Validate` 및 `Execute` 메서드에 대한 매개 변수로 지정합니다. 그러면 이벤트가 발생할 때 런타임 엔진에 의해 해당 클래스의 메서드가 호출됩니다.  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> 클래스는 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> 인터페이스를 이미 구현하는 클래스이므로 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents>를 직접 구현하는 다른 방법은 <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents>의 파생 클래스를 만들고 응답할 특정 이벤트를 재정의하는 것입니다. 그런 다음 해당 클래스를 <xref:Microsoft.SqlServer.Dts.Runtime.Package>의 `Validate` 및 `Execute` 메서드에 대한 매개 변수로 지정하여 이벤트 콜백을 받을 수 있습니다.  
  
 다음 코드 예제에서는 <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents>의 파생 클래스를 보여 주고 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnPreExecute%2A> 메서드를 재정의합니다. 그런 다음 클래스는 `Validate` 패키지의 및 메서드에 대 한 aparameter로 제공 됩니다 `Execute` .  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      MyEventsClass eventsClass = new MyEventsClass();  
  
      p.Validate(null, null, eventsClass, null);  
      p.Execute(null, null, eventsClass, null, null);  
  
      Console.Read();  
    }  
  }  
  class MyEventsClass : DefaultEvents  
  {  
    public override void OnPreExecute(Executable exec, ref bool fireAgain)  
    {  
      // TODO: Add custom code to handle the event.  
      Console.WriteLine("The PreExecute event of the " +  
        exec.ToString() + " has been raised.");  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    Dim eventsClass As MyEventsClass = New MyEventsClass()  
  
    p.Validate(Nothing, Nothing, eventsClass, Nothing)  
    p.Execute(Nothing, Nothing, eventsClass, Nothing, Nothing)  
  
    Console.Read()  
  
  End Sub  
  
End Module  
  
Class MyEventsClass  
  Inherits DefaultEvents  
  
  Public Overrides Sub OnPreExecute(ByVal exec As Executable, ByRef fireAgain As Boolean)  
  
    ' TODO: Add custom code to handle the event.  
    Console.WriteLine("The PreExecute event of the " & _  
      exec.ToString() & " has been raised.")  
  
  End Sub  
  
End Class  
```  
  
## <a name="creating-dtseventhandler-objects"></a>DtsEventHandler 개체 만들기  
 런타임 엔진에서는 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 개체를 통해 강력하고 매우 유연한 이벤트 처리 및 알림 시스템을 제공합니다. 이러한 개체를 사용하면 이벤트 처리기가 속해 있는 이벤트가 발생할 때만 실행되는 이벤트 처리기 내의 전체 워크플로를 디자인할 수 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 개체는 상위 개체에 대해 해당 이벤트가 발생할 때 실행되는 컨테이너입니다. 이 아키텍처를 사용하면 컨테이너에서 발생하는 이벤트에 대한 응답으로 실행되는 격리된 워크플로를 만들 수 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 개체는 동기적이므로 이벤트에 연결된 이벤트 처리기가 반환되기 전까지는 실행이 다시 시작되지 않습니다.  
  
 다음 코드에서는 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 개체를 만드는 방법을 보여 줍니다. 이 코드는 패키지의 <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> 컬렉션에 <xref:Microsoft.SqlServer.Dts.Runtime.Package.Executables%2A>를 추가한 다음 해당 태스크의 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 이벤트에 대한 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnError%2A> 개체를 만듭니다. <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>는 첫 번째 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnError%2A>에 대해 <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> 이벤트가 발생할 때 실행되는 이벤트 처리기에 추가됩니다. 이 예에서는 C:\Windows\Temp\DemoFile.txt라는 테스트용 파일이 있다고 가정합니다. 이 샘플을 처음 실행할 때는 이 파일이 성공적으로 복사되므로 이벤트 처리기가 호출되지 않습니다. 그러나 두 번째로 이 샘플을 실행할 때는 <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask> 값이 `false`여서 첫 번째 <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask.OverwriteDestinationFile%2A>가 파일을 복사하지 못하므로 이벤트 처리기가 호출됩니다. 두 번째 <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>는 원본 파일을 삭제하며 패키지에서는 발생한 오류로 인한 실패를 보고합니다.  
  
## <a name="example"></a>예제  
  
```csharp  
using System;  
using System.IO;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string f = "DemoFile.txt";  
      Executable e;  
      TaskHost th;  
      FileSystemTask fst;  
  
      Package p = new Package();  
  
      p.Variables.Add("sourceFile", true, String.Empty,  
        @"C:\Windows\Temp\" + f);  
      p.Variables.Add("destinationFile", true, String.Empty,  
        Path.Combine(Directory.GetCurrentDirectory(), f));  
  
      // Create a first File System task and add it to the package.  
      // This task tries to copy a file from one folder to another.  
      e = p.Executables.Add("STOCK:FileSystemTask");  
      th = e as TaskHost;  
      th.Name = "FileSystemTask1";  
      fst = th.InnerObject as FileSystemTask;  
  
      fst.Operation = DTSFileSystemOperation.CopyFile;  
      fst.OverwriteDestinationFile = false;  
      fst.Source = "sourceFile";  
      fst.IsSourcePathVariable = true;  
      fst.Destination = "destinationFile";  
      fst.IsDestinationPathVariable = true;  
  
      // Add an event handler for the FileSystemTask's OnError event.  
      DtsEventHandler ehOnError = (DtsEventHandler)th.EventHandlers.Add("OnError");  
  
      // Create a second File System task and add it to the event handler.  
      // This task deletes the source file if the event handler is called.  
      e = ehOnError.Executables.Add("STOCK:FileSystemTask");  
      th = e as TaskHost;  
      th.Name = "FileSystemTask2";  
      fst = th.InnerObject as FileSystemTask;  
  
      fst.Operation = DTSFileSystemOperation.DeleteFile;  
      fst.Source = "sourceFile";  
      fst.IsSourcePathVariable = true;  
  
      DTSExecResult vr = p.Validate(null, null, null, null);  
      Console.WriteLine("ValidationResult = " + vr.ToString());  
      if (vr == DTSExecResult.Success)  
      {  
        DTSExecResult er = p.Execute(null, null, null, null, null);  
        Console.WriteLine("ExecutionResult = " + er.ToString());  
        if (er == DTSExecResult.Failure)  
          if (!File.Exists(@"C:\Windows\Temp\" + f))  
            Console.WriteLine("Source file has been deleted by the event handler.");  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports System.IO  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim f As String = "DemoFile.txt"  
    Dim e As Executable  
    Dim th As TaskHost  
    Dim fst As FileSystemTask  
  
    Dim p As Package = New Package()  
  
    p.Variables.Add("sourceFile", True, String.Empty, _  
      "C:\Windows\Temp\" & f)  
    p.Variables.Add("destinationFile", True, String.Empty, _  
      Path.Combine(Directory.GetCurrentDirectory(), f))  
  
    ' Create a first File System task and add it to the package.  
    ' This task tries to copy a file from one folder to another.  
    e = p.Executables.Add("STOCK:FileSystemTask")  
    th = CType(e, TaskHost)  
    th.Name = "FileSystemTask1"  
    fst = CType(th.InnerObject, FileSystemTask)  
  
    fst.Operation = DTSFileSystemOperation.CopyFile  
    fst.OverwriteDestinationFile = False  
    fst.Source = "sourceFile"  
    fst.IsSourcePathVariable = True  
    fst.Destination = "destinationFile"  
    fst.IsDestinationPathVariable = True  
  
    ' Add an event handler for the FileSystemTask's OnError event.  
    Dim ehOnError As DtsEventHandler = CType(th.EventHandlers.Add("OnError"), DtsEventHandler)  
  
    ' Create a second File System task and add it to the event handler.  
    ' This task deletes the source file if the event handler is called.  
    e = ehOnError.Executables.Add("STOCK:FileSystemTask")  
    th = CType(e, TaskHost)  
    th.Name = "FileSystemTask1"  
    fst = CType(th.InnerObject, FileSystemTask)  
  
    fst.Operation = DTSFileSystemOperation.DeleteFile  
    fst.Source = "sourceFile"  
    fst.IsSourcePathVariable = True  
  
    Dim vr As DTSExecResult = p.Validate(Nothing, Nothing, Nothing, Nothing)  
    Console.WriteLine("ValidationResult = " + vr.ToString())  
    If vr = DTSExecResult.Success Then  
      Dim er As DTSExecResult = p.Execute(Nothing, Nothing, Nothing, Nothing, Nothing)  
      Console.WriteLine("ExecutionResult = " + er.ToString())  
      If er = DTSExecResult.Failure Then  
        If Not File.Exists("C:\Windows\Temp\" + f) Then  
          Console.WriteLine("Source file has been deleted by the event handler.")  
        End If  
      End If  
    End If  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
![Integration Services 아이콘 (작은 아이콘)](../media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지를 방문하세요.](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services &#40;SSIS&#41; 이벤트 처리기](../integration-services-ssis-event-handlers.md)   
 [패키지에 이벤트 처리기 추가](../add-an-event-handler-to-a-package.md)  
  
  
