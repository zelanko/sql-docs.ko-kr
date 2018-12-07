---
title: 스크립트 태스크와 스크립트 구성 요소 비교 | Microsoft Docs
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
- Script task [Integration Services], comparing to Script component
- Script component [Integration Services], comparing to Script task
ms.assetid: 4b73753a-4239-491b-b7a6-abc63ba83d2d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c58385a1e38c19ed25785cd2da472544af3be171
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52407770"
---
# <a name="comparing-the-script-task-and-the-script-component"></a>스크립트 태스크와 스크립트 구성 요소 비교
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 디자이너의 제어 흐름 창에서 사용할 수 있는 스크립트 태스크와 데이터 흐름 창에서 사용할 수 있는 스크립트 구성 요소는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 서로 매우 다른 용도로 사용됩니다. 태스크는 일반적인 용도의 제어 흐름 도구인 반면 구성 요소는 데이터 흐름에서 원본, 변환 또는 대상으로 사용됩니다. 이러한 차이에도 불구하고 스크립트 태스크와 스크립트 구성 요소는 사용하는 코딩 도구와 개발자가 사용할 수 있는 패키지의 개체에서 약간의 유사성이 있습니다. 이러한 유사점과 차이점을 이해하면 태스크와 구성 요소 모두를 보다 효율적으로 사용할 수 있습니다.  
  
## <a name="similarities-between-the-script-task-and-the-script-component"></a>스크립트 태스크와 스크립트 구성 요소의 유사점  
 스크립트 태스크와 스크립트 구성 요소는 모두 다음과 같은 일반적인 기능이 있습니다.  
  
