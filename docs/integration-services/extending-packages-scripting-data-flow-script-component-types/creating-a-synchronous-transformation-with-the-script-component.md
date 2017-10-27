---
title: "스크립트 구성 요소를 사용 하 여 동기 변환 만들기 | Microsoft Docs"
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
- synchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: aa1bee1a-ab06-44d8-9944-4bff03d73016
caps.latest.revision: 64
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3d4a507c31f77449aba7eb884c39bf68c7c78581
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-synchronous-transformation-with-the-script-component"></a>스크립트 구성 요소를 사용하여 동기 변환 만들기
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 데이터 흐름에서 변환 구성 요소를 사용하여 데이터가 원본에서 대상으로 전달될 때 데이터를 수정하고 분석할 수 있습니다. 동기 출력을 사용하는 변환에서는 각 입력 행이 이 구성 요소를 통해 전달될 때 이를 처리합니다. 그러나 비동기 출력을 사용하는 변환에서는 입력 행을 모두 받을 때까지 기다렸다가 처리를 완료합니다. 이 항목에서는 동기 변환에 대해 설명합니다. 비동기 변환에 대 한 정보를 참조 하십시오. [스크립트 구성 요소를 사용 하 여 비동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)합니다. 동기 및 비동기 구성 요소 간의 차이 대 한 자세한 내용은 참조 [이해 동기 및 비동기 변환](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)합니다.  
  
 스크립트 구성 요소 개요를 참조 하십시오. [Extending the Data Flow with the Script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)합니다.  
  
 스크립트 구성 요소 및 해당 구성 요소가 생성하는 인프라 코드를 사용하면 사용자 지정 데이터 흐름 구성 요소를 개발하는 과정이 훨씬 간단해집니다. 그러나 스크립트 구성 요소의 작동 방식을 이해 하려면 유용할 수 있습니다 것에서 섹션에는 사용자 지정 데이터 흐름 구성 요소 개발에 수행 해야 하는 단계를 알아보려면 [사용자 지정 데이터 흐름 구성 요소 개발](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md), 특히 및 [동기 출력을 사용 하는 사용자 지정 변환 구성 요소 개발](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)합니다.  
  
## <a name="getting-started-with-a-synchronous-transformation-component"></a>동기 변환 구성 요소 시작  
 데이터 흐름 창에 스크립트 구성 요소를 추가 하면 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 **스크립트 구성 요소 유형 선택** 대화 상자가 열리고 원본, 대상 또는 변환 구성 요소 유형 선택 하 라는 메시지가 표시 됩니다. 이 대화 상자에서 선택 **변환**합니다.  
  
## <a name="configuring-a-synchronous-transformation-component-in-metadata-design-mode"></a>메타데이터 디자인 모드에서 동기 변환 구성 요소 구성  
 사용 하 여 구성 요소를 구성 하는 변환 구성 요소를 만드는 옵션을 선택한 후는 **스크립트 변환 편집기**합니다. 자세한 내용은 참조 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)합니다.  
  
 스크립트 구성 요소에 대 한 스크립트 언어를 설정 하려면 설정는 **u a g e** 속성에는 **스크립트** 의 페이지는 **스크립트 변환 편집기**합니다.  
  
> [!NOTE]  
>  스크립트 언어 스크립트 구성 요소에 대 한 기본값을 설정 하려면는 **스크립트 언어** 옵션에 **일반** 의 페이지는 **옵션** 대화 상자. 자세한 내용은 참조 [일반 페이지](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)합니다.  
  
 데이터 흐름 변환 구성 요소는 하나의 입력을 사용하며 하나 이상의 출력을 지원합니다. 구성 요소를 사용 하 여 메타 데이터 디자인 모드에서 완료 해야 하는 단계 중 하나에 대 한 구성 요소의 입력과 출력에서 **스크립트 변환 편집기**사용자 지정 스크립트를 작성 하기 전에, 합니다.  
  
