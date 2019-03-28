---
title: 프로그래밍 방식으로 패키지 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: e44bcc70-32d3-43e8-a84b-29aef819d5d3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 87a757f007b2a4b30172c51971e56dd585c166f6
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58280662"
---
# <a name="creating-a-package-programmatically"></a>프로그래밍 방식으로 패키지 만들기
  <xref:Microsoft.SqlServer.Dts.Runtime.Package> 개체는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 프로젝트 솔루션에 있는 다른 모든 개체의 최상위 컨테이너입니다. 최상위 컨테이너인 패키지는 첫 번째로 만들어지는 개체이며 그 이후에 만들어지는 개체는 패키지에 추가된 다음 패키지의 컨텍스트 내에서 실행됩니다. 패키지 자체는 데이터를 이동하거나 변환하지 않습니다. 패키지는 패키지에 포함된 태스크를 통해서만 작업을 수행합니다. 태스크는 패키지에서 수행하는 대부분의 작업을 수행하고 패키지의 기능을 정의합니다. 단 세 줄의 코드만으로도 패키지를 만들고 실행할 수 있지만 다양한 태스크와 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 개체를 추가하면 패키지에 추가 기능을 제공할 수 있습니다. 이 섹션에서는 프로그래밍 방식으로 패키지를 만드는 방법을 설명하며, 태스크 또는 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>를 만드는 방법에 대해서는 설명하지 않습니다. 이러한 내용은 뒷부분의 섹션에서 설명합니다.  
  
## <a name="example"></a>예제  
 Visual Studio IDE를 사용하여 코드를 작성하려면 Microsoft.SqlServer.Dts.Runtime에 `using` 문(Visual Basic .NET의 경우 `Imports`)을 만들기 위한 Microsoft.SqlServer.ManagedDTS.DLL에 대한 참조가 필요합니다. 다음 코드 예제에서는 빈 패키지를 만드는 방법을 보여 줍니다.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package package;  
      package = new Package();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Package  
    package = New Package  
  
  End Sub  
  
End Module  
```  
  
 예제를 컴파일하고 실행하려면 Visual Studio에서 F5 키를 누릅니다. C# 컴파일러인 **csc.exe**를 사용하여 코드를 빌드하려면 명령 프롬프트에서 다음 명령과 파일 참조를 사용하여 코드를 컴파일합니다. 이때 *\<filename>* 은 .cs 또는 .vb 파일의 이름으로 바꾸고 원하는 *\<outputfilename>* 을 지정합니다.  
  
 **csc /target:library /out: \<outputfilename>.dll \<filename>.cs /r:Microsoft.SqlServer.Managed DTS.dll" /r:System.dll**  
  
 Visual Basic .NET 컴파일러인 **vbc.exe**를 사용하여 코드를 빌드하려면 명령 프롬프트에서 다음 명령과 파일 참조를 사용하여 코드를 컴파일합니다.  
  
 **vbc /target:library /out: \<outputfilename>.dll \<filename>.vb /r:Microsoft.SqlServer.Managed DTS.dll" /r:System.dll**  
  
 디스크에 저장된 기존 패키지를 파일 시스템이나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드하여 패키지를 만들 수도 있습니다. 이때 차이점은 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 개체가 먼저 만들어진 다음 패키지 개체가 응용 프로그램의 오버로드된 메서드인 **LoadPackage**(플랫 파일의 경우), **LoadFromSQLServer**([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장된 패키지의 경우) 또는 <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A>(파일 시스템에 저장된 패키지의 경우) 중 하나로 채워진다는 것입니다. 다음 예에서는 디스크에서 기존 패키지를 로드한 다음 패키지의 여러 속성을 확인합니다.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class ApplicationTests  
  {  
    static void Main(string[] args)  
    {  
      // The variable pkg points to the location of the  
      // ExecuteProcess package sample that was installed with  
      // the SSIS samples.  
      string pkg = @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\ExecuteProcess Sample\ExecuteProcess\UsingExecuteProcess.dtsx";  
  
      Application app = new Application();  
      Package p = app.LoadPackage(pkg, null);  
  
      // Now that the package is loaded, we can query on  
      // its properties.  
      int n = p.Configurations.Count;  
      DtsProperty p2 = p.Properties["VersionGUID"];  
      DTSProtectionLevel pl = p.ProtectionLevel;  
  
      Console.WriteLine("Number of configurations = " + n.ToString());  
      Console.WriteLine("VersionGUID = " + (string)p2.GetValue(p));  
      Console.WriteLine("ProtectionLevel = " + pl.ToString());  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module ApplicationTests  
  
  Sub Main()  
  
    ' The variable pkg points to the location of the  
    ' ExecuteProcess package sample that was installed with  
    ' the SSIS samples.  
    Dim pkg As String = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\ExecuteProcess Sample\ExecuteProcess\UsingExecuteProcess.dtsx"  
  
    Dim app As Application = New Application()  
    Dim p As Package = app.LoadPackage(pkg, Nothing)  
  
    ' Now that the package is loaded, we can query on  
    ' its properties.  
    Dim n As Integer = p.Configurations.Count  
    Dim p2 As DtsProperty = p.Properties("VersionGUID")  
    Dim pl As DTSProtectionLevel = p.ProtectionLevel  
  
    Console.WriteLine("Number of configurations = " & n.ToString())  
    Console.WriteLine("VersionGUID = " & CType(p2.GetValue(p), String))  
    Console.WriteLine("ProtectionLevel = " & pl.ToString())  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **샘플 출력:**  
  
 `Number of configurations = 2`  
  
 `VersionGUID = {09016682-89B8-4406-AAC9-AF1E527FF50F}`  
  
 `ProtectionLevel = DontSaveSensitive`  
  
## <a name="external-resources"></a>외부 리소스  
  
-   blogs.msdn.com의 블로그 항목 - [API 예제 - OleDB 원본 및 OleDB 대상](https://go.microsoft.com/fwlink/?LinkId=220824)  
  
-   blogs.msdn.com의 블로그 항목 - [EzAPI – SQL Server 2012용으로 업데이트됨](https://go.microsoft.com/fwlink/?LinkId=243223)  
  
## <a name="see-also"></a>참고 항목  
 [프로그래밍 방식으로 태스크 추가](../../integration-services/building-packages-programmatically/adding-tasks-programmatically.md)  
  
  
