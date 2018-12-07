---
title: 동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom data flow components [Integration Services], transformation components
- ProcessInput method
- buffer allocations [Integration Services]
- synchronous outputs [Integration Services]
- transformation components [Integration Services]
- output columns [Integration Services]
- data flow components [Integration Services], transformation components
ms.assetid: b694d21f-9919-402d-9192-666c6449b0b7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1e38ff05819e3ca6b8717ae4c19b554bae57861b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542534"
---
# <a name="developing-a-custom-transformation-component-with-synchronous-outputs"></a>동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발
  동기 출력을 사용하는 변환 구성 요소는 업스트림 구성 요소에서 행을 받고, 이러한 행을 다운스트림 구성 요소에 전달할 때 해당 행의 열 값을 읽거나 수정합니다. 또한 업스트림 구성 요소가 제공한 열에서 파생된 추가 출력 열도 정의할 수 있지만 데이터 흐름에 행을 추가하지는 않습니다. 동기 구성 요소와 비동기 구성 요소 간의 차이점에 대한 자세한 내용은 [동기 및 비동기 변환 이해](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)를 참조하세요.  
  
 이러한 종류의 구성 요소는 데이터가 구성 요소에 제공될 때 인라인으로 수정되는 태스크와 구성 요소에서 행을 처리하기 전에 모든 행을 볼 필요가 없는 태스크에 적합합니다. 동기 출력을 사용하는 변환은 일반적으로 외부 데이터 원본에 연결하거나 외부 메타데이터 열을 관리하거나 출력 버퍼에 행을 추가하지 않으므로 개발하기가 가장 쉬운 구성 요소입니다.  
  
 동기 출력을 사용하는 변환 구성 요소를 만들려면 구성 요소에 대해 선택한 업스트림 열을 포함할 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>과 구성 요소에서 만드는 파생 열을 포함할 수 있는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 개체를 추가해야 합니다. 또한 디자인 타임 메서드를 구현하고, 실행 중 들어오는 버퍼 행의 열을 읽거나 수정하는 코드를 제공해야 합니다.  
  
 이 섹션에서는 사용자 지정 변환 구성 요소를 구현하는 데 필요한 정보를 제공하고 개념을 보다 쉽게 이해할 수 있도록 코드 예를 제공합니다.  
  
## <a name="design-time"></a>디자인 타임  
 이 구성 요소의 디자인 타임 코드에서는 입력 및 출력을 만들고, 구성 요소에서 생성하는 다른 출력 열을 추가하고, 구성 요소의 구성에 대한 유효성을 검사해야 합니다.  
  
### <a name="creating-the-component"></a>구성 요소 만들기  
 구성 요소의 입력, 출력 및 사용자 지정 속성은 일반적으로 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 메서드 실행 중에 만들어집니다. 동기 출력을 사용하는 변환 구성 요소의 입력 및 출력을 추가하는 방법에는 두 가지가 있습니다. 메서드의 기본 클래스 구현을 사용한 다음 만들어진 기본 입력 및 출력을 수정하거나, 개발자가 직접 입력 및 출력을 명시적으로 추가할 수 있습니다.  
  
 다음 코드 예에서는 입력 및 출력 개체를 명시적으로 추가하는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>의 구현을 보여 줍니다. 동일한 동작을 수행하는 기본 클래스에 대한 호출은 주석에 포함되어 있습니다.  
  
```csharp  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "SynchronousComponent", ComponentType = ComponentType.Transform)]  
    public class SyncComponent : PipelineComponent  
    {  
  
        public override void ProvideComponentProperties()  
        {  
            // Add the input.  
            IDTSInput100 input = ComponentMetaData.InputCollection.New();  
            input.Name = "Input";  
  
            // Add the output.  
            IDTSOutput100 output = ComponentMetaData.OutputCollection.New();  
            output.Name = "Output";  
            output.SynchronousInputID = input.ID;  
  
            // Alternatively, you can let the base class add the input and output  
            // and set the SynchronousInputID of the output to the ID of the input.  
            // base.ProvideComponentProperties();  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsPipelineComponent(DisplayName:="SynchronousComponent", ComponentType:=ComponentType.Transform)> _  
Public Class SyncComponent  
    Inherits PipelineComponent  
  
    Public Overrides Sub ProvideComponentProperties()  
  
        ' Add the input.  
        Dim input As IDTSInput100 = ComponentMetaData.InputCollection.New()  
        input.Name = "Input"  
  
        ' Add the output.  
        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.New()  
        output.Name = "Output"  
        output.SynchronousInputID = Input.ID  
  
        ' Alternatively, you can let the base class add the input and output  
        ' and set the SynchronousInputID of the output to the ID of the input.  
        ' base.ProvideComponentProperties();  
  
    End Sub  
  
End Class  
```  
  
