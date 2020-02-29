---
title: 비동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발 | Microsoft Docs
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
- custom data flow components [Integration Services], transformation components
- asynchronous outputs [Integration Services]
- ProcessInput method
- cache [Integration Services]
- buffer allocations [Integration Services]
- transformation components [Integration Services]
- output columns [Integration Services]
- PrimeOutput method
- data flow components [Integration Services], transformation components
ms.assetid: 1c3e92c7-a4fa-4fdd-b9ca-ac3069536274
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0f5b96d22881f3ee42d0cba2fb79a911d77842c1
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176373"
---
# <a name="developing-a-custom-transformation-component-with-asynchronous-outputs"></a>비동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발
  변환이 구성 요소에서 입력 행을 모두 받을 때까지 행을 출력할 수 없거나 변환이 입력으로 받은 각 행에 대해 출력 행을 정확히 하나만 생성하지 않는 경우에는 비동기 출력을 사용하는 구성 요소를 사용합니다. 예를 들어 집계 변환은 행을 모두 읽기 전까지는 행 합계를 계산할 수 없습니다. 반면 각 데이터 행이 전달될 때 해당 행을 수정하는 경우에는 언제든지 동기 출력을 사용하는 구성 요소를 사용할 수 있습니다. 각 행의 데이터를 현재 위치에서 수정하거나 각 입력 행의 값을 각각 포함하는 새 행을 하나 이상 만들 수 있습니다. 동기 구성 요소와 비동기 구성 요소 간의 차이점에 대한 자세한 내용은 [동기 및 비동기 변환 이해](../understanding-synchronous-and-asynchronous-transformations.md)를 참조하세요.

 비동기 출력을 사용하는 변환 구성 요소는 대상 구성 요소와 원본 구성 요소 모두로 작동하므로 고유합니다. 이러한 종류의 구성 요소는 업스트림 구성 요소에서 행을 받고 다운스트림 구성 요소에서 사용되는 행을 추가합니다. 다른 데이터 흐름 구성 요소는 이 두 작업을 모두 수행하지 않습니다.

 동기 출력을 사용하는 구성 요소에서 사용할 수 있는 업스트림 구성 요소의 열은 해당 구성 요소의 다운스트림 구성 요소에서도 자동으로 사용할 수 있습니다. 따라서 동기 출력을 사용하는 구성 요소에서는 다음 구성 요소에 열과 행을 제공하기 위해 출력 열을 정의할 필요가 없습니다. 반면 비동기 출력을 사용하는 구성 요소에서는 출력 열을 제공하고 다운스트림 구성 요소에 행을 제공해야 합니다. 따라서 비동기 출력을 사용하는 구성 요소에는 디자인 및 실행 시 수행해야 할 태스크가 더 많이 있으며 해당 구성 요소 개발자는 더 많은 코드를 구현해야 합니다.

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에는 비동기 출력이 있는 몇 가지 변환이 포함되어 있습니다. 예를 들어 정렬 변환의 경우에는 행을 정렬하기 전에 모든 행이 있어야 하며 행을 정렬하는 데는 비동기 출력이 사용됩니다. 정렬 변환에서는 행을 모두 받은 후 이를 정렬하고 출력에 추가합니다.

 이 섹션에서는 비동기 출력을 사용하는 변환의 개발 방법을 자세히 설명합니다. 원본 구성 요소 개발에 대한 자세한 내용은 [사용자 지정 원본 구성 요소 개발](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)을 참조하세요.

## <a name="design-time"></a>디자인 타임

### <a name="creating-the-component"></a>구성 요소 만들기
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> 개체의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 속성은 출력이 동기적인지 비동기적인지를 식별합니다. 비동기 출력을 만들려면 구성 요소에 출력을 추가하고 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A>를 0으로 설정합니다. 이 속성을 설정하면 데이터 흐름 태스크에서 구성 요소의 입력과 출력 모두에 대해 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 개체를 할당할지, 아니면 단일 버퍼만 할당하여 두 개체 간에 이를 공유할지도 결정됩니다.

 다음 예제 코드에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 구현에서 비동기 출력을 만드는 구성 요소를 보여 줍니다.

