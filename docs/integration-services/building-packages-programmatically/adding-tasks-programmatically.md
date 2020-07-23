---
title: 프로그래밍 방식으로 태스크 추가 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- tasks [Integration Services], packages
- adding package tasks
ms.assetid: 5d4652d5-228c-4238-905c-346dd8503fdf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f23f4f68c6856ad86db206d19551c564b5121d67
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921329"
---
# <a name="adding-tasks-programmatically"></a>프로그래밍 방식으로 태스크 추가

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  런타임 엔진에서 다음과 같은 유형의 개체에 태스크를 추가할 수 있습니다.  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Package>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Sequence>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForLoop>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>  
  
 이러한 클래스는 컨테이너로 간주되며 모두 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSequence.Executables%2A> 속성을 상속합니다. 컨테이너에는 해당 컨테이너를 실행하는 동안 런타임에서 처리할 수 있는 실행 개체인 태스크의 컬렉션이 포함될 수 있습니다. 컬렉션에 있는 개체의 실행 순서는 컨테이너의 각 태스크에 설정된 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>에 따라 결정됩니다. 선행 제약 조건을 사용하면 컬렉션에 있는 <xref:Microsoft.SqlServer.Dts.Runtime.Executable>의 성공, 실패 또는 완료 상태에 따라 실행을 분기할 수 있습니다.  
  
 각 컨테이너에는 개별 <xref:Microsoft.SqlServer.Dts.Runtime.Executables> 개체가 들어 있는 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 컬렉션이 있습니다. 각 실행 태스크는 <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Execute%2A> 메서드와 <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Validate%2A> 메서드를 상속하고 구현합니다. 런타임 엔진에서는 이 두 메서드를 호출하여 각 <xref:Microsoft.SqlServer.Dts.Runtime.Executable>을 처리합니다.  
  
 패키지에 태스크를 추가하려면 기존 <xref:Microsoft.SqlServer.Dts.Runtime.Executables> 컬렉션이 있는 컨테이너가 필요합니다. 대부분의 경우 컬렉션에 추가할 태스크는 패키지입니다. 새 태스크 실행 파일을 해당 컨테이너의 컬렉션에 추가하려면 <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> 메서드를 호출합니다. 이 메서드에는 추가할 태스크의 CLSID, PROGID, STOCK 모니커 또는 <xref:Microsoft.SqlServer.Dts.Runtime.TaskInfo.CreationName%2A>이 들어 있는 단일 문자열 매개 변수가 있습니다.  
  
## <a name="task-names"></a>태스크 이름  
 태스크는 이름이나 ID로 지정할 수 있지만 <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> 메서드에서 가장 자주 사용되는 매개 변수는 **STOCK** 모니커입니다. **STOCK** 모니커로 식별된 실행 파일에 태스크를 추가하려면 다음 구문을 사용합니다.  
  
```csharp  
Executable exec = package.Executables.Add("STOCK:BulkInsertTask");  
  
```  
  
```vb  
Dim exec As Executable = package.Executables.Add("STOCK:BulkInsertTask")  
  
```  
  
 다음 목록에서는 **STOCK** 모니커 다음에 사용되는 각 태스크의 이름을 보여 줍니다.  
  
-   ActiveXScriptTask  
  
-   BulkInsertTask  
  
-   ExecuteProcessTask  
  
-   ExecutePackageTask  
  
-   Exec80PackageTask  
  
-   FileSystemTask  
  
-   FTPTask  
  
-   MSMQTask  
  
-   PipelineTask  
  
-   ScriptTask  
  
-   SendMailTask  
  
-   SQLTask  
  
-   TransferStoredProceduresTask  
  
-   TransferLoginsTask  
  
-   TransferErrorMessagesTask  
  
-   TransferJobsTask  
  
-   TransferObjectsTask  
  
-   TransferDatabaseTask  
  
-   WebServiceTask  
  
-   WmiDataReaderTask  
  
-   WmiEventWatcherTask  
  
-   XMLTask  
  
 보다 명시적인 구문을 사용하려는 경우나 추가할 태스크에 STOCK 모니커가 없는 경우에는 긴 이름을 사용하여 실행 파일에 태스크를 추가할 수 있습니다. 이 구문을 사용하려면 태스크의 버전 번호도 지정해야 합니다.  
  