### <a name="creating-and-configuring-output-columns"></a>출력 열 만들기 및 구성  
 동기 출력을 사용하는 변환 구성 요소에서는 버퍼에 행을 추가하지는 않지만 다른 출력 열을 해당 출력에 추가할 수 있습니다. 일반적으로 구성 요소에서 출력 열을 추가할 경우 새 출력 열의 값은 런타임에 업스트림 구성 요소에서 해당 구성 요소에 제공한 열 중 하나 이상의 열에 포함된 데이터로부터 파생됩니다.  
  
 출력 열이 만들어진 후에는 해당 데이터 형식 속성을 설정해야 합니다. 출력 열의 데이터 형식 속성을 설정하는 작업은 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.SetDataTypeProperties%2A> 메서드 호출을 통해 수행되며 이 작업에는 특수한 처리가 필요합니다. <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Length%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Precision%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.CodePage%2A> 속성은 각기 다른 속성의 설정에 따라 달라지기 때문에 개별적으로 읽기 전용이며 이 때문에 이 메서드가 필요합니다. 이 메서드는 이러한 속성의 값이 일관성 있게 설정되도록 하며 데이터 흐름 태스크에서는 해당 값이 올바르게 설정되어 있는지 확인합니다.  
  
 열의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A>은 다른 속성에 대해 설정되는 값을 결정합니다. 다음 표에서는 각 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A>의 종속 속성에 대한 요구 사항을 보여 줍니다. 이 목록에 포함되지 않은 데이터 형식의 종속 속성은 0으로 설정됩니다.  
  
|DataType|길이|소수 자릿수|전체 자릿수|CodePage|  
|--------------|------------|-----------|---------------|--------------|  
|DT_DECIMAL|0|0보다 크고 28보다 작거나 같습니다.|0|0|  
|DT_CY|0|0|0|0|  
|DT_NUMERIC|0|0보다 크고 28보다 작거나 같으며 Precision보다 작습니다.|1보다 크거나 같고 38보다 작거나 같습니다.|0|  
|DT_BYTES|0보다 큽니다.|0|0|0|  
|DT_STR|0보다 크고 8000보다 작습니다.|0|0|0이 아니며 올바른 코드 페이지가 아닙니다.|  
|DT_WSTR|0보다 크고 4000보다 작습니다.|0|0|0|  
  
 데이터 형식 속성에 대한 제한 사항은 출력 열의 데이터 형식을 기준으로 하므로 관리되는 형식을 사용할 때는 올바른 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식을 선택해야 합니다. 기본 클래스에서는 관리되는 구성 요소 개발자가 관리되는 형식의 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 데이터 형식을 선택하는 데 도움이 되는 세 개의 도우미 메서드 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ConvertBufferDataTypeToFitManaged%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferTypeToDataRecordType%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.DataRecordTypeToBufferType%2A>을 제공합니다. 이러한 메서드는 관리되는 데이터 형식을 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 데이터 형식으로 변환하거나 그 반대로 변환합니다.  
  
## <a name="run-time"></a>런타임  
 일반적으로 구성 요소의 런타임 부분에 대한 구현은 버퍼에서 구성 요소의 입력 및 출력 열을 찾는 태스크와 들어오는 버퍼 행에서 이러한 열의 값을 읽거나 쓰는 태스크로 분류됩니다.  
  
