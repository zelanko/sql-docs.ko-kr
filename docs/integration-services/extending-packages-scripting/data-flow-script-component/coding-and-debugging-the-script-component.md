---
title: 스크립트 구성 요소 코딩 및 디버깅 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: extending-packages-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, development environment
- Script component [Integration Services], debugging
- Script component [Integration Services], coding
- SSIS Script component, debugging
- Script component [Integration Services], development environment
- debugging [Integration Services], scripts
- SSIS Script component, coding
- VSTA
ms.assetid: c3913c15-66aa-4b61-89b5-68488fa5f0a4
caps.latest.revision: 66
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fdd0dd3f27fe66b6945f4b7855a9378b7b96f096
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="coding-and-debugging-the-script-component"></a>스크립트 구성 요소 코딩 및 디버깅
  [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 스크립트 구성 요소에는 메타데이터 디자인 모드와 코드 디자인 모드의 두 가지 모드가 있습니다. **스크립트 변환 편집기**를 열면 구성 요소가 메타데이터 디자인 모드로 전환됩니다. 여기서는 메타데이터를 구성하고 구성 요소 속성을 설정할 수 있습니다. 메타데이터 디자인 모드에서 스크립트 구성 요소 속성을 설정하고 입/출력을 구성한 후에는 코드 디자인 모드로 전환하여 사용자 지정 스크립트를 작성할 수 있습니다. 메타데이터 디자인 모드 및 코드 디자인 모드에 대한 자세한 내용은 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)을 참조하세요.  
  
## <a name="writing-the-script-in-code-design-mode"></a>코드 디자인 모드에서 스크립트 작성  
  
### <a name="script-component-development-environment"></a>스크립트 구성 요소 개발 환경  
 스크립트를 작성하려면 **스크립트 변환 편집기**의 **스크립트** 페이지에서 **스크립트 편집**을 클릭하여 VSTA([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications) IDE를 엽니다. VSTA IDE에는 색 구분 기능이 포함된 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 편집기, IntelliSense, 개체 브라우저 등 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] .NET 환경의 모든 표준 기능이 포함됩니다.  
  
 스크립트 코드는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#으로 작성됩니다. **스크립트 변환 편집기**에서 **ScriptLanguage** 속성을 설정하여 스크립트 언어를 지정합니다. 다른 프로그래밍 언어를 사용하고 싶으면 원하는 언어로 사용자 지정 어셈블리를 개발하고 스크립트 구성 요소의 코드에서 해당 기능을 호출할 수 있습니다.  
  
 스크립트 구성 요소에서 작성하는 스크립트는 패키지 정의에 저장됩니다. 별도의 스크립트 파일은 없습니다. 따라서 스크립트 구성 요소를 사용해도 패키지 배포에 영향을 주지 않습니다.  
  
> [!NOTE]  
>  패키지를 디자인하는 동안 스크립트 코드는 임시로 프로젝트 파일에 기록됩니다. 중요한 정보를 파일에 저장하면 보안상 위험할 수 있으므로 암호와 같은 중요한 정보는 스크립트 코드에 포함하지 않는 것이 좋습니다.  
  
 기본적으로 **Option Strict**는 IDE에서 비활성화되어 있습니다.  
  
### <a name="script-component-project-structure"></a>스크립트 구성 요소 프로젝트 구조  
 스크립트 구성 요소의 장점은, 개발자가 작성해야 할 코드 분량을 줄여주는 인프라 코드를 생성할 수 있다는 것입니다. 이 기능은 입/출력 및 해당 열과 속성이 고정되어 있고 미리 알려져 있다는 사실을 기반으로 합니다. 따라서 그 이후에 구성 요소의 메타데이터 내용을 변경하면 작성한 코드가 무효화될 수 있습니다. 그러면 패키지 실행 중 컴파일 오류가 발생합니다.  
  
