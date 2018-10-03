---
title: 데이터 흐름 구성 요소 유효성 검사 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ReinitializeMetaData method
- Validate method
- component validation [Integration Services]
- custom data flow components [Integration Services], validating
- validation [Integration Services], components
- data flow components [Integration Services], validating
- validation [Integration Services]
ms.assetid: 1a7d5925-b387-4e31-af7f-c7f3c5151040
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8c25471732d4be4f241689c6c2abb3d4dc4d0672
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789631"
---
# <a name="validating-a-data-flow-component"></a>데이터 흐름 구성 요소의 유효성 검사
  <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 기본 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 메서드는 올바르게 구성되지 않은 구성 요소가 실행되는 것을 방지하기 위해 제공됩니다. 이 메서드를 사용하여 구성 요소에 입력 및 출력 개체 수가 필요한 만큼 있는지, 구성 요소의 사용자 지정 속성 값이 허용되는 값인지, 필요한 경우 연결이 지정되어 있는지를 확인할 수 있습니다. 또한 이 메서드를 사용하여 입력 및 출력 컬렉션의 열 데이터 형식이 올바른지와 각 열의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType>이 해당 구성 요소에 적절하게 설정되어 있는지 확인할 수 있습니다. 기본 클래스 구현은 유효성 검사 프로세스에서 구성 요소의 입력 열 컬렉션을 검사하고 컬렉션의 각 열이 업스트림 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputCollection100>에 있는 열을 참조하는지 확인하는 데 유용합니다.  
  
## <a name="validate-method"></a>Validate 메서드  
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 메서드는 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 구성 요소를 편집할 때 반복적으로 호출됩니다. <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus> 열거형의 반환 값을 통해 또는 경고 및 오류를 게시하여 구성 요소의 디자이너와 사용자에게 피드백을 제공할 수 있습니다. <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus> 열거형에는 다양한 오류 단계를 나타내는 세 개의 값과 구성 요소가 올바르게 구성되어 있고 실행할 수 있는 상태인지를 나타내는 네 번째 값 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_ISVALID>가 포함되어 있습니다.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_NEEDSNEWMETADATA> 값은 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A>에 오류가 있는지와 해당 구성 요소에서 오류를 복구할 수 있는지를 나타냅니다. 구성 요소에서 복구할 수 없는 메타데이터 오류가 발생하는 경우에는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 메서드에서 오류를 수정하면 안 되며 유효성 검사 도중 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A>를 수정해서도 안 됩니다. 대신 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 메서드에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_NEEDSNEWMETADATA>만 반환해야 하고, 구성 요소에서는 이 섹션의 뒷부분에 설명된 대로 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 메서드가 호출될 때 오류를 복구해야 합니다.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_ISBROKEN> 값은 디자이너에서 구성 요소를 편집하는 방법으로는 해결할 수 없는 오류가 구성 요소에 있음을 나타냅니다. 이 오류는 일반적으로 사용자 지정 속성 또는 필요한 연결이 지정되지 않았거나 올바르게 설정되지 않은 경우에 발생합니다.  
  
 최종 오류 값은 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_ISCORRUPT>입니다. 이 값은 패키지 XML을 편집하거나 개체 모델을 사용하여 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> 속성을 직접 수정한 경우에만 발생하는 오류를 구성 요소에서 발견했음을 나타냅니다. 이러한 종류의 오류는 예를 들어 구성 요소에서 입력을 하나만 추가했는데 유효성 검사 과정에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A>에 둘 이상의 입력이 있음을 발견한 경우에 발생합니다. 이 반환 값을 생성하는 오류는 **고급 편집기** 대화 상자에서 **다시 설정** 단추를 사용하여 구성 요소를 다시 설정하는 방법으로만 복구할 수 있습니다.  
  
 구성 요소에서는 오류 값을 반환할 뿐 아니라 유효성 검사 도중 경고 또는 오류를 게시하여 피드백을 제공하기도 합니다. 이 메커니즘은 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A> 메서드에서 제공합니다. 이러한 메서드가 호출되면 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]의 **오류 목록** 창에 해당 이벤트가 게시됩니다. 그런 다음 구성 요소 개발자는 발생한 오류와 적절한 경우 이를 수정하는 방법에 대한 직접적인 피드백을 사용자에게 제공할 수 있습니다.  
  
 다음 코드 예에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A>의 재정의된 구현을 보여 줍니다.  
  
```csharp  
public override DTSValidationStatus Validate()  
{  
    bool pbCancel = false;  
  
    // Validate that there is one input.  
    if (ComponentMetaData.InputCollection.Count != 1)  
    {  
    ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of inputs.", "", 0, out pbCancel);  
    return DTSValidationStatus.VS_ISCORRUPT;  
    }  
  
    // Validate that the UserName custom property is set.  
    if (ComponentMetaData.CustomPropertyCollection["UserName"].Value == null || ((string)ComponentMetaData.CustomPropertyCollection["UserName"].Value).Length == 0)  
    {  
        ComponentMetaData.FireError(0, ComponentMetaData.Name, "The UserName property must be set.", "", 0, out pbCancel);  
        return DTSValidationStatus.VS_ISBROKEN;  
    }  
  
    // Validate that there is one output.  
    if (ComponentMetaData.OutputCollection.Count != 1)  
    {  
        ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of outputs.", "", 0, out pbCancel);  
        return DTSValidationStatus.VS_ISCORRUPT;  
    }  
  
    // Let the base class verify that the input column reflects the output   
    // of the upstream component.  
    return base.Validate();  
}  
```  
  
