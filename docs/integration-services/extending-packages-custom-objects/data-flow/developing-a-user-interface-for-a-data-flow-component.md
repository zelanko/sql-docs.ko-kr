---
title: "데이터 흐름 구성 요소의 사용자 인터페이스 개발 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow components [Integration Services], custom editors
- user interfaces [Integration Services]
- custom data flow components [Integration Services], custom editors
- custom component editors [Integration Services]
- IDtsComponentUI interface
- UITypeName property
- custom user interface [Integration Services], custom data flow component
- editors [Integration Services]
ms.assetid: 10b829a1-609b-42e3-9070-cfe5a2bb698c
caps.latest.revision: "59"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ce13ece34803cd0f30c0ec5633e59b6dbb1151cb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="developing-a-user-interface-for-a-data-flow-component"></a>데이터 흐름 구성 요소의 사용자 인터페이스 개발
  구성 요소 개발자는 구성 요소를 편집할 때 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에 표시되는 사용자 지정 사용자 인터페이스를 구성 요소에 제공할 수 있습니다. 사용자 지정 사용자 인터페이스를 구현하면 해당 구성 요소가 데이터 흐름 태스크에 추가되거나 데이터 흐름 태스크에서 삭제될 때와 해당 구성 요소에 대한 도움말이 요청될 때 이에 대한 알림을 받을 수 있습니다.  
  
 구성 요소에 사용자 지정 사용자 인터페이스를 제공하지 않는 경우에도 최종 사용자는 고급 편집기를 사용하여 구성 요소와 해당 구성 요소의 사용자 지정 속성을 구성할 수 있습니다. 고급 편집기에서는 적절할 때 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.TypeConverter%2A>의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100> 속성을 사용하여 사용자 지정 속성 값을 적절하게 편집할 수 있습니다. 자세한 내용은 [데이터 흐름 구성 요소의 디자인 타임 메서드](../../../integration-services/extending-packages-custom-objects/data-flow/design-time-methods-of-a-data-flow-component.md)의 "사용자 지정 속성 만들기"를 참조하세요.  
  
## <a name="setting-the-uitypename-property"></a>UITypeName 속성 설정  
 사용자 지정 사용자 인터페이스를 개발하려면 개발자는 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.UITypeName%2A>의 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 속성을 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> 인터페이스를 구현하는 클래스의 이름으로 설정해야 합니다. 구성 요소에 의해 이 속성이 설정된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서는 구성 요소가 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 편집될 때 사용자 지정 사용자 인터페이스를 로드하고 호출합니다.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.UITypeName%2A> 속성은 해당 형식의 정규화된 이름을 식별하는 쉼표로 구분된 문자열입니다. 다음 목록에서는 형식 식별 요소를 순서대로 보여 줍니다.  
  
-   형식 이름  
  
-   어셈블리 이름  
  
-   파일 버전  
  
-   Culture  
  
-   공개 키 토큰  
  
 다음 코드 예에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 기본 클래스에서 파생되는 클래스를 보여 주고 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.UITypeName%2A> 속성을 지정합니다.  
  
```csharp  
[DtsPipelineComponent(  
DisplayName="SampleComponent",  
UITypeName="MyNamespace.MyComponentUIClassName,MyAssemblyName,Version=1.0.0.0,Culture=neutral,PublicKeyToken=abcd...",  
ComponentType = ComponentType.Transform)]  
public class SampleComponent : PipelineComponent  
{  
//TODO: Implement the component here.  
}  
```  
  
```vb  
<DtsPipelineComponent(DisplayName="SampleComponent", _  
UITypeName="MyNamespace.MyComponentUIClassName,MyAssemblyName,Version=1.0.0.0,Culture=neutral,PublicKeyToken=abcd...", ComponentType=ComponentType.Transform)> _   
Public Class SampleComponent   
 Inherits PipelineComponent   
End Class  
```  
  
## <a name="implementing-the-idtscomponentui-interface"></a>IDtsComponentUI 인터페이스 구현  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> 인터페이스에는 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 구성 요소가 추가, 삭제 및 편집될 때 호출하는 메서드가 있습니다. 구성 요소 개발자는 이러한 메서드의 구현에서 구성 요소 사용자와 상호 작용하기 위한 코드를 제공할 수 있습니다.  
  
 이 클래스는 일반적으로 구성 요소와는 별개의 어셈블리에 구현됩니다. 반드시 별개의 어셈블리를 사용해야 하는 것은 아니지만 이렇게 하면 개발자가 구성 요소와 사용자 인터페이스를 서로 독립적으로 빌드 및 배포하고 구성 요소의 이진 사용 공간을 작게 유지할 수 있습니다.  
  
 사용자 지정 사용자 인터페이스를 구현하면 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 해당 구성 요소가 편집될 때 구성 요소 개발자가 구성 요소를 보다 효율적으로 제어할 수 있습니다. 예를 들어 구성 요소에서는 구성 요소가 처음 데이터 흐름 태스크에 추가될 때 호출되는 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.New%2A> 메서드에 코드를 추가하고, 구성 요소의 초기 구성을 사용자에게 안내해 주는 마법사를 표시할 수 있습니다.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> 인터페이스를 구현하는 클래스를 만든 후에는 사용자와 구성 요소의 상호 작용에 응답하기 위한 코드를 추가해야 합니다. <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Initialize%2A> 메서드는 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 인터페이스를 제공하며, <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.New%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A> 메서드보다 먼저 호출됩니다. 이 참조는 전용 멤버 변수에 저장되어 이후 구성 요소의 메타데이터를 수정하는 데 사용되어야 합니다.  
  
