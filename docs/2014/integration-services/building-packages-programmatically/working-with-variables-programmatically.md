---
title: 프로그래밍 방식으로 변수 사용 | Microsoft Docs
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
- System namespace
- scope [Integration Services]
- variables [Integration Services], programmatically
- configuration files [Integration Services]
- Variables collection
- User namespace
- custom variables [Integration Services]
- variables [Integration Services], customizing
ms.assetid: c4b76a3d-94ca-4a8e-bb45-cb8bd0ea3ec1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 42ac0e7f8b2c41fa30dd41c8255e0b8f04f6e730
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176544"
---
# <a name="working-with-variables-programmatically"></a>프로그래밍 방식으로 변수 사용
  변수는 패키지, 컨테이너, 태스크 및 이벤트 처리기에서 동적으로 값을 설정하고 프로세스를 제어하는 데 사용됩니다. 선행 제약 조건에서 변수를 사용하여 다른 태스크로의 데이터 흐름 방향을 제어할 수도 있습니다. 다음과 같은 다양한 용도로 변수를 사용할 수 있습니다.

-   런타임에 패키지의 속성을 업데이트합니다.

-   런타임에 Transact-SQL 문의 매개 변수 값을 채웁니다.

-   Foreach 루프의 흐름을 제어합니다. 자세한 내용은 [제어 흐름에 열거 추가](../control-flow/control-flow.md)를 참조하세요.

-   선행 제약 조건의 식에 사용하여 선행 제약 조건을 제어합니다. 선행 제약 조건의 제약 조건 정의에는 변수가 포함될 수 있습니다. 자세한 내용은 [선행 제약 조건에 식 추가](../control-flow/precedence-constraints.md)를 참조하세요.

-   For 루프 컨테이너의 조건부 반복을 제어합니다. 자세한 내용은 [제어 흐름에 반복 추가](../add-iteration-to-a-control-flow.md)를 참조하세요.

-   변수 값이 포함된 식을 작성합니다.

-   사용자 지정 변수는 패키지, **Foreach 루프** 컨테이너, **For 루프** 컨테이너, **시퀀스** 컨테이너, TaskHost 및 이벤트 처리기와 같은 모든 컨테이너 유형에 대해 만들 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](../use-variables-in-packages.md)을 참조하세요.

## <a name="scope"></a>범위
 각 컨테이너에는 고유한 <xref:Microsoft.SqlServer.Dts.Runtime.Variables> 컬렉션이 있습니다. 새 변수를 만들면 해당 변수는 부모 컨테이너의 범위 내에서 작동합니다. 패키지 컨테이너는 컨테이너 계층 구조의 최상위에 있으므로 패키지 범위의 변수는 전역 변수와 같은 기능을 수행하며 해당 패키지 내의 모든 컨테이너에 표시됩니다. 또한 컨테이너의 자식 컨테이너에서는 변수 이름이나 컬렉션에서의 변수 인덱스를 사용하여 <xref:Microsoft.SqlServer.Dts.Runtime.Variables> 컬렉션을 통해 컨테이너의 변수 컬렉션에 액세스할 수 있습니다.

 변수의 표시 범위는 하향식으로 결정되므로 패키지 수준에서 선언된 변수는 해당 패키지의 모든 컨테이너에 표시됩니다. 따라서 컨테이너의 <xref:Microsoft.SqlServer.Dts.Runtime.Variables> 컬렉션에는 해당 컨테이너의 변수뿐 아니라 부모 컨테이너에 속하는 모든 변수가 포함됩니다.

 반면, 태스크에 포함된 변수는 범위 및 표시 여부가 제한적이므로 해당 태스크에만 표시됩니다.

 패키지에서 다른 패키지를 실행할 경우 호출하는 패키지의 범위에 정의된 변수를 호출되는 패키지에서 사용할 수 있습니다. 단, 같은 이름의 변수가 호출되는 패키지에도 있는 경우는 예외입니다. 이러한 충돌이 발생할 경우에는 호출되는 패키지의 변수 값이 호출하는 패키지의 값보다 우선합니다. 반대로 호출되는 패키지의 범위에 정의된 변수를 호출하는 패키지에서 사용할 수는 없습니다.

 다음 코드 예에서는 패키지 범위에서 프로그래밍 방식으로 `myCustomVar` 변수를 만든 다음 해당 패키지에 표시된 모든 변수를 반복하여 각 변수의 이름, 데이터 형식 및 값을 출력합니다.

