---
title: "스크립트 구성 요소를 사용 하 여 비동기 변환 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- asynchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: 0d814404-21e4-4a68-894c-96fa47ab25ae
caps.latest.revision: 63
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4da61e00337430a3eaef84e40f9f732a572cc45b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="creating-an-asynchronous-transformation-with-the-script-component"></a>스크립트 구성 요소를 사용하여 비동기 변환 만들기
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 데이터 흐름에서 변환 구성 요소를 사용하여 데이터가 원본에서 대상으로 전달될 때 데이터를 수정하고 분석할 수 있습니다. 동기 출력을 사용하는 변환에서는 각 입력 행이 이 구성 요소를 통해 전달될 때 이를 처리합니다. 비동기 출력을 사용 하는 변환 입력된 행을 모두 받기 전에 특정 행을 출력할 수 또는 모든 입력된 행을 받을 때까지 처리 완료를 기다릴 수 있습니다. 이 항목에서는 비동기 변환에 대해 설명합니다. 처리 필요한 경우 동기 변환, 참조 [스크립트 구성 요소를 사용 하 여 동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)합니다. 동기 및 비동기 구성 요소 간의 차이점에 대 한 자세한 내용은 참조 [이해 동기 및 비동기 변환](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)합니다.  
  
 스크립트 구성 요소 개요를 참조 하십시오. [Extending the Data Flow with the Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)합니다.  
  
 스크립트 구성 요소 및 해당 구성 요소가 생성하는 인프라 코드를 사용하면 사용자 지정 데이터 흐름 구성 요소를 개발하는 과정이 간단해집니다. 그러나 스크립트 구성 요소의 작동 방식을 이해 하려면 있습니다 유용할 수의 사용자 지정 데이터 흐름 구성 요소 개발에 수행 해야 하는 단계를 읽을 수는 [사용자 지정 데이터 흐름 구성 요소 개발](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) 섹션 및 특히 [동기 출력을 사용자 지정 변환 구성 요소 개발](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)합니다.  
  
## <a name="getting-started-with-an-asynchronous-transformation-component"></a>비동기 변환 구성 요소 시작  
 데이터 흐름 탭에 스크립트 구성 요소를 추가 하면 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 **스크립트 구성 요소 유형 선택** 대화 상자가 나타나면 미리 구성 요소를 구성 하기 위한 원본, 변환 또는 대상으로 합니다. 이 대화 상자에서 선택 **변환**합니다.  
  
## <a name="configuring-an-asynchronous-transformation-component-in-metadata-design-mode"></a>메타데이터 디자인 모드에서 비동기 변환 구성 요소 구성  
 사용 하 여 구성 요소를 구성 하는 변환 구성 요소를 만드는 옵션을 선택한 후는 **스크립트 변환 편집기**합니다. 자세한 내용은 참조 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)합니다.  
  
 설정 스크립트 구성 요소에서 사용할 스크립트 언어를 선택 하려면는 **u a g e** 속성에는 **스크립트** 의 페이지는 **스크립트 변환 편집기** 대화 상자 상자입니다.  
  
> [!NOTE]  
>  스크립트 언어 스크립트 구성 요소에 대 한 기본값을 설정 하려면는 **스크립트 언어** 옵션에 **일반** 의 페이지는 **옵션** 대화 상자. 자세한 내용은 [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)을 참조하세요.  
  
 데이터 흐름 변환 구성 요소는 하나의 입력을 사용하며 하나 이상의 출력을 지원합니다. 사용 하 여 메타 데이터 디자인 모드에서 완료 해야 하는 단계 중 하나는 구성 요소의 입력과 출력을 구성 된 **스크립트 변환 편집기**사용자 지정 스크립트를 작성 하기 전에, 합니다.  
  
### <a name="configuring-input-columns"></a>입력 열 구성  
 스크립트 구성 요소를 사용하여 만들어진 변환 구성 요소에서는 하나의 입력만 사용합니다.  
  
 에 **입력 열** 의 페이지는 **스크립트 변환 편집기**, 열 목록 데이터 흐름의 업스트림 구성 요소의 출력에서 사용 가능한 열을 표시 합니다. 이 목록에서 변환하거나 전달할 열을 선택합니다. 현재 위치에서 변환할 모든 열은 읽기/쓰기로 표시합니다.  
  
 에 대 한 자세한 내용은 **입력 열** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 변환 편집기 &#40; 입력 열 페이지 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)합니다.  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>입력, 출력 및 출력 열 구성  
 변환 구성 요소는 하나 이상의 출력을 지원합니다.  
  
 비동기 출력을 사용하는 변환에는 두 개의 출력이 있는 경우가 많습니다. 예를 들어 특정 도시에 있는 주소의 수를 계산할 때 주소 데이터를 하나의 출력에 전달하고 집계 결과는 다른 출력으로 보낼 수 있습니다. 집계 출력에는 새 출력 열도 필요합니다.  
  
 에 **입 / 출력** 의 페이지는 **스크립트 변환 편집기**, 기본적으로 단일 출력이 만든 하지만 생성 된 출력 열을 참조 하십시오. 편집기의 이 페이지에서 다음과 같은 항목을 구성할 수 있습니다.  
  