```csharp
using Microsoft.SqlServer.Dts.Pipeline;
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;
using Microsoft.SqlServer.Dts.Runtime;

namespace Microsoft.Samples.SqlServer.Dts
{
    [DtsPipelineComponent(DisplayName = "AsyncComponent",ComponentType = ComponentType.Transform)]
    public class AsyncComponent : PipelineComponent
    {
        public override void ProvideComponentProperties()
        {
            // Call the base class, which adds a synchronous input
            // and output.
            base.ProvideComponentProperties();

            // Make the output asynchronous.
            IDTSOutput100 output = ComponentMetaData.OutputCollection[0];
            output.SynchronousInputID = 0;
        }
    }
}
```

```vb
Imports Microsoft.SqlServer.Dts.Pipeline
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper
Imports Microsoft.SqlServer.Dts.Runtime

<DtsPipelineComponent(DisplayName:="AsyncComponent", ComponentType:=ComponentType.Transform)> _
Public Class AsyncComponent
    Inherits PipelineComponent

    Public Overrides Sub ProvideComponentProperties()

        ' Call the base class, which adds a synchronous input
        ' and output.
        Me.ProvideComponentProperties()

        ' Make the output asynchronous.
        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)
        output.SynchronousInputID = 0

    End Sub

End Class
```

### <a name="creating-and-configuring-output-columns"></a>출력 열 만들기 및 구성
 앞에서 설명한 대로 비동기 구성 요소는 출력 열 컬렉션에 열을 추가하여 다운스트림 구성 요소에 열을 제공합니다. 디자인 타임에 선택할 수 있는 메서드는 구성 요소의 필요에 따라 몇 가지가 있습니다. 예를 들어 모든 열을 업스트림 구성 요소에서 다운스트림 구성 요소로 전달하려는 경우에는 구성 요소에서 입력 열을 사용할 수 있는 첫 번째 메서드가 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.OnInputPathAttached%2A> 메서드이므로 이 메서드를 재정의하여 열을 추가합니다.

 구성 요소에서 입력에 대해 선택된 열을 기준으로 출력 열을 만드는 경우에는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.SetUsageType%2A> 메서드를 재정의하여 출력 열을 선택하고 해당 열의 사용 방법을 나타냅니다.

 비동기 출력을 사용하는 구성 요소에서 업스트림 구성 요소의 열을 기준으로 출력 열을 만들며 사용 가능한 업스트림 구성 요소가 변경되는 경우에는 구성 요소에서 출력 열 컬렉션을 업데이트해야 합니다. 구성 요소에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A>가 실행될 때 이러한 변경 내용을 검색하고 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A>가 실행될 때 이를 수정해야 합니다.

> [!NOTE]
>  출력 열이 출력 열 컬렉션에서 제거되면 데이터 흐름에서 해당 열을 참조하는 다운스트림 구성 요소가 부정적인 영향을 받습니다. 다운스트림 구성 요소가 손상되지 않도록 하려면 출력 열을 제거하거나 다시 만들지 않고 해당 열을 복구해야 합니다. 예를 들어 열의 데이터 형식이 변경된 경우에는 데이터 형식을 업데이트해야 합니다.

 다음 코드 예에서는 업스트림 구성 요소의 사용 가능한 각 열에 대해 해당 출력 열 컬렉션에 출력 열을 추가하는 구성 요소를 보여 줍니다.

