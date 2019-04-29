---
title: 프로그래밍 방식으로 데이터 흐름 구성 요소 추가 | Microsoft Docs
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
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: c06065cf-43e5-4b6b-9824-7309d7f5e35e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 286b37195b200761ce8cd8e941076c8a27e61011
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62836809"
---
# <a name="adding-data-flow-components-programmatically"></a>프로그래밍 방식으로 데이터 흐름 구성 요소 추가
  데이터 흐름을 작성할 때는 먼저 구성 요소를 추가합니다. 그런 다음 해당 구성 요소를 구성하고 서로 연결하여 런타임에 데이터의 흐름을 구성합니다. 이 섹션에서는 데이터 흐름 태스크에 구성 요소를 추가하고 해당 구성 요소의 디자인 타임 인스턴스를 만든 다음 구성 요소를 구성하는 방법을 설명합니다. 구성 요소를 연결하는 방법에 대한 자세한 내용은 [프로그래밍 방식으로 데이터 흐름 구성 요소 연결](../building-packages-programmatically/connecting-data-flow-components-programmatically.md)을 참조하세요.  
  
## <a name="adding-a-component"></a>구성 요소 추가  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaDataCollection100.New%2A> 컬렉션의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.ComponentMetaDataCollection%2A> 메서드를 호출하여 새 구성 요소를 만들고 이를 데이터 흐름 태스크에 추가할 수 있습니다. 이 메서드는 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 인터페이스를 반환합니다. 하지만 이 시점에서 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>에는 구성 요소와 관련된 정보가 들어 있지 않습니다. 구성 요소의 형식을 식별하려면 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> 속성을 설정합니다. 데이터 흐름 태스크에서는 런타임에 이 속성 값을 사용하여 구성 요소의 인스턴스를 만듭니다.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> 속성에 지정된 값은 CLSID, PROGID 또는 구성 요소의 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo.CreationName%2A> 속성일 수 있습니다. CLSID는 일반적으로 속성 창에서 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> 속성 값으로 표시됩니다. 이 속성과 사용 가능한 구성 요소의 다른 속성을 가져오는 방법은 [프로그래밍 방식으로 데이터 흐름 구성 요소 검색](../building-packages-programmatically/discovering-data-flow-components-programmatically.md)을 참조하세요.  
  
## <a name="adding-a-managed-component"></a>관리되는 구성 요소 추가  
 CLSID나 PROGID는 구성 요소 자체가 아니라 래퍼를 가리키므로 이러한 값을 사용하여 데이터 흐름에 관리되는 데이터 흐름 구성 요소를 추가할 수는 없습니다. 대신 다음 예제에 표시된 대로 `CreationName` 속성이나 `AssemblyQualifiedName` 속성을 사용할 수 있습니다.  
  
 `AssemblyQualifiedName` 속성을 사용하려면 관리되는 구성 요소가 들어 있는 어셈블리에 대한 참조를 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 프로젝트에 추가해야 합니다. 이러한 어셈블리는 **참조 추가** 대화 상자의 .NET 탭에 표시되지 않습니다. 일반적으로 **C:\Program Files\Microsoft SQL Server\100\DTS\PipelineComponents** 폴더의 어셈블리를 찾도록 이동해야 합니다.  
  
 기본 제공되는 관리되는 데이터 흐름 구성 요소에는 다음이 포함됩니다.  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 원본  
  
-   XML 원본  
  
-   DataReader 대상  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 대상  
  
-   스크립트 구성 요소  
  
 다음 코드 예제에서는 데이터 흐름에 관리되는 구성 요소를 추가하는 두 가지 방법을 모두 보여 줍니다.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Microsoft.SqlServer.Dts.Runtime.Package package = new Microsoft.SqlServer.Dts.Runtime.Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      Microsoft.SqlServer.Dts.Runtime.TaskHost thMainPipe = (Microsoft.SqlServer.Dts.Runtime.TaskHost)e;  
      MainPipe dataFlowTask = (MainPipe)thMainPipe.InnerObject;  
  
      // The Application object will be used to obtain the CreationName  
      //  of a PipelineComponentInfo from its PipelineComponentInfos collection.  
      Application app = new Application();  
  
      // Add a first ADO NET source to the data flow.  
      //  The CreationName property requires an Application instance.  
      IDTSComponentMetaData100 component1 = dataFlowTask.ComponentMetaDataCollection.New();  
      component1.Name = "DataReader Source";  
      component1.ComponentClassID = app.PipelineComponentInfos["DataReader Source"].CreationName;  
  
      // Add a second ADO NET source to the data flow.  
      //  The AssemblyQualifiedName property requires a reference to the assembly.  
      IDTSComponentMetaData100 component2 = dataFlowTask.ComponentMetaDataCollection.New();  
      component2.Name = "DataReader Source";  
      component2.ComponentClassID = typeof(Microsoft.SqlServer.Dts.Pipeline.DataReaderSourceAdapter).AssemblyQualifiedName;  
    }  
  }  
}  
  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' The Application object will be used to obtain the CreationName  
    '  of a PipelineComponentInfo from its PipelineComponentInfos collection.  
    Dim app As New Application()  
  
    ' Add a first ADO NET source to the data flow.  
    '  The CreationName property requires an Application instance.  
    Dim component1 As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component1.Name = "DataReader Source"  
    component1.ComponentClassID = app.PipelineComponentInfos("DataReader Source").CreationName  
  
    ' Add a second ADO NET source to the data flow.  
    '  The AssemblyQualifiedName property requires a reference to the assembly.  
    Dim component2 As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component2.Name = "DataReader Source"  
    component2.ComponentClassID = _  
      GetType(Microsoft.SqlServer.Dts.Pipeline.DataReaderSourceAdapter).AssemblyQualifiedName  
  
  End Sub  
  