|기능|설명|  
|-------------|-----------------|  
|두 개의 디자인 타임 모드|태스크에서든 구성 요소에서든 코드를 작성하려면 먼저 편집기에서 속성을 지정한 다음 개발 환경으로 전환합니다.|  
|VSTA([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications)|태스크와 구성 요소는 모두 동일한 VSTA IDE를 사용하며 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#에서 작성된 코드를 지원합니다.|  
|미리 컴파일된 스크립트|[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 이상에서는 모든 스크립트가 미리 컴파일되어 있습니다. 이전 버전에서는 스크립트가 미리 컴파일되었는지를 지정할 수 있었습니다.<br /><br /> 스크립트는 보다 빠르게 실행될 수 있도록 이진 코드로 미리 컴파일되지만 이 경우 패키지 크기는 늘어납니다.|  
|디버깅|태스크 및 구성 요소 모두 디자인 환경에서 디버깅하는 동안 중단점과 단계별 코드 실행을 지원합니다. 자세한 내용은은 [스크립트 태스크 코딩 및 디버깅](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md) 및 [스크립트 구성 요소 코딩 및 디버깅](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)을 참조하십시오.|  
  
## <a name="differences-between-the-script-task-and-the-script-component"></a>스크립트 태스크와 스크립트 구성 요소의 차이점  
 스크립트 태스크와 스크립트 구성 요소는 다음과 같은 중요한 차이점이 있습니다.  
  
|기능|스크립트 태스크|스크립트 구성 요소|  
|-------------|-----------------|----------------------|  
|제어 흐름/데이터 흐름|스크립트 태스크는 디자이너의 제어 흐름 탭에서 구성되며 패키지의 데이터 흐름 외부에서 실행됩니다.|스크립트 구성 요소는 디자이너의 데이터 흐름 페이지에서 구성되며 데이터 흐름 태스크의 원본, 변환 또는 대상을 나타냅니다.|  
|용도|스크립트 태스크에서는 일반적인 용도의 거의 모든 태스크를 수행할 수 있습니다.|스크립트 구성 요소를 사용하여 원본, 변환 또는 대상 중 무엇을 만들지를 지정해야 합니다.|  
|실행|스크립트 태스크에서는 패키지 워크플로의 일부 지점에서 사용자 지정 코드를 실행합니다. 사용자 지정 코드를 루프 컨테이너나 이벤트 처리기에 추가하지 않은 경우 해당 코드는 한 번만 실행됩니다.|스크립트 구성 요소도 한 번만 실행되지만 일반적으로 스크립트 구성 요소에서는 주 처리 루틴을 데이터 흐름의 각 데이터 행에 대해 한 번씩 실행합니다.|  
|편집기|**스크립트 태스크 편집기**에는 **일반**, **스크립트** 및 **식**이라는 3개 페이지가 있습니다. **ReadOnlyVariables**과 **ReadWriteVariables** 및 **ScriptLanguage** 속성만 사용자가 작성하는 코드에 직접적인 영향을 미칩니다.|**스크립트 변환 편집기**에는 **입력 열**, **입/출력**, **스크립트** 및 **연결 관리자** 등 최대 4개 페이지가 있습니다. 이러한 각 페이지에서 구성하는 메타데이터 및 속성은 코딩에 사용할 수 있도록 자동으로 생성되는 기본 클래스의 멤버를 결정합니다.|  
|패키지와의 상호 작용|스크립트 태스크용으로 작성된 코드에서는 **Dts** 속성을 사용하여 패키지의 다른 기능에 액세스합니다. **Dts** 속성은 **ScriptMain** 클래스의 구성원입니다.|스크립트 구성 요소 코드에서는 형식화된 접근자 속성을 사용하여 변수 및 연결 관리자와 같은 일부 패키지 기능에 액세스합니다.<br /><br /> **PreExecute** 메서드는 읽기 전용 변수만 액세스할 수 있습니다. **PostExecute** 메서드는 읽기 전용 변수 및 읽기/쓰기 변수 모두에 액세스할 수 있습니다.<br /><br /> 이러한 메서드에 대한 자세한 내용은 [스크립트 구성 요소 코딩 및 디버깅](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)을 참조하세요.|  
|변수 사용|스크립트 태스크에서는 **Dts** 개체의 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 속성을 사용하여 태스크의 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A> 및 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A> 속성을 통해 사용할 수 있는 변수에 액세스합니다. 예를 들어 다음과 같이 사용할 수 있습니다.<br /><br /> [Visual Basic]<br /><br /> `Dim myVar as String` <br /> `myVar = Dts.Variables("MyStringVariable").Value.ToString`<br /><br /> [C#]<br /><br /> `string myVar;` <br /> `myVar = Dts.Variables["MyStringVariable"].Value.ToString();`|스크립트 구성 요소에서는 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> 속성에서 만들어진 자동 생성 기본 클래스의 형식화된 접근자 속성을 사용합니다. 예를 들어 다음과 같이 사용할 수 있습니다.<br /><br /> [Visual Basic]<br /><br /> `Dim myVar as String` <br /> `myVar = Me.Variables.MyStringVariable`<br /><br /> [C#]<br /><br /> `string myVar;` <br /> `myVar = this.Variables.MyStringVariable;`|  
|연결 사용|스크립트 태스크에서는 **Dts** 개체의 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> 속성을 사용하여 패키지에 정의된 연결 관리자에 액세스합니다. 예를 들어 다음과 같이 사용할 수 있습니다.<br /><br /> [Visual Basic]<br /><br /> `Dim myFlatFileConnection As String` <br /> `myFlatFileConnection = _     DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _     String)`<br /><br /> [C#]<br /><br /> `string myFlatFileConnection;` <br /> `myFlatFileConnection = (Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);`|스크립트 구성 요소에서는 사용자가 편집기의 연결 관리자 페이지에서 입력한 연결 관리자 목록에서 만들어진 자동 생성 기본 클래스의 형식화된 접근자 속성을 사용합니다. 예를 들어 다음과 같이 사용할 수 있습니다.<br /><br /> [Visual Basic]<br /><br /> `Dim connMgr As IDTSConnectionManager100` <br /> `connMgr = Me.Connections.MyADONETConnection`<br /><br /> [C#]<br /><br /> `IDTSConnectionManager100 connMgr;` <br /> `connMgr = this.Connections.MyADONETConnection;`|  
|이벤트 발생|스크립트 태스크에서는 **Dts** 개체의 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> 속성을 사용하여 이벤트를 발생시킵니다. 예를 들어 다음과 같이 사용할 수 있습니다.<br /><br /> [Visual Basic]<br /><br /> `Dts.Events.FireError(0, "Event Snippet", _     ex.Message & ControlChars.CrLf & ex.StackTrace, _     "", 0)`<br /><br /> [C#]<br /><br /> `Dts.Events.FireError(0, "Event Snippet", ex.Message + "\r" + ex.StackTrace, "", 0);`|스크립트 구성 요소에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 속성에서 반환된 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 인터페이스의 메서드를 사용하여 오류, 경고 및 정보 메시지를 발생시킵니다. 예를 들어 다음과 같이 사용할 수 있습니다.<br /><br /> [Visual Basic]<br /><br /> `Dim myMetadata as IDTSComponentMetaData100 myMetaData = Me.ComponentMetaData myMetaData.FireError(...)`|  
|로깅|스크립트 태스크에서는 **Dts** 개체의 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 메서드를 사용하여 설정된 로그 공급자에 정보를 로깅합니다. 예를 들어 다음과 같이 사용할 수 있습니다.<br /><br /> [Visual Basic]<br /><br /> `Dim bt(0) As Byte Dts.Log("Test Log Event", _     0, _     bt)`<br /><br /> [C#]<br /><br /> `byte[] bt = new byte[0];` <br /> `Dts.Log("Test Log Event", 0, bt);`|스크립트 구성 요소에서는 자동으로 생성된 기본 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 메서드를 사용하여 설정된 로그 공급자에 정보를 로깅합니다. 예를 들어 다음과 같이 사용할 수 있습니다.<br /><br /> [Visual Basic]<br /><br /> `Dim bt(0) As Byte`<br /><br /> `Me.Log("Test Log Event", _`<br /><br /> `0, _`<br /><br /> `bt)`<br /><br /> [C#]<br /><br /> `byte[] bt = new byte[0]; this.Log("Test Log Event", 0, bt);`|  
|결과 반환|스크립트 태스크에서는 **Dts** 개체의 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> 속성과 선택적 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> 속성을 모두 사용하여 런타임에 결과를 알려 줍니다.|스크립트 구성 요소는 데이터 흐름 태스크의 일부로 실행되며 이러한 속성 중 하나를 사용하여 결과를 보고하지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [스크립트 태스크를 사용하여 패키지 확장](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [스크립트 구성 요소를 사용하여 데이터 흐름 확장](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)   
  
  
