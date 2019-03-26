---
title: 스크립트 구성 요소를 사용하여 비동기 변환 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- asynchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: 0d814404-21e4-4a68-894c-96fa47ab25ae
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d24b53d8f94f2478198aa8678d309703d0af274e
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58282971"
---
# <a name="creating-an-asynchronous-transformation-with-the-script-component"></a>스크립트 구성 요소를 사용하여 비동기 변환 만들기
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 데이터 흐름에서 변환 구성 요소를 사용하여 데이터가 원본에서 대상으로 전달될 때 데이터를 수정하고 분석할 수 있습니다. 동기 출력을 사용하는 변환에서는 각 입력 행이 이 구성 요소를 통해 전달될 때 이를 처리합니다. 비동기 출력을 사용하는 변환에서는 입력 행을 모두 받을 때까지 기다렸다가 처리를 완료하거나 입력 행을 모두 받기 전에 일부 행을 출력할 수 있습니다. 이 항목에서는 비동기 변환에 대해 설명합니다. 처리에 동기 변환이 필요한 경우에는 [스크립트 구성 요소를 사용하여 동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)를 참조하세요. 동기 구성 요소와 비동기 구성 요소 간 차이에 대한 자세한 내용은 [동기 및 비동기 변환 이해](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)를 참조하세요.  
  
 스크립트 구성 요소에 대한 개요는 [스크립트 구성 요소를 사용하여 데이터 흐름 확장](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)을 참조하세요.  
  
 스크립트 구성 요소 및 해당 구성 요소가 생성하는 인프라 코드를 사용하면 사용자 지정 데이터 흐름 구성 요소를 개발하는 과정이 간단해집니다. 하지만 스크립트 구성 요소의 작동 방식을 이해하려면 [사용자 지정 데이터 흐름 구성 요소 개발](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) 섹션과 이 섹션의 [동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)을 통해 사용자 지정 데이터 흐름 구성 요소를 개발하는 데 필요한 단계를 파악하는 것이 좋습니다.  
  
## <a name="getting-started-with-an-asynchronous-transformation-component"></a>비동기 변환 구성 요소 시작  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 데이터 흐름 탭에 스크립트 구성 요소를 추가하면 구성 요소를 원본, 변환 또는 대상으로 미리 구성하기 위한 **스크립트 구성 요소 유형 선택** 대화 상자가 나타납니다. 이 대화 상자에서 **변환**을 선택합니다.  
  
## <a name="configuring-an-asynchronous-transformation-component-in-metadata-design-mode"></a>메타데이터 디자인 모드에서 비동기 변환 구성 요소 구성  
 변환 구성 요소를 만드는 옵션을 선택한 후에는 **스크립트 변환 편집기**를 사용하여 구성 요소를 구성합니다. 자세한 내용은 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)을 참조하세요.  
  
 스크립트 구성 요소에서 사용할 스크립트 언어를 선택하려면 **스크립트 변환 편집기** 대화 상자의 **스크립트** 페이지에서 **ScriptLanguage** 속성을 설정합니다.  
  
> [!NOTE]  
>  스크립트 구성 요소에 대한 기본 스크립트 언어를 설정하려면 **옵션** 대화 상자의 **일반** 페이지에서 **스크립트 언어** 옵션을 사용합니다. 자세한 내용은 [General Page](../general-page-of-integration-services-designers-options.md)을 참조하세요.  
  
 데이터 흐름 변환 구성 요소는 하나의 입력을 사용하며 하나 이상의 출력을 지원합니다. 구성 요소의 입력과 출력을 구성하는 것은 사용자 지정 스크립트를 작성하기 전에 메타데이터 디자인 모드에서 **스크립트 변환 편집기**를 사용하여 완료해야 하는 단계 중 하나입니다.  
  
