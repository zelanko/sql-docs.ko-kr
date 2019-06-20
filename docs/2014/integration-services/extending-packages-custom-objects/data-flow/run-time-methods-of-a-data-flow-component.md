---
title: 데이터 흐름 구성 요소의 런타임 메서드 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- run-time [Integration Services]
- data flow components [Integration Services], run-time methods
ms.assetid: fd9e4317-18dd-43af-bbdc-79db32183ac4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e107660073716019f48def8578a424ead92abf32
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768639"
---
# <a name="run-time-methods-of-a-data-flow-component"></a>데이터 흐름 구성 요소의 런타임 메서드
  런타임에 데이터 흐름 태스크에서는 구성 요소의 시퀀스를 검사하고, 실행 계획을 준비하고, 작업 계획을 실행하는 작업자 스레드의 풀을 관리합니다. 또한 원본에서 데이터 행을 로드하고 이를 변환을 통해 처리한 다음 대상에 저장합니다.  
  
## <a name="sequence-of-method-execution"></a>메서드 실행 순서  
 데이터 흐름 구성 요소를 실행하는 동안에는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 기본 클래스에 포함된 일련의 메서드가 호출됩니다. 이러한 메서드와 메서드가 호출되는 순서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드만 제외하고 항상 동일합니다. 이 두 메서드가 호출되는 방식은 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 개체가 있는지 여부와 해당 구성에 따라 다릅니다.  
  
 다음 목록에서는 구성 요소가 실행되는 동안 호출되는 메서드를 호출 순서대로 보여 줍니다. <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>이 호출될 때는 항상 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>보다 먼저 호출됩니다.  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrepareForExecute%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PostExecute%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Cleanup%2A>  
  
### <a name="primeoutput-method"></a>PrimeOutput 메서드  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.PrimeOutput%2A> 메서드는 구성 요소에 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 개체를 통해 다운스트림 구성 요소에 연결된 출력이 하나 이상 있고 이 출력의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> 속성이 0인 경우에 호출됩니다. 비동기 출력을 사용하는 원본 구성 요소 및 변환의 경우에는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.PrimeOutput%2A>이 호출됩니다. 아래에 설명된 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드와 달리 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 메서드는 해당 메서드가 필요한 각 구성 요소에 대해 한 번씩만 호출됩니다.  
  
### <a name="processinput-method"></a>ProcessInput 메서드  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.ProcessInput%2A> 메서드는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 개체를 통해 업스트림 구성 요소에 연결된 하나 이상의 입력이 있는 구성 요소에 대해 호출됩니다. <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.ProcessInput%2A> 메서드는 대상 구성 요소와 동기 출력을 사용하는 변환에 대해 호출됩니다 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>은 업스트림 구성 요소에서 더 이상 처리할 행이 없을 때까지 반복적으로 호출됩니다.  
  
## <a name="working-with-inputs-and-outputs"></a>입/출력 작업  
 런타임에 데이터 흐름 구성 요소에서는 다음 태스크를 수행합니다.  
  
-   원본 구성 요소가 행을 추가합니다.  
  
-   동기 출력을 사용하는 변환 구성 요소가 원본 구성 요소에서 제공된 행을 받습니다.  
  
-   비동기 출력을 사용하는 변환 구성 요소가 행을 받고 추가합니다.  
  
-   대상 구성 요소가 행을 받은 다음 대상으로 로드합니다.  
  
 실행 중 데이터 흐름 태스크에서는 구성 요소 시퀀스의 출력 열 컬렉션에 정의된 모든 열이 포함된 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer>를 할당합니다. 예를 들어 데이터 흐름 시퀀스에 있는 네 개의 구성 요소가 각각 해당 출력 열 컬렉션에서 출력 열을 하나씩 추가할 경우 각 구성 요소에 제공된 버퍼에는 이 네 개의 출력 열이 모두 포함됩니다. 이 동작으로 인해 구성 요소가 받는 버퍼에 해당 구성 요소에서 사용하지 않는 열이 포함된 경우가 종종 있습니다.  
  
 구성 요소가 받는 버퍼에는 해당 구성 요소에서 사용하지 않는 열이 포함되는 경우가 있으므로 구성 요소의 입력 및 출력 열 컬렉션에 사용할 열은 데이터 흐름 태스크가 해당 구성 요소에 제공한 버퍼에서 찾아야 합니다. 이렇게 하려면 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> 속성의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> 메서드를 사용합니다. 성능상의 이유로 이 태스크는 일반적으로 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 또는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 대신 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드에서 수행됩니다.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A>는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드보다 먼저 호출되므로 구성 요소에서 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A>를 사용할 수 있게 된 후 이 작업을 수행할 수 있는 첫 번째 메서드는 이 메서드입니다. 이 메서드가 실행될 때 구성 요소는 버퍼에서 해당 구성 요소의 열을 찾고 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 또는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드에서 해당 열을 사용할 수 있도록 이 정보를 내부에 저장해야 합니다.  
  
 다음 코드 예에서는 동기 출력을 사용하는 변환 구성 요소가 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 실행 중 버퍼에서 입력 열을 찾는 방법을 보여 줍니다.  
  
```csharp  
private int []bufferColumnIndex;  
public override void PreExecute()  
{  
    IDTSInput100 input = ComponentMetaData.InputCollection[0];  
    bufferColumnIndex = new int[input.InputColumnCollection.Count];  
  
    for( int x=0; x < input.InputColumnCollection.Count; x++)  
    {  
        IDTSInputColumn100 column = input.InputColumnCollection[x];  
        bufferColumnIndex[x] = BufferManager.FindColumnByLineageID( input.Buffer, column.LineageID);  
    }  
}  
```  
  
