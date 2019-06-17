---
title: 데이터 흐름 구성 요소에서 오류 출력 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- errors [Integration Services], alternative outputs
- synchronous error outputs [Integration Services]
- alternative error outputs [Integration Services]
- custom data flow components [Integration Services], error outputs
- data flow components [Integration Services], error outputs
- populating error columns [Integration Services]
- redirecting error output [Integration Services]
- error outputs [Integration Services]
- asynchronous error outputs [Integration Services]
ms.assetid: a2a3e7c8-1de2-45b3-97fb-60415d3b0934
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d852aef3321878ba01c535c9e0d8f696dc7d4e0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65724598"
---
# <a name="using-error-outputs-in-a-data-flow-component"></a>데이터 흐름 구성 요소에서 오류 출력 사용

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  구성 요소에 오류 출력이라는 특수한 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 개체를 추가하면 실행 중 해당 구성 요소에서 처리할 수 없는 행을 리디렉션할 수 있습니다. 구성 요소에서 발생할 수 있는 문제는 일반적으로 오류 또는 잘림으로 분류되며 각 구성 요소와만 관련이 있습니다. 구성 요소에서 오류 출력을 제공할 경우 해당 구성 요소의 사용자는 결과 집합에서 오류 행을 필터링하거나, 문제가 발생할 때 해당 구성 요소를 실패로 처리하거나, 오류를 무시하고 계속하는 방법으로 유연하게 오류 조건을 처리할 수 있습니다.  
  
 구성 요소에서 오류 출력을 구현 및 지원하려면 먼저 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.UsesDispositions%2A> 속성을 **true**로 설정해야 합니다. 그런 다음 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.IsErrorOut%2A> 속성이 **true**로 설정된 구성 요소에 출력을 추가해야 합니다. 마지막으로, 오류 또는 잘림이 발생할 경우 오류 출력으로 행을 리디렉션하는 코드를 구성 요소에 포함해야 합니다. 이 항목에서는 이러한 세 단계를 설명하고 동기 오류 출력과 비동기 오류 출력의 차이점에 대해 설명합니다.  
  
## <a name="creating-an-error-output"></a>오류 출력 만들기  
 오류 출력을 만들려면 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputCollection100.New%2A>의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.OutputCollection%2A> 메서드를 호출한 다음 새 출력의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.IsErrorOut%2A> 속성을 **true**로 설정합니다. 출력이 비동기적인 경우에는 출력에 대해 아무 작업도 수행하지 않아야 합니다. 출력이 동기적이고 동일한 입력에 대해 동기적인 다른 출력이 더 있는 경우에는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.ExclusionGroup%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> 속성도 설정해야 합니다. 두 속성은 모두 동일한 입력에 대해 동기적인 다른 출력과 동일한 값으로 설정되어야 합니다. 이러한 속성이 0이 아닌 값으로 설정되어 있는 경우 입력에서 제공된 행은 해당 입력에 동기적인 두 출력 모두로 보내집니다.  
  
 실행 중 구성 요소에서 오류나 잘림이 발생할 경우에는 오류가 발생한 입력/출력 또는 입력/출력 열의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100.ErrorRowDisposition%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100.TruncationRowDisposition%2A> 속성 설정에 따라 진행 방식이 결정됩니다. 이러한 속성 값은 기본적으로 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition.RD_NotUsed>로 설정됩니다. 구성 요소의 오류 출력이 다운스트림 구성 요소에 연결된 경우 이 속성은 구성 요소 사용자가 설정하며 사용자는 이 속성을 통해 구성 요소에서 오류 또는 잘림을 처리하는 방식을 제어할 수 있습니다.  
  
