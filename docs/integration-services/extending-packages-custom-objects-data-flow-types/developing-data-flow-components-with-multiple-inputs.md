---
title: "여러 입력을 지 원하는 데이터 흐름 구성 요소 개발 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects-data-flow-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 3c7b50e8-2aa6-4f6a-8db4-e8293bc21027
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2cafe3a18fbe930088347304ed758afe505771d6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="developing-data-flow-components-with-multiple-inputs"></a>여러 입력을 지원하는 데이터 흐름 구성 요소 개발
  여러 입력을 지원하는 데이터 흐름 구성 요소는 여러 입력에서 데이터가 생성되는 속도가 균일하지 않을 경우 과도한 메모리를 사용할 수 있습니다. 두 개 이상의 입력을 지 원하는 사용자 지정 데이터 흐름 구성 요소를 개발 하는 경우에 Microsoft.SqlServer.Dts.Pipeline 네임 스페이스에는 다음과 같은 멤버를 사용 하 여이 메모리가 중을 관리할 수 있습니다.  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 속성 - 사용자 지정 데이터 흐름 구성 요소에서 속도가 균일하지 않은 데이터를 관리하는 데 필요한 코드를 구현하려면 이 속성 값을 **true** 로 설정합니다.  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 메서드 - 설정한 경우이 메서드의 구현을 제공 해야 합니다는 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 속성을 **true**합니다. 그러지 않으면 데이터 흐름 엔진에서 런타임 시 예외가 발생합니다.  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 메서드 - 설정한 경우에이 메서드의 구현을 제공 해야 합니다는 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 속성을 **true** 하 고 사용자 지정 구성 요소 두 개 이상의 입력을 지원 합니다. 그러지 않으면 사용자가 세 개 이상의 입력을 연결할 경우 데이터 흐름 엔진에서 런타임 시 예외가 발생합니다.  
  
 이러한 멤버를 함께 사용하여 Microsoft에서 병합 및 병합 조인 변환을 위해 개발한 솔루션과 유사한 메모리 가중 관리 솔루션을 개발할 수 있습니다.  
  
## <a name="setting-the-supportsbackpressure-property"></a>SupportsBackPressure 속성 설정  
 값을 설정 하는 여러 입력을 지 원하는 사용자 지정 데이터 흐름 구성 요소에 대해 더 나은 메모리 관리를 구현 하는 첫 번째 단계는 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 속성을 **true** 에 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>합니다. 때의 값 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 은 **true**, 데이터 흐름 엔진 호출은 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 메서드를 두 개 이상의 입력을 호출 또한는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 메서드 실행 시.  
  
### <a name="example"></a>예제  
 다음 예제에서는의 구현에에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 의 값을 설정 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 를 **true**합니다.  
  
```csharp  
[DtsPipelineComponent(ComponentType = ComponentType.Transform,  
        DisplayName = "Shuffler",  
        Description = "Shuffle the rows from input.",  
        SupportsBackPressure = true,  
        LocalizationType = typeof(Localized),  
        IconResource = "Microsoft.Samples.SqlServer.Dts.MIBPComponent.ico")  
]  
public class Shuffler : Microsoft.SqlServer.Dts.Pipeline.PipelineComponent  
        {  
          ...  
        }  
```  
  
## <a name="implementing-the-isinputready-method"></a>IsInputReady 메서드 구현  
 값을 설정 하면는 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 속성을 **true** 에 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 개체에 대 한 구현을 제공 해야는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 의 메서드는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 클래스입니다.  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 메서드의 구현은 기본 클래스의 구현을 호출해서는 안 됩니다. 기본 클래스의 이 메서드에 대한 기본 구현은 **NotImplementedException**만 발생시킵니다.  
  
 이 메서드를 구현할 때는 구성 요소의 각 입력에 대해 요소 상태를 부울 *canProcess* 배열로 설정합니다. (입력에서 해당 ID 값으로 식별 되는 *inputIDs* 배열입니다.) 에 있는 요소의 값을 설정 하면는 *canProcess* 배열을 **true** 입력에 대해 데이터 흐름 엔진에서는 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드는 지정 된 입력에 대 한 더 많은 데이터를 제공 합니다.  
  
 추가 업스트림 데이터를 사용할 수 있는 경우에도 하나 이상의 입력에 대한 *canProcess* 배열 요소 값은 항상 **true**여야 합니다. 그렇지 않으면 처리가 중지됩니다.  
  
 데이터 흐름 엔진은 추가 데이터를 받기 위해 대기 중인 입력을 확인하기 위해 각 데이터 버퍼를 보내기 전에 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 메서드를 호출합니다. 입력이 차단되었음을 나타내는 값이 반환된 경우 데이터 흐름 엔진은 해당 입력에 대한 추가 데이터 버퍼를 구성 요소에 보내는 대신 일시적으로 캐시합니다.  
  
> [!NOTE]  
>  사용자가 작성한 코드에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 또는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 메서드를 호출하지 않아야 합니다. 이러한 메서드와 사용자가 재정의한 **PipelineComponent** 클래스의 다른 메서드는 사용자의 구성 요소를 실행할 때 데이터 흐름 엔진에서 호출합니다.  
  