```vb  
Dim bufferColumnIndex As Integer()  
  
    Public Overrides Sub PreExecute()  
  
        Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)  
  
        ReDim bufferColumnIndex(input.InputColumnCollection.Count)  
  
        For x As Integer = 0 To input.InputColumnCollection.Count  
  
            Dim column As IDTSInputColumn100 = input.InputColumnCollection(x)  
            bufferColumnIndex(x) = BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID)  
  
        Next  
  
    End Sub  
```  
  
### <a name="adding-rows"></a>행 추가  
 구성 요소에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 개체에 행을 추가하는 방법으로 다운스트림 구성 요소에 행을 제공합니다. 데이터 흐름 태스크에서는 다운스트림 구성 요소에 연결된 각 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 개체에 대한 출력 버퍼가 하나씩 포함된 출력 버퍼 배열을 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 메서드에 대한 매개 변수로 제공합니다. 원본 구성 요소와 비동기 출력을 사용하는 변환 구성 요소에서는 버퍼에 행을 추가하고 행 추가가 완료되면 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetEndOfRowset%2A> 메서드를 호출합니다. 데이터 흐름 태스크에서는 해당 태스크가 구성 요소에 제공한 출력 버퍼를 관리하고 버퍼가 가득 차면 해당 버퍼의 행을 자동으로 다음 구성 요소로 이동합니다. <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 메서드는 반복적으로 호출되는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드와 달리 구성 요소마다 한 번씩 호출됩니다.  
  
 다음 코드 예에서는 구성 요소에서 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 메서드 실행 중 출력 버퍼에 행을 추가한 다음 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetEndOfRowset%2A> 메서드를 호출하는 방법을 보여 줍니다.  
  
```csharp  
public override void PrimeOutput( int outputs, int []outputIDs,PipelineBuffer []buffers)  
{  
    for( int x=0; x < outputs; x++ )  
    {  
        IDTSOutput100 output = ComponentMetaData.OutputCollection.GetObjectByID( outputIDs[x]);  
        PipelineBuffer buffer = buffers[x];  
  
        // TODO: Add rows to the output buffer.  
    }  
    foreach( PipelineBuffer buffer in buffers )  
    {  
        /// Notify the data flow task that no more rows are coming.  
        buffer.SetEndOfRowset();  
    }  
}  
```  
  
```vb  
public overrides sub PrimeOutput( outputs as Integer , outputIDs() as Integer ,buffers() as PipelineBuffer buffers)  
  
    For x As Integer = 0 To outputs.MaxValue  
  
        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.GetObjectByID(outputIDs(x))  
        Dim buffer As PipelineBuffer = buffers(x)  
  
        ' TODO: Add rows to the output buffer.  
  
    Next  
  
    For Each buffer As PipelineBuffer In buffers  
  
        ' Notify the data flow task that no more rows are coming.  
        buffer.SetEndOfRowset()  
  
    Next  
  
End Sub  
```  
  
 출력 버퍼에 행을 추가하는 구성 요소 개발에 대한 자세한 내용은 [사용자 지정 원본 구성 요소 개발](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md) 및 [비동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)을 참조하세요.  
  
### <a name="receiving-rows"></a>파일 받기  
 구성 요소는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 개체에서 업스트림 구성 요소의 행을 받습니다. 데이터 흐름 태스크에서는 업스트림 구성 요소가 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 메서드에 대한 매개 변수로 데이터 흐름에 추가한 행이 들어 있는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 개체를 제공합니다. 이 입력 버퍼를 사용하여 버퍼의 행 및 열을 검사하거나 수정할 수 있지만 행을 추가하거나 제거할 수는 없습니다. <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드는 사용할 수 없는 버퍼가 더 이상 없을 때까지 반복적으로 호출됩니다. 이 메서드가 마지막으로 호출될 때는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 속성이 `true`로 설정됩니다. 버퍼 내에서 다음 행으로 진행하는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.NextRow%2A> 메서드를 사용하면 버퍼의 행 컬렉션을 반복할 수 있습니다. 버퍼가 컬렉션의 마지막 행에 있으면 이 메서드는 `false`를 반환합니다. 마지막 데이터 행이 처리된 후 추가 동작을 수행해야 하는 경우가 아니면 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 속성을 확인할 필요가 없습니다.  
  
 다음 텍스트는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.NextRow%2A> 메서드와 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 속성을 사용할 때 올바른 패턴을 보여 줍니다.  
  
 `while (buffer.NextRow())`  
  
 `{`  
  
 `// Do something with each row.`  
  
 `}`  
  
 `if (buffer.EndOfRowset)`  
  
 `{`  
  
 `// Optionally, do something after all rows have been processed.`  
  
 `}`  
  
 다음 코드 예에서는 구성 요소에서 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드 실행 중 입력 버퍼의 행을 처리하는 방법을 보여 줍니다.  
  
```csharp  
public override void ProcessInput( int inputID, PipelineBuffer buffer )  
{  
    {  
        IDTSInput100 input = ComponentMetaData.InputCollection.GetObjectByID(inputID);  
        while( buffer.NextRow())  
        {  
            // TODO: Examine the columns in the current row.  
        }  
}  
```  
  
```vb  
Public Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)  
  
        Dim input As IDTSInput100 = ComponentMetaData.InputCollection.GetObjectByID(inputID)  
        While buffer.NextRow() = True  
  
            ' TODO: Examine the columns in the current row.  
        End While  
  
End Sub  
```  
  
 입력 버퍼에 행을 받는 구성 요소 개발에 대한 자세한 내용은 [사용자 지정 원본 구성 요소 개발](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md) 및 [동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)을 참조하세요.  
  
![Integration Services 아이콘 (작은)](../../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 흐름 구성 요소의 디자인 타임 메서드](design-time-methods-of-a-data-flow-component.md)  
  
  
