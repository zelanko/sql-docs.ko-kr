---
title: "디자인 타임 메서드는 데이터 흐름 구성 요소 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom data flow components [Integration Services], method execution sequence
- ProcessInput method
- method execution sequence [Integration Services]
- PrimeOutput method
- data flow components [Integration Services], method execution sequence
ms.assetid: b5a121a1-b87c-441b-a42c-2cec628dc81c
caps.latest.revision: 58
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cf248d93b1b1e581c3315cde9b1f96edc58bcfde
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="design-time-methods-of-a-data-flow-component"></a>데이터 흐름 구성 요소의 디자인 타임 메서드
  실행 전 데이터 흐름 태스크에서 증분 변경 작업이 수행될 때 해당 데이터 흐름 태스크는 디자인 타임 상태에 있다고 합니다. 변경 작업에는 구성 요소의 추가 또는 제거, 구성 요소를 연결하는 경로 개체의 추가 또는 제거, 구성 요소의 메타데이터 변경 등이 포함됩니다. 메타데이터가 변경되면 구성 요소에서는 변경 내용을 모니터링하고 그에 따라 반응할 수 있습니다. 예를 들어 변경에 대한 응답으로 구성 요소에서는 특정 변경 작업을 허용하지 않거나 추가 변경 작업을 수행할 수 있습니다. 디자인 타임에 디자이너는 디자인 타임 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 인터페이스를 통해 구성 요소와 상호 작용합니다.  
  
## <a name="design-time-implementation"></a>디자인 타임 구현  
 구성 요소의 디자인 타임 인터페이스는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 인터페이스에 의해 기술됩니다. 이 인터페이스를 명시적으로 구현하지는 않지만 이 인터페이스에 정의된 메서드를 잘 알고 있으면 구성 요소의 디자인 타임 인스턴스에 해당하는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 기본 클래스의 메서드를 쉽게 이해할 수 있습니다.  
  
 구성 요소를 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에 로드하면 구성 요소의 디자인 타임 인스턴스가 인스턴스화되고 구성 요소를 편집할 때 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 인터페이스의 메서드가 호출됩니다. 기본 클래스의 구현을 사용하여 구성 요소에서 필요한 메서드만 재정의할 수 있습니다. 대부분의 경우 이러한 메서드를 재정의하여 구성 요소가 적절하지 않게 편집되는 것을 방지할 수 있습니다. 예를 들어 사용자가 구성 요소에 출력을 추가할 수 없도록 하려면 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.InsertOutput%2A> 메서드를 재정의합니다. 이 메서드를 재정의하지 않고 기본 클래스에 구현된 메서드를 호출하면 구성 요소에 출력이 추가됩니다.  
  
 구성 요소의 목적 또는 기능에 관계없이 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 메서드를 재정의해야 합니다. 에 대 한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A>, 참조 [유효성을 검사 하는 데이터 흐름 구성 요소](../../../integration-services/extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md)합니다.  
  
## <a name="providecomponentproperties-method"></a>ProvideComponentProperties 메서드  
 구성 요소는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 메서드에서 초기화됩니다. 이 메서드는 클래스 생성자와 비슷하며 데이터 흐름 태스크에 구성 요소를 추가하면 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 이 메서드가 호출됩니다. 구성 요소 개발자는 이 메서드가 호출될 때 구성 요소의 입력, 출력 및 사용자 지정 속성을 만들고 초기화해야 합니다. <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 메서드가 생성자와 다른 점은 구성 요소의 디자인 타임 인스턴스나 런타임 인스턴스가 인스턴스화될 때마다 호출되지는 않는다는 점입니다.  
  
 이 메서드의 기본 클래스 구현에서는 구성 요소에 입력 및 출력을 추가하고 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> 속성에 입력의 ID를 할당합니다. 그러나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 기본 클래스에 의해 추가된 입력 및 출력 개체에는 이름이 지정되지 않습니다. 입력이 포함 된 구성 요소를 포함 하는 패키지 또는 출력 개체 인 Name 속성이 설정 되어 있지 성공적으로 로드 되지 않습니다. 따라서 기본 구현을 사용 하는 경우 값을 할당 해야 명시적으로 기본 입력 및 출력의 Name 속성에 있습니다.  
  
```csharp  
public override void ProvideComponentProperties()  
{  
    /// TODO: Reset the component.  
    /// TODO: Add custom properties.  
    /// TODO: Add input objects.  
    /// TODO: Add output objects.  
}  
```  
  
```vb  
Public Overrides Sub ProvideComponentProperties()  
    ' TODO: Reset the component.  
    ' TODO: Add custom properties.  
    ' TODO: Add input objects.  
    ' TODO: Add output objects.  
End Sub  
```  
  
