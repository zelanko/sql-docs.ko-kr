---
title: 프로그래밍 방식으로 로컬 패키지 로드 및 실행 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Integration Services packages, running
- events [Integration Services], capturing
- packages [Integration Services], running
- loading packages programmatically
- Visual Basic [Integration Services]
- running packages [Integration Services]
- programmatically load and run packages [SSIS]
ms.assetid: 2f9fc1a8-a001-4c54-8c64-63b443725422
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3f127aeb7d9e86e70460190d11ea7c61b57c1d24
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028577"
---
# <a name="loading-and-running-a-local-package-programmatically"></a>프로그래밍 방식으로 로컬 패키지 로드 및 실행

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [패키지 실행](../packages/run-integration-services-ssis-packages.md)에 설명된 방법을 사용하여 필요에 따라 또는 미리 지정한 시간에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 실행할 수 있습니다. 그러나 단 몇 줄의 코드로도 Windows Forms 애플리케이션, 콘솔 애플리케이션, ASP.NET Web Form 또는 웹 서비스, Windows 서비스 등의 사용자 지정 애플리케이션에서 패키지를 실행할 수 있습니다.  
  
 이 항목에서는 다음과 같은 주제를 다룹니다.  
  
-   프로그래밍 방식으로 패키지 로드  
  
-   프로그래밍 방식으로 패키지 실행  
  
 이 항목에서 패키지를 로드하고 실행하는 데 사용되는 모든 메서드에는 **Microsoft.SqlServer.ManagedDTS** 어셈블리에 대한 참조가 필요합니다. 새 프로젝트에 참조를 추가한 후 **using** 또는 **Imports** 문을 사용하여 <xref:Microsoft.SqlServer.Dts.Runtime> 네임스페이스를 가져옵니다.  
  
## <a name="loading-a-package-programmatically"></a>프로그래밍 방식으로 패키지 로드  
 로컬 컴퓨터에서 프로그래밍 방식으로 패키지를 로드하려면 패키지가 로컬 위치에 저장되어 있든 원격 위치에 저장되어 있든 관계없이 다음 메서드 중 하나를 호출합니다.  
  
|스토리지 위치|호출할 메서드|  
|----------------------|--------------------|  
|파일|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadPackage%2A>|  
|SSIS 패키지 저장소|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromSqlServer%2A>|  
  
> [!IMPORTANT]  
>  SSIS 패키지 저장소를 사용하기 위한 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 클래스의 메서드는 ".", localhost 또는 로컬 서버의 서버 이름만 지원합니다. "(local)"은 사용할 수 없습니다.  
  
## <a name="running-a-package-programmatically"></a>프로그래밍 방식으로 패키지 실행  
 로컬 컴퓨터에서 패키지를 실행하는 관리 코드로 사용자 지정 애플리케이션을 개발하려면 다음 방법이 필요합니다. 여기에 요약된 단계는 뒷부분의 예제 콘솔 애플리케이션에서 자세히 보여 줍니다.  
  
#### <a name="to-run-a-package-on-the-local-computer-programmatically"></a>로컬 컴퓨터에서 프로그래밍 방식으로 패키지를 실행하려면  
  
1.  Visual Studio 개발 환경을 시작하고 원하는 개발 언어로 새 애플리케이션을 만듭니다. 이 예에서는 콘솔 애플리케이션을 사용하지만 Windows Forms 애플리케이션, ASP.NET Web Form 또는 Web 서비스, Windows 서비스 등에서 패키지를 실행할 수도 있습니다.  
  
2.  **프로젝트** 메뉴에서 **참조 추가**를 클릭하고 **Microsoft.SqlServer.ManagedDTS.dll**에 대한 참조를 추가합니다. **확인**을 클릭합니다.  
  
3.  Visual Basic **Imports** 문 또는 C# **using** 문을 사용하여 **Microsoft.SqlServer.Dts.Runtime** 네임스페이스를 가져옵니다.  
  
4.  기본 루틴에 다음 코드를 추가합니다. 완성된 콘솔 애플리케이션은 다음 예와 같습니다.  
  
    > [!NOTE]  
    >  예제 코드에서는 <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadPackage%2A> 메서드를 사용하여 파일 시스템에서 패키지를 로드하는 방법을 보여 줍니다. 그러나 <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromSqlServer%2A> 메서드를 호출하여 MSDB 데이터베이스에서 패키지를 로드하거나 <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A> 메서드를 호출하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 저장소에서 패키지를 로드할 수도 있습니다.  
  
5.  프로젝트를 실행합니다. 예제 코드에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 예제와 함께 설치된 CalculatedColumns 예제 패키지를 실행합니다. 패키지 실행 결과는 콘솔 창에 표시됩니다.  
  