-   집계 결과에 대한 출력과 같은 추가 출력을 하나 이상 만들 수 있습니다. 사용 하 여는 **출력 추가** 및 **출력 제거** 비동기 변환 구성 요소의 출력을 관리 하는 단추입니다. 설정의 **SynchronousInputID** 출력 않습니다 단순히 업스트림 구성 요소에서 데이터를 통과 또는 변환에서 기존 행과 열 위치에 나타내기 위해 0으로 각 출력의 속성입니다. 입력과 출력이 비동기적으로 이루어지게 하는 것은 이 설정입니다.  
  
-   입력 및 출력에 이름을 지정할 수 있습니다. 스크립트 구성 요소에서는 이러한 이름을 사용하여 스크립트에서 입력 및 출력을 참조하는 데 사용할 형식화된 접근자 속성을 생성합니다.  
  
-   비동기 변환에서는 데이터 흐름에 열을 추가하는 경우가 많습니다. 경우는 **SynchronousInputID** 출력의 속성은 0, 단순히 업스트림 구성 요소에서 데이터를 통과 또는 추가 하 고 구성 해야이 현재 위치에서 기존 행과 열을 변환 출력 되지 않은 것을 나타내는 출력에 명시적으로 열을 출력 합니다. 출력 열의 이름은 해당 열이 매핑된 입력 열의 이름과 같지 않아도 됩니다.  
  
-   추가 정보를 포함할 열을 추가할 수 있습니다. 이 경우 추가 열에 데이터를 채우기 위한 코드를 직접 작성해야 합니다. 표준 오류 출력의 동작을 재현 하는 방법에 대 한 정보를 참조 하십시오. [스크립트 구성 요소에 대 한 오류 출력 시뮬레이션](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)합니다.  
  
 에 대 한 자세한 내용은 **입 / 출력** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 변환 편집기 &#40; 입력 및 출력 페이지 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)합니다.  
  
### <a name="adding-variables"></a>변수 추가  
 스크립트에서 사용 하려는 값을 가진 모든 기존 변수가 없으면 추가할 수 있습니다 ReadOnlyVariables 및 ReadWriteVariables 속성 필드에 **스크립트** 의 페이지는 **스크립트 변환 편집기** .  
  
 속성 필드에 여러 변수를 추가하는 경우 변수 이름을 쉼표로 구분하십시오. 줄임표를 클릭 하 여 여러 변수를 선택할 수도 있습니다 (**...** ) 단추 옆에 **ReadOnlyVariables** 및 **ReadWriteVariables** 속성 필드를 한 다음 변수를 선택 하 고 **변수 선택** 대화 상자입니다.  
  
 스크립트 구성 요소와 변수를 사용 하는 방법에 대 한 일반 정보를 참조 하십시오. [스크립트 구성 요소에서 변수를 사용 하 여](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)합니다.  
  
 에 대 한 자세한 내용은 **스크립트** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 변환 편집기 &#40; 스크립트 페이지 &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-an-asynchronous-transformation-component-in-code-design-mode"></a>코드 디자인 모드에서 비동기 변환 구성 요소 스크립팅  
 구성 요소에 대한 메타데이터를 모두 구성한 후에는 사용자 지정 스크립트를 작성할 수 있습니다. 에 **스크립트 변환 편집기**의 **스크립트** 페이지 **스크립트 편집** 열려는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA Tools for Applications () IDE 여기서 사용자 지정 스크립트를 추가할 수 있습니다. 사용 하는 스크립팅 언어 선택 여부에 따라 달라 집니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#에 대 한 스크립트 언어로 **u a g e** 속성에는 **스크립트** 페이지입니다.  
  
 모든 종류의 스크립트 구성 요소를 사용 하 여 만든 구성 요소에 적용 되는 중요 한 정보를 참조 하십시오. [코딩 및 스크립트 구성 요소 디버깅](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)합니다.  
  
