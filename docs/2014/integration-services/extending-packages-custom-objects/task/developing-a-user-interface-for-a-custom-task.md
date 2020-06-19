---
title: 사용자 지정 태스크의 사용자 인터페이스 개발 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom user interfaces [Integration Services]
- IDtsTaskUI interface
- DtsTaskAttribute attribute
- custom tasks [Integration Services], user interface
- custom user interface [Integration Services], custom tasks
- user interface [Integration Services]
- SSIS custom tasks, user interface
ms.assetid: 1e940cd1-c5f8-4527-b678-e89ba5dc398a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4e4246898e5b054af8cbbdc86aff41cb7ea087e2
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968643"
---
# <a name="developing-a-user-interface-for-a-custom-task"></a>사용자 지정 태스크의 사용자 인터페이스 개발
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 개체 모델을 사용하면 사용자 지정 태스크 개발자가 태스크의 사용자 지정 사용자 인터페이스를 쉽게 만들 수 있으며 이러한 태스크는 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에 통합 및 표시될 수 있습니다. 사용자 인터페이스는 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 사용자에게 유용한 정보를 제공하고 사용자 지정 태스크의 속성 및 설정을 올바르게 구성할 수 있도록 안내해 줍니다.  
  
 태스크의 사용자 지정 사용자 인터페이스를 개발할 때는 두 개의 중요한 클래스를 사용합니다. 다음 표에서는 이러한 클래스에 대해 설명합니다.  
  