```csharp
using System;
using Microsoft.SqlServer.Dts.Runtime;

namespace Microsoft.SqlServer.Dts.Samples
{
  class Program
  {
    static void Main(string[] args)
    {
      Application app = new Application();
      // Load a sample package that contains a variable that sets the file name.
      Package pkg = app.LoadPackage(
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +
        @"\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx",
        null);
      Variables pkgVars = pkg.Variables;
      Variable myVar = pkg.Variables.Add("myCustomVar", false, "User", "3");
      foreach (Variable pkgVar in pkgVars)
      {
        Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name,
          pkgVar.DataType, pkgVar.Value.ToString());
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

    Dim app As Application = New Application()
    ' Load a sample package that contains a variable that sets the file name.
    Dim pkg As Package = app.LoadPackage( _
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _
      "\Package Samples\CaptureDataLineage Sample\CaptureDataLineage\CaptureDataLineage.dtsx", _
      Nothing)
    Dim pkgVars As Variables = pkg.Variables
    Dim myVar As Variable = pkg.Variables.Add("myCustomVar", False, "User", "3")
    Dim pkgVar As Variable
    For Each pkgVar In pkgVars
      Console.WriteLine("Variable: {0}, {1}, {2}", pkgVar.Name, _
        pkgVar.DataType, pkgVar.Value.ToString())
    Next
    Console.Read()

  End Sub

End Module
```

 **샘플 출력:**

 `Variable: CancelEvent, Int32, 0`

 `Variable: CreationDate, DateTime, 4/18/2003 11:57:00 AM`

 `Variable: CreatorComputerName, String,`

 `Variable: CreatorName, String,`

 `Variable: ExecutionInstanceGUID, String, {237AB5A4-7E59-4FC9-8D61-E8F20363DF25}`

 `Variable: FileName, String, Junk`

 `Variable: InteractiveMode, Boolean, False`

 `Variable: LocaleID, Int32, 1033`

 `Variable: MachineName, String, MYCOMPUTERNAME`

 `Variable: myCustomVar, String, 3`

 `Variable: OfflineMode, Boolean, False`

 `Variable: PackageID, String, {F0D2E396-A6A5-42AE-9467-04CE946A810C}`

 `Variable: PackageName, String, DTSPackage1`

 `Variable: StartTime, DateTime, 1/28/2005 7:55:39 AM`

 `Variable: UserName, String, <domain>\<userid>`

 `Variable: VersionBuild, Int32, 198`

 `Variable: VersionComments, String,`

 `Variable: VersionGUID, String, {90E105B4-B4AF-4263-9CBD-C2050C2D6148}`

 `Variable: VersionMajor, Int32, 1`

 `Variable: VersionMinor, Int32, 0`

 범위가 **System** 네임스페이스인 모든 변수는 패키지에서 사용할 수 있습니다. 자세한 내용은 [System Variables](../system-variables.md)을 참조하세요.

## <a name="namespaces"></a>네임스페이스
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)])는 변수가 있는 두 개의 기본 네임 스페이스 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 제공 합니다. **사용자** 및 **시스템** 네임 스페이스 기본적으로 개발자가 만드는 모든 사용자 지정 변수는 **User** 네임스페이스에 추가됩니다. 시스템 변수는 **System** 네임스페이스에 있습니다. **User** 네임스페이스 외의 추가 네임스페이스를 만들어 사용자 지정 변수를 저장하거나, **User** 네임스페이스의 이름을 변경할 수는 있지만 **System** 네임스페이스의 변수를 추가 또는 수정하거나, 시스템 변수를 다른 네임스페이스에 할당할 수는 없습니다.

 사용할 수 있는 시스템 변수는 컨테이너 유형에 따라 달라집니다. 패키지, 컨테이너, 태스크 및 이벤트 처리기에서 사용할 수 있는 시스템 변수의 목록은 [시스템 변수](../system-variables.md)를 참조하세요.

## <a name="value"></a>값
 사용자 지정 변수의 값은 리터럴 또는 식일 수 있습니다.