#### <a name="project-items-and-classes-in-the-script-component-project"></a>스크립트 구성 요소 프로젝트의 프로젝트 항목 및 클래스  
 코드 디자인 모드로 전환하면 VSTA IDE에서 **ScriptMain** 프로젝트 항목을 열어 표시합니다. **ScriptMain** 프로젝트 항목에는 편집 가능한 **ScriptMain** 클래스가 포함되어 있습니다. 이 클래스는 스크립트의 진입점 역할을 하며 코드를 작성하는 위치입니다. 클래스의 코드 요소는 스크립트 태스크용으로 선택한 프로그래밍 언어에 따라 다릅니다.  
  
 스크립트 프로젝트는 다음과 같은 두 가지 추가 자동 생성 읽기 전용 프로젝트 항목을 포함합니다.  
  
-   **ComponentWrapper** 프로젝트 항목은 다음 세 클래스를 포함합니다.  
  
    -   **UserComponent** 클래스 - <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>에서 상속되며, 데이터를 처리하고 패키지와 상호 작용하는 데 사용할 메서드와 속성을 포함합니다. **ScriptMain** 클래스는 **UserComponent** 클래스에서 상속됩니다.  
  
    -   **Connections** 컬렉션 클래스 - 스크립트 변환 편집기의 연결 관리자 페이지에서 선택한 연결에 대한 참조를 포함합니다.  
  
    -   **Variables** 컬렉션 클래스 - **스크립트 변환 편집기**의 **스크립트** 페이지에서 **ReadOnlyVariable** 및 **ReadWriteVariables** 속성에 입력한 변수에 대한 참조를 포함합니다.  
  
-   **BufferWrapper** 프로젝트 항목은 **스크립트 변환 편집기**의 **입/출력** 페이지에서 구성한 각 입력 및 출력에 대해 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>에서 상속된 클래스를 포함합니다. 각 클래스는 구성된 입/출력 열과 그 열이 포함된 데이터 흐름 버퍼에 해당하는 형식화된 접근자 속성을 포함합니다.  
  
 이러한 개체, 메서드 및 속성을 사용하는 방법에 대한 자세한 내용은 [스크립트 구성 요소 개체 모델 이해](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)를 참조하세요. 특정 유형의 스크립트 구성 요소에서 이러한 클래스의 메서드와 속성을 사용하는 방법에 대한 자세한 내용은 [추가 스크립트 구성 요소 예제](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md) 섹션을 참조하세요. 예 항목에는 전체 코드 예제도 들어 있습니다.  
  
 스크립트 구성 요소를 변환으로 구성하면 **ScriptMain** 프로젝트 항목에 다음과 같은 자동 생성 코드가 포함됩니다. 코드 템플릿은 또한 스크립트 구성 요소에 대한 개요와 SSIS 개체(예: 변수, 이벤트 및 연결)를 검색 및 조작하는 방법에 대한 추가 정보를 제공합니다.  
  
```vb  
' Microsoft SQL Server Integration Services Script Component  
' Write scripts using Microsoft Visual Basic 2008.  
' ScriptMain is the entry point class of the script.  
  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
  
<Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute> _  
<CLSCompliant(False)> _  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub PreExecute()  
        MyBase.PreExecute()  
        '  
        ' Add your code here for preprocessing or remove if not needed  
        '  
    End Sub  
  
    Public Overrides Sub PostExecute()  
        MyBase.PostExecute()  
        '  
        ' Add your code here for postprocessing or remove if not needed  
        ' You can set read/write variables here, for example:  
        ' Me.Variables.MyIntVar = 100  
        '  
    End Sub  
  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
        '  
        ' Add your code here  
        '  
    End Sub  
  
End Class  
```  
  
```csharp  
/* Microsoft SQL Server Integration Services user script component  
*  Write scripts using Microsoft Visual C# 2008.  
*  ScriptMain is the entry point class of the script.*/  
  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
[Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute]  
public class ScriptMain : UserComponent  
{  
  
    public override void PreExecute()  
    {  
        base.PreExecute();  
        /*  
          Add your code here for preprocessing or remove if not needed  
        */  
    }  
  
    public override void PostExecute()  
    {  
        base.PostExecute();  
        /*  
          Add your code here for postprocessing or remove if not needed  
          You can set read/write variables here, for example:  
          Variables.MyIntVar = 100  
        */  
    }  
  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
        /*  
          Add your code here  
        */  
    }  
  
}  
```  
  