### <a name="example"></a>예제  
 다음 예에서 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 메서드의 구현은 다음 조건을 충족하는 경우 입력이 추가 데이터를 받기 위해 대기 중임을 나타냅니다.  
  
-   추가 업스트림 데이터를 입력에 사용할 수 있는 경우(`!inputEOR`)  
  
-   구성 요소에서 이미 받은 버퍼에 현재 입력에 대해 처리할 수 있는 데이터가 없는 경우(`inputBuffers[inputIndex].CurrentRow() == null`)  
  
 입력이 추가 데이터를 받기 위해 대기 중인 경우 데이터 흐름 구성 요소는 해당 입력에 해당하는 **true** 배열의 요소 값을 *canProcess* 로 설정하여 이를 나타냅니다.  
  
 반면, 입력에 대해 처리할 수 있는 데이터가 구성 요소에 있는 경우 이 예는 입력 처리를 일시 중단합니다. 즉, 해당 입력에 해당하는 **false** 배열의 요소 값을 *canProcess* 로 설정합니다.  
  
```csharp  
public override void IsInputReady(int[] inputIDs, ref bool[] canProcess)  
{  
    for (int i = 0; i < inputIDs.Length; i++)  
    {  
        int inputIndex = ComponentMetaData.InputCollection.GetObjectIndexByID(inputIDs[i]);  
  
        canProcess[i] = (inputBuffers[inputIndex].CurrentRow() == null)  
            && !inputEOR[inputIndex];  
    }  
}  
```  
  
 위의 예에서는 부울 `inputEOR` 배열을 사용하여 각 입력에 사용 가능한 추가 업스트림 데이터가 있는지 여부를 나타냅니다. 이 배열 이름에서 `EOR`은 "행 집합의 끝(end of rowset)"을 나타내며 데이터 흐름 버퍼의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 속성을 참조합니다. 이 예에서 여기에 표시되지 않은 일부분인 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드는 받은 각 데이터 버퍼의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 속성 값을 확인합니다. 값 **true** 입력에 사용할 수 있는 추가 업스트림 데이터가 없음을 값과의 값을 설정 하는 예제는 `inputEOR` 배열 요소에 해당 입력에 대 한 **true**합니다. 에 대 한이 예제는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 에 해당 하는 요소의 값을 설정 하는 메서드는 *canProcess* 배열을 **false** 입력에 대 한 경우의 값은 `inputEOR` 배열 요소를 나타냅니다 입력에 대해 사용할 수 있는 추가 업스트림 데이터가 없음이 있습니다.  
  
## <a name="implementing-the-getdependentinputs-method"></a>GetDependentInputs 메서드 구현  
 사용자 지정 데이터 흐름 구성 요소가 세 개 이상의 입력을 지원하는 경우에는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 메서드에 대한 구현도 제공해야 합니다.  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 메서드의 구현은 기본 클래스의 구현을 호출해서는 안 됩니다. 기본 클래스의 이 메서드에 대한 기본 구현은 **NotImplementedException**만 발생시킵니다.  
  
 데이터 흐름 엔진은 사용자가 구성 요소에 세 개 이상의 입력을 연결한 경우에만 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 메서드를 호출합니다. 구성 요소에 입력이 두 개뿐일 때 및 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 메서드는 하나의 입력이 차단 되었음을 나타냅니다 (*canProcess* = **false**), 데이터 흐름 엔진은 다른은 입력 알고 더 많은 데이터를 수신 대기 합니다. 그러나 입력이 세 개 이상일 때 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 메서드가 하나의 입력이 차단되었음을 나타내는 경우에는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>의 추가 코드가 추가 데이터를 받기 위해 대기 중인 입력을 식별합니다.  
  
> [!NOTE]  
>  사용자가 작성한 코드에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 또는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 메서드를 호출하지 않아야 합니다. 이러한 메서드와 사용자가 재정의한 **PipelineComponent** 클래스의 다른 메서드는 사용자의 구성 요소를 실행할 때 데이터 흐름 엔진에서 호출합니다.  
  
### <a name="example"></a>예제  
 다음 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 메서드의 구현은 차단된 특정 입력에 대해 추가 데이터를 받기 위해 대기 중이므로 지정된 입력을 차단하는 입력 컬렉션을 반환합니다. 구성 요소는 차단된 입력 외에 구성 요소에서 이미 받은 버퍼에 현재 처리할 수 있는 데이터가 없는(`inputBuffers[i].CurrentRow() == null`) 입력을 확인하는 방식으로 차단된 입력을 식별합니다. 그런 다음 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 메서드에서 차단된 입력 컬렉션을 입력 ID 컬렉션으로 반환합니다.  
  
```csharp  
public override Collection<int> GetDependentInputs(int blockedInputID)  
{  
    Collection<int> currentDependencies = new Collection<int>();  
    for (int i = 0; i < ComponentMetaData.InputCollection.Count; i++)  
    {  
        if (ComponentMetaData.InputCollection[i].ID != blockedInputID  
            && inputBuffers[i].CurrentRow() == null)  
        {  
            currentDependencies.Add(ComponentMetaData.InputCollection[i].ID);  
        }  
    }  
  
    return currentDependencies;  
}  
```  
  
  