### <a name="configuring-input-columns"></a>입력 열 구성  
 변환 구성 요소에서는 하나의 입력을 사용합니다.  
  
 에 **입력 열** 의 페이지는 **스크립트 변환 편집기** 나타나는 열 목록 데이터 흐름의 업스트림 구성 요소의 출력에서 사용 가능한 열을 표시 합니다. 이 목록에서 변환하거나 전달할 열을 선택합니다. 현재 위치에서 변환할 모든 열은 읽기/쓰기로 표시합니다.  
  
 에 대 한 자세한 내용은 **입력 열** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 변환 편집기 &#40; 입력 열 페이지 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)합니다.  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>입력, 출력 및 출력 열 구성  
 변환 구성 요소는 하나 이상의 출력을 지원합니다.  
  
 에 **입 / 출력** 의 페이지는 **스크립트 변환 편집기**, 단일 출력이 만들어져 있지만 출력에 열이 없습니다. 편집기의 이 페이지에서 다음과 같은 항목을 구성할 수 있습니다.  
  
-   예기치 않은 값이 포함된 행에 대한 시뮬레이션된 오류 출력과 같은 추가 출력을 하나 이상 만들 수 있습니다. 사용 하 여는 **출력 추가** 및 **출력 제거** 동기 변환 구성 요소의 출력을 관리 하는 단추입니다. 각 행을 한 출력 또는 다른 출력으로 리디렉션하도록 지정하지 않은 경우에는 모든 입력 행이 사용 가능한 모든 출력으로 전송됩니다. 0이 아닌 정수 값을 지정 하 여 행을 리디렉션하도록 하려면 표시는 **ExclusionGroup** 출력에는 속성입니다. 에 특정 정수 값 입력 **ExclusionGroup** 출력 식별 하려면 중요 하지는 않지만 지정한 출력 그룹에 대 한 일관 되 게 동일한 정수를 사용 해야 합니다.  
  
    > [!NOTE]  
    >  0이 아닌를 사용할 수도 있습니다 **ExclusionGroup** 모든 행을 출력 하지 않을 경우 단일 출력과 함께 속성 값입니다. 그러나이 경우 명시적으로 호출 해야는 **DirectRowTo\<outputbuffer >** 메서드 출력으로 전송 하려는 경우 각 행에 대 한 합니다.  
  
-   입력 및 출력에 보다 알기 쉬운 이름을 지정할 수 있습니다. 스크립트 구성 요소에서는 이러한 이름을 사용하여 스크립트에서 입력 및 출력을 참조하는 데 사용할 형식화된 접근자 속성을 생성합니다.  
  
-   동기 변환의 경우 열을 현재 상태로 둘 수 있습니다. 일반적으로 동기 변환에서는 데이터 흐름에 열을 추가하지 않습니다. 데이터는 버퍼의 현재 위치에서 수정되고 해당 버퍼는 데이터 흐름의 다음 구성 요소로 전달됩니다. 이 경우 변환의 출력에서 출력 열을 명시적으로 추가하거나 구성할 필요가 없습니다. 출력은 편집기에서 명시적으로 정의된 열이 없는 상태로 나타납니다.  
  
-   행 수준 오류에 대한 시뮬레이션된 오류 출력에 새 열을 추가할 수 있습니다. 일반적으로 여러 출력에 동일한 **ExclusionGroup** 동일한 출력 열 집합이 있습니다. 그러나 시뮬레이션된 오류 출력을 만드는 경우 오류 정보를 포함할 다른 열을 추가할 수 있습니다. 오류 행을 처리 하는 데이터 흐름 엔진이 하는 방법에 대 한 정보를 참조 [데이터 흐름 구성 요소의 오류 출력을 사용 하 여](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)합니다. 스크립트 구성 요소에서는 개발자가 직접 코드를 작성하여 추가 열을 적절한 오류 정보로 채워야 합니다. 자세한 내용은 참조 [스크립트 구성 요소에 대 한 오류 출력 시뮬레이션](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)합니다.  
  
 에 대 한 자세한 내용은 **입 / 출력** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 변환 편집기 &#40; 입력 및 출력 페이지 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)합니다.  
  