-   변수에 리터럴 값을 포함하려면 변수의 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> 속성 값을 설정합니다.

-   식의 결과를 값으로 사용할 수 있도록 변수에 식을 포함하려면 변수의 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> 속성을 `true`로 설정하고 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Expression%2A> 속성에서 식을 지정합니다. 런타임에는 이 식이 계산되고 식 결과가 변수 값으로 사용됩니다. 예를 들어 변수의 식 속성이 `"100 * 2""100 * 2"`이면 이 변수는 값 200으로 계산됩니다.

 변수의 경우에는 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> 값을 명시적으로 설정할 수 없습니다. <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> 값은 변수에 할당된 초기 값에서 유추되며 이후에는 변경할 수 없습니다. 변수 데이터 형식에 대한 자세한 내용은 [Integration Services 데이터 형식](../data-flow/integration-services-data-types.md)을 참조하세요.

 다음 코드 예에서는 새 변수를 만들고, <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A>을 `true`로 설정하고, 변수의 식 속성에 `"100 * 2"` 식을 할당한 다음, 변수 값을 출력합니다.

```csharp
using System;
using Microsoft.SqlServer.Dts.Runtime;

namespace Microsoft.SqlServer.Dts.Samples
{
  class Program
  {
    static void Main(string[] args)
    {
      Package pkg = new Package();
      Variable v100 = pkg.Variables.Add("myVar", false, "", 1);
      v100.EvaluateAsExpression = true;
      v100.Expression = "100 * 2";
      Console.WriteLine("Expression for myVar: {0}", 
        v100.Properties["Expression"].GetValue(v100));
      Console.WriteLine("Value of myVar: {0}", v100.Value.ToString());
      Console.Read();
    }
  }
}
```

```vb
Imports Microsoft.SqlServer.Dts.Runtime

Module Module1

  Sub Main()

    Dim pkg As Package = New Package
    Dim v100 As Variable = pkg.Variables.Add("myVar", False, "", 1)
    v100.EvaluateAsExpression = True
    v100.Expression = "100 * 2"
    Console.WriteLine("Expression for myVar: {0}", _
      v100.Properties("Expression").GetValue(v100))
    Console.WriteLine("Value of myVar: {0}", v100.Value.ToString)
    Console.Read()

  End Sub

End Module
```

 **샘플 출력:**

 `Expression for myVar: 100 * 2`

 `Value of myVar: 200`

 식은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 식 구문을 사용하는 유효한 식이어야 합니다. 변수 식에는 식 구문에서 제공하는 연산자와 함수뿐 아니라 리터럴도 사용할 수 있지만 식에서 다른 변수 또는 열을 참조할 수는 없습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../expressions/integration-services-ssis-expressions.md)가 될 때까지 워크플로를 반복합니다.

## <a name="configuration-files"></a>구성 파일
 구성 파일에 사용자 지정 변수가 포함된 경우 런타임에 해당 변수를 업데이트할 수 있습니다. 즉, 패키지를 실행할 때 패키지의 원래 변수 값을 구성 파일의 새 값으로 바꿀 수 있습니다. 이 기술은 패키지가 각기 다른 변수 값이 필요한 여러 서버에 배포된 경우에 유용합니다. 예를 들어 변수는 **Foreach 루프** 컨테이너가 워크플로를 반복하는 횟수를 지정하거나, 오류가 발생할 경우 이벤트 처리기에서 보내는 전자 메일의 받는 사람을 나열하거나, 패키지가 실패한 것으로 처리되기 전에 발생할 수 있는 오류 횟수를 변경할 수 있습니다. 이러한 변수는 각 환경의 구성 파일에서 동적으로 제공됩니다. 따라서 구성 파일에는 읽기/쓰기가 가능한 변수만 포함될 수 있습니다. 자세한 내용은 [패키지 구성 만들기](../create-package-configurations.md)를 참조하세요.

![Integration Services 아이콘 (작은 아이콘)](../media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하십시오.

## <a name="see-also"></a>참고 항목
 [Integration Services &#40;SSIS&#41; 변수가](../integration-services-ssis-variables.md) [패키지에서 변수를 사용](../use-variables-in-packages.md) 합니다.