```csharp  
Executable exec = package.Executables.Add(  
  "Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask, " +  
  "Microsoft.SqlServer.ScriptTask, Version=10.0.000.0, " +  
  "Culture=neutral, PublicKeyToken=89845dcd8080cc91");  
```  
  
```vb  
Dim exec As Executable = package.Executables.Add( _  
  "Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask, " & _  
  "Microsoft.SqlServer.ScriptTask, Version=10.0.000.0, " & _  
  "Culture=neutral, PublicKeyToken=89845dcd8080cc91")  
```  
  
 다음 예와 같이 클래스의 **AssemblyQualifiedName** 속성을 사용하면 태스크 버전을 지정하지 않고도 프로그래밍 방식으로 태스크의 긴 이름을 가져올 수 있습니다. 이 예에는 Microsoft.SqlServer.SQLTask 어셈블리에 대한 참조가 필요합니다.  
  
```csharp  
using Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask;  
...  
      Executable exec = package.Executables.Add(  
        typeof(Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask).AssemblyQualifiedName);  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask  
...  
    Dim exec As Executable = package.Executables.Add( _  
      GetType(Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask).AssemblyQualifiedName)  
```  
  
 다음 코드 예에서는 새 패키지에서 <xref:Microsoft.SqlServer.Dts.Runtime.Executables> 컬렉션을 만든 다음 **STOCK** 모니커를 사용하여 컬렉션에 파일 시스템 태스크 및 대량 삽입 태스크를 추가하는 방법을 보여 줍니다. 이 예에는 Microsoft.SqlServer.FileSystemTask 및 Microsoft.SqlServer.BulkInsertTask 어셈블리에 대한 참조가 필요합니다.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
using Microsoft.SqlServer.Dts.Tasks.BulkInsertTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      // Add a File System task to the package.  
      Executable exec1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileSystemTask = exec1 as TaskHost;  
      // Add a Bulk Insert task to the package.  
      Executable exec2 = p.Executables.Add("STOCK:BulkInsertTask");  
      TaskHost thBulkInsertTask = exec2 as TaskHost;  
  
      // Iterate through the package Executables collection.  
      Executables pExecs = p.Executables;  
      foreach (Executable pExec in pExecs)  
      {  
        TaskHost taskHost = (TaskHost)pExec;  
        Console.WriteLine("Type {0}", taskHost.InnerObject.ToString());  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
Imports Microsoft.SqlServer.Dts.Tasks.BulkInsertTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task to the package.  
    Dim exec1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileSystemTask As TaskHost = CType(exec1, TaskHost)  
    ' Add a Bulk Insert task to the package.  
    Dim exec2 As Executable = p.Executables.Add("STOCK:BulkInsertTask")  
    Dim thBulkInsertTask As TaskHost = CType(exec2, TaskHost)  
  
    ' Iterate through the package Executables collection.  
    Dim pExecs As Executables = p.Executables  
    Dim pExec As Executable  
    For Each pExec In pExecs  
      Dim taskHost As TaskHost = CType(pExec, TaskHost)  
      Console.WriteLine("Type {0}", taskHost.InnerObject.ToString())  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **샘플 출력:**  
  
 `Type Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask`  
  
 `Type Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask`  
  
## <a name="taskhost-container"></a>TaskHost 컨테이너  
 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 클래스는 그래픽 사용자 인터페이스에는 나타나지 않는 컨테이너이지만 프로그래밍에서 매우 중요합니다. 이 클래스는 모든 태스크에 대한 래퍼입니다. <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> 메서드를 사용하여 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 개체로 패키지에 추가된 태스크는 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 개체로 캐스팅할 수 있습니다. 태스크를 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>로 캐스팅하면 태스크에서 추가 속성 및 메서드를 사용할 수 있습니다. 또한 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A>의 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 속성을 통해 태스크 자체에 액세스할 수 있습니다. 필요에 따라 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 컬렉션을 통해 태스크의 속성을 사용할 수 있도록 태스크를 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> 개체로 유지할 수 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A>를 사용하면 보다 일반적인 코드를 작성할 수 있다는 장점이 있습니다. 태스크에 대한 매우 구체적인 코드가 필요한 경우에는 태스크를 적절한 개체로 캐스팅해야 합니다.  
  
 다음 코드 예에서는 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>가 들어 있는 <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>인 thBulkInsertTask를 <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask> 개체로 캐스팅하는 방법을 보여 줍니다.  
  
```csharp  
BulkInsertTask myTask = thBulkInsertTask.InnerObject as BulkInsertTask;  
```  
  
```vb  
Dim myTask As BulkInsertTask = CType(thBulkInsertTask.InnerObject, BulkInsertTask)  
```  
  
 다음 코드 예에서는 실행 파일을 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>로 캐스팅한 다음 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A> 속성을 사용하여 호스트에 의해 포함된 실행 파일의 유형을 확인하는 방법을 보여 줍니다.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
using Microsoft.SqlServer.Dts.Tasks.BulkInsertTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      // Add a File System task to the package.  
      Executable exec1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileSystemTask1 = exec1 as TaskHost;  
      // Add a Bulk Insert task to the package.  
      Executable exec2 = p.Executables.Add("STOCK:BulkInsertTask");  
      TaskHost thFileSystemTask2 = exec2 as TaskHost;  
  
      // Iterate through the package Executables collection.  
      Executables pExecs = p.Executables;  
      foreach (Executable pExec in pExecs)  
      {  
        TaskHost taskHost = (TaskHost)pExec;  
        if (taskHost.InnerObject is Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask)  
        {  
          // Do work with FileSystemTask here.  
          Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString());  
        }  
        else if (taskHost.InnerObject is Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask)  
        {  
          // Do work with BulkInsertTask here.  
          Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString());  
        }  
        // Add additional statements to check InnerObject, if desired.  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