## <a name="populating-error-columns"></a>오류 열 채우기  
 오류 출력이 만들어지면 데이터 흐름 태스크에서는 출력 열 컬렉션에 두 개의 열을 자동으로 추가합니다. 이러한 열은 구성 요소에서 오류 또는 잘림을 발생시킨 열의 ID를 지정하고 구성 요소별 오류 코드를 제공하는 데 사용됩니다. 이러한 열은 자동으로 생성되지만 열에 포함되는 값은 구성 요소에서 설정해야 합니다.  
  
 이러한 열의 값을 설정하는 데 사용되는 메서드는 오류 출력이 동기적인지 비동기적인지에 따라 달라집니다. 동기 출력을 사용하는 구성 요소에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.DirectErrorRow%2A> 메서드를 호출하고(자세한 내용은 다음 섹션 참조) 오류 코드 및 오류 열 값을 매개 변수로 제공합니다. 비동기 출력을 사용하는 구성 요소에서는 두 가지 방법 중 하나로 이러한 열의 값을 설정할 수 있습니다. 출력 버퍼의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetErrorInfo%2A> 메서드를 호출하고 값을 지정하거나, <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A>를 사용하여 버퍼에서 오류 열을 찾고 해당 열의 값을 직접 설정할 수 있습니다. 하지만 열 이름이 변경되거나 출력 열 컬렉션에서의 열 위치가 수정된 경우도 있을 수 있으므로 두 번째 방법은 안정적이지 않습니다. <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetErrorInfo%2A> 메서드는 이러한 오류 열의 값을 자동으로 설정하므로 오류 열을 수동으로 찾을 필요가 없습니다.  
  
 특정 오류 코드에 해당하는 오류 설명을 가져와야 하는 경우 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> 속성을 통해 사용할 수 있는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 인터페이스의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> 메서드를 사용할 수 있습니다.  
  
 다음 코드 예에서는 하나의 입력과 오류 출력을 포함한 두 개의 출력을 사용하는 구성 요소를 보여 줍니다. 첫 번째 예에서는 입력에 동기적인 오류 출력을 만드는 방법을 보여 줍니다. 두 번째 예에서는 비동기적인 오류 출력을 만드는 방법을 보여 줍니다.  
  
```csharp  
public override void ProvideComponentProperties()  
{  
    // Specify that the component has an error output.  
    ComponentMetaData.UsesDispositions = true;  
    // Create the input.  
    IDTSInput100 input = ComponentMetaData.InputCollection.New();  
    input.Name = "Input";  
    input.ErrorRowDisposition = DTSRowDisposition.RD_NotUsed;  
    input.ErrorOrTruncationOperation = "A string describing the possible error or truncation that may occur during execution.";  
  
    // Create the default output.  
    IDTSOutput100 output = ComponentMetaData.OutputCollection.New();  
    output.Name = "Output";  
    output.SynchronousInputID = input.ID;  
    output.ExclusionGroup = 1;  
  
    // Create the error output.  
    IDTSOutput100 errorOutput = ComponentMetaData.OutputCollection.New();  
    errorOutput.IsErrorOut = true;  
    errorOutput.Name = "ErrorOutput";  
    errorOutput.SynchronousInputID = input.ID;  
    errorOutput.ExclusionGroup = 1;  
  
}  
```  
  
```vb  
Public  Overrides Sub ProvideComponentProperties()   
  
 ' Specify that the component has an error output.  
 ComponentMetaData.UsesDispositions = True   
  
 Dim input As IDTSInput100 = ComponentMetaData.InputCollection.New   
  
 ' Create the input.  
 input.Name = "Input"   
 input.ErrorRowDisposition = DTSRowDisposition.RD_NotUsed   
 input.ErrorOrTruncationOperation = "A string describing the possible error or truncation that may occur during execution."   
  
 ' Create the default output.  
 Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.New   
 output.Name = "Output"   
 output.SynchronousInputID = input.ID   
 output.ExclusionGroup = 1   
  
 ' Create the error output.  
 Dim errorOutput As IDTSOutput100 = ComponentMetaData.OutputCollection.New   
 errorOutput.IsErrorOut = True   
 errorOutput.Name = "ErrorOutput"   
 errorOutput.SynchronousInputID = input.ID   
 errorOutput.ExclusionGroup = 1   
  
End Sub  
```  
  
 다음 코드 예에서는 비동기적인 오류 출력을 만듭니다.  
  