### <a name="locating-columns-in-the-buffer"></a>버퍼에서 열 찾기  
 실행 중 구성 요소에 제공되는 버퍼의 열 수는 구성 요소의 입력 또는 출력 컬렉션에 있는 열 수를 초과할 수 있습니다. 이는 각 버퍼에 데이터 흐름의 구성 요소에 정의된 출력 열이 모두 들어 있기 때문입니다. 버퍼의 열 수가 입력 또는 출력의 열 수와 정확하게 일치하도록 하려면 구성 요소 개발자가 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A>의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> 메서드를 사용해야 합니다. 이 메서드는 지정된 버퍼에서 열의 계보 ID로 열을 찾습니다. 런타임에 처음으로 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 속성을 사용할 수 있게 되는 메서드는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A>이므로 일반적으로 이 메서드가 실행될 때 열을 찾을 수 있습니다.  
  
 다음 코드 예에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 실행 중 입력 및 출력 열 컬렉션에서 열의 인덱스를 찾는 구성 요소를 보여 줍니다. 열 인덱스는 정수 배열에 저장되며 구성 요소에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 실행 중 열 인덱스에 액세스할 수 있습니다.  
  
```csharp  
int []inputColumns;  
int []outputColumns;  
  
public override void PreExecute()  
{  
    IDTSInput100 input = ComponentMetaData.InputCollection[0];  
    IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
  
    inputColumns = new int[input.InputColumnCollection.Count];  
    outputColumns = new int[output.OutputColumnCollection.Count];  
  
    for(int col=0; col < input.InputColumnCollection.Count; col++)  
    {  
        IDTSInputColumn100 inputColumn = input.InputColumnCollection[col];  
        inputColumns[col] = BufferManager.FindColumnByLineageID(input.Buffer, inputColumn.LineageID);  
    }  
  
    for(int col=0; col < output.OutputColumnCollection.Count; col++)  
    {  
        IDTSOutputColumn100 outputColumn = output.OutputColumnCollection[col];  
        outputColumns[col] = BufferManager.FindColumnByLineageID(input.Buffer, outputColumn.LineageID);  
    }  
  
}  
```  
  
```vb  
Public Overrides Sub PreExecute()  
  
    Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)  
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
  
    ReDim inputColumns(input.InputColumnCollection.Count)  
    ReDim outputColumns(output.OutputColumnCollection.Count)  
  
    For col As Integer = 0 To input.InputColumnCollection.Count  
  
        Dim inputColumn As IDTSInputColumn100 = input.InputColumnCollection(col)  
        inputColumns(col) = BufferManager.FindColumnByLineageID(input.Buffer, inputColumn.LineageID)  
    Next  
  
    For col As Integer = 0 To output.OutputColumnCollection.Count  
  
        Dim outputColumn As IDTSOutputColumn100 = output.OutputColumnCollection(col)  
        outputColumns(col) = BufferManager.FindColumnByLineageID(input.Buffer, outputColumn.LineageID)  
    Next  
  
End Sub  
```  
  
### <a name="processing-rows"></a>행 처리  
 구성 요소는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 메서드에서 행 및 열이 들어 있는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 개체를 받습니다. 이 메서드가 실행되는 동안에는 버퍼의 행을 반복하고 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 실행 중 식별된 열을 읽고 수정합니다. 이 메서드는 업스트림 구성 요소에서 더 이상 행을 제공하지 않을 때까지 데이터 흐름 태스크에서 반복적으로 호출됩니다.  
  
 버퍼의 개별 열은 배열 인덱서 액세스 메서드를 사용하거나 **Get** 또는 **Set** 메서드 중 하나를 사용하여 읽거나 쓸 수 있습니다. **Get** 및 **Set** 메서드가 보다 효율적이므로 버퍼에 있는 열의 데이터 형식을 알고 있는 경우에는 이 두 메서드를 사용해야 합니다.  
  
 다음 코드 예에서는 들어오는 행을 처리하는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드의 구현을 보여 줍니다.  
  
```csharp  
public override void ProcessInput( int InputID, PipelineBuffer buffer)  
{  
       while( buffer.NextRow())  
       {  
            for(int x=0; x < inputColumns.Length;x++)  
            {  
                if(!buffer.IsNull(inputColumns[x]))  
                {  
                    object columnData = buffer[inputColumns[x]];  
                    // TODO: Modify the column data.  
                    buffer[inputColumns[x]] = columnData;  
                }  
            }  
  
      }  
}  
```  
  