```csharp
public override void OnInputPathAttached(int inputID)
{
   IDTSInput100 input = ComponentMetaData.InputCollection.GetObjectByID(inputID);
   IDTSOutput100 output = ComponentMetaData.OutputCollection[0];
   IDTSVirtualInput100 vInput = input.GetVirtualInput();

   foreach (IDTSVirtualInputColumn100 vCol in vInput.VirtualInputColumnCollection)
   {
      IDTSOutputColumn100 outCol = output.OutputColumnCollection.New();
      outCol.Name = vCol.Name;
      outCol.SetDataTypeProperties(vCol.DataType, vCol.Length, vCol.Precision, vCol.Scale, vCol.CodePage);
   }
}
```

```vb
Public Overrides Sub OnInputPathAttached(ByVal inputID As Integer)

    Dim input As IDTSInput100 = ComponentMetaData.InputCollection.GetObjectByID(inputID)
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)
    Dim vInput As IDTSVirtualInput100 = input.GetVirtualInput()

    For Each vCol As IDTSVirtualInputColumn100 In vInput.VirtualInputColumnCollection

        Dim outCol As IDTSOutputColumn100 = output.OutputColumnCollection.New()
        outCol.Name = vCol.Name
        outCol.SetDataTypeProperties(vCol.DataType, vCol.Length, vCol.Precision, vCol.Scale, vCol.CodePage)

    Next
End Sub
```

## <a name="run-time"></a>런타임
 또한 비동기 출력을 사용하는 구성 요소에서는 런타임에 다른 유형의 구성 요소와는 다른 일련의 메서드를 실행합니다. 먼저 이러한 구성 요소는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드에 대한 호출을 모두 받는 유일한 구성 요소입니다. 또한 비동기 출력을 사용하는 구성 요소에서는 처리를 시작하기 전에 들어오는 모든 행에 액세스해야 하므로 모든 행을 읽기 전까지 입력 행을 내부에 캐시해야 합니다. 마지막으로 비동기 출력을 사용하는 구성 요소는 다른 구성 요소와 달리 입력 버퍼와 출력 버퍼를 모두 받습니다.

### <a name="understanding-the-buffers"></a>버퍼 이해
 구성 요소에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>이 실행될 때 입력 버퍼를 받습니다. 이 버퍼는 업스트림 구성 요소에서 버퍼에 추가한 행을 포함합니다. 또한 업스트림 구성 요소의 출력에서 제공되었지만 비동기 구성 요소의 입력 컬렉션에 추가되지는 않은 열과 구성 요소의 입력 열도 포함합니다.

 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>에서 구성 요소에 제공되는 출력 버퍼는 처음에는 행을 포함하지 않습니다. 구성 요소는 이 버퍼에 행을 추가하고, 버퍼가 가득 차면 다운스트림 구성 요소에 버퍼를 제공합니다. 출력 버퍼는 다른 다운스트림 구성 요소에서 자체 출력에 추가한 모든 열과 구성 요소의 출력 열 컬렉션에 정의된 열을 포함합니다.

 이와 달리 동기 출력을 사용하는 구성 요소에서는 단일 공유 버퍼를 받습니다. 동기 출력을 사용하는 구성 요소의 공유 버퍼는 업스트림 및 다운스트림 구성 요소의 출력에 추가된 열과 구성 요소의 입력 및 출력 열을 모두 포함합니다.

### <a name="processing-rows"></a>행 처리

#### <a name="caching-input-rows"></a>입력 행 캐시
 비동기 출력을 사용하는 구성 요소를 작성할 때 출력 버퍼에 행을 추가하는 세 가지 방법 중 하나를 선택할 수 있습니다. 즉, 입력 행을 받을 때 행을 추가하거나, 구성 요소가 업스트림 구성 요소에서 모든 행을 받을 때까지 행을 캐시하거나, 구성 요소에 적절한 시기에 행을 추가할 수 있습니다. 구성 요소의 요구 사항에 따라 다른 방법을 선택합니다. 예를 들어 정렬 구성 요소의 경우에는 업스트림 행을 모두 받은 후에야 행을 정렬할 수 있습니다. 따라서 모든 행을 읽을 때까지 기다렸다가 출력 버퍼에 행을 추가해야 합니다.

 입력 버퍼에서 받은 행은 구성 요소에서 처리할 준비가 될 때까지 내부에 캐시되어야 합니다. 들어오는 버퍼 행은 데이터 테이블, 다차원 배열 또는 그 밖의 내부 구조에 캐시할 수 있습니다.