Imports Microsoft.SqlServer.Dts.Tasks.BulkInsertTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task to the package.  
    Dim exec1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileSystemTask1 As TaskHost = CType(exec1, TaskHost)  
    ' Add a Bulk Insert task to the package.  
    Dim exec2 As Executable = p.Executables.Add("STOCK:BulkInsertTask")  
    Dim thFileSystemTask2 As TaskHost = CType(exec2, TaskHost)  
  
    ' Iterate through the package Executables collection.  
    Dim pExecs As Executables = p.Executables  
    Dim pExec As Executable  
    For Each pExec In pExecs  
      Dim taskHost As TaskHost = CType(pExec, TaskHost)  
      If TypeOf taskHost.InnerObject Is Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask Then  
        ' Do work with FileSystemTask here.  
        Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString())  
      ElseIf TypeOf taskHost.InnerObject Is Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask Then  
        ' Do work with BulkInsertTask here.  
        Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString())  
      End If  
      ' Add additional statements to check InnerObject, if desired.  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **샘플 출력:**  
  
 `Found task of type Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask`  
  
 `Found task of type Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask`  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> 문은 새로 만든 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 개체에서 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 개체로 캐스팅된 실행 파일을 반환합니다.  
  
 새 개체의 속성을 설정하거나 메서드를 호출하려면 다음 두 가지 방법을 사용합니다.  
  
1.  <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A>의 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 컬렉션을 사용합니다. 예를 들어 개체의 속성을 가져오려면 `th.Properties["propertyname"].GetValue(th))`를 사용하고, 속성을 설정하려면 `th.Properties["propertyname"].SetValue(th, <value>);`를 사용합니다.  
  
2.  <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A>의 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>를 태스크 클래스로 캐스팅합니다. 예를 들어 대량 삽입 태스크가 <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>로 패키지에 추가된 후 이 태스크를 <xref:Microsoft.SqlServer.Dts.Runtime.Executable>로 캐스팅하고 이후에 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>로 캐스팅하려면 `BulkInsertTask myTask = th.InnerObject as BulkInsertTask;`를 사용합니다.  
  
 태스크별 클래스로 캐스팅하는 대신 코드에서 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 클래스를 사용하면 다음과 같은 장점이 있습니다.  
  