```csharp  
public override void ProvideComponentProperties()  
{  
    // Specify that the component has an error output.  
    ComponentMetaData.UsesDispositions = true;  
  
    // Create the input.  
    IDTSInput100 input = ComponentMetaData.InputCollection.New();  
    input.Name = "Input";  
    input.ErrorRowDisposition = DTSRowDisposition.RD_NotUsed;  
    input.ErrorOrTruncationOperation = "A string describing the possible error or truncation that may occur during execution.";  
  
    // Create the default output.  
    IDTSOutput100 output = ComponentMetaData.OutputCollection.New();  
    output.Name = "Output";  
  
    // Create the error output.  
    IDTSOutput100 errorOutput = ComponentMetaData.OutputCollection.New();  
    errorOutput.Name = "ErrorOutput";  
    errorOutput.IsErrorOut = true;  
}  
```  
  
```vb  
Public  Overrides Sub ProvideComponentProperties()   
  
 ' Specify that the component has an error output.  
 ComponentMetaData.UsesDispositions = True   
  
 ' Create the input.  
 Dim input As IDTSInput100 = ComponentMetaData.InputCollection.New   
  
 ' Create the default output.  
 input.Name = "Input"   
 input.ErrorRowDisposition = DTSRowDisposition.RD_NotUsed   
 input.ErrorOrTruncationOperation = "A string describing the possible error or truncation that may occur during execution."   
  
 ' Create the error output.  
 Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.New   
 output.Name = "Output"   
 Dim errorOutput As IDTSOutput100 = ComponentMetaData.OutputCollection.New   
 errorOutput.Name = "ErrorOutput"   
 errorOutput.IsErrorOut = True   
  
End Sub  
```  
  
## <a name="redirecting-a-row-to-an-error-output"></a>행을 오류 출력으로 리디렉션  
 구성 요소에 오류 출력을 추가한 후에는 해당 구성 요소와 관련된 오류 또는 잘림 조건을 처리하고 해당 오류 또는 잘림 행을 오류 출력으로 리디렉션하는 코드를 제공해야 합니다. 이 작업은 오류 출력이 동기적인지 비동기적인지에 따라 두 가지 방법 중 하나로 수행할 수 있습니다.  
  
### <a name="redirecting-a-row-with-synchronous-outputs"></a>동기 출력을 사용하는 경우 행 리디렉션  
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.DirectErrorRow%2A> 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 메서드를 호출하면 행이 동기 출력으로 보내집니다. 이 메서드를 호출할 때는 오류 출력의 ID, 구성 요소에 정의된 오류 코드 및 구성 요소에서 처리하지 못한 열의 인덱스를 매개 변수로 지정해야 합니다.  
  
 다음 코드 예에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.DirectErrorRow%2A> 메서드를 사용하여 버퍼의 행을 동기 오류 출력으로 전송하는 방법을 보여 줍니다.  
  
