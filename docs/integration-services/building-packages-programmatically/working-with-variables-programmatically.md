---
title: "변수를 프로그래밍 방식으로 작업 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 5c8968302f42e1b8fde55894810ecb77cf715ab6
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="working-with-variables-programmatically"></a>프로그래밍 방식으로 변수 사용
  변수는 패키지, 컨테이너, 태스크 및 이벤트 처리기에서 동적으로 값을 설정하고 프로세스를 제어하는 데 사용됩니다. 선행 제약 조건에서 변수를 사용하여 다른 태스크로의 데이터 흐름 방향을 제어할 수도 있습니다. 다음과 같은 다양한 용도로 변수를 사용할 수 있습니다.  
  
-   런타임에 패키지의 속성을 업데이트합니다.  
  
-   런타임에 Transact-SQL 문의 매개 변수 값을 채웁니다.  
  
-   Foreach 루프의 흐름을 제어합니다. 자세한 내용은 참조 [제어 흐름에 열거 추가](http://msdn.microsoft.com/library/f212b5fb-3cc4-422e-9b7c-89eb769a812a)합니다.  
  
-   선행 제약 조건의 식에 사용하여 선행 제약 조건을 제어합니다. 선행 제약 조건의 제약 조건 정의에는 변수가 포함될 수 있습니다. 자세한 내용은 [선행 제약 조건에 식 추가](http://msdn.microsoft.com/library/5574d89a-a68e-4b84-80ea-da93305e5ca1)를 참조하세요.  
  
-   For 루프 컨테이너의 조건부 반복을 제어합니다. 자세한 내용은 참조 [제어 흐름에 반복 추가](http://msdn.microsoft.com/library/eb3a7494-88ae-4165-9d0f-58715eb1734a)합니다.  
  
-   변수 값이 포함된 식을 작성합니다.  
  
-   모든 컨테이너 유형에 대해 사용자 지정 변수를 만들 수 있습니다: 패키지, **Foreach 루프** 컨테이너 **For 루프** 컨테이너 **시퀀스** 컨테이너, Taskhost 및 이벤트 처리기입니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)을 참조하세요.  
  
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
  
 모든 변수 범위는 **시스템** 네임 스페이스는 패키지에 사용할 수 있습니다. 자세한 내용은 [System Variables](../../integration-services/system-variables.md)을 참조하세요.  
  
## <a name="namespaces"></a>네임스페이스  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]); 변수 상주 하는 두 개의 기본 네임 스페이스를 제공 합니다. **사용자** 및 **시스템** 네임 스페이스입니다. 기본적으로 개발자가 만든 모든 사용자 지정 변수를 추가 **사용자** 네임 스페이스입니다. 에 있는 시스템 변수는 **시스템** 네임 스페이스입니다. 이외의 다른 네임 스페이스를 추가로 만들 수 있습니다는 **사용자** 있습니다 및 사용자 지정 변수를 저장 하는 네임 스페이스의 이름을 변경할 수는 **사용자** 수 있지만 네임 스페이스를 추가 하거나에서 변수를 수정는 **시스템** 네임 스페이스 또는 시스템 변수를 다른 네임 스페이스에 할당 합니다.  
  
 사용할 수 있는 시스템 변수는 컨테이너 유형에 따라 달라집니다. 패키지, 컨테이너, 태스크 및 이벤트 처리기를 사용할 수 있는 시스템 변수 목록은 참조 [시스템 변수](../../integration-services/system-variables.md)합니다.  
  
## <a name="value"></a>Value  
 사용자 지정 변수의 값은 리터럴 또는 식일 수 있습니다.  
  
-   변수에 리터럴 값을 포함하려면 변수의 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Value%2A> 속성 값을 설정합니다.  
  
-   해당 값으로 식의 결과 사용할 수 있도록 하는 식을 포함 하면 변수를 원하는 경우 설정의 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> 변수의 속성 **true**에 식을 제공 하 고는 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.Expression%2A> 속성입니다. 런타임에는 이 식이 계산되고 식 결과가 변수 값으로 사용됩니다. 예를 들어 변수의 식 속성이 `"100 * 2""100 * 2"`이면 이 변수는 값 200으로 계산됩니다.  
  
 변수의 경우에는 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> 값을 명시적으로 설정할 수 없습니다. <xref:Microsoft.SqlServer.Dts.Runtime.Variable.DataType%2A> 값은 변수에 할당된 초기 값에서 유추되며 이후에는 변경할 수 없습니다. 변수 데이터 형식에 대 한 자세한 내용은 참조 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)합니다.  
  
 다음 코드 예제에서는 새 변수 집합을 만듭니다 <xref:Microsoft.SqlServer.Dts.Runtime.Variable.EvaluateAsExpression%2A> 를 **true**, 식을 할당 `"100 * 2"` 들어 변수의 식 속성에 변수 값을 출력 합니다.  
  
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
  
 식은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 식 구문을 사용하는 유효한 식이어야 합니다. 변수 식에는 식 구문에서 제공하는 연산자와 함수뿐 아니라 리터럴도 사용할 수 있지만 식에서 다른 변수 또는 열을 참조할 수는 없습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../integration-services/expressions/integration-services-ssis-expressions.md)가 될 때까지 워크플로를 반복합니다.  
  
## <a name="configuration-files"></a>구성 파일  
 구성 파일에 사용자 지정 변수가 포함된 경우 런타임에 해당 변수를 업데이트할 수 있습니다. 즉, 패키지를 실행할 때 패키지의 원래 변수 값을 구성 파일의 새 값으로 바꿀 수 있습니다. 이 기술은 패키지가 각기 다른 변수 값이 필요한 여러 서버에 배포된 경우에 유용합니다. 예를 들어 변수 횟수를 지정할 수는 **Foreach 루프** 컨테이너가 반복 하는 워크플로, 또는 목록의 받는 사람 이벤트 처리기에서 보내는 오류가 발생 하는 경우 전자 메일을 또는 패키지가 실패 하기 전에 발생할 수 있는 오류 수를 변경 합니다. 이러한 변수는 각 환경의 구성 파일에서 동적으로 제공됩니다. 따라서 구성 파일에는 읽기/쓰기가 가능한 변수만 포함될 수 있습니다. 자세한 내용은 [패키지 구성 만들기](../../integration-services/packages/create-package-configurations.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services &#40; Ssis&#41; 변수](../../integration-services/integration-services-ssis-variables.md)   
 [패키지에서 변수 사용](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  