## <a name="modifying-a-component-and-persisting-changes"></a>구성 요소 수정 및 변경 내용 지속  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 인터페이스는 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Initialize%2A> 메서드에 대한 매개 변수로 제공됩니다. 이 참조는 사용자 인터페이스에 의해 멤버 변수에 캐시된 다음 사용자와 사용자 인터페이스의 상호 작용에 대한 응답으로 구성 요소를 수정하는 데 사용되어야 합니다.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 인터페이스를 통해 직접 구성 요소를 수정할 수도 있지만 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapper> 메서드를 사용하여 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.Instantiate%2A>의 인스턴스를 만드는 것이 더 좋습니다. 이 인터페이스를 사용하여 직접 구성 요소를 편집하면 구성 요소 보호를 위한 유효성 검사가 무시됩니다. 그러나 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapper>를 통해 구성 요소의 디자인 타임 인스턴스를 사용하면 구성 요소에서 해당 구성 요소에 대한 변경을 제어할 수 있다는 장점이 있습니다.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A> 메서드의 반환 값은 구성 요소의 변경 내용이 지속되는지 삭제되는지를 결정합니다. 이 메서드가 **false**를 반환하면 모든 변경 내용이 삭제되고, **true**를 반환하면 구성 요소의 변경 내용이 유지되고 패키지가 저장되어야 하는 것으로 표시됩니다.  
  
### <a name="using-the-services-of-the-ssis-designer"></a>SSIS 디자이너의 서비스 사용  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Initialize%2A> 메서드의 **IServiceProvider** 매개 변수는 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너의 다음 서비스에 액세스할 수 있도록 합니다.  
  
|서비스|Description|  
|-------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Design.IDtsClipboardService>|구성 요소가 복사/붙여넣기 또는 잘라내기/붙여넣기 작업 중 어떤 작업의 일부로 생성되었는지를 확인하는 데 사용됩니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionService>|기존 연결에 액세스하거나 패키지에 새 연결을 만드는 데 사용됩니다.|  
|<xref:Microsoft.SqlServer.Dts.Design.IErrorCollectionService>|마지막 오류 또는 경고만 받는 것이 아니라 구성 요소에 의해 발생한 오류 및 경고를 모두 캡처해야 하는 경우 데이터 흐름 구성 요소에서 발생한 이벤트를 캡처하는 데 사용됩니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsVariableService>|기존 변수에 액세스하거나 패키지에 새 변수를 만드는 데 사용됩니다.|  
|<xref:Microsoft.SqlServer.Dts.Design.IDtsPipelineEnvironmentService>|데이터 흐름 구성 요소에서 부모 데이터 흐름 태스크와 데이터 흐름의 다른 구성 요소에 액세스하는 데 사용됩니다. 이 기능을 사용하면 필요할 때 추가 데이터 흐름 구성 요소를 만들고 연결하는 느린 변경 차원 마법사와 같은 구성 요소를 개발할 수 있습니다.|  
  
 개발자는 이러한 서비스를 사용하여 구성 요소가 로드된 패키지의 개체에 액세스하거나 패키지에 개체를 만들 수 있습니다.  
  
## <a name="sample"></a>예제  
 다음 코드 예제에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> 인터페이스를 구현하는 사용자 지정 사용자 인터페이스 클래스와 구성 요소의 편집기로 사용되는 Windows Form의 통합을 보여 줍니다.  
  
### <a name="custom-user-interface-class"></a>사용자 지정 사용자 인터페이스 클래스  
 다음 코드에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI> 인터페이스를 구현하는 클래스를 보여 줍니다. <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A> 메서드는 구성 요소 편집기를 만든 다음 해당 폼을 표시합니다. 폼의 반환 값은 구성 요소의 변경 내용이 지속되는지 여부를 결정합니다.  
  
```csharp  
using System;  
using System.Windows.Forms;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Pipeline.Design;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    public class SampleComponentUI : IDtsComponentUI  
    {  
        IDTSComponentMetaData100 md;  
        IServiceProvider sp;  
  
        public void Help(System.Windows.Forms.IWin32Window parentWindow)  
        {  
        }  
        public void New(System.Windows.Forms.IWin32Window parentWindow)  
        {  
        }  
        public void Delete(System.Windows.Forms.IWin32Window parentWindow)  
        {  
        }  
        public bool Edit(System.Windows.Forms.IWin32Window parentWindow, Variables vars, Connections cons)  
        {  
            // Create and display the form for the user interface.  
            SampleComponentUIForm componentEditor = new SampleComponentUIForm(cons, vars, md);  
  
            DialogResult result  = componentEditor.ShowDialog(parentWindow);  
  
            if (result == DialogResult.OK)  
                return true;  
  
            return false;  
        }  
        public void Initialize(IDTSComponentMetaData100 dtsComponentMetadata, IServiceProvider serviceProvider)  
        {  
            // Store the component metadata.  
            this.md = dtsComponentMetadata;  
        }  
    }  
}  
```  
  