### <a name="adding-variables"></a>변수 추가  
 스크립트에서 기존 변수를 사용 하려는 경우에 추가할 수 있습니다는 **ReadOnlyVariables** 및 **ReadWriteVariables** 속성 필드에 **스크립트** 의 페이지는 **스크립트 변환 편집기**합니다.  
  
 속성 필드에 여러 변수를 추가하는 경우 변수 이름을 쉼표로 구분하십시오. 줄임표를 클릭 하 여 여러 변수를 선택할 수도 있습니다 (**...** ) 단추 옆에 **ReadOnlyVariables** 및 **ReadWriteVariables** 속성 필드를 한 다음 변수를 선택 하 고 **변수 선택** 대화 상자입니다.  
  
 스크립트 구성 요소와 변수를 사용 하는 방법에 대 한 일반 정보를 참조 하십시오. [스크립트 구성 요소에서 변수를 사용 하 여](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)합니다.  
  
 에 대 한 자세한 내용은 **스크립트** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 변환 편집기 &#40; 스크립트 페이지 &#41; ](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-synchronous-transformation-component-in-code-design-mode"></a>코드 디자인 모드에서 동기 변환 구성 요소 스크립팅  
 구성 요소에 대한 메타데이터를 구성한 후에는 사용자 지정 스크립트를 작성할 수 있습니다. 에 **스크립트 변환 편집기**의 **스크립트** 페이지 **스크립트 편집** 열려는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA Tools for Applications () IDE 여기서 사용자 지정 스크립트를 추가할 수 있습니다. 사용 하는 스크립팅 언어 선택 여부에 따라 달라 집니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#에 대 한 스크립트 언어로 **u a g e** 속성에는 **스크립트** 페이지입니다.  
  
 모든 종류의 스크립트 구성 요소를 사용 하 여 만든 구성 요소에 적용 되는 중요 한 정보를 참조 하십시오. [코딩 및 스크립트 구성 요소 디버깅](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)합니다.  
  
### <a name="understanding-the-auto-generated-code"></a>자동 생성 코드 이해  
 변환 구성 요소를 편집 가능한 구성과 만들고 구성한 후 VSTA IDE를 열 때 **ScriptMain** 클래스에 대 한 스텁과 함께 코드 편집기에 표시 된 **ProcessInputRow** 메서드. **ScriptMain** 클래스는 사용자 지정 코드를 작성 해야 하 고 **ProcessInputRow** 는 변환 구성 요소에서 가장 중요 한 메서드입니다.  
  
 여는 경우는 **프로젝트 탐색기** VSTA에서 창, 스크립트 구성 요소 읽기 전용 생성도을 확인할 수 있습니다 **BufferWrapper** 및 **ComponentWrapper** 프로젝트 항목입니다. **ScriptMain** 클래스에서 상속 된 **UserComponent** 클래스에 **ComponentWrapper** 프로젝트 항목입니다.  
  
 런타임 시 데이터 흐름 엔진 호출는 **ProcessInput** 에서 메서드는 **UserComponent** 재정의 하는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> 의 메서드는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 부모 클래스입니다. **ProcessInput** 메서드를 차례로 호출 고 입력된 버퍼에서 행을 반복 하는 **ProcessInputRow** 메서드를 각 행에 대해 한 번입니다.  
  
### <a name="writing-your-custom-code"></a>사용자 지정 코드 작성  
 동기 출력을 사용하는 변환 구성 요소는 모든 데이터 흐름 구성 요소 중에서 작성하기가 가장 간단합니다. 예를 들어 이 항목의 뒷부분에 있는 단일 출력 예는 다음과 같은 사용자 지정 코드로 구성되어 있습니다.  
  
```vb  
Row.City = UCase(Row.City)  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
```  
  
 사용자 지정 동기 변환 구성 요소 생성을 완료 하려면 재정의 된 사용 **ProcessInputRow** 메서드를 입력된 버퍼의 각 행에 데이터를 변환 합니다. 데이터 흐름 엔진에서는 이 버퍼가 가득 차면 데이터 흐름의 다음 구성 요소로 버퍼를 전달합니다.  
  
 요구 사항에 따라 있습니다 수도 스크립트를 작성 하는 **PreExecute** 및 **PostExecute** 에서 사용할 수 있는 메서드는 **ScriptMain** 수행 하도록 클래스 예비 또는 최종 처리 합니다.  
  