### <a name="creating-custom-properties"></a>사용자 지정 속성 만들기  
 구성 요소 개발자는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 메서드가 호출될 때 구성 요소에 사용자 지정 속성(<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100>)을 추가해야 합니다. 사용자 지정 속성에는 데이터 형식 속성이 없습니다. 사용자 지정 속성의 데이터 형식은 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.Value%2A> 속성에 할당한 값의 데이터 형식에 따라 설정됩니다. 그러나 사용자 지정 속성에 초기 값을 할당한 후에는 데이터 형식이 다른 값을 할당할 수 없습니다.  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100> 인터페이스 형식의 속성 값에 대 한 지원이 제한 **개체**합니다. 사용자 지정 속성의 값으로는 문자열 또는 정수와 같은 단순 형식의 배열만 저장할 수 있습니다.  
  
 사용자 지정 속성의 값을 설정 하 여 속성 식의 지원 하도록 지정할 수는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.ExpressionType%2A> 속성을 **CPET_NOTIFY** 에서 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSCustomPropertyExpressionType> 다음 예제 에서처럼 열거형입니다. 사용자가 입력한 속성 식을 처리하거나 유효성을 검사하기 위한 코드를 추가할 필요는 없습니다. 속성의 기본값을 설정하고 해당 값의 유효성을 검사한 다음 값을 정상적으로 읽고 사용할 수 있습니다.  
  
```csharp  
IDTSCustomProperty100 myCustomProperty;  
...  
myCustomProperty.ExpressionType = DTSCustomPropertyExpressionType.CPET_NOTIFY;  
```  
  
```vb  
Dim myCustomProperty As IDTSCustomProperty100  
...  
myCustomProperty.ExpressionType = DTSCustomPropertyExpressionType.CPET_NOTIFY  
```  
  
 열거형에서 사용 하 여 사용자 지정 속성 값을 선택 하려면 사용자가 제한할 수 있습니다는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.TypeConverter%2A> 속성을 라는 공용 열거형을 정의 했다고 가정 하는 다음 예에서 같이 **MyValidValues**합니다.  
  
```csharp  
IDTSCustomProperty100 customProperty = outputColumn.CustomPropertyCollection.New();  
customProperty.Name = "My Custom Property";  
// This line associates the type with the custom property.  
customProperty.TypeConverter = typeof(MyValidValues).AssemblyQualifiedName;  
// Now you can use the enumeration values directly.  
customProperty.Value = MyValidValues.ValueOne;    
```  
  
```vb  
Dim customProperty As IDTSCustomProperty100 = outputColumn.CustomPropertyCollection.New   
customProperty.Name = "My Custom Property"   
' This line associates the type with the custom property.  
customProperty.TypeConverter = GetType(MyValidValues).AssemblyQualifiedName   
' Now you can use the enumeration values directly.  
customProperty.Value = MyValidValues.ValueOne  
```  
  
 자세한 내용은 "일반화 된 형식 변환" 및 "형식 변환기 구현"의 참조는 [MSDN Library](http://go.microsoft.com/fwlink/?LinkId=7022)합니다.  
  
 다음 예와 같이 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A> 속성을 사용하여 사용자 지정 속성의 값에 사용자 지정 편집기 대화 상자를 지정할 수 있습니다. 먼저 만들어야 사용자 지정 형식에서 상속 되는 편집기 **System.Drawing.Design.UITypeEditor**, 필요에 맞는 기존 UI 형식 편집기 클래스를 찾을 수 없습니다.  
  
```csharp  
public class MyCustomTypeEditor : UITypeEditor  
{  
...  
}  
```  
  
```vb  
Public Class MyCustomTypeEditor  
  Inherits UITypeEditor   
  ...  
End Class  
```  
  
 그런 다음 이 클래스를 사용자 지정 속성의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A> 속성 값으로 지정합니다.  
  
```csharp  
IDTSCustomProperty100 customProperty = outputColumn.CustomPropertyCollection.New();  
customProperty.Name = "My Custom Property";  
// This line associates the editor with the custom property.  
customProperty.UITypeEditor = typeof(MyCustomTypeEditor).AssemblyQualifiedName;  
```  
  
```vb  
Dim customProperty As IDTSCustomProperty100 = outputColumn.CustomPropertyCollection.New   
customProperty.Name = "My Custom Property"   
' This line associates the editor with the custom property.  
customProperty.UITypeEditor = GetType(MyCustomTypeEditor).AssemblyQualifiedName  
```  
  
 "형식 UI 편집기 구현"에 대 한 자세한 내용은 참조는 [MSDN Library](http://go.microsoft.com/fwlink/?LinkId=7022)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 흐름 구성 요소의 런타임 메서드](../../../integration-services/extending-packages-custom-objects/data-flow/run-time-methods-of-a-data-flow-component.md)  
  
  