```csharp  
public override void ProcessInput(int inputID, PipelineBuffer buffer)  
{  
        IDTSInput100 input = ComponentMetaData.InputCollection.GetObjectByID(inputID);  
  
        // This code sample assumes the component has two outputs, one the default,  
        // the other the error output. If the errorOutputIndex returned from GetErrorOutputInfo  
        // is 0, then the default output is the second output in the collection.  
        int defaultOutputID = -1;  
        int errorOutputID = -1;  
        int errorOutputIndex = -1;  
  
        GetErrorOutputInfo(ref errorOutputID,ref errorOutputIndex);  
  
        if (errorOutputIndex == 0)  
            defaultOutputID = ComponentMetaData.OutputCollection[1].ID;  
        else  
            defaultOutputID = ComponentMetaData.OutputCollection[0].ID;  
  
        while (buffer.NextRow())  
        {  
            try  
            {  
                // TODO: Implement code to process the columns in the buffer row.  
  
                // Ideally, your code should detect potential exceptions before they occur, rather  
                // than having a generic try/catch block such as this.   
                // However, because the error or truncation implementation is specific to each component,  
                // this sample focuses on actually directing the row, and not a single error or truncation.  
  
                // Unless an exception occurs, direct the row to the default   
                buffer.DirectRow(defaultOutputID);  
            }  
            catch  
            {  
                // Yes, has the user specified to redirect the row?  
                if (input.ErrorRowDisposition == DTSRowDisposition.RD_RedirectRow)  
                {  
                    // Yes, direct the row to the error output.  
                    // TODO: Add code to include the errorColumnIndex.  
                    buffer.DirectErrorRow(errorOutputID, 0, errorColumnIndex);  
                }  
                else if (input.ErrorRowDisposition == DTSRowDisposition.RD_FailComponent || input.ErrorRowDisposition == DTSRowDisposition.RD_NotUsed)  
                {  
                    // No, the user specified to fail the component, or the error row disposition was not set.  
                    throw new Exception("An error occurred, and the DTSRowDisposition is either not set, or is set to fail component.");  
                }  
                else  
                {  
                    // No, the user specified to ignore the failure so   
                    // direct the row to the default output.  
                    buffer.DirectRow(defaultOutputID);  
                }  
  
            }  
        }  
}  
```  
  
```vb  
Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)   
   Dim input As IDTSInput100 = ComponentMetaData.InputCollection.GetObjectByID(inputID)   
  
   ' This code sample assumes the component has two outputs, one the default,  
   ' the other the error output. If the errorOutputIndex returned from GetErrorOutputInfo  
   ' is 0, then the default output is the second output in the collection.  
   Dim defaultOutputID As Integer = -1   
   Dim errorOutputID As Integer = -1   
   Dim errorOutputIndex As Integer = -1   
  
   GetErrorOutputInfo(errorOutputID, errorOutputIndex)   
  
   If errorOutputIndex = 0 Then   
     defaultOutputID = ComponentMetaData.OutputCollection(1).ID   
   Else   
     defaultOutputID = ComponentMetaData.OutputCollection(0).ID   
   End If   
  
   While buffer.NextRow   
     Try   
       ' TODO: Implement code to process the columns in the buffer row.  
  
       ' Ideally, your code should detect potential exceptions before they occur, rather  
       ' than having a generic try/catch block such as this.   
       ' However, because the error or truncation implementation is specific to each component,  
       ' this sample focuses on actually directing the row, and not a single error or truncation.  
  
       ' Unless an exception occurs, direct the row to the default   
       buffer.DirectRow(defaultOutputID)   
     Catch   
       ' Yes, has the user specified to redirect the row?  
       If input.ErrorRowDisposition = DTSRowDisposition.RD_RedirectRow Then   
         ' Yes, direct the row to the error output.  
         ' TODO: Add code to include the errorColumnIndex.  
         buffer.DirectErrorRow(errorOutputID, 0, errorColumnIndex)   
       Else   
         If input.ErrorRowDisposition = DTSRowDisposition.RD_FailComponent OrElse input.ErrorRowDisposition = DTSRowDisposition.RD_NotUsed Then   
           ' No, the user specified to fail the component, or the error row disposition was not set.  
           Throw New Exception("An error occurred, and the DTSRowDisposition is either not set, or is set to fail component.")   
         Else   
           ' No, the user specified to ignore the failure so   
           ' direct the row to the default output.  
           buffer.DirectRow(defaultOutputID)   
         End If   
       End If   
     End Try   
   End While   
End Sub  
```  
  