### <a name="working-with-multiple-outputs"></a>여러 출력 작업  
 입력 행을 둘 이상의 가능한 출력 중 하나로 전송하는 데 필요한 사용자 지정 코드는 앞에서 설명한 단일 출력을 사용하는 경우보다 그다지 많지 않습니다. 예를 들어 이 항목의 뒷부분에 있는 두 개의 출력을 사용하는 예는 다음과 같은 사용자 지정 코드로 구성되어 있습니다.  
  
```vb  
Row.City = UCase(Row.City)  
If Row.City = "REDMOND" Then  
    Row.DirectRowToMyRedmondAddresses()  
Else  
    Row.DirectRowToMyOtherAddresses()  
End If  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
if (Row.City=="REDMOND")  
{  
    Row.DirectRowToMyRedmondAddresses();  
}  
else  
{  
    Row.DirectRowToMyOtherAddresses();  
}  
```  
  
 이 예제에서는 스크립트 구성 요소는 다음과 같이 생성 됩니다.는 **DirectRowTo\<OutputBufferX >** 메서드를 사용자가 구성한 출력의 이름에 기반 합니다. 비슷한 코드를 사용하여 오류 출력을 시뮬레이션된 오류 출력으로 전송할 수 있습니다.  
  
## <a name="examples"></a>예  
 여기에 있는 예제에 필요한 사용자 지정 코드를 보여 줍니다.는 **ScriptMain** 동기 변환 구성 요소를 만드는 클래스입니다.  
  
> [!NOTE]  
>  이러한 예에서 사용 된 **Person.Address** 테이블에 **AdventureWorks** 예제 데이터베이스를 해당 첫 번째 및 네 번째 열을 전달는 **intAddressID** 및  **nvarchar (30) 도시** 데이터 흐름을 통해 열입니다. 이 섹션의 원본, 변환 및 대상 예제에는 동일한 데이터가 사용됩니다. 각 예에 대해 필수 구성 요소 및 가정도 설명되어 있습니다.  
  
### <a name="single-output-synchronous-transformation-example"></a>단일 출력 동기 변환 예  
 이 예에서는 단일 출력을 사용하는 동기 변환 구성 요소를 보여 줍니다. 이 변환을 통과 **AddressID** 열 및 변환의 **도시** 열을 대문자로 합니다.  
  
 이 예제 코드를 실행하려면 다음과 같이 패키지와 구성 요소를 구성해야 합니다.  
  
1.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 변환으로 구성합니다.  
  
2.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 원본 또는 다른 변환의 출력을 새 변환 구성 요소에 연결합니다. 이 출력 데이터를 제공 해야는 **Person.Address** 목차는 **AdventureWorks** 포함 된 예제 데이터베이스는 **AddressID** 및 **도시**  열입니다.  
  
3.  열기는 **스크립트 변환 편집기**합니다. 에 **입력 열** 선택 페이지는 **AddressID** 및 **도시** 열입니다. 표시는 **도시** 읽기/쓰기 권한으로 열입니다.  
  
4.  에 **입 / 출력** 페이지에서 입력의 이름을와 같은 보다 알기 쉬운 이름으로 출력 **MyAddressInput** 및 **MyAddressOutput**합니다. 다음에 유의 **SynchronousInputID** 에 해당 하는 출력의는 **ID** 입력 합니다. 따라서 출력 열을 추가하고 구성하지 않아도 됩니다.  
  
5.  에 **스크립트** 페이지 **스크립트 편집** 뒤에 스크립트를 입력 합니다. 다음 스크립트 개발 환경을 닫습니다 및 **스크립트 변환 편집기**합니다.  
  