End Module  
```  
  
## <a name="creating-the-design-time-instance-of-the-component"></a>구성 요소의 디자인 타임 인스턴스 만들기  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.Instantiate%2A> 메서드를 호출하여 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> 속성으로 식별된 구성 요소의 디자인 타임 인스턴스를 만들 수 있습니다. 이 메서드는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapper> 인터페이스의 관리되는 래퍼인 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 개체를 반환합니다.  
  
 가능하면 항상 구성 요소 메타데이터를 직접 수정하는 대신 디자인 타임 인스턴스의 메서드를 사용하여 구성 요소를 수정해야 합니다. 메타데이터에는 연결과 같이 직접 설정해야 하는 항목도 있지만 일반적으로 메타데이터를 직접 수정할 경우에는 구성 요소의 변경 내용 모니터링 및 유효성 검사 기능을 사용할 수 없으므로 이 방법은 권장되지 않습니다.  
  
## <a name="assigning-connections"></a>연결 할당  
 OLE DB 원본 구성 요소와 같은 일부 구성 요소에서는 외부 데이터에 연결해야 하며 이 용도로 패키지의 기존 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 개체를 사용합니다. <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnectionCollection100.Count%2A> 컬렉션의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> 속성은 구성 요소에 필요한 런타임 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 개체의 수를 나타냅니다. 이 수가 0보다 크면 해당 구성 요소에는 연결이 필요합니다. <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100.ConnectionManager%2A>에 있는 첫 번째 연결의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100.Name%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> 속성을 지정하면 패키지의 연결 관리자를 구성 요소에 할당할 수 있습니다. 런타임 연결 컬렉션에 있는 연결 관리자의 이름은 패키지에서 참조하는 연결 관리자의 이름과 일치해야 합니다.  
  
## <a name="setting-the-values-of-custom-properties"></a>사용자 지정 속성 값 설정  
 구성 요소의 디자인 타임 인스턴스를 만든 후에는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A> 메서드를 호출합니다. 이 메서드는 사용자 지정 속성과 입력 및 출력 개체를 만들어 새로 만든 구성 요소를 초기화하므로 생성자와 비슷합니다. 한 구성 요소에 대해 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A>를 두 번 이상 호출하면 구성 요소가 다시 설정되고 이전의 메타데이터 수정 내용을 잃을 수 있으므로 이 메서드는 한 번만 호출해야 합니다.  
  
 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.CustomPropertyCollection%2A>에는 해당 구성 요소와 관련된 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100> 개체의 컬렉션이 들어 있습니다. 개체 속성을 해당 개체에서 항상 볼 수 있는 다른 프로그래밍 모델과 달리 구성 요소는 개발자가 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A> 메서드를 호출할 때 해당 구성 요소의 사용자 지정 속성 컬렉션만 채웁니다. 메서드를 호출한 후에는 디자인 타임 구성 요소 인스턴스의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.SetComponentProperty%2A> 메서드를 사용하여 사용자 지정 속성에 값을 할당합니다. 이 메서드는 사용자 지정 속성을 식별하고 새 값을 제공하는 이름/값 쌍을 받아들입니다.  
  
## <a name="initializing-output-columns"></a>출력 열 초기화  
 구성 요소를 태스크에 추가하고 구성한 후에는 개체의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>에서 열 컬렉션을 초기화합니다. 이 단계는 특히 원본 구성 요소와 관련이 있지만 변환 및 대상 구성 요소는 일반적으로 업스트림 구성 요소에서 받는 열에 의존하므로 이러한 구성 요소의 열은 초기화하지 않을 수 있습니다.  
  
 원본 구성 요소의 출력에 있는 열을 초기화하려면 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReinitializeMetaData%2A> 메서드를 호출합니다. 구성 요소에서는 외부 데이터 원본에 자동으로 연결하지 않으므로 구성 요소에서 외부 데이터 원본에 액세스하고 해당 열 메타데이터를 채울 수 있도록 하려면 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.AcquireConnections%2A>를 호출하기 전에 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReinitializeMetaData%2A> 메서드를 호출해야 합니다. 마지막으로 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReleaseConnections%2A> 메서드를 호출하여 연결을 해제합니다.  
  
## <a name="next-step"></a>다음 단계  
 구성 요소를 추가하고 구성한 다음에는 구성 요소 간의 경로를 만들어야 합니다. 이 단계에 대한 자세한 내용은 [프로그래밍 방식으로 데이터 흐름 구성 요소 연결](../building-packages-programmatically/connecting-data-flow-components-programmatically.md) 항목에서 설명합니다.  
  
## <a name="sample"></a>예제  
 다음 코드 예제에서는 데이터 흐름 태스크에 OLE DB 원본 구성 요소를 추가하고 해당 구성 요소의 디자인 타임 인스턴스를 만든 다음 구성 요소의 속성을 구성합니다. 이 예에는 Microsoft.SqlServer.DTSRuntimeWrap 어셈블리에 대한 참조가 필요합니다.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Runtime.Package package = new Runtime.Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      Runtime.TaskHost thMainPipe = e as Runtime.TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;  
  
      // Add an OLEDB connection manager to the package.  
      ConnectionManager cm = package.Connections.Add("OLEDB");  
      cm.Name = "OLEDB ConnectionManager";  
      cm.ConnectionString = "Data Source=(local);" +   
        "Initial Catalog=AdventureWorks;Provider=SQLOLEDB.1;" +   
        "Integrated Security=SSPI;"  
  
      // Add an OLE DB source to the data flow.  
      IDTSComponentMetaData100 component =   
        dataFlowTask.ComponentMetaDataCollection.New();  
      component.Name = "OLEDBSource";  
      component.ComponentClassID = "DTSAdapter.OleDbSource.1";  
      // You can also use the CLSID of the component instead of the PROGID.  
      //component.ComponentClassID = "{2C0A8BE5-1EDC-4353-A0EF-B778599C65A0}";  
  
      // Get the design time instance of the component.  
      CManagedComponentWrapper instance = component.Instantiate();  
  
      // Initialize the component  
      instance.ProvideComponentProperties();  
  
      // Specify the connection manager.  
      if (component.RuntimeConnectionCollection.Count > 0)  
      {  
        component.RuntimeConnectionCollection[0].ConnectionManager =   
          DtsConvert.GetExtendedInterface(package.Connections[0]);  
        component.RuntimeConnectionCollection[0].ConnectionManagerID =   
          package.Connections[0].ID;      }  
  
      // Set the custom properties.  
      instance.SetComponentProperty("AccessMode", 2);  
      instance.SetComponentProperty("SqlCommand",   
        "Select * from Production.Product");  
  
      // Reinitialize the metadata.  
      instance.AcquireConnections(null);  
      instance.ReinitializeMetaData();  
      instance.ReleaseConnections();  
  
      // Add other components to the data flow and connect them.  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' Add an OLEDB connection manager to the package.  
    Dim cm As ConnectionManager = package.Connections.Add("OLEDB")  
    cm.Name = "OLEDB ConnectionManager"  
    cm.ConnectionString = "Data Source=(local);" & _  
      "Initial Catalog=AdventureWorks;Provider=SQLOLEDB.1;" & _  
      "Integrated Security=SSPI;"  
  
    ' Add an OLE DB source to the data flow.  
    Dim component As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component.Name = "OLEDBSource"  
    component.ComponentClassID = "DTSAdapter.OleDbSource.1"  
    ' You can also use the CLSID of the component instead of the PROGID.  
    'component.ComponentClassID = "{2C0A8BE5-1EDC-4353-A0EF-B778599C65A0}";  
  
    ' Get the design time instance of the component.  
    Dim instance As CManagedComponentWrapper = component.Instantiate()  
  
    ' Initialize the component.  
    instance.ProvideComponentProperties()  
  
    ' Specify the connection manager.  
    If component.RuntimeConnectionCollection.Count > 0 Then  
      component.RuntimeConnectionCollection(0).ConnectionManager = _  
        DtsConvert.GetExtendedInterface(package.Connections(0))  
      component.RuntimeConnectionCollection(0).ConnectionManagerID = _  
        package.Connections(0).ID  
    End If  
  
    ' Set the custom properties.  
    instance.SetComponentProperty("AccessMode", 2)  
    instance.SetComponentProperty("SqlCommand", _  
      "Select * from Production.Product")  
  
    ' Reinitialize the metadata.  
    instance.AcquireConnections(vbNull)  
    instance.ReinitializeMetaData()  
    instance.ReleaseConnections()  
  
    ' Add other components to the data flow and connect them.  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>외부 리소스  
 blogs.msdn.com의 블로그 항목 - [EzAPI – SQL Server 2012용으로 업데이트됨](https://go.microsoft.com/fwlink/?LinkId=243223)  
  
![Integration Services 아이콘 (작은)](../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [프로그래밍 방식으로 데이터 흐름 구성 요소 연결](../building-packages-programmatically/connecting-data-flow-components-programmatically.md)  
  
  