-   코드에서 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost><xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> 공급자가 어셈블리를 참조할 필요가 없습니다.  
  
-   컴파일 시 태스크 이름을 몰라도 되므로 모든 태스크에 대해 작동하는 일반 루틴을 코딩할 수 있습니다. 이러한 일반 루틴에 포함된 메서드에서는 사용자가 해당 메서드에 태스크 이름을 전달하며 모든 메서드 코드가 모든 태스크에 대해 작동합니다. 따라서 이 메서드는 테스트 코드를 작성하는 데 유용합니다.  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>에서 태스크별 클래스로 캐스팅하면 다음과 같은 장점이 있습니다.  
  
-   Visual Studio 프로젝트에서 문 완성 기능(IntelliSense)을 제공합니다.  
  
-   코드가 보다 빨리 실행될 수 있습니다.  
  
-   태스크별 개체를 사용하면 초기 바인딩 및 결과 최적화 기능을 사용할 수 있습니다. 초기 바인딩과 런타임 바인딩에 대한 자세한 내용은 Visual Basic 언어 개념의 "초기 바인딩 및 런타임에 바인딩" 항목을 참조하십시오.  
  
 다음 코드 예에서는 태스크 코드 재사용의 개념을 확장하여, 태스크를 해당되는 특정 클래스로 캐스팅하는 대신 실행 파일을 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>로 캐스팅한 다음 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A>를 사용하여 모든 태스크에 대한 일반 코드를 작성하는 방법을 보여 줍니다.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package package = new Package();  
  
      string[] tasks = { "STOCK:SQLTask", "STOCK:ScriptTask",   
        "STOCK:ExecuteProcessTask", "STOCK:PipelineTask",   
        "STOCK:FTPTask", "STOCK:SendMailTask", "STOCK:MSMQTask" };  
  
      foreach (string s in tasks)  
      {  
        TaskHost taskhost = package.Executables.Add(s) as TaskHost;  
        DtsProperties props = taskhost.Properties;  
        Console.WriteLine("Enumerating properties on " + taskhost.Name);  
        Console.WriteLine(" TaskHost.InnerObject is " + taskhost.InnerObject.ToString());  
        Console.WriteLine();  
  
        foreach (DtsProperty prop in props)  
        {  
          Console.WriteLine("Properties for " + prop.Name);  
          Console.WriteLine("Name : " + prop.Name);  
          Console.WriteLine("Type : " + prop.Type.ToString());  
          Console.WriteLine("Readable : " + prop.Get.ToString());  
          Console.WriteLine("Writable : " + prop.Set.ToString());  
          Console.WriteLine();  
        }  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Package = New Package()  
  
    Dim tasks() As String = New String() {"STOCK:SQLTask", "STOCK:ScriptTask", _  
              "STOCK:ExecuteProcessTask", "STOCK:PipelineTask", _  
              "STOCK:FTPTask", "STOCK:SendMailTask", "STOCK:MSMQTask"}  
  
    For Each s As String In tasks  
  
      Dim taskhost As TaskHost = CType(package.Executables.Add(s), TaskHost)  
      Dim props As DtsProperties = taskhost.Properties  
      Console.WriteLine("Enumerating properties on " & taskhost.Name)  
      Console.WriteLine(" TaskHost.InnerObject is " & taskhost.InnerObject.ToString())  
      Console.WriteLine()  
  
      For Each prop As DtsProperty In props  
        Console.WriteLine("Properties for " + prop.Name)  
        Console.WriteLine(" Name : " + prop.Name)  
        Console.WriteLine(" Type : " + prop.Type.ToString())  
        Console.WriteLine(" Readable : " + prop.Get.ToString())  
        Console.WriteLine(" Writable : " + prop.Set.ToString())  
        Console.WriteLine()  
      Next  
  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>외부 리소스  
 blogs.msdn.com의 블로그 항목 - [EzAPI – SQL Server 2012용으로 업데이트됨](https://go.microsoft.com/fwlink/?LinkId=243223)  

## <a name="see-also"></a>참고 항목  
 [프로그래밍 방식으로 태스크 연결](../../integration-services/building-packages-programmatically/connecting-tasks-programmatically.md)  
  
  
