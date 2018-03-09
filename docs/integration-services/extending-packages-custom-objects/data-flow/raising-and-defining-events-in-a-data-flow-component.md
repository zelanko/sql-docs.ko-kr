---
title: "데이터 흐름 구성 요소에서 이벤트 발생 및 정의 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow components [Integration Services], events
- events [Integration Services], custom
- custom events [Integration Services]
- custom data flow components [Integration Services], events
- events [Integration Services], raising
- predefined events [Integration Services]
ms.assetid: 1d8c5358-9384-47a8-b7cb-7b0650384119
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 29e81f38876b25e3a789ef1eebdbdf9d1abebe1a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="raising-and-defining-events-in-a-data-flow-component"></a>데이터 흐름 구성 요소에서 이벤트 발생 및 정의
  구성 요소 개발자는 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> 속성에 제공된 메서드를 호출하여 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> 인터페이스에 정의된 일부 이벤트를 발생시킬 수 있습니다. <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.EventInfos%2A> 컬렉션을 사용하여 사용자 지정 이벤트를 정의하고 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A> 메서드를 사용하여 실행하는 동안 해당 이벤트를 발생시킬 수도 있습니다. 이 섹션에서는 이벤트를 만들고 발생시키는 방법을 설명하고 디자인 타임에 이벤트를 발생시켜야 하는 경우에 대한 지침을 제공합니다.  
  
## <a name="raising-events"></a>이벤트 발생  
 구성 요소에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 인터페이스의 **Fire\<X>** 메서드를 사용하여 이벤트를 발생시킵니다. 구성 요소를 디자인하거나 실행할 때 이벤트를 발생시킬 수 있습니다. 일반적으로 구성 요소를 디자인할 때는 유효성 검사 과정에서 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireWarning%2A> 메서드가 호출됩니다. 이러한 이벤트는 구성 요소가 잘못 구성되어 있는 경우 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]의 **오류 목록** 창에 메시지를 표시하고 구성 요소 사용자에게 피드백을 제공합니다.  
  
 또한 구성 요소에서는 실행 중 어느 시점에서나 이벤트를 발생시킬 수 있습니다. 구성 요소 개발자는 이벤트를 통해 구성 요소가 실행될 때 구성 요소 사용자에게 피드백을 제공할 수 있습니다. 실행 중 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A> 메서드를 호출하면 패키지가 실패할 수 있습니다.  
  
## <a name="defining-and-raising-custom-events"></a>사용자 지정 이벤트 정의 및 발생  
  
### <a name="defining-a-custom-event"></a>사용자 지정 이벤트 정의  
 사용자 지정 이벤트는 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSEventInfos100.Add%2A> 컬렉션의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.EventInfos%2A> 메서드를 호출하여 만듭니다. 이 컬렉션은 데이터 흐름 태스크에서 설정되며 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 기본 클래스를 통해 구성 요소 개발자에게 속성으로 제공됩니다. 이 클래스에는 데이터 흐름 태스크에서 정의된 사용자 지정 이벤트와 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> 메서드 실행 중 구성 요소에서 정의된 사용자 지정 이벤트가 들어 있습니다.  
  
 구성 요소의 사용자 지정 이벤트는 패키지 XML에 저장되지 않습니다. 따라서 구성 요소가 해당 구성 요소에서 발생하는 이벤트를 정의할 수 있도록 디자인할 때와 실행할 때 모두 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> 메서드가 호출됩니다.  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSEventInfos100.Add%2A> 메서드의 *allowEventHandlers* 매개 변수는 구성 요소에서 이벤트에 대한 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 개체를 만들 수 있는지 여부를 지정합니다. <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandlers>는 동기 개체이므로 구성 요소에서는 사용자 지정 이벤트에 연결된 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>가 실행을 마칠 때까지 실행을 다시 시작하지 않습니다. *allowEventHandlers* 매개 변수가 **true**인 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 런타임에서 자동으로 만들어지고 채워진 변수를 통해 모든 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 개체가 자동으로 해당 이벤트의 각 매개 변수를 사용할 수 있게 됩니다.  
  
### <a name="raising-a-custom-event"></a>사용자 지정 이벤트 발생  
 구성 요소에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A> 메서드를 호출하고 이벤트의 이름, 텍스트 및 매개 변수를 제공하여 사용자 지정 이벤트를 발생시킵니다. *allowEventHandlers* 매개 변수가 **true**인 경우 해당 사용자 지정 이벤트에 대해 만들어진 모든 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandlers>가 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 런타임 엔진에 의해 실행됩니다.  
  
### <a name="custom-event-sample"></a>사용자 지정 이벤트 예제  
 다음 코드 예에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> 메서드 실행 중 사용자 지정 이벤트를 정의한 다음 런타임에 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A> 메서드를 호출하여 이벤트를 발생시키는 구성 요소를 보여 줍니다.  
  
```csharp  
public override void RegisterEvents()  
{  
    string [] parameterNames = new string[2]{"RowCount", "StartTime"};  
    ushort [] parameterTypes = new ushort[2]{ DtsConvert.VarTypeFromTypeCode(TypeCode.Int32), DtsConvert.VarTypeFromTypeCode(TypeCode.DateTime)};  
    string [] parameterDescriptions = new string[2]{"The number of rows to sort.", "The start time of the Sort operation."};  
    EventInfos.Add("StartingSort","Fires when the component begins sorting the rows.",false,ref parameterNames, ref paramterTypes, ref parameterDescriptions);  
}  
public override void ProcessInput(int inputID, PipelineBuffer buffer)  
{  
    while (buffer.NextRow())  
    {  
       // Process buffer rows.  
    }  
  
    IDTSEventInfo100 eventInfo = EventInfos["StartingSort"];  
    object []arguments = new object[2]{buffer.RowCount, DateTime.Now };  
    ComponentMetaData.FireCustomEvent("StartingSort", "Beginning sort operation.", ref arguments, ComponentMetaData.Name, ref FireSortEventAgain);  
}  
```  
  
```vb  
Public  Overrides Sub RegisterEvents()   
  Dim parameterNames As String() = New String(2) {"RowCount", "StartTime"}   
  Dim parameterTypes As System.UInt16() = New System.UInt16(2) {DtsConvert.VarTypeFromTypeCode(TypeCode.Int32), DtsConvert.VarTypeFromTypeCode(TypeCode.DateTime)}   
  Dim parameterDescriptions As String() = New String(2) {"The number of rows to sort.", "The start time of the Sort operation."}   
  EventInfos.Add("StartingSort", "Fires when the component begins sorting the rows.", False, parameterNames, paramterTypes, parameterDescriptions)   
End Sub   
  
Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)   
  While buffer.NextRow   
  End While   
  Dim eventInfo As IDTSEventInfo100 = EventInfos("StartingSort")   
  Dim arguments As Object() = New Object(2) {buffer.RowCount, DateTime.Now}   
  ComponentMetaData.FireCustomEvent("StartingSort", _  
    "Beginning sort operation.", arguments, _  
    ComponentMetaData.Name, FireSortEventAgain)   
End Sub  
```  

## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 이벤트 처리기](../../../integration-services/integration-services-ssis-event-handlers.md)   
 [패키지에 이벤트 처리기 추가](http://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)  
  
  