|클래스|Description|  
|-----------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>|관리되는 태스크를 식별하고, [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 개체를 표시하고 개체와 상호 작용하는 방식을 제어하기 위해 해당 속성을 통해 디자인 타임 정보를 제공하는 특성입니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>|태스크에서 해당 태스크를 사용자 지정 사용자 인터페이스와 연결하는 데 사용되는 인터페이스입니다.|  
  
 이 섹션에서는 사용자 지정 태스크의 사용자 인터페이스를 개발할 때 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 특성 및 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI> 인터페이스가 하는 역할을 설명하고, [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너 내에서 태스크를 만들고, 통합, 배포 및 디버깅하는 방법에 대한 세부 정보를 제공합니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서는 태스크의 사용자 인터페이스에 대한 여러 진입점을 제공합니다. 즉, 사용자는 바로 가기 메뉴에서 **편집**을 선택하거나, 태스크를 두 번 클릭하거나, 속성 시트의 아래쪽에 있는 **편집기 표시** 링크를 클릭할 수 있습니다. 사용자가 이러한 진입점 중 하나에 액세스하면 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서는 태스크의 사용자 인터페이스가 들어 있는 어셈블리를 찾아서 로드합니다. 태스크의 사용자 인터페이스는 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 사용자에게 표시되는 속성 대화 상자를 만듭니다.  
  
 태스크와 태스크의 해당 사용자 인터페이스는 별개의 엔터티입니다. 따라서 지역화, 배포 및 유지 관리 작업을 줄이려면 태스크와 태스크의 사용자 인터페이스를 별개의 어셈블리에 구현해야 합니다. 태스크 DLL은 태스크에 코딩된 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 특성 값에 들어 있는 정보를 제외하고는 사용자 인터페이스에 대한 어떤 정보도 로드하거나 호출하지 않으며 일반적으로 이러한 정보를 포함하지도 않습니다. 태스크와 사용자 인터페이스는 이러한 방식으로만 연결됩니다.  
  
## <a name="the-dtstask-attribute"></a>DtsTask 특성  
 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 특성은 태스크 클래스 코드에 포함되어 태스크와 해당 사용자 인터페이스를 연결합니다. [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서는 이 특성의 속성을 사용하여 디자이너에 태스크를 표시하는 방법을 결정합니다. 이러한 속성에는 표시할 이름과 해당되는 경우 아이콘이 포함되어 있습니다.  
  
 다음 표에서는 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 특성의 속성에 대해 설명합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.DisplayName%2A>|제어 흐름 도구 상자에 태스크 이름을 표시합니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.Description%2A>|<xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute>에서 상속된 태스크 설명입니다. 이 속성은 도구 설명에 표시됩니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.IconResource%2A>|[!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에 표시되는 아이콘입니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.RequiredProductLevel%2A>|사용되는 경우 이 속성은 <xref:Microsoft.SqlServer.Dts.Runtime.DTSProductLevel> 열거형의 값 중 하나로 설정합니다. `RequiredProductLevel = DTSProductLevel.None`)을 입력합니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.TaskContact%2A>|태스크에 기술 지원이 필요한 경우를 위해 연락처 정보를 포함합니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.TaskType%2A>|태스크에 유형을 할당합니다.|  
|Attribute.TypeId|파생 클래스에서 구현된 경우 이 특성에 대한 고유 식별자를 가져옵니다. 자세한 내용은 .NET Framework 클래스 라이브러리의 `Attribute.TypeID` 속성을 참조하십시오.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.UITypeName%2A>|[!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 어셈블리를 로드하는 데 사용되는 어셈블리 유형 이름입니다. 이 속성은 태스크의 사용자 인터페이스 어셈블리를 찾는 데 사용됩니다.|  
  
 다음 코드 예에서는 클래스 정의 위에 코딩된 경우의 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>를 보여 줍니다.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
namespace Microsoft.SSIS.Samples  
{  
  [DtsTask  
  (  
   DisplayName = "MyTask",  
   IconResource = "MyTask.MyTaskIcon.ico",  
   UITypeName = "My Custom Task," +  
   "Version=1.0.0.0," +  
   "Culture = Neutral," +  
   "PublicKeyToken = 12345abc6789de01",  
   TaskType = "PackageMaintenance",  
   TaskContact = "MyTask; company name; any other information",  
   RequiredProductLevel = DTSProductLevel.None  
   )]  
  public class MyTask : Task  
  {  
    // Your code here.  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsTask(DisplayName:="MyTask", _  
 IconResource:="MyTask.MyTaskIcon.ico", _  
 UITypeName:="My Custom Task," & _  
 "Version=1.0.0.0,Culture=Neutral," & _  
 "PublicKeyToken=12345abc6789de01", _  
 TaskType:="PackageMaintenance", _  
 TaskContact:="MyTask; company name; any other information", _  
 RequiredProductLevel:=DTSProductLevel.None)> _  
Public Class MyTask  
  Inherits Task  
  
  ' Your code here.  
  
End Class 'MyTask  
```  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서는 어셈블리 이름, 유형 이름, 버전, culture 및 공개 키 토큰이 들어 있는 특성의 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.UITypeName%2A> 속성을 사용하여 GAC(전역 어셈블리 캐시)에서 어셈블리를 찾고, 디자이너에서 사용할 수 있도록 해당 어셈블리를 로드합니다.  
  
 어셈블리를 찾은 후 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서는 특성의 다른 속성을 사용하여 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에 태스크의 이름, 아이콘 및 설명과 같은 추가 정보를 표시합니다.  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.DisplayName%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.Localization.DtsLocalizableAttribute.Description%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.IconResource%2A> 속성은 태스크가 사용자에게 표시되는 방식을 지정합니다. <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute.IconResource%2A> 속성에는 사용자 인터페이스 어셈블리에 포함된 아이콘의 리소스 ID가 들어 있습니다. 디자이너에서는 어셈블리에서 ID를 기준으로 아이콘 리소스를 로드하고, 태스크가 패키지에 추가될 때 도구 상자와 디자이너 화면의 태스크 이름 옆에 해당 아이콘을 표시합니다. 태스크에서 아이콘 리소스를 제공하지 않는 경우에는 태스크의 기본 아이콘을 사용합니다.  
  
## <a name="the-idtstaskui-interface"></a>IDTSTaskUI 인터페이스  
 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI> 인터페이스는 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 태스크와 연결된 사용자 인터페이스를 초기화하고 표시하기 위해 호출하는 메서드 및 속성의 컬렉션을 정의합니다. 태스크의 사용자 인터페이스가 호출되면 디자이너에서는 태스크 사용자 인터페이스를 작성할 때 해당 사용자 인터페이스에 의해 구현된 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.Initialize%2A> 메서드를 호출한 다음 태스크와 패키지의 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 및 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 컬렉션을 각각 매개 변수로 제공합니다. 이러한 컬렉션은 로컬로 저장되었다가 나중에 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.GetView%2A> 메서드에서 사용됩니다.  
  
 디자이너에서는 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.GetView%2A> 메서드를 호출하여 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에 표시되는 창을 요청합니다. 태스크에서는 해당 태스크의 사용자 인터페이스가 들어 있는 창의 인스턴스를 만들고 표시를 위해 해당 사용자 인터페이스를 디자이너에 반환합니다. 일반적으로 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 및 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 개체는 오버로드된 생성자를 통해 창에 제공되므로 이들 개체를 사용하여 태스크를 구성할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서는 태스크 UI의 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI.GetView%2A> 메서드를 호출하여 태스크의 사용자 인터페이스를 표시합니다. 태스크 사용자 인터페이스는 이 메서드에서 Windows Form을 반환하고 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서는 이 폼을 모달 대화 상자로 표시합니다. 폼이 닫히면 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서는 폼의 `DialogResult` 속성 값을 검사하여 태스크가 수정되었는지와 수정 내용을 저장해야 하는지를 결정합니다. `DialogResult` 속성 값이 `OK`인 경우 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서는 태스크의 지속성 메서드를 호출하여 변경 내용을 저장하고, 그렇지 않은 경우 변경 내용은 무시됩니다.  
  
 다음 코드 예제에서는 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI> 인터페이스를 구현하며 SampleTaskForm이라는 Windows Form 클래스가 있다고 가정합니다.  
  
```csharp  
using System;  
using System.Windows.Forms;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Runtime.Design;  
  
namespace Sample  
{  
   public class HelloWorldTaskUI : IDtsTaskUI  
   {  
      TaskHost   taskHost;  
      Connections connections;  
      public void Initialize(TaskHost taskHost, IServiceProvider serviceProvider)  
      {  
         this.taskHost = taskHost;  
         IDtsConnectionService cs = serviceProvider.GetService  
         ( typeof( IDtsConnectionService ) ) as   IDtsConnectionService;   
         this.connections = cs.GetConnections();  
      }  
      public ContainerControl GetView()  
      {  
        return new HelloWorldTaskForm(this.taskHost, this.connections);  
      }  
     public void Delete(IWin32Window parentWindow)  
     {  
     }  
     public void New(IWin32Window parentWindow)  
     {  
     }  
   }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Runtime.Design  
Imports System.Windows.Forms  
  
Public Class HelloWorldTaskUI  
  Implements IDtsTaskUI  
  
  Dim taskHost As TaskHost  
  Dim connections As Connections  
  
  Public Sub Initialize(ByVal taskHost As TaskHost, ByVal serviceProvider As IServiceProvider) _  
    Implements IDtsTaskUI.Initialize  
  
    Dim cs As IDtsConnectionService  
  
    Me.taskHost = taskHost  
    cs = DirectCast(serviceProvider.GetService(GetType(IDtsConnectionService)), IDtsConnectionService)  
    Me.connections = cs.GetConnections()  
  
  End Sub  
  
  Public Function GetView() As ContainerControl _  
    Implements IDtsTaskUI.GetView  
  
    Return New HelloWorldTaskForm(Me.taskHost, Me.connections)  
  
  End Function  
  
  Public Sub Delete(ByVal parentWindow As IWin32Window) _  
    Implements IDtsTaskUI.Delete  
  
  End Sub  
  
  Public Sub [New](ByVal parentWindow As IWin32Window) _  
    Implements IDtsTaskUI.[New]  
  
  End Sub  
  
End Class  
```  
  
![Integration Services 아이콘 (작은 아이콘)](../../media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지를 방문하세요.](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>참고 항목  
 [사용자 지정 태스크 만들기](creating-a-custom-task.md)   
 [사용자 지정 태스크 코딩](coding-a-custom-task.md)   
 [사용자 지정 태스크의 사용자 인터페이스 개발](developing-a-user-interface-for-a-custom-task.md)  
  
  