#### <a name="additional-project-items-in-the-script-component-project"></a>스크립트 구성 요소 프로젝트의 추가 프로젝트 항목  
 스크립트 구성 요소 프로젝트에는 기본 **ScriptMain** 항목 이외의 다른 항목이 포함될 수 있습니다. 클래스, 모듈, 코드 파일 및 폴더를 프로젝트에 추가할 수 있고, 항목 그룹을 구성하기 위해 폴더를 사용할 수 있습니다.  
  
 추가하는 모든 항목은 패키지 내부에 지속됩니다.  
  
#### <a name="references-in-the-script-component-project"></a>스크립트 구성 요소 프로젝트의 참조  
 **프로젝트 탐색기**에서 스크립트 태스크 프로젝트를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 클릭하여 관리되는 어셈블리에 대한 참조를 추가할 수 있습니다. 자세한 내용은 [스크립팅 솔루션에서 다른 어셈블리 참조](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)를 참조하세요.  
  
> [!NOTE]  
>  프로젝트 참조는 VSTA IDE의 **클래스 뷰** 또는 **프로젝트 탐색기**에서 볼 수 있습니다. **보기** 메뉴에서 이러한 창 중 하나를 엽니다. **프로젝트** 메뉴, **프로젝트 탐색기** 또는 **클래스 뷰**에서 새 참조를 추가할 수 있습니다.  
  
## <a name="interacting-with-the-package-in-the-script-component"></a>스크립트 구성 요소에서 패키지와 상호 작용  
 스크립트 구성 요소에서 작성하는 사용자 지정 스크립트는 자동 생성된 기본 클래스의 강력한 형식의 접근자를 통해 포함하는 패키지에서 변수 및 연결 관리자를 액세스하고 사용할 수 있습니다. 그러나 변수 및 연결 관리자를 스크립트에서 사용할 수 있게 만들려면 코드 디자인 모드로 들어가기 전에 이들을 구성해야 합니다. 또한 스크립트 구성 요소 코드에서 이벤트를 발생시키고 로깅을 수행할 수 있습니다.  
  
 스크립트 구성 요소 프로젝트의 자동 생성된 프로젝트 항목은 다음과 같은 개체, 메서드 및 속성을 사용하여 패키지와 상호 작용합니다.  
  
|패키지 기능|액세스 방법|  
|---------------------|-------------------|  
|변수|**ScriptMain** 클래스의 **Variables** 속성을 통해 노출되는 **ComponentWrapper** 프로젝트 항목의 **Variables** 컬렉션 클래스에서 명명되고 형식화된 접근자 속성을 사용합니다.<br /><br /> **PreExecute** 메서드는 읽기 전용 변수만 액세스할 수 있습니다. **PostExecute** 메서드는 읽기 전용 변수 및 읽기/쓰기 변수 모두에 액세스할 수 있습니다.|  
|Connections|**ScriptMain** 클래스의 **Connections** 속성을 통해 노출되는 **ComponentWrapper** 프로젝트 항목의 **Connections** 컬렉션 클래스에서 명명되고 형식화된 접근자 속성을 사용합니다.|  
|이벤트|**ScriptMain** 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 속성과 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 인터페이스의 **Fire\<X>** 메서드를 사용하여 이벤트를 발생시킵니다.|  
|로깅|**ScriptMain** 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 메서드를 사용하여 로깅을 수행합니다.|  
  