```vb  
Imports System   
Imports System.Windows.Forms   
Imports Microsoft.SqlServer.Dts.Runtime   
Imports Microsoft.SqlServer.Dts.Pipeline.Design   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
  
Namespace Microsoft.Samples.SqlServer.Dts   
  
 Public Class SampleComponentUI   
 Implements IDtsComponentUI   
   Private md As IDTSComponentMetaData100   
   Private sp As IServiceProvider   
  
   Public Sub Help(ByVal parentWindow As System.Windows.Forms.IWin32Window)   
   End Sub   
  
   Public Sub New(ByVal parentWindow As System.Windows.Forms.IWin32Window)   
   End Sub   
  
   Public Sub Delete(ByVal parentWindow As System.Windows.Forms.IWin32Window)   
   End Sub   
  
   Public Function Edit(ByVal parentWindow As System.Windows.Forms.IWin32Window, ByVal vars As Variables, ByVal cons As Connections) As Boolean   
     ' Create and display the form for the user interface.  
     Dim componentEditor As SampleComponentUIForm = New SampleComponentUIForm(cons, vars, md)   
     Dim result As DialogResult = componentEditor.ShowDialog(parentWindow)   
     If result = DialogResult.OK Then   
       Return True   
     End If   
     Return False   
   End Function   
  
   Public Sub Initialize(ByVal dtsComponentMetadata As IDTSComponentMetaData100, ByVal serviceProvider As IServiceProvider)   
     Me.md = dtsComponentMetadata   
   End Sub   
 End Class   
  
End Namespace  
```  
  
### <a name="custom-editor"></a>사용자 지정 편집기  
 다음 코드에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI.Edit%2A> 메서드를 호출하는 동안 표시되는 Windows Form의 구현을 보여 줍니다.  
  
```csharp  
using System;  
using System.Drawing;  
using System.Collections;  
using System.ComponentModel;  
using System.Windows.Forms;  
using System.Data;  
  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    public partial class SampleComponentUIForm : System.Windows.Forms.Form  
    {  
        private Connections connections;  
        private Variables variables;  
        private IDTSComponentMetaData100 metaData;  
        private CManagedComponentWrapper designTimeInstance;  
        private System.ComponentModel.IContainer components = null;  
  
        public SampleComponentUIForm( Connections cons, Variables vars, IDTSComponentMetaData100 md)  
        {  
            variables = vars;  
            connections = cons;  
            metaData = md;  
        }  
  
        private void btnOk_Click(object sender, System.EventArgs e)  
        {  
            if (designTimeInstance == null)  
                designTimeInstance = metaData.Instantiate();  
  
            designTimeInstance.SetComponentProperty( "CustomProperty", txtCustomPropertyValue.Text);  
  
            this.Close();  
        }  
  
        private void btnCancel_Click(object sender, System.EventArgs e)  
        {  
            this.Close();  
        }  
    }  
}  
```  
  
```vb  
Imports System   
Imports System.Drawing   
Imports System.Collections   
Imports System.ComponentModel   
Imports System.Windows.Forms   
Imports System.Data   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
Imports Microsoft.SqlServer.Dts.Runtime   
  
Namespace Microsoft.Samples.SqlServer.Dts   
  
 Public Partial Class SampleComponentUIForm   
  Inherits System.Windows.Forms.Form   
   Private connections As Connections   
   Private variables As Variables   
   Private metaData As IDTSComponentMetaData100   
   Private designTimeInstance As CManagedComponentWrapper   
   Private components As System.ComponentModel.IContainer = Nothing   
  
   Public Sub New(ByVal cons As Connections, ByVal vars As Variables, ByVal md As IDTSComponentMetaData100)   
     variables = vars   
     connections = cons   
     metaData = md   
   End Sub   
  
   Private Sub btnOk_Click(ByVal sender As Object, ByVal e As System.EventArgs)   
     If designTimeInstance Is Nothing Then   
       designTimeInstance = metaData.Instantiate   
     End If   
     designTimeInstance.SetComponentProperty("CustomProperty", txtCustomPropertyValue.Text)   
     Me.Close   
   End Sub   
  
   Private Sub btnCancel_Click(ByVal sender As Object, ByVal e As System.EventArgs)   
     Me.Close   
   End Sub   
 End Class   
  
End Namespace  
```
  
## <a name="see-also"></a>관련 항목:  
 [사용자 지정 데이터 흐름 구성 요소 만들기](../../../integration-services/extending-packages-custom-objects/data-flow/creating-a-custom-data-flow-component.md)  
  
  