### <a name="redirecting-a-row-with-asynchronous-outputs"></a>비동기 출력을 사용하는 경우 행 리디렉션  
 비동기 출력을 사용하는 구성 요소에서는 동기 오류 출력을 사용할 때와 같이 행을 출력으로 전송하는 대신 출력 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer>에 행을 명시적으로 추가하여 행을 오류 출력으로 보냅니다. 비동기 오류 출력을 사용하는 구성 요소를 구현하려면 다운스트림 구성 요소에 제공된 오류 출력에 열을 추가하고 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 메서드 실행 중 구성 요소에 제공된 오류 출력에 대한 출력 버퍼를 캐시해야 합니다. 비동기 출력을 사용하는 구성 요소 구현에 대한 세부 정보는 [비동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md) 항목에 자세히 설명되어 있습니다. 오류 출력에 열이 명시적으로 추가되지 않을 경우 출력 버퍼에 추가된 버퍼 행에는 두 개의 오류 열만 있습니다.  
  
 행을 비동기 오류 출력으로 보내려면 오류 출력 버퍼에 행을 추가해야 합니다. 일부 경우에는 행이 이미 오류가 아닌 출력 버퍼에 추가되어 있을 수 있으며 이 경우 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.RemoveRow%2A> 메서드를 사용하여 해당 행을 제거해야 합니다. 그런 다음 출력 버퍼의 열 값을 설정하고, 마지막으로 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetErrorInfo%2A> 메서드를 호출하여 구성 요소별 오류 코드와 오류 열 값을 제공합니다.  
  
 다음 예에서는 비동기 출력을 사용하는 구성 요소에 대해 오류 출력을 사용하는 방법을 보여 줍니다. 시뮬레이션된 오류가 발생하면 해당 구성 요소에서는 오류 출력 버퍼에 행을 추가하고, 이전에 오류가 아닌 출력 버퍼에 추가된 값을 오류 출력 버퍼에 복사하고, 오류가 아닌 출력 버퍼에 추가된 행을 제거한 다음, 마지막으로 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetErrorInfo%2A> 메서드를 호출하여 오류 코드와 오류 열 값을 설정합니다.  
  
```csharp  
int []columnIndex;  
int errorOutputID = -1;  
int errorOutputIndex = -1;  
  
public override void PreExecute()  
{  
    IDTSOutput100 defaultOutput = null;  
  
    this.GetErrorOutputInfo(ref errorOutputID, ref errorOutputIndex);  
    foreach (IDTSOutput100 output in ComponentMetaData.OutputCollection)  
    {  
        if (output.ID != errorOutputID)  
            defaultOutput = output;  
    }  
  
    columnIndex = new int[defaultOutput.OutputColumnCollection.Count];  
  
    for(int col =0 ; col < defaultOutput.OutputColumnCollection.Count; col++)  
    {  
        IDTSOutputColumn100 column = defaultOutput.OutputColumnCollection[col];  
        columnIndex[col] = BufferManager.FindColumnByLineageID(defaultOutput.Buffer, column.LineageID);  
    }  
}  
  
public override void PrimeOutput(int outputs, int[] outputIDs, PipelineBuffer[] buffers)  
{  
    for( int x=0; x < outputs; x++ )  
    {  
        if (outputIDs[x] == errorOutputID)  
            this.errorBuffer = buffers[x];  
        else  
            this.defaultBuffer = buffers[x];  
    }  
  
    int rows = 100;  
  
    Random random = new Random(System.DateTime.Now.Millisecond);  
  
    for (int row = 0; row < rows; row++)  
    {  
        try  
        {  
            defaultBuffer.AddRow();  
  
            for (int x = 0; x < columnIndex.Length; x++)  
                defaultBuffer[columnIndex[x]] = random.Next();  
  
            // Simulate an error.  
            if ((row % 2) == 0)  
                throw new Exception("A simulated error.");  
        }  
        catch  
        {  
            // Add a row to the error buffer.  
            errorBuffer.AddRow();  
  
            // Get the values from the default buffer  
            // and copy them to the error buffer.  
            for (int x = 0; x < columnIndex.Length; x++)  
                errorBuffer[columnIndex[x]] = defaultBuffer[columnIndex[x]];  
  
            // Set the error information.  
            errorBuffer.SetErrorInfo(errorOutputID, 1, 0);  
  
            // Remove the row that was added to the default buffer.  
            defaultBuffer.RemoveRow();  
        }  
    }  
  
    if (defaultBuffer != null)  
        defaultBuffer.SetEndOfRowset();  
  
    if (errorBuffer != null)  
        errorBuffer.SetEndOfRowset();  
}  
```  
  