6.  만들기 및 구성에 필요한 대상 구성 요소는 **AddressID** 및 **도시** 열의 경우와 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서보여준예제대상구성요소나대상또는[스크립트 구성 요소를 사용 하 여 대상 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)합니다. 그런 다음 변환의 출력을 대상 구성 요소에 연결합니다. 다음 명령을 실행 하 여 대상 테이블을 만들 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령에 **AdventureWorks** 데이터베이스:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
7.  예제를 실행합니다.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        Row.City = UCase(Row.City)  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        Row.City = (Row.City).ToUpper();  
  
    }  
  
}  
```  
  
### <a name="two-output-synchronous-transformation-example"></a>두 개의 출력을 사용하는 동기 변환 예  
 이 예에서는 두 개의 출력을 사용하는 동기 변환 구성 요소를 보여 줍니다. 이 변환을 통과 **AddressID** 열 및 변환의 **도시** 열을 대문자로 합니다. 도시 이름이 Redmond이면 해당 행은 한 출력으로 전송되고 다른 모든 행은 다른 출력으로 전송됩니다.  
  
 이 예제 코드를 실행하려면 다음과 같이 패키지와 구성 요소를 구성해야 합니다.  
  
1.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 변환으로 구성합니다.  
  
2.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 원본 또는 다른 변환의 출력을 새 변환 구성 요소에 연결합니다. 이 출력 데이터를 제공 해야는 **Person.Address** 목차는 **AdventureWorks** 예제 데이터베이스에 포함 된 적어도 **AddressID** 및  **도시** 열입니다.  
  
3.  열기는 **스크립트 변환 편집기**합니다. 에 **입력 열** 선택 페이지는 **AddressID** 및 **도시** 열입니다. 표시는 **도시** 읽기/쓰기 권한으로 열입니다.  
  
4.  에 **입 / 출력** 페이지에서 두 번째 출력을 만듭니다. 새 출력을 추가한 후 설정 했는지 확인 해당 **SynchronousInputID** 에 **ID** 입력 합니다. 기본적으로 만들어진 첫 번째 출력에는 이 속성이 이미 설정되어 있습니다. 각 출력에 대 한 설정의 **ExclusionGroup** 속성을 동일한 0이 아닌 값은 상호 배타적인 두 개의 출력 간에 입력된 행 분할을 나타냅니다. 출력에 출력 열을 추가할 필요는 없습니다.  
  
5.  와 같은 입력 및 출력 보다 설명적인 이름으로 이름 바꾸기 **MyAddressInput**, **MyRedmondAddresses**, 및 **MyOtherAddresses**합니다.  
  
6.  에 **스크립트** 페이지 **스크립트 편집** 뒤에 스크립트를 입력 합니다. 다음 스크립트 개발 환경을 닫습니다 및 **스크립트 변환 편집기**합니다.  
  
7.  만들기 및 구성 하는 두 개의 대상 구성 요소는 **AddressID** 및 **도시** 열의 경우와 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상, 플랫 파일 대상 또는 예제 대상 구성 요소 에 설명 된 [스크립트 구성 요소를 사용 하 여 대상 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)합니다. 그런 다음 변환의 각 출력을 대상 구성 요소 중 하나에 연결합니다. 실행 하 여 대상 테이블을 만들 수 있습니다는 [!INCLUDE[tsql](../../includes/tsql-md.md)] (고유 테이블 이름 포함)에 다음과 비슷한 명령을 **AdventureWorks** 데이터베이스:  
  
    ```sql
    CREATE TABLE [Person].[Address2](  
        [AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL  
    ```  
  
8.  예제를 실행합니다.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        Row.City = UCase(Row.City)  
  
        If Row.City = "REDMOND" Then  
            Row.DirectRowToMyRedmondAddresses()  
        Else  
            Row.DirectRowToMyOtherAddresses()  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        Row.City = (Row.City).ToUpper();  
  
        if (Row.City == "REDMOND")  
        {  
            Row.DirectRowToMyRedmondAddresses();  
        }  
        else  
        {  
            Row.DirectRowToMyOtherAddresses();  
        }  
  
    }  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [동기 및 비동기 변환 이해] (~/integration-services/understanding-synchronous-and-asynchronous-transformations.md   
 [스크립트 구성 요소를 사용 하 여 비동기 변환 만들기] (~/integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md   
 [동기 출력을 사용 하는 사용자 지정 변환 구성 요소 개발] (~/integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md  
  
  



