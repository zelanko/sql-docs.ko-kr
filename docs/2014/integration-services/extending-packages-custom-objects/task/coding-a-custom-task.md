---
title: 사용자 지정 태스크 코딩 | Microsoft Docs
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
- Validate method
- custom tasks [Integration Services], validating
- validation [Integration Services], design-time tasks
- SSIS custom tasks, validating
ms.assetid: dc224f4f-b339-4eb6-a008-1b4fe0ea4fd2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0cc4026c8eae44ab8dacff62a72cfa66470c07fb
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176283"
---
# <a name="coding-a-custom-task"></a>사용자 지정 태스크 코딩
  <xref:Microsoft.SqlServer.Dts.Runtime.Task> 기본 클래스에서 상속된 클래스를 만들고 이 클래스에 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 특성을 적용한 후에는 기본 클래스의 속성 및 메서드 구현을 재정의하여 사용자 지정 기능을 제공해야 합니다.

## <a name="configuring-the-task"></a>태스크 구성

### <a name="validating-the-task"></a>태스크 유효성 검사
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 패키지를 디자인하는 경우 모든 오류를 런타임에만 찾는 것이 아니라 태스크에 대한 설정 작업이 수행되는 즉시 올바르지 않거나 적절하지 않은 설정을 catch할 수 있도록 유효성 검사를 통해 각 태스크에 대한 설정을 확인할 수 있습니다. 유효성 검사의 목적은 태스크가 성공적으로 실행되지 못하게 하는 잘못된 설정이나 연결이 태스크에 포함되어 있는지 확인하는 것입니다. 이렇게 하면 첫 번째 실행에서 실행될 가능성이 높은 태스크가 패키지에 포함되도록 할 수 있습니다.

 사용자 지정 코드에서 `Validate` 메서드를 사용하여 유효성 검사 기능을 구현할 수 있습니다. 런타임 엔진에서는 태스크에 대해 `Validate` 메서드를 호출하여 해당 태스크의 유효성을 검사합니다. 태스크 유효성 검사의 성공 여부를 결정하는 조건을 정의하고 평가 결과를 런타임 엔진에 알리는 작업은 태스크 개발자가 수행해야 합니다.