### <a name="sample-code"></a>예제 코드  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkgLocation As String  
    Dim pkg As New Package  
    Dim app As New Application  
    Dim pkgResults As DTSExecResult  
  
    pkgLocation = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx"  
    pkg = app.LoadPackage(pkgLocation, Nothing)  
    pkgResults = pkg.Execute()  
  
    Console.WriteLine(pkgResults.ToString())  
    Console.ReadKey()  
  
  End Sub  
  
End Module  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace RunFromClientAppCS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string pkgLocation;  
      Package pkg;  
      Application app;  
      DTSExecResult pkgResults;  
  
      pkgLocation =  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx";  
      app = new Application();  
      pkg = app.LoadPackage(pkgLocation, null);  
      pkgResults = pkg.Execute();  
  
      Console.WriteLine(pkgResults.ToString());  
      Console.ReadKey();  
    }  
  }  
}  
```  
  
## <a name="capturing-events-from-a-running-package"></a>실행 중인 패키지에서 이벤트 캡처  
 위의 예제에 표시된 대로 패키지를 프로그래밍 방식으로 실행할 경우 패키지를 실행할 때 발생하는 오류와 기타 이벤트를 캡처할 수도 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> 클래스에서 상속되는 클래스를 추가하고 패키지를 로드할 때 해당 클래스에 대한 참조를 전달하여 이 작업을 수행할 수 있습니다. 다음 예에서는 <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents.OnError%2A> 이벤트만 캡처하지만 <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> 클래스에서 캡처할 수 있는 다른 이벤트도 여러 가지 있습니다.  
  
#### <a name="to-run-a-package-on-the-local-computer-programmatically-and-capture-package-events"></a>로컬 컴퓨터에서 프로그래밍 방식으로 패키지를 실행하고 패키지 이벤트를 캡처하려면  
  
1.  위 예의 단계에 따라 이 예에서 사용할 프로젝트를 만듭니다.  
  
2.  기본 루틴에 다음 코드를 추가합니다. 완성된 콘솔 애플리케이션은 다음 예와 같습니다.  
  
3.  프로젝트를 실행합니다. 예제 코드에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 예제와 함께 설치된 CalculatedColumns 예제 패키지를 실행합니다. 패키지 실행 결과는 발생한 오류와 함께 콘솔 창에 표시됩니다.  
  
### <a name="sample-code"></a>예제 코드  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkgLocation As String  
    Dim pkg As New Package  
    Dim app As New Application  
    Dim pkgResults As DTSExecResult  
  
    Dim eventListener As New EventListener()  
  
    pkgLocation = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx"  
    pkg = app.LoadPackage(pkgLocation, eventListener)  
    pkgResults = pkg.Execute(Nothing, Nothing, eventListener, Nothing, Nothing)  
  
    Console.WriteLine(pkgResults.ToString())  
    Console.ReadKey()  
  
  End Sub  
  
End Module  
  
Class EventListener  
  Inherits DefaultEvents  
  
  Public Overrides Function OnError(ByVal source As Microsoft.SqlServer.Dts.Runtime.DtsObject, _  
    ByVal errorCode As Integer, ByVal subComponent As String, ByVal description As String, _  
    ByVal helpFile As String, ByVal helpContext As Integer, _  
    ByVal idofInterfaceWithError As String) As Boolean  
  
    ' Add application-specific diagnostics here.  
    Console.WriteLine("Error in {0}/{1} : {2}", source, subComponent, description)  
    Return False  
  
  End Function  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace RunFromClientAppWithEventsCS  
{  
  class MyEventListener : DefaultEvents  
  {  
    public override bool OnError(DtsObject source, int errorCode, string subComponent,   
      string description, string helpFile, int helpContext, string idofInterfaceWithError)  
    {  
      // Add application-specific diagnostics here.  
      Console.WriteLine("Error in {0}/{1} : {2}", source, subComponent, description);  
      return false;  
    }  
  }  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string pkgLocation;  
      Package pkg;  
      Application app;  
      DTSExecResult pkgResults;  
  
      MyEventListener eventListener = new MyEventListener();  
  
      pkgLocation =  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx";  
      app = new Application();  
      pkg = app.LoadPackage(pkgLocation, eventListener);  
      pkgResults = pkg.Execute(null, null, eventListener, null, null);  
  
      Console.WriteLine(pkgResults.ToString());  
      Console.ReadKey();  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [로컬 실행과 원격 실행의 차이점 이해](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [프로그래밍 방식으로 원격 패키지 로드 및 실행](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [로컬 패키지의 출력 로드](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