#### <a name="adding-output-rows"></a>출력 행 추가
 행을 받을 때 출력 버퍼에 행을 추가하든 모든 행을 받은 후에 출력 버퍼에 행을 추가하든 항상 출력 버퍼에서 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddRow%2A> 메서드를 호출해야 합니다. 행을 추가한 후에는 새 행에서 각 열의 값을 설정합니다.

 출력 버퍼에는 구성 요소의 출력 열 컬렉션에 있는 것보다 많은 열이 있는 경우가 종종 있으므로 열 값을 설정하려면 먼저 버퍼에서 적절한 열의 인덱스를 찾아야 합니다. <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> 속성의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> 메서드는 버퍼 행에서 지정된 계보 ID를 갖는 열 인덱스를 반환하며, 이 인덱스는 버퍼 열에 값을 할당하는 데 사용됩니다.

 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 메서드는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 메서드나 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드보다 먼저 호출되므로 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> 속성을 사용할 수 있으면서 입력 및 출력 버퍼에서 열 인덱스를 찾을 수 있는 첫 번째 메서드는 이 메서드입니다.

## <a name="sample"></a>샘플
 다음 예제에서는 비동기 출력을 사용하며 행을 받을 때 출력 버퍼에 행을 추가하는 간단한 변환 구성 요소를 보여 줍니다. 이 예제는 이 항목에 설명된 메서드 및 기능의 일부를 보여 줍니다. 여기에서는 비동기 출력을 사용하는 모든 사용자 지정 변환 구성 요소에서 재정의해야 하는 중요한 메서드를 보여 주지만 디자인 타임 유효성 검사를 위한 코드는 포함하지 않습니다. 또한 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>의 코드에서는 출력 열 컬렉션에 입력 열 컬렉션의 각 열에 대한 하나씩의 열이 있는 것으로 가정합니다.

```csharp
using System;
using Microsoft.SqlServer.Dts.Pipeline;
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;
using Microsoft.SqlServer.Dts.Runtime.Wrapper;

namespace Microsoft.Samples.SqlServer.Dts
{
   [DtsPipelineComponent(DisplayName = "AsynchronousOutput")]
   public class AsynchronousOutput : PipelineComponent
   {
      PipelineBuffer outputBuffer;
      int[] inputColumnBufferIndexes;
      int[] outputColumnBufferIndexes;

      public override void ProvideComponentProperties()
      {
         // Let the base class add the input and output objects.
         base.ProvideComponentProperties();

         // Name the input and output, and make the
         // output asynchronous.
         ComponentMetaData.InputCollection[0].Name = "Input";
         ComponentMetaData.OutputCollection[0].Name = "AsyncOutput";
         ComponentMetaData.OutputCollection[0].SynchronousInputID = 0;
      }
      public override void PreExecute()
      {
         IDTSInput100 input = ComponentMetaData.InputCollection[0];
         IDTSOutput100 output = ComponentMetaData.OutputCollection[0];

         inputColumnBufferIndexes = new int[input.InputColumnCollection.Count];
         outputColumnBufferIndexes = new int[output.OutputColumnCollection.Count];

         for (int col = 0; col < input.InputColumnCollection.Count; col++)
            inputColumnBufferIndexes[col] = BufferManager.FindColumnByLineageID(input.Buffer, input.InputColumnCollection[col].LineageID);

         for (int col = 0; col < output.OutputColumnCollection.Count; col++)
            outputColumnBufferIndexes[col] = BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection[col].LineageID);

      }

      public override void PrimeOutput(int outputs, int[] outputIDs, PipelineBuffer[] buffers)
      {
         if (buffers.Length != 0)
            outputBuffer = buffers[0];
      }
      public override void ProcessInput(int inputID, PipelineBuffer buffer)
      {
            // Advance the buffer to the next row.
            while (buffer.NextRow())
            {
               // Add a row to the output buffer.
               outputBuffer.AddRow();
               for (int x = 0; x < inputColumnBufferIndexes.Length; x++)
               {
                  // Copy the data from the input buffer column to the output buffer column.
                  outputBuffer[outputColumnBufferIndexes[x]] = buffer[inputColumnBufferIndexes[x]];
               }
            }
         if (buffer.EndOfRowset)
         {
            // EndOfRowset on the input buffer is true.
            // Set EndOfRowset on the output buffer.
            outputBuffer.SetEndOfRowset();
         }
      }
   }
}
```