```vb  
Private columnIndex As Integer()   
Private errorOutputID As Integer = -1   
Private errorOutputIndex As Integer = -1   
  
Public  Overrides Sub PreExecute()   
 Dim defaultOutput As IDTSOutput100 = Nothing   
 Me.GetErrorOutputInfo(errorOutputID, errorOutputIndex)   
 For Each output As IDTSOutput100 In ComponentMetaData.OutputCollection   
   If Not (output.ID = errorOutputID) Then   
     defaultOutput = output   
   End If   
 Next   
 columnIndex = New Integer(defaultOutput.OutputColumnCollection.Count) {}   
 Dim col As Integer = 0   
 While col < defaultOutput.OutputColumnCollection.Count   
   Dim column As IDTSOutputColumn100 = defaultOutput.OutputColumnCollection(col)   
   columnIndex(col) = BufferManager.FindColumnByLineageID(defaultOutput.Buffer, column.LineageID)   
   System.Math.Min(System.Threading.Interlocked.Increment(col),col-1)   
 End While   
End Sub   
  
Public  Overrides Sub PrimeOutput(ByVal outputs As Integer, ByVal outputIDs As Integer(), ByVal buffers As PipelineBuffer())   
 Dim x As Integer = 0   
 While x < outputs   
   If outputIDs(x) = errorOutputID Then   
     Me.errorBuffer = buffers(x)   
   Else   
     Me.defaultBuffer = buffers(x)   
   End If   
   System.Math.Min(System.Threading.Interlocked.Increment(x),x-1)   
 End While   
 Dim rows As Integer = 100   
 Dim random As Random = New Random(System.DateTime.Now.Millisecond)   
 Dim row As Integer = 0   
 While row < rows   
   Try   
     defaultBuffer.AddRow   
     Dim x As Integer = 0   
     While x < columnIndex.Length   
       defaultBuffer(columnIndex(x)) = random.Next   
       System.Math.Min(System.Threading.Interlocked.Increment(x),x-1)   
     End While   
     ' Simulate an error.  
     If (row Mod 2) = 0 Then   
       Throw New Exception("A simulated error.")   
     End If   
   Catch   
     ' Add a row to the error buffer.  
     errorBuffer.AddRow   
     ' Get the values from the default buffer  
     ' and copy them to the error buffer.  
     Dim x As Integer = 0   
     While x < columnIndex.Length   
       errorBuffer(columnIndex(x)) = defaultBuffer(columnIndex(x))   
       System.Math.Min(System.Threading.Interlocked.Increment(x),x-1)   
     End While   
     ' Set the error information.  
     errorBuffer.SetErrorInfo(errorOutputID, 1, 0)   
     ' Remove the row that was added to the default buffer.  
     defaultBuffer.RemoveRow   
   End Try   
   System.Math.Min(System.Threading.Interlocked.Increment(row),row-1)   
 End While   
 If Not (defaultBuffer Is Nothing) Then   
   defaultBuffer.SetEndOfRowset   
 End If   
 If Not (errorBuffer Is Nothing) Then   
   errorBuffer.SetEndOfRowset   
 End If   
End Sub  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 오류 처리](../../../integration-services/data-flow/error-handling-in-data.md)   
 [오류 출력 사용](../../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)  
  
  