```vb  
Public Overrides Sub ProcessInput(ByVal InputID As Integer, ByVal buffer As PipelineBuffer)  
  
        While (buffer.NextRow())  
  
            For x As Integer = 0 To inputColumns.Length  
  
                if buffer.IsNull(inputColumns(x)) = false then  
  
                    Dim columnData As Object = buffer(inputColumns(x))  
                    ' TODO: Modify the column data.  
                    buffer(inputColumns(x)) = columnData  
  
                End If  
            Next  
  
        End While  
End Sub  
```  
  
## <a name="sample"></a>예제  
 다음 예제에서는 동기 출력을 사용하며 모든 문자열 열의 값을 대문자로 변환하는 간단한 변환 구성 요소를 보여 줍니다. 이 예제는 이 항목에 설명된 메서드 및 기능의 일부를 보여 줍니다. 여기에서는 동기 출력을 사용하는 모든 사용자 지정 변환 구성 요소에서 재정의해야 하는 중요한 메서드를 보여 주지만 디자인 타임 유효성 검사를 위한 코드는 포함하지 않습니다.  
  
```csharp  
using System;  
using System.Collections;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
namespace Uppercase  
{  
  [DtsPipelineComponent(DisplayName = "Uppercase")]  
  public class Uppercase : PipelineComponent  
  {  
    ArrayList m_ColumnIndexList = new ArrayList();  
  
    public override void ProvideComponentProperties()  
    {  
      base.ProvideComponentProperties();  
      ComponentMetaData.InputCollection[0].Name = "Uppercase Input";  
      ComponentMetaData.OutputCollection[0].Name = "Uppercase Output";  
    }  
  
    public override void PreExecute()  
    {  
      IDTSInput100 input = ComponentMetaData.InputCollection[0];  
      IDTSInputColumnCollection100 inputColumns = input.InputColumnCollection;  
  
      foreach (IDTSInputColumn100 column in inputColumns)  
      {  
        if (column.DataType == DataType.DT_STR || column.DataType == DataType.DT_WSTR)  
        {  
          m_ColumnIndexList.Add((int)BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID));  
        }  
      }  
    }  
  
    public override void ProcessInput(int inputID, PipelineBuffer buffer)  
    {  
      while (buffer.NextRow())  
      {  
        foreach (int columnIndex in m_ColumnIndexList)  
        {  
          string str = buffer.GetString(columnIndex);  
          buffer.SetString(columnIndex, str.ToUpper());  
        }  
      }  
    }  
  }  
}  
```  
  
```vb  
Imports System   
Imports System.Collections   
Imports Microsoft.SqlServer.Dts.Pipeline   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper   
Namespace Uppercase   
  
 <DtsPipelineComponent(DisplayName="Uppercase")> _   
 Public Class Uppercase   
 Inherits PipelineComponent   
   Private m_ColumnIndexList As ArrayList = New ArrayList   
  
   Public  Overrides Sub ProvideComponentProperties()   
     MyBase.ProvideComponentProperties   
     ComponentMetaData.InputCollection(0).Name = "Uppercase Input"   
     ComponentMetaData.OutputCollection(0).Name = "Uppercase Output"   
   End Sub   
  
   Public  Overrides Sub PreExecute()   
     Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)   
     Dim inputColumns As IDTSInputColumnCollection100 = input.InputColumnCollection   
     For Each column As IDTSInputColumn100 In inputColumns   
       If column.DataType = DataType.DT_STR OrElse column.DataType = DataType.DT_WSTR Then   
         m_ColumnIndexList.Add(CType(BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID), Integer))   
       End If   
     Next   
   End Sub   
  
   Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)   
     While buffer.NextRow   
       For Each columnIndex As Integer In m_ColumnIndexList   
         Dim str As String = buffer.GetString(columnIndex)   
         buffer.SetString(columnIndex, str.ToUpper)   
       Next   
     End While   
   End Sub   
 End Class   
End Namespace  
```  
  
## <a name="see-also"></a>참고 항목  
 [비동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)   
 [동기 및 비동기 변환 이해](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)   
 [스크립트 구성 요소를 사용하여 동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
  
  