```vb
Imports System
Imports Microsoft.SqlServer.Dts.Pipeline
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper

Namespace Microsoft.Samples.SqlServer.Dts

    <DtsPipelineComponent(DisplayName:="AsynchronousOutput")> _
    Public Class AsynchronousOutput

        Inherits PipelineComponent

        Private outputBuffer As PipelineBuffer
        Private inputColumnBufferIndexes As Integer()
        Private outputColumnBufferIndexes As Integer()

        Public Overrides Sub ProvideComponentProperties()

            ' Let the base class add the input and output objects.
            Me.ProvideComponentProperties()

            ' Name the input and output, and make the
            ' output asynchronous.
            ComponentMetaData.InputCollection(0).Name = "Input"
            ComponentMetaData.OutputCollection(0).Name = "AsyncOutput"
            ComponentMetaData.OutputCollection(0).SynchronousInputID = 0
        End Sub

        Public Overrides Sub PreExecute()

            Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)
            Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)

            ReDim inputColumnBufferIndexes(input.InputColumnCollection.Count)
            ReDim outputColumnBufferIndexes(output.OutputColumnCollection.Count)

            For col As Integer = 0 To input.InputColumnCollection.Count
                inputColumnBufferIndexes(col) = BufferManager.FindColumnByLineageID(input.Buffer, input.InputColumnCollection(col).LineageID)
            Next

            For col As Integer = 0 To output.OutputColumnCollection.Count
                outputColumnBufferIndexes(col) = BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection(col).LineageID)
            Next

        End Sub
        Public Overrides Sub PrimeOutput(ByVal outputs As Integer, ByVal outputIDs As Integer(), ByVal buffers As PipelineBuffer())

            If buffers.Length <> 0 Then
                outputBuffer = buffers(0)
            End If

        End Sub

        Public Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)

                ' Advance the buffer to the next row.
                While (buffer.NextRow())

                    ' Add a row to the output buffer.
                    outputBuffer.AddRow()
                    For x As Integer = 0 To inputColumnBufferIndexes.Length

                        ' Copy the data from the input buffer column to the output buffer column.
                        outputBuffer(outputColumnBufferIndexes(x)) = buffer(inputColumnBufferIndexes(x))

                    Next
                End While

            If buffer.EndOfRowset = True Then
                ' EndOfRowset on the input buffer is true.
                ' Set the end of row set on the output buffer.
                outputBuffer.SetEndOfRowset()
            End If
        End Sub
    End Class
End Namespace
```

![Integration Services 아이콘 (작은 아이콘)](../media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하십시오.

## <a name="see-also"></a>참고 항목
 [동기 출력을 사용 하 여 사용자 지정 변환 구성 요소 개발](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md) [동기 및 비동기 변환 이해](../understanding-synchronous-and-asynchronous-transformations.md) [스크립트 구성 요소를 사용 하 여 비동기 변환 만들기](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)