### <a name="understanding-the-auto-generated-code"></a>자동 생성 코드 이해  
 만들고 변환 구성 요소를 편집 가능한를 구성한 후 VSTA IDE를 열면 **ScriptMain** 클래스가 고 ProcessInputRow 및 CreateNewOutputRows 메서드에 대 한 스텁과 함께 코드 편집기에 나타납니다. ScriptMain 클래스 이며 여기서 사용자 지정 코드를 작성 합니다 ProcessInputRow는 변환 구성 요소에서 가장 중요 한 메서드입니다. **CreateNewOutputRows** 메서드 구성 요소가 모두 개별적인 출력 행을 만들어야 한다는 점에서 비동기 변환과 비슷합니다는 원본 구성 요소에서 보다 일반적인 방법으로 사용 됩니다.  
  
 VSTA를 열면 **프로젝트 탐색기** 창, 스크립트 구성 요소 읽기 전용 생성도을 확인할 수 있습니다 **BufferWrapper** 및 **ComponentWrapper** 프로젝트 항목 . ScriptMain 클래스에서 UserComponent 클래스에서 상속 된 **ComponentWrapper** 프로젝트 항목입니다.  
  
 런타임 시 데이터 흐름 엔진의 PrimeOutput 메서드를 호출는 **UserComponent** 재정의 하는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A> 의 메서드는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 부모 클래스입니다. 그러면의 PrimeOutput 메서드가 CreateNewOutputRows 메서드를 호출 합니다.  
  
 데이터 흐름 엔진 UserComponent 클래스에서 재정의 된 ProcessInput 메서드를 호출 하는 다음으로 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> 의 메서드는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 부모 클래스입니다. ProcessInput 메서드를 차례로 입력된 버퍼의 행과 각 행에 대해 ProcessInputRow 메서드를 한 번 호출입니다.  
  
### <a name="writing-your-custom-code"></a>사용자 지정 코드 작성  
 사용자 지정 비동기 변환 구성 요소 생성을 완료 하려면 입력된 버퍼의 각 행에 데이터를 처리할 재정의 ProcessInputRow 메서드를 사용 해야 합니다. 출력은 입력과 동기적으로 이루어지지 않으므로 데이터 행을 출력에 명시적으로 써야 합니다.  
  
 비동기 변환에서는 ProcessInputRow 또는 ProcessInput 메서드 내에서 적절 하 게 출력에 행을 추가할 AddRow 메서드를 사용할 수 있습니다. CreateNewOutputRows 메서드를 사용할 필요가 없습니다. 특정 출력으로 결과 집계 결과 등의 단일 행을 작성 하는 경우 CreateNewOutputRows 메서드를 사용 하 여 출력 행을 미리 만들 수 있으며 모든 입력된 행을 처리 한 후 나중에 해당 값을 채웁니다. 그러나 유용 하지 않습니다 CreateNewOutputRows 메서드에서 여러 행을 만들려고 하면 있기 때문에 스크립트 구성 요소만 입력 또는 출력에서 현재 행을 사용 합니다. CreateNewOutputRows 방법은 원본 구성 요소에서 보다 중요 처리할 입력된 행이 없는 경우가 있습니다.  
  
 수 하려는 자체 ProcessInput 메서드를 재정의 추가 예비 또는 최종 처리 전 또는 후 입력된 버퍼를 반복 하 고 각 행에 대해 ProcessInputRow를 호출 하는 작업을 수행할 수 있도록 합니다. 행을 반복할 ProcessInputRow로 특정 도시의 주소 수를 계산 하는 ProcessInput 재정의이 항목의 코드 예제 중 하나는 예를 들어**합니다.** 이 예제에서는 모든 행이 처리 된 후 두 번째 출력에는 요약 값을 씁니다. 이 예제에서는 PostExecute 호출 될 때 출력 버퍼는 더 이상 사용할 수 있으므로 ProcessInput에서 출력을 완료 합니다.  
  
 요구 사항에 따라 예비 또는 최종 처리를 수행 하려면 ScriptMain 클래스에서 사용할 수 있는 PreExecute 및 PostExecute 메서드에서 스크립트를 작성할 수도 있습니다.  
  