#### <a name="task-abstract-base-class"></a>태스크 추상 기본 클래스
 
  <xref:Microsoft.SqlServer.Dts.Runtime.Task> 추상 기본 클래스에서는 `Validate` 메서드를 제공하며 각 태스크에서는 이 메서드를 재정의하여 유효성 검사 조건을 정의할 수 있습니다. 
  [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서는 패키지를 디자인하는 동안 `Validate` 메서드를 자동으로 여러 번 호출하고 경고나 오류가 발생할 때 태스크의 구성과 관련된 문제를 식별하는 데 유용한 시각적 표시를 사용자에게 제공합니다. 태스크에서는 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 열거형의 값을 반환하고 경고 및 오류 이벤트를 발생시켜 유효성 검사 결과를 제공합니다. 이러한 이벤트에는 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 사용자에게 표시되는 정보가 들어 있습니다.

 다음은 유효성 검사의 몇 가지 예입니다.

-   연결 관리자가 특정 파일 이름의 유효성을 검사합니다.

-   연결 관리자가 입력 형식이 XML 파일과 같은 필요한 형식인지 확인합니다.

-   데이터베이스 입력이 필요한 태스크에서 데이터베이스 연결이 아닌 연결을 통해 데이터를 받을 수 없는지 확인합니다.

-   태스크에서 해당 태스크에 설정된 다른 속성과 충돌하는 속성이 없는지 확인합니다.

-   태스크에서 실행 시 태스크에 사용되는 필수 리소스를 모두 사용할 수 있는지 확인합니다.

 유효성 검사를 수행할 대상 항목을 결정할 때는 성능을 고려해야 합니다. 예를 들어 태스크에 대한 입력이 대역폭이 낮거나 트래픽이 많은 네트워크 연결을 통해 이루어지는 경우 유효성 검사를 통해 리소스의 사용 가능성을 확인하는 데는 몇 초 정도만 소요되지만 다른 유효성 검사 작업에는 사용량이 많은 서버로의 왕복이 필요하므로 유효성 검사 루틴의 속도가 느릴 수 있습니다. 유효성을 검사할 수 있는 속성 및 설정은 여러 가지가 있지만 모든 속성 및 설정에 대해 유효성을 검사해야 하는 것은 아닙니다.

-   태스크가 실행되기 전에 `Validate`에서도 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 메서드의 코드를 호출하며 이때 유효성 검사가 실패하면 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>에서는 실행을 취소합니다.

#### <a name="user-interface-considerations-during-validation"></a>유효성 검사 중 사용자 인터페이스 고려 사항
 
  <xref:Microsoft.SqlServer.Dts.Runtime.Task>에는 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> 메서드에 대한 매개 변수로 `Validate` 인터페이스가 포함됩니다. <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> 인터페이스에는 태스크에서 런타임 엔진에 이벤트를 발생시키기 위해 호출하는 메서드가 포함되어 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A> 메서드는 유효성 검사 중 경고 또는 오류 조건이 발생할 때 호출됩니다. 두 경고 메서드에는 동일한 매개 변수가 필요하며 이러한 매개 변수에는 오류 코드, 원본 구성 요소, 설명, 도움말 파일, 및 도움말 컨텍스트 정보가 포함됩니다. [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서는 이 정보를 사용하여 디자인 화면에 시각적 표시를 제공합니다. 디자이너에서 제공하는 시각적 표시로는 디자이너 화면에서 태스크 옆에 나타나는 느낌표 아이콘이 있습니다. 이 시각적 표시는 실행을 계속하기 전에 태스크에 추가 구성이 필요함을 나타냅니다.

 느낌표 아이콘에는 오류 메시지가 포함된 도구 설명도 표시됩니다. 오류 메시지는 태스크에서 이벤트의 설명 매개 변수로 제공됩니다. 오류 메시지는 **의** 태스크 목록[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 창에도 표시되어 사용자에게 모든 유효성 검사 오류를 볼 수 있는 중앙 위치를 제공합니다.

#### <a name="validation-example"></a>유효성 검사 예
 다음 코드 예에서는 `UserName` 속성을 사용하는 태스크를 보여 줍니다. 이 속성은 유효성 검사를 성공적으로 수행하기 위한 필수 항목으로 지정되었습니다. 이 속성이 설정되어 있지 않으면 태스크에서는 오류를 게시하고 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Failure> 열거형의 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>를 반환합니다. 
  `Validate` 메서드는 try/catch 블록에 래핑되며 예외가 발생하면 유효성 검사가 실패합니다.

```csharp
using System;
using Microsoft.SqlServer.Dts.Runtime;

public class SampleTask : Task
{
  private string userName = "";

  public override DTSExecResult Validate(Connections connections,
     VariableDispenser variableDispenser, IDTSComponentEvents events,
     IDTSLogging log)
  {
    try
    {
      if (this.userName == "")
      {
        //   Raise an OnError event.
        events.FireError(0, "SampleTask", "The UserName property must be configured.", "", 0);
        //   Fail validation.
        return DTSExecResult.Failure;
      }
      //   Return success.
      return DTSExecResult.Success;
    }
    catch (System.Exception exception)
    {
      //   Capture exceptions, post an error, and fail validation.
      events.FireError(0, "Sampletask", exception.Message, "", 0);
      return DTSExecResult.Failure;
    }
  }
  public string UserName
  {
    get
    {
      return this.userName;
    }
    set
    {
      this.userName = value;
    }
  }
}
```

```vb
Imports System
Imports Microsoft.SqlServer.Dts.Runtime

Public Class SampleTask
  Inherits Task

  Private _userName As String = ""

  Public Overrides Function Validate(ByVal connections As Connections, _
     ByVal variableDispenser As VariableDispenser, _
     ByVal events As IDTSComponentEvents, _
     ByVal log As IDTSLogging) As DTSExecResult

    Try
      If Me._userName = "" Then
        '   Raise an OnError event.
        events.FireError(0, "SampleTask", "The UserName property must be configured.", "", 0)
        '   Fail validation.
        Return DTSExecResult.Failure
      End If
      '   Return success.
      Return DTSExecResult.Success
    Catch exception As System.Exception
      '   Capture exceptions, post an error, and fail validation.
      events.FireError(0, "Sampletask", exception.Message, "", 0)
      Return DTSExecResult.Failure
    End Try

  End Function

  Public Property UserName() As String
    Get
      Return Me._userName
    End Get
    Set(ByVal Value As String)
      Me._userName = Value
    End Set
  End Property

End Class
```

### <a name="persisting-the-task"></a>태스크 지속
 일반적으로 태스크의 사용자 지정 지속성은 구현할 필요가 없습니다. 사용자 지정 지속성은 개체의 속성이 복합 데이터 형식을 사용할 때만 필요합니다. 자세한 내용은[Integration Services 사용자 지정 개체 개발](../developing-custom-objects-for-integration-services.md)을 참조하세요.

## <a name="executing-the-task"></a>태스크 실행
 이 섹션에서는 태스크에서 상속하고 재정의한 `Execute` 메서드의 사용 방법을 보여 주며, 태스크 실행 결과에 대한 정보를 제공하는 다양한 방법에 대해 설명합니다.

### <a name="execute-method"></a>Execute 메서드
 패키지에 포함된 태스크는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 런타임에서 해당 `Execute` 메서드를 호출하면 실행됩니다. 태스크는이 메서드에서 핵심 비즈니스 논리 및 기능을 구현 하 고, 메시지를 게시 하 고, <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 열거형에서 값을 반환 하 고, `get` `ExecutionValue` 속성의 속성을 재정의 하 여 실행 결과를 제공 합니다.

 <xref:Microsoft.SqlServer.Dts.Runtime.Task> 기본 클래스는 <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> 메서드의 기본 구현을 제공합니다. 사용자 지정 태스크에서는 이 메서드를 재정의하여 해당 태스크의 런타임 기능을 정의합니다. <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 개체는 태스크를 런타임 엔진과 패키지의 다른 개체에서 격리하여 해당 태스크를 래핑합니다. 이 격리로 인해 태스크는 실행 순서와 관련된 패키지 내에서의 태스크 위치를 알 수 없으므로 런타임에서 호출될 때만 실행됩니다. 이 아키텍처를 통해 실행 중 태스크에서 패키지를 수정할 때 발생할 수 있는 문제를 방지할 수 있습니다. 격리된 태스크에서는 <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> 메서드에 매개 변수로 지정된 개체를 통해서만 패키지의 다른 개체에 액세스할 수 있습니다. 태스크에서는 이러한 매개 변수를 통해 패키지의 안정성을 보장하는 데 필요한 격리 상태를 유지하면서 이벤트를 발생시키고, 이벤트 로그에 항목을 기록하고, 변수 컬렉션에 액세스하고, 데이터 원본에 대한 연결을 트랜잭션에 참여시킬 수 있습니다.

 다음 표에서는 <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> 메서드에서 태스크에 제공되는 매개 변수를 설명합니다.

|매개 변수|Description|
|---------------|-----------------|
|<xref:Microsoft.SqlServer.Dts.Runtime.Connections>|태스크에서 사용할 수 있는 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 개체의 컬렉션을 포함합니다.|
|<xref:Microsoft.SqlServer.Dts.Runtime.VariableDispenser>|태스크에서 사용할 수 있는 변수를 포함합니다. 태스크에서는 변수를 직접 사용하는 것이 아니라 VariableDispenser를 통해 사용합니다. VariableDispenser는 변수를 잠그거나 잠금 해제하고 교착 상태나 덮어쓰기를 방지합니다.|
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents>|태스크에서 런타임 엔진에 이벤트를 발생시키기 위해 호출하는 메서드를 포함합니다.|
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSLogging>|태스크에서 이벤트 로그에 항목을 기록하는 데 사용하는 메서드 및 속성을 포함합니다.|
|Object|해당 컨테이너가 포함된 트랜잭션 개체가 있는 경우 이를 포함합니다. 이 값은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> 개체의 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 메서드에 매개 변수로 전달됩니다.|

### <a name="providing-execution-feedback"></a>실행 피드백 제공
 태스크에서는 해당 코드를 `try/catch` 블록에 래핑하여 런타임 엔진에 예외가 발생하지 않도록 합니다. 이렇게 하면 패키지 실행이 끝까지 완료되며 예기치 않게 중지되는 경우가 없습니다. 그러나 런타임 엔진에서는 태스크 실행 중 발생할 수 있는 오류 조건을 처리하기 위한 다른 메커니즘을 제공합니다. 이러한 메커니즘에는 오류 및 경고 메시지 게시, <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 구조의 값 반환, 메시지 게시, <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 값 반환 및 <xref:Microsoft.SqlServer.Dts.Runtime.Task.ExecutionValue%2A> 속성을 통한 태스크 실행 결과에 대한 정보 공개 등이 포함됩니다.

 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> 인터페이스에는 태스크에서 런타임 엔진에 오류 및 경고 메시지를 게시하기 위해 호출할 수 있는 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A> 메서드가 포함되어 있습니다. 두 메서드에는 오류 코드, 원본 구성 요소, 설명, 도움말 파일 및 도움말 컨텍스트 정보와 같은 매개 변수가 필요합니다. 런타임에서는 태스크의 구성에 따라 이벤트 및 중단점을 발생시키거나 이벤트 로그에 정보를 기록하는 방식으로 이러한 메시지에 응답합니다.

 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>에서는 실행 결과에 대한 추가 정보를 제공하는 데 사용할 수 있는 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> 속성도 제공합니다. 예를 들어 태스크에서 `Execute` 메서드 실행 중 테이블의 행을 삭제할 경우 삭제한 행 수를 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> 속성의 값으로 반환할 수 있습니다. 또한 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>에서는 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecValueVariable%2A> 속성을 제공합니다. 이 속성을 통해 사용자는 태스크에서 반환된 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A>를 태스크에 표시되는 변수에 매핑할 수 있습니다. 그런 다음 지정한 변수를 사용하여 태스크 간에 선행 제약 조건을 설정할 수 있습니다.

### <a name="execution-example"></a>실행 예
 다음 코드 예제서는 `Execute` 메서드의 구현과 재정의된 `ExecutionValue` 속성을 보여 줍니다. 태스크에서는 해당 태스크의 `fileName` 속성으로 지정된 파일을 삭제하고, 파일이 없거나 `fileName` 속성이 빈 문자열인 경우에는 경고를 게시합니다. 또한 `Boolean` 속성에서 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> 값을 반환하여 파일이 삭제되었는지 여부를 나타냅니다.

```csharp
using System;
using Microsoft.SqlServer.Dts.Runtime;

public class SampleTask : Task
{
  private string fileName = "";
  private bool fileDeleted = false;

  public override DTSExecResult Execute(Connections cons,
     VariableDispenser vars, IDTSComponentEvents events,
     IDTSLogging log, Object txn)
  {
    try
    {
      if (this.fileName == "")
      {
        events.FireWarning(0, "SampleTask", "No file specified.", "", 0);
        this.fileDeleted = false;
      }
      else
      {
        if (System.IO.File.Exists(this.fileName))
        {
          System.IO.File.Delete(this.fileName);
          this.fileDeleted = true;
        }
        else
          this.fileDeleted = false;
      }
      return DTSExecResult.Success;
    }
    catch (System.Exception exception)
    {
      //   Capture the exception and post an error.
      events.FireError(0, "Sampletask", exception.Message, "", 0);
      return DTSExecResult.Failure;
    }
  }
  public string FileName
  {
    get { return this.fileName; }
    set { this.fileName = value; }
  }
  public override object ExecutionValue
  {
    get { return this.fileDeleted; }
  }
}
```

```vb
Imports System
Imports Microsoft.SqlServer.Dts.Runtime

Public Class SampleTask
  Inherits Task

  Private _fileName As String = ""
  Private _fileDeleted As Boolean = False

  Public Overrides Function Execute(ByVal cons As Connections, _
     ByVal vars As VariableDispenser, ByVal events As IDTSComponentEvents, _
     ByVal log As IDTSLogging, ByVal txn As Object) As DTSExecResult

    Try
      If Me._fileName = "" Then
        events.FireWarning(0, "SampleTask", "No file specified.", "", 0)
        Me._fileDeleted = False
      Else
        If System.IO.File.Exists(Me._fileName) Then
          System.IO.File.Delete(Me._fileName)
          Me._fileDeleted = True
        Else
          Me._fileDeleted = False
        End If
      End If
      Return DTSExecResult.Success
    Catch exception As System.Exception
      '   Capture the exception and post an error.
      events.FireError(0, "Sampletask", exception.Message, "", 0)
      Return DTSExecResult.Failure
    End Try

  End Function

  Public Property FileName() As String
    Get
      Return Me._fileName
    End Get
    Set(ByVal Value As String)
      Me._fileName = Value
    End Set
  End Property

  Public Overrides ReadOnly Property ExecutionValue() As Object
    Get
      Return Me._fileDeleted
    End Get
  End Property

End Class
```

![Integration Services 아이콘 (작은 아이콘)](../../media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하십시오.

## <a name="see-also"></a>참고 항목
 사용자 지정 [작업 만들기](creating-a-custom-task.md) 사용자 지정 태스크 [코딩](coding-a-custom-task.md) 사용자 지정 태스크 [에 대 한 사용자 인터페이스 개발](developing-a-user-interface-for-a-custom-task.md)