```vb  
Public  Overrides Function Validate() As DTSValidationStatus   
  
 Dim pbCancel As Boolean = False  
  
 ' Validate that there is one input.  
 If Not (ComponentMetaData.InputCollection.Count = 1) Then   
   ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of inputs.", "", 0, pbCancel)   
   Return DTSValidationStatus.VS_ISCORRUPT   
 End If   
  
 ' Validate that the UserName custom property is set.  
 If ComponentMetaData.CustomPropertyCollection("UserName").Value Is Nothing OrElse CType(ComponentMetaData.CustomPropertyCollection("UserName").Value, String).Length = 0 Then   
   ComponentMetaData.FireError(0, ComponentMetaData.Name, "The UserName property must be set.", "", 0, pbCancel)   
   Return DTSValidationStatus.VS_ISBROKEN   
 End If   
  
 ' Validate that there is one output.  
 If Not (ComponentMetaData.OutputCollection.Count = 1) Then   
   ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of outputs.", "", 0, pbCancel)   
   Return DTSValidationStatus.VS_ISCORRUPT   
 End If   
  
 ' Let the base class verify that the input column reflects the output   
 ' of the upstream component.  
  
 Return MyBase.Validate   
  
End Function  
```  
  
## <a name="reinitializemetadata-method"></a>ReinitializeMetaData 메서드  
 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 메서드는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_NEEDSNEWMETADATA> 메서드에서 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A>를 반환하는 구성 요소를 편집할 때마다 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 호출됩니다. 구성 요소에는 유효성 검사 도중 구성 요소에 의해 식별된 문제를 검색하고 수정하는 코드가 포함되어야 합니다.  
  
 다음 예에서는 유효성 검사 도중 문제를 검색하고 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 메서드에서 이러한 오류를 수정하는 구성 요소를 보여 줍니다.  
  
```csharp  
private bool areInputColumnsValid = true;  
public override DTSValidationStatus Validate()  
{  
    IDTSInput100 input = ComponentMetaData.InputCollection[0];  
    IDTSVirtualInput100 vInput = input.GetVirtualInput();  
  
    bool Cancel = false;  
    foreach (IDTSInputColumn100 column in input.InputColumnCollection)  
    {  
        try  
        {  
            IDTSVirtualInputColumn100 vColumn = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID);  
        }  
        catch  
        {  
            ComponentMetaData.FireError(0, ComponentMetaData.Name, "The input column " + column.IdentificationString + " does not match a column in the upstream component.", "", 0, out Cancel);  
            areInputColumnsValid = false;  
            return DTSValidationStatus.VS_NEEDSNEWMETADATA;  
        }  
    }  
  
    return DTSValidationStatus.VS_ISVALID;  
}  
public override void ReinitializeMetaData()  
{  
    if (!areInputColumnsValid)  
    {  
        IDTSInput100 input = ComponentMetaData.InputCollection[0];  
        IDTSVirtualInput100 vInput = input.GetVirtualInput();  
  
        foreach (IDTSInputColumn100 column in input.InputColumnCollection)  
        {  
            IDTSVirtualInputColumn100 vColumn = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID);  
  
            if (vColumn == null)  
                input.InputColumnCollection.RemoveObjectByID(column.ID);  
        }  
        areInputColumnsValid = true;  
    }  
}  
```  
  
```vb  
Private areInputColumnsValid As Boolean = True   
  
Public  Overrides Function Validate() As DTSValidationStatus   
 Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)   
 Dim vInput As IDTSVirtualInput100 = input.GetVirtualInput   
 Dim Cancel As Boolean = False   
 For Each column As IDTSInputColumn100 In input.InputColumnCollection   
   Try   
     Dim vColumn As IDTSVirtualInputColumn100 = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID)   
   Catch   
     ComponentMetaData.FireError(0, ComponentMetaData.Name, "The input column " + column.IdentificationString + " does not match a column in the upstream component.", "", 0, Cancel)   
     areInputColumnsValid = False   
     Return DTSValidationStatus.VS_NEEDSNEWMETADATA   
   End Try   
 Next   
 Return DTSValidationStatus.VS_ISVALID   
End Function   
  
Public  Overrides Sub ReinitializeMetaData()   
 If Not areInputColumnsValid Then   
   Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)   
   Dim vInput As IDTSVirtualInput100 = input.GetVirtualInput   
   For Each column As IDTSInputColumn100 In input.InputColumnCollection   
     Dim vColumn As IDTSVirtualInputColumn100 = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID)   
     If vColumn Is Nothing Then   
       input.InputColumnCollection.RemoveObjectByID(column.ID)   
     End If   
   Next   
   areInputColumnsValid = True   
 End If   
End Sub  
```  
  