> [!NOTE]  
>  처음부터는 사용자 지정 데이터 흐름 구성 요소를 개발 하려는 경우 나중에 버퍼의 데이터는 행을 추가할 수 있도록 출력 버퍼에 캐시 참조에 대 한 PrimeOutput 메서드를 재정의 하는 것이 중요 됩니다. 스크립트 구성 요소에서는이 작업이 필요 없습니다에 각 출력 버퍼를 나타내는 자동 생성된 클래스가 있으므로 **BufferWrapper** 프로젝트 항목입니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 하는 데 필요한 ScriptMain 클래스에서 비동기 변환 구성 요소를 만들고 사용자 지정 코드를 보여 줍니다.  
  
> [!NOTE]  
>  이러한 예에서 사용 된 **Person.Address** 테이블에 **AdventureWorks** 예제 데이터베이스를 해당 첫 번째 및 네 번째 열을 전달는 **intAddressID** 및  **nvarchar (30) 도시** 데이터 흐름을 통해 열입니다. 이 섹션의 원본, 변환 및 대상 예제에는 동일한 데이터가 사용됩니다. 각 예에 대해 필수 구성 요소 및 가정도 설명되어 있습니다.  
  
 이 예에서는 두 개의 출력을 사용하는 비동기 변환 구성 요소를 보여 줍니다. 이 변환을 통과 **AddressID** 및 **도시** 열 (Redmond 미국 워싱턴주), 특정 도시에 있는 주소의 수를 계산 하는 동안 하나의 출력 및 출력에는 두 번째 출력에 결과 값입니다.  
  
 이 예제 코드를 실행하려면 다음과 같이 패키지와 구성 요소를 구성해야 합니다.  
  
1.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 변환으로 구성합니다.  
  
2.  디자이너에서 원본 또는 다른 변환의 출력을 새 변환 구성 요소에 연결합니다. 이 출력 데이터를 제공 해야는 **Person.Address** 목차는 **AdventureWorks** 예제 데이터베이스에 포함 된 적어도 **AddressID** 및  **도시** 열입니다.  
  
3.  열기는 **스크립트 변환 편집기**합니다. 에 **입력 열** 선택 페이지는 **AddressID** 및 **도시** 열입니다.  
  
4.  에 **입 / 출력** 페이지, 추가 및 구성의 **AddressID** 및 **도시** 첫 번째 출력에 열을 출력 합니다. 두 번째 출력을 추가하고 이 두 번째 출력에 요약 값에 대한 출력 열을 추가합니다. 이 예에서는 각 입력 행을 첫 번째 출력에 명시적으로 복사하므로 첫 번째 출력의 SynchronousInputID 속성은 0으로 설정합니다. 새로 만든 출력의 SynchronousInputID 속성은 이미 0으로 설정되어 있습니다.  
  
5.  입력, 출력 및 새 출력 열의 이름을 보다 알기 쉬운 이름으로 바꿉니다. 이 예에서는 사용 **MyAddressInput** 의 입력을 이름으로 **MyAddressOutput** 및 **MySummaryOutput** , 출력 및 **MyRedmondCount** 두 번째 출력의 출력 열에 대 한 합니다.  
  
6.  에 **스크립트** 페이지 **스크립트 편집** 뒤에 스크립트를 입력 합니다. 다음 스크립트 개발 환경을 닫습니다 및 **스크립트 변환 편집기**합니다.  
  
7.  만들기 및 구성에 대 한 첫 번째 출력에는 대상 구성 요소는 **AddressID** 및 **도시** 열의 경우와 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상 또는 예제 대상 구성 요소 에 설명 된 [스크립트 구성 요소를 사용 하 여 대상 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)합니다. 그런 다음는 변환의 첫 번째 출력 연결 **MyAddressOutput**, 대상 구성 요소입니다. 다음 명령을 실행 하 여 대상 테이블을 만들 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령에 **AdventureWorks** 데이터베이스:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  두 번째 출력에 대한 다른 대상 구성 요소를 만들고 구성합니다. 그런 다음는 변환의 두 번째 출력 연결 **MySummaryOutput**, 대상 구성 요소입니다. 두 번째 출력은 단일 값이 있는 단일 행을 쓰므로 단일 열이 있는 새 파일에 연결하는 플랫 파일 연결 관리자를 사용하여 대상을 쉽게 구성할 수 있습니다. 예제에서는이 대상 열의 이름은 **MyRedmondCount**합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [동기 및 비동기 변환 이해](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)   
 [스크립트 구성 요소를 사용 하 여 동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [비동기 출력을 사용 하는 사용자 지정 변환 구성 요소 개발](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  