### <a name="configuring-input-columns"></a>입력 열 구성  
 스크립트 구성 요소를 사용하여 만들어진 변환 구성 요소에서는 하나의 입력만 사용합니다.  
  
 **스크립트 변환 편집기**의 **입력 열** 페이지에 나타나는 열 목록에는 업스트림 데이터 흐름 구성 요소의 출력에서 가져온 사용 가능한 열이 표시됩니다. 이 목록에서 변환하거나 전달할 열을 선택합니다. 현재 위치에서 변환할 모든 열은 읽기/쓰기로 표시합니다.  
  
 **스크립트 변환 편집기**의 **입력 열** 페이지에 대한 자세한 내용은 [스크립트 변환 편집기&#40;입력 열 페이지&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)를 참조하세요.  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>입력, 출력 및 출력 열 구성  
 변환 구성 요소는 하나 이상의 출력을 지원합니다.  
  
 비동기 출력을 사용하는 변환에는 두 개의 출력이 있는 경우가 많습니다. 예를 들어 특정 도시에 있는 주소의 수를 계산할 때 주소 데이터를 하나의 출력에 전달하고 집계 결과는 다른 출력으로 보낼 수 있습니다. 집계 출력에는 새 출력 열도 필요합니다.  
  
 **스크립트 변환 편집기**의 **입/출력** 페이지에서는 기본적으로 단일 출력이 만들어졌지만 출력 열은 만들어지지 않았음을 확인할 수 있습니다. 편집기의 이 페이지에서 다음과 같은 항목을 구성할 수 있습니다.  
  
-   집계 결과에 대한 출력과 같은 추가 출력을 하나 이상 만들 수 있습니다. 비동기 변환 구성 요소의 출력을 관리하려면 **출력 추가** 및 **출력 제거** 단추를 사용합니다. 출력이 단순히 업스트림 구성 요소에서 데이터를 전달하거나 기존 행 및 열의 현재 위치에서 데이터를 변환하지 않음을 나타내려면 각 출력의 **SynchronousInputID** 속성을 0으로 설정합니다. 입력과 출력이 비동기적으로 이루어지게 하는 것은 이 설정입니다.  
  
-   입력 및 출력에 이름을 지정할 수 있습니다. 스크립트 구성 요소에서는 이러한 이름을 사용하여 스크립트에서 입력 및 출력을 참조하는 데 사용할 형식화된 접근자 속성을 생성합니다.  
  
-   비동기 변환에서는 데이터 흐름에 열을 추가하는 경우가 많습니다. 출력의 **SynchronousInputID** 속성이 0으로 설정되어 출력이 단순히 업스트림 구성 요소에서 데이터를 전달하거나 기존 행 및 열의 현재 위치에서 데이터를 변환하지 않음을 나타내는 경우에는 출력에서 명시적으로 출력 열을 추가하고 구성해야 합니다. 출력 열의 이름은 해당 열이 매핑된 입력 열의 이름과 같지 않아도 됩니다.  
  
-   추가 정보를 포함할 열을 추가할 수 있습니다. 이 경우 추가 열에 데이터를 채우기 위한 코드를 직접 작성해야 합니다. 표준 오류 출력의 동작을 재현하는 방법에 대한 자세한 내용은 [스크립트 구성 요소의 오류 출력 시뮬레이션](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)을 참조하세요.  
  
 **스크립트 변환 편집기**의 **입/출력** 페이지에 대한 자세한 내용은 [스크립트 변환 편집기&#40;입/출력 페이지&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)를 참조하세요.  
  
### <a name="adding-variables"></a>변수 추가  
 스크립트에 사용하려는 값을 포함하는 기존 변수가 있는 경우 **스크립트 변환 편집기**의 **스크립트** 페이지에서 ReadOnlyVariables 및 ReadWriteVariables 속성 필드에 해당 변수를 추가할 수 있습니다.  
  
 속성 필드에 여러 변수를 추가하는 경우 변수 이름을 쉼표로 구분하십시오. 또한 **ReadOnlyVariables** 및 **ReadWriteVariables** 속성 필드 옆에 있는 줄임표(**...**) 단추를 클릭한 다음, **변수 선택** 대화 상자에서 변수를 선택하면 여러 개의 변수를 선택할 수 있습니다.  
  
 스크립트 구성 요소에서 변수를 사용하는 방법에 대한 일반적인 내용은 [스크립트 구성 요소에서 변수 사용](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)을 참조하세요.  
  
 **스크립트 변환 편집기**의 **스크립트** 페이지에 대한 자세한 내용은 [스크립트 변환 편집기&#40;스크립트 페이지&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md)를 참조하세요.  
  
## <a name="scripting-an-asynchronous-transformation-component-in-code-design-mode"></a>코드 디자인 모드에서 비동기 변환 구성 요소 스크립팅  
 구성 요소에 대한 메타데이터를 모두 구성한 후에는 사용자 지정 스크립트를 작성할 수 있습니다. **스크립트 변환 편집기**의 **스크립트** 페이지에서 **스크립트 편집**을 클릭하여 사용자 지정 스크립트를 추가할 수 있는 VSTA([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications) IDE를 엽니다. 사용하는 스크립트 언어는 **스크립트** 페이지에서 **ScriptLanguage** 속성에 대한 스크립트 언어로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 중에서 선택한 언어에 따라 달라집니다.  
  
 스크립트 구성 요소를 사용하여 만든 모든 종류의 구성 요소에 적용되는 중요한 정보는 [스크립트 구성 요소 코딩 및 디버깅](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)을 참조하세요.  
  
### <a name="understanding-the-auto-generated-code"></a>자동 생성 코드 이해  
 변환 구성 요소를 만들고 구성한 후 VSTA IDE를 열면 편집 가능한 **ScriptMain** 클래스가 ProcessInputRow 및 CreateNewOutputRows 메서드에 대한 스텁과 함께 코드 편집기에 나타납니다. 이 ScriptMain 클래스에서 사용자 지정 코드를 작성해야 하며 ProcessInputRow는 변환 구성 요소에서 가장 중요한 메서드입니다. **CreateNewOutputRows** 메서드는 원본 구성 요소에서 보다 일반적으로 사용되는데 이는 두 구성 요소가 모두 개별적인 출력 행을 만들어야 한다는 점에서 비동기 변환과 비슷합니다.  
  
 VSTA **프로젝트 탐색기** 창을 열면 스크립트 구성 요소가 읽기 전용 **BufferWrapper** 및 **ComponentWrapper** 프로젝트 항목도 생성했음을 확인할 수 있습니다. ScriptMain 클래스는 **ComponentWrapper** 프로젝트 항목의 UserComponent 클래스에서 상속됩니다.  
  
 런타임에 데이터 흐름 엔진은 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 부모 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A> 메서드를 재정의하는 **UserComponent** 클래스의 PrimeOutput 메서드를 호출합니다. PrimeOutput 메서드는 차례로 CreateNewOutputRows 메서드를 호출합니다.  
  
 다음으로, 데이터 흐름 엔진은 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 부모 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> 메서드를 재정의하는 UserComponent 클래스의 ProcessInput 메서드를 호출합니다. 그러면 ProcessInput 메서드는 입력 버퍼의 행을 반복하고 각 행에 대해 ProcessInputRow 메서드를 한 번씩 호출합니다.  
  
### <a name="writing-your-custom-code"></a>사용자 지정 코드 작성  
 사용자 지정 비동기 변환 구성 요소 만들기를 마치려면 재정의된 ProcessInputRow 메서드를 사용하여 입력 버퍼의 각 행에 있는 데이터를 처리해야 합니다. 출력은 입력과 동기적으로 이루어지지 않으므로 데이터 행을 출력에 명시적으로 써야 합니다.  
  
 비동기 변환에서는 ProcessInputRow 또는 ProcessInput 메서드 내에서 AddRow 메서드를 사용하여 출력에 행을 적절하게 추가할 수 있습니다. CreateNewOutputRows 메서드를 사용할 필요가 없습니다. 집계 결과와 같은 결과를 특정 출력에 한 행으로 작성하려는 경우 먼저 CreateNewOutputRows 메서드를 사용하여 출력 행을 만들고 나중에 모든 입력 행을 처리한 후에 해당 값을 채울 수 있습니다. 그러나 스크립트 구성 요소에서는 입력 또는 출력에 현재 행만 사용할 수 있으므로 CreateNewOutputRows 메서드에서 여러 행을 만드는 것은 유용하지 않습니다. CreateNewOutputRows 메서드는 처리할 입력 행이 없는 원본 구성 요소에서 보다 중요합니다.  
  
 ProcessInput 메서드 자체를 재정의할 수도 있으므로 입력 버퍼를 반복하고 각 행에 대해 ProcessInputRow를 호출하기 전이나 그 후에 예비 또는 최종 처리를 추가로 수행할 수 있습니다. 예를 들어 이 항목의 코드 예제 중 하나는 ProcessInputRow가 행을 반복하면서 특정 도시의 주소 수를 계산하도록 ProcessInput을 재정의합니다 **.** 이 예제에서는 모든 행이 처리된 후 요약 값을 두 번째 출력에 기록합니다. PostExecute가 호출되면 출력 버퍼를 더 이상 사용할 수 없으므로 이 예에서는 ProcessInput에서 출력을 완료합니다.  
  
 요구 사항에 따라 ScriptMain 클래스에서 사용할 수 있는 PreExecute 및 PostExecute 메서드에서 스크립트를 작성하여 예비 또는 최종 처리를 수행할 수도 있습니다.  
  
> [!NOTE]  
>  사용자 지정 데이터 흐름 구성 요소를 처음부터 새로 개발하려는 경우에는 나중에 출력 버퍼에 데이터 행을 추가할 수 있도록 PrimeOutput 메서드를 재정의하여 출력 버퍼에 대한 참조를 캐시하는 것이 중요합니다. 스크립트 구성 요소에서는 **BufferWrapper** 프로젝트 항목에 각 출력 버퍼를 나타내는 자동 생성 클래스가 있으므로 이 작업이 필요하지 않습니다.  
  
## <a name="example"></a>예제  
 이 예에서는 ScriptMain 클래스에서 비동기 변환 구성 요소를 만드는 데 필요한 사용자 지정 코드를 보여 줍니다.  
  
> [!NOTE]  
>  이 예에서는 **AdventureWorks** 예제 데이터베이스의 **Person.Address** 테이블을 사용하고 이 테이블의 첫 번째 열과 네 번째 열, **intAddressID** 및 **nvarchar(30)City**를 데이터 흐름을 통해 전달합니다. 이 섹션의 원본, 변환 및 대상 예제에는 동일한 데이터가 사용됩니다. 각 예에 대해 필수 구성 요소 및 가정도 설명되어 있습니다.  
  
 이 예에서는 두 개의 출력을 사용하는 비동기 변환 구성 요소를 보여 줍니다. 이 변환에서는 **AddressID** 및 **City** 열을 한 출력에 전달하고 동시에 특정 도시에 있는 주소의 수를 계산한 다음 이 결과 값을 두 번째 출력에 출력합니다.  
  
 이 예제 코드를 실행하려면 다음과 같이 패키지와 구성 요소를 구성해야 합니다.  
  
1.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 변환으로 구성합니다.  
  
2.  디자이너에서 원본 또는 다른 변환의 출력을 새 변환 구성 요소에 연결합니다. 이 출력은 **AdventureWorks** 샘플 데이터베이스에 있는 **Person.Address** 테이블의 데이터를 제공해야 하며, 이 데이터에는 적어도 **AddressID** 및 **City** 열이 포함됩니다.  
  
3.  **스크립트 변환 편집기**를 엽니다. **입력 열** 페이지에서 **AddressID** 및 **City** 열을 선택합니다.  
  
4.  **입/출력** 페이지에서 첫 번째 출력에 **AddressID** 및 **City** 출력 열을 추가하고 구성합니다. 두 번째 출력을 추가하고 이 두 번째 출력에 요약 값에 대한 출력 열을 추가합니다. 이 예에서는 각 입력 행을 첫 번째 출력에 명시적으로 복사하므로 첫 번째 출력의 SynchronousInputID 속성은 0으로 설정합니다. 새로 만든 출력의 SynchronousInputID 속성은 이미 0으로 설정되어 있습니다.  
  
5.  입력, 출력 및 새 출력 열의 이름을 보다 알기 쉬운 이름으로 바꿉니다. 이 예에서는 입력 이름으로 **MyAddressInput**을 사용하고, 출력 이름으로 **MyAddressOutput** 및 **MySummaryOutput**을 사용하며, 두 번째 출력의 출력 열 이름으로는 **MyRedmondCount**를 사용합니다.  
  
6.  **스크립트** 페이지에서 **스크립트 편집**을 클릭하고 다음과 같이 스크립트를 입력합니다. 그런 다음 스크립트 개발 환경 및 **스크립트 변환 편집기**를 닫습니다.  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상이나 [스크립트 구성 요소를 사용하여 대상 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)에서 보여 준 예제 대상 구성 요소와 같이 **AddressID** 및 **City** 열을 필요로 하는 대상 구성 요소를 첫 번째 출력에 대해 만들고 구성합니다. 그런 다음 변환의 첫 번째 출력인 **MyAddressOutput**을 대상 구성 요소에 연결합니다. **AdventureWorks** 데이터베이스에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 실행하여 대상 테이블을 만들 수 있습니다.  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  두 번째 출력에 대한 다른 대상 구성 요소를 만들고 구성합니다. 그런 다음 변환의 두 번째 출력인 **MySummaryOutput**을 대상 구성 요소에 연결합니다. 두 번째 출력은 단일 값이 있는 단일 행을 쓰므로 단일 열이 있는 새 파일에 연결하는 플랫 파일 연결 관리자를 사용하여 대상을 쉽게 구성할 수 있습니다. 이 예에서 이 대상 열의 이름은 **MyRedmondCount**입니다.  
  
9. 예제를 실행합니다.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Private myRedmondAddressCount As Integer  
  
    Public Overrides Sub CreateNewOutputRows()  
  
        MySummaryOutputBuffer.AddRow()  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInput(ByVal Buffer As MyAddressInputBuffer)  
  
        While Buffer.NextRow()  
            MyAddressInput_ProcessInputRow(Buffer)  
        End While  
  
        If Buffer.EndOfRowset Then  
            MyAddressOutputBuffer.SetEndOfRowset()  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount  
            MySummaryOutputBuffer.SetEndOfRowset()  
        End If  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With MyAddressOutputBuffer  
            .AddRow()  
            .AddressID = Row.AddressID  
            .City = Row.City  
        End With  
  
        If Row.City.ToUpper = "REDMOND" Then  
            myRedmondAddressCount += 1  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    private int myRedmondAddressCount;  
  
    public override void CreateNewOutputRows()  
    {  
  
        MySummaryOutputBuffer.AddRow();  
  
    }  
  
    public override void MyAddressInput_ProcessInput(MyAddressInputBuffer Buffer)  
    {  
  
        while (Buffer.NextRow())  
        {  
            MyAddressInput_ProcessInputRow(Buffer);  
        }  
  
        if (Buffer.EndOfRowset())  
        {  
            MyAddressOutputBuffer.SetEndOfRowset();  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount;  
            MySummaryOutputBuffer.SetEndOfRowset();  
        }  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            MyAddressOutputBuffer.AddRow();  
            MyAddressOutputBuffer.AddressID = Row.AddressID;  
            MyAddressOutputBuffer.City = Row.City;  
        }  
  
        if (Row.City.ToUpper() == "REDMOND")  
        {  
            myRedmondAddressCount += 1;  
        }  
  
    }  
  
}  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [동기 및 비동기 변환 이해](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)   
 [스크립트 구성 요소를 사용하여 동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [비동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  