## <a name="debugging-the-script-component"></a>스크립트 구성 요소 디버깅  
 스크립트 구성 요소의 코드를 디버깅하려면 코드에 하나 이상의 중단점을 설정한 다음 VSTA IDE를 닫고 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 패키지를 실행합니다. 패키지 실행 중 스크립트 구성 요소 실행이 시작되면 VSTA IDE가 다시 열리고 코드가 읽기 전용 모드에서 열립니다. 중단점에 도달한 후에는 변수 값을 검사하고 나머지 코드를 단계별로 실행할 수 있습니다.  
  
> [!NOTE]  
>  스크립트 구성 요소를 패키지 실행 태스크에서 실행된 자식 패키지의 일부로 실행할 경우에는 스크립트 구성 요소를 디버깅할 수 없습니다. 이러한 경우에는 자식 패키지에서 스크립트 구성 요소에 설정한 중단점이 무시됩니다. 자식 패키지는 별도로 실행하여 정상적으로 디버깅할 수 있습니다.  
  
> [!NOTE]  
>  여러 스크립트 구성 요소가 포함되어 있는 패키지를 디버깅하는 경우 디버거는 한 개의 스크립트 구성 요소를 디버깅합니다. Foreach 루프 또는 For 루프 컨테이너의 경우와 같이 디버거가 완료되는 경우 시스템에서 다른 스크립트 구성 요소를 디버깅할 수 있습니다.  
  
 다음 방법을 사용하여 스크립트 구성 요소의 실행을 모니터링할 수도 있습니다.  
  
-   **System.Windows.Forms** 네임스페이스의 **MessageBox.Show** 메서드를 사용하여 실행을 중단하고 모달 메시지를 표시합니다. (이 코드는 디버깅 프로세스를 완료한 후 제거하십시오.)  
  
-   정보 메시지, 경고 및 오류에 대한 이벤트를 발생시킵니다. FireInformation, FireWarning 및 FireError 메서드는 Visual Studio **출력** 창에 이벤트 설명을 표시합니다. 그러나 FireProgress 메서드, Console.Write 메서드 및 Console.WriteLine 메서드는 **출력** 창에 어떠한 정보도 표시하지 않습니다. FireProgress 이벤트의 메시지는 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너의 **진행률** 탭에 표시됩니다. 자세한 내용은 [스크립트 구성 요소에서 이벤트 발생](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md)을 참조하세요.  
  
-   이벤트 또는 사용자 정의 메시지를 활성화된 로깅 공급자에 기록합니다. 자세한 내용은 [스크립트 구성 요소의 로깅](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md)을 참조하세요.  
  
 데이터를 대상에 저장하지 않고 원본 또는 변형으로 구성된 스크립트 구성 요소의 출력을 검사하려는 경우, [행 개수 변환](../../../integration-services/data-flow/transformations/row-count-transformation.md)을 사용하여 데이터 흐름을 중지하고 데이터 뷰어를 스크립트 구성 요소의 출력에 연결할 수 있습니다. 데이터 뷰어에 대한 자세한 내용은 [데이터 흐름 디버깅](../../../integration-services/troubleshooting/debugging-data-flow.md)을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 스크립트 구성 요소 코딩에 대한 자세한 내용은 이 섹션의 다음 항목을 참조하십시오.  
  
 [스크립트 구성 요소 개체 모델 이해](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 스크립트 구성 요소에 제공되는 개체, 메서드 및 속성을 사용하는 방법을 설명합니다.  
  
 [스크립팅 솔루션에서 다른 어셈블리 참조](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)  
 스크립트 구성 요소의 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 클래스 라이브러리에서 개체를 참조하는 방법을 설명합니다.  
  
 [스크립트 구성 요소의 오류 출력 시뮬레이션](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)  
 스크립트 구성 요소에서 처리 중 오류가 발생하는 행의 오류 출력을 시뮬레이션하는 방법을 설명합니다.  
  
## <a name="external-resources"></a>외부 리소스  
  
-   blogs.msdn.com의 블로그 항목 - [SSIS 2008 및 R2 설치의 VSTA 설치 및 구성 문제](http://go.microsoft.com/fwlink/?LinkId=215661)  
  
## <a name="see-also"></a>참고 항목  
 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
  
  
