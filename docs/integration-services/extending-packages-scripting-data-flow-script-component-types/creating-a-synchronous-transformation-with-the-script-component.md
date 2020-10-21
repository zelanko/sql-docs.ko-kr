---
description: 스크립트 구성 요소를 사용하여 동기 변환 만들기
title: 스크립트 구성 요소를 사용하여 동기 변환 만들기 | Microsoft Docs
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
- synchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: aa1bee1a-ab06-44d8-9944-4bff03d73016
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 71a22131a6852708f087ddda67cabc19cdbfd87e
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193125"
---
# <a name="creating-a-synchronous-transformation-with-the-script-component"></a>스크립트 구성 요소를 사용하여 동기 변환 만들기

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 데이터 흐름에서 변환 구성 요소를 사용하여 데이터가 원본에서 대상으로 전달될 때 데이터를 수정하고 분석할 수 있습니다. 동기 출력을 사용하는 변환에서는 각 입력 행이 이 구성 요소를 통해 전달될 때 이를 처리합니다. 그러나 비동기 출력을 사용하는 변환에서는 입력 행을 모두 받을 때까지 기다렸다가 처리를 완료합니다. 이 항목에서는 동기 변환에 대해 설명합니다. 비동기 변환에 대한 자세한 내용은 [스크립트 구성 요소를 사용하여 비동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)를 참조하세요. 동기 구성 요소와 비동기 구성 요소 간의 차이점에 대한 자세한 내용은 [동기 및 비동기 변환 이해](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)를 참조하세요.  
  
 스크립트 구성 요소에 대한 개요는 [스크립트 구성 요소를 사용하여 데이터 흐름 확장](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)을 참조하세요.  
  
 스크립트 구성 요소 및 해당 구성 요소가 생성하는 인프라 코드를 사용하면 사용자 지정 데이터 흐름 구성 요소를 개발하는 과정이 훨씬 간단해집니다. 하지만 스크립트 구성 요소의 작동 방식을 이해하려면 [사용자 지정 데이터 흐름 구성 요소 개발](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) 섹션과 이 섹션의 [동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)에서 사용자 지정 데이터 흐름 구성 요소를 개발하는 데 필요한 단계를 파악하는 것이 좋습니다.  
  
## <a name="getting-started-with-a-synchronous-transformation-component"></a>동기 변환 구성 요소 시작  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 데이터 흐름 창에 스크립트 구성 요소를 추가하면 원본, 대상 또는 변환 구성 요소 유형을 선택하기 위한 **스크립트 구성 요소 유형 선택** 대화 상자가 열립니다. 이 대화 상자에서 **변환**을 선택합니다.  
  
## <a name="configuring-a-synchronous-transformation-component-in-metadata-design-mode"></a>메타데이터 디자인 모드에서 동기 변환 구성 요소 구성  
 변환 구성 요소를 만드는 옵션을 선택한 후에는 **스크립트 변환 편집기**를 사용하여 구성 요소를 구성합니다. 자세한 내용은 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)을 참조하세요.  
  
 스크립트 구성 요소의 스크립트 언어를 설정하려면 **스크립트 변환 편집기**의 **스크립트** 페이지에서 **ScriptLanguage** 속성을 설정합니다.  
  
> [!NOTE]  
>  스크립트 구성 요소에 대한 기본 스크립트 언어를 설정하려면 **옵션** 대화 상자의 **일반** 페이지에서 **스크립트 언어** 옵션을 사용합니다. 자세한 내용은 [일반 페이지](../general-page-of-integration-services-designers-options.md)를 참조하세요.  
  
 데이터 흐름 변환 구성 요소는 하나의 입력을 사용하며 하나 이상의 출력을 지원합니다. 구성 요소의 입력과 출력을 구성하는 것은 사용자 지정 스크립트를 작성하기 전에 메타데이터 디자인 모드에서 **스크립트 변환 편집기**를 사용하여 완료해야 하는 단계 중 하나입니다.  
  
### <a name="configuring-input-columns"></a>입력 열 구성  
 변환 구성 요소에서는 하나의 입력을 사용합니다.  
  
 **스크립트 변환 편집기**의 **입력 열** 페이지에 나타나는 열 목록에는 업스트림 데이터 흐름 구성 요소의 출력에서 가져온 사용 가능한 열이 표시됩니다. 이 목록에서 변환하거나 전달할 열을 선택합니다. 현재 위치에서 변환할 모든 열은 읽기/쓰기로 표시합니다.  
  
 **스크립트 변환 편집기**의 **입력 열** 페이지에 대한 자세한 내용은 [스크립트 변환 편집기&#40;입력 열 페이지&#41;](../data-flow/transformations/script-component.md)를 참조하세요.  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>입력, 출력 및 출력 열 구성  
 변환 구성 요소는 하나 이상의 출력을 지원합니다.  
  
 **스크립트 변환 편집기**의 **입/출력** 페이지에서는 단일 출력이 만들어져 있지만 해당 출력에 열은 없음을 확인할 수 있습니다. 편집기의 이 페이지에서 다음과 같은 항목을 구성할 수 있습니다.  
  
-   예기치 않은 값이 포함된 행에 대한 시뮬레이션된 오류 출력과 같은 추가 출력을 하나 이상 만들 수 있습니다. 동기 변환 구성 요소의 출력을 관리하려면 **출력 추가** 및 **출력 제거** 단추를 사용합니다. 각 행을 한 출력 또는 다른 출력으로 리디렉션하도록 지정하지 않은 경우에는 모든 입력 행이 사용 가능한 모든 출력으로 전송됩니다. 출력의 **ExclusionGroup** 속성에 0이 아닌 정수 값을 지정하면 행을 리디렉션하도록 지정할 수 있습니다. 출력을 식별하기 위해 **ExclusionGroup**에 입력하는 특정 정수 값은 중요하지 않지만 지정한 출력 그룹에는 일관되게 동일한 정수를 사용해야 합니다.  
  
    > [!NOTE]  
    >  모든 행을 출력하지 않으려는 경우 단일 출력과 함께 0이 아닌 **ExclusionGroup** 속성 값을 사용할 수도 있습니다. 그러나 이 경우 출력으로 보낼 각 행에 대해 **DirectRowTo\<outputbuffer>** 메서드를 명시적으로 호출해야 합니다.  
  
-   입력 및 출력에 보다 알기 쉬운 이름을 지정할 수 있습니다. 스크립트 구성 요소에서는 이러한 이름을 사용하여 스크립트에서 입력 및 출력을 참조하는 데 사용할 형식화된 접근자 속성을 생성합니다.  
  
-   동기 변환의 경우 열을 현재 상태로 둘 수 있습니다. 일반적으로 동기 변환에서는 데이터 흐름에 열을 추가하지 않습니다. 데이터는 버퍼의 현재 위치에서 수정되고 해당 버퍼는 데이터 흐름의 다음 구성 요소로 전달됩니다. 이 경우 변환의 출력에서 출력 열을 명시적으로 추가하거나 구성할 필요가 없습니다. 출력은 편집기에서 명시적으로 정의된 열이 없는 상태로 나타납니다.  
  
-   행 수준 오류에 대한 시뮬레이션된 오류 출력에 새 열을 추가할 수 있습니다. 일반적으로 동일한 **ExclusionGroup**의 여러 출력에는 동일한 출력 열 집합이 있습니다. 그러나 시뮬레이션된 오류 출력을 만드는 경우 오류 정보를 포함할 다른 열을 추가할 수 있습니다. 데이터 흐름 엔진에서 오류 행을 처리하는 방법은 [데이터 흐름 구성 요소에서 오류 출력 사용](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)을 참조하세요. 스크립트 구성 요소에서는 개발자가 직접 코드를 작성하여 추가 열을 적절한 오류 정보로 채워야 합니다. 자세한 내용은 [스크립트 구성 요소의 오류 출력 시뮬레이션](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)을 참조하세요.  
  
 **스크립트 변환 편집기**의 **입/출력** 페이지에 대한 자세한 내용은 [스크립트 변환 편집기&#40;입/출력 페이지&#41;](../data-flow/transformations/script-component.md)를 참조하세요.  
  
### <a name="adding-variables"></a>변수 추가  
 스크립트에서 기존 변수를 사용하려는 경우 **스크립트 변환 편집기**의 **스크립트** 페이지에 있는 **ReadOnlyVariables** 및 **ReadWriteVariables** 속성 필드에서 해당 변수를 추가할 수 있습니다.  
  
 속성 필드에 여러 변수를 추가하는 경우 변수 이름을 쉼표로 구분하십시오. 또한 **ReadOnlyVariables** 및 **ReadWriteVariables** 속성 필드 옆에 있는 줄임표( **...** ) 단추를 클릭한 다음, **변수 선택** 대화 상자에서 변수를 선택하면 여러 개의 변수를 선택할 수 있습니다.  
  
 스크립트 구성 요소에서 변수를 사용하는 방법에 대한 일반적인 내용은 [스크립트 구성 요소에서 변수 사용](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)을 참조하세요.  
  
 **스크립트 변환 편집기**의 **스크립트** 페이지에 대한 자세한 내용은 [스크립트 변환 편집기&#40;스크립트 페이지&#41;](../data-flow/transformations/script-component.md)를 참조하세요.  
  
## <a name="scripting-a-synchronous-transformation-component-in-code-design-mode"></a>코드 디자인 모드에서 동기 변환 구성 요소 스크립팅  
 구성 요소에 대한 메타데이터를 구성한 후에는 사용자 지정 스크립트를 작성할 수 있습니다. **스크립트 변환 편집기**의 **스크립트** 페이지에서 **스크립트 편집**을 클릭하여 사용자 지정 스크립트를 추가할 수 있는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] VSTA([!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications) IDE를 엽니다. 사용하는 스크립트 언어는 **스크립트** 페이지에서 **ScriptLanguage** 속성에 대한 스크립트 언어로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 중에서 선택한 언어에 따라 달라집니다.  
  
 스크립트 구성 요소를 사용하여 만든 모든 종류의 구성 요소에 적용되는 중요한 정보는 [스크립트 구성 요소 코딩 및 디버깅](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)을 참조하세요.  
  
### <a name="understanding-the-auto-generated-code"></a>자동 생성 코드 이해  
 변환 구성 요소를 만들고 구성한 후 VSTA IDE를 열면 편집 가능한 **ScriptMain** 클래스가 **ProcessInputRow** 메서드에 대한 스텁과 함께 코드 편집기에 나타납니다. 이 **ScriptMain** 클래스에서 사용자 지정 코드를 작성해야 하며 **ProcessInputRow**는 변환 구성 요소에서 가장 중요한 메서드입니다.  
  
 VSTA에서 **프로젝트 탐색기** 창을 열면 스크립트 구성 요소에서 읽기 전용 **BufferWrapper** 및 **ComponentWrapper** 프로젝트 항목도 생성했음을 확인할 수 있습니다. **ScriptMain** 클래스는 **ComponentWrapper** 프로젝트 항목의 **UserComponent** 클래스에서 상속됩니다.  
  
 런타임에 데이터 흐름 엔진에서 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 부모 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> 메서드를 재정의하는 **UserComponent** 클래스의 **ProcessInput** 메서드를 호출합니다. 그러면 **ProcessInput** 메서드에서 입력 버퍼의 행을 반복하고 각 행에 대해 **ProcessInputRow** 메서드를 한 번씩 호출합니다.  
  
### <a name="writing-your-custom-code"></a>사용자 지정 코드 작성  
 동기 출력을 사용하는 변환 구성 요소는 모든 데이터 흐름 구성 요소 중에서 작성하기가 가장 간단합니다. 예를 들어 이 항목의 뒷부분에 있는 단일 출력 예는 다음과 같은 사용자 지정 코드로 구성되어 있습니다.  
  
```vb  
Row.City = UCase(Row.City)  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
```  
  
 사용자 지정 동기 변환 구성 요소 만들기를 마치려면 재정의된 **ProcessInputRow** 메서드를 사용하여 입력 버퍼의 각 행에 있는 데이터를 변환합니다. 데이터 흐름 엔진에서는 이 버퍼가 가득 차면 데이터 흐름의 다음 구성 요소로 버퍼를 전달합니다.  
  
 요구 사항에 따라 **ScriptMain** 클래스에서 사용할 수 있는 **PreExecute** 및 **PostExecute** 메서드에서 스크립트를 작성하여 예비 또는 최종 처리를 수행할 수도 있습니다.  
  
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
  
 이 예에서 스크립트 구성 요소는 개발자가 구성한 출력의 이름을 따라 **DirectRowTo\<OutputBufferX>** 메서드를 자동으로 생성합니다. 비슷한 코드를 사용하여 오류 출력을 시뮬레이션된 오류 출력으로 전송할 수 있습니다.  
  
## <a name="examples"></a>예  
 이 예에서는 **ScriptMain** 클래스에서 동기 변환 구성 요소를 만드는 데 필요한 사용자 지정 코드를 보여 줍니다.  
  
> [!NOTE]  
>  이 예에서는 **AdventureWorks** 예제 데이터베이스의 **Person.Address** 테이블을 사용하고 이 테이블의 첫 번째 열과 네 번째 열, **intAddressID** 및 **nvarchar(30)City**를 데이터 흐름을 통해 전달합니다. 이 섹션의 원본, 변환 및 대상 예제에는 동일한 데이터가 사용됩니다. 각 예에 대해 필수 구성 요소 및 가정도 설명되어 있습니다.  
  
### <a name="single-output-synchronous-transformation-example"></a>단일 출력 동기 변환 예  
 이 예에서는 단일 출력을 사용하는 동기 변환 구성 요소를 보여 줍니다. 이 변환에서는 **AddressID** 열을 전달하고 **City** 열을 대문자로 변환합니다.  
  
 이 예제 코드를 실행하려면 다음과 같이 패키지와 구성 요소를 구성해야 합니다.  
  
1.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 변환으로 구성합니다.  
  
2.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 원본 또는 다른 변환의 출력을 새 변환 구성 요소에 연결합니다. 이 출력은 **AdventureWorks** 예제 데이터베이스의 **Person.Address** 테이블에서 **AddressID** 및 **City** 열이 포함된 데이터를 제공해야 합니다.  
  
3.  **스크립트 변환 편집기**를 엽니다. **입력 열** 페이지에서 **AddressID** 및 **City** 열을 선택합니다. **City** 열을 읽기/쓰기로 표시합니다.  
  
4.  **입/출력** 페이지에서 입력 및 출력의 이름을 **MyAddressInput** 및 **MyAddressOutput**과 같이 보다 알기 쉬운 이름으로 바꿉니다. 출력의 **SynchronousInputID**는 입력의 **ID**에 해당합니다. 따라서 출력 열을 추가하고 구성하지 않아도 됩니다.  
  
5.  **스크립트** 페이지에서 **스크립트 편집**을 클릭하고 다음 스크립트를 입력합니다. 그런 다음 스크립트 개발 환경 및 **스크립트 변환 편집기**를 닫습니다.  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상이나 [스크립트 구성 요소를 사용하여 대상 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)에서 보여 준 예제 대상 구성 요소와 같이 **AddressID** 및 **City** 열을 필요로 하는 대상 구성 요소를 만들고 구성합니다. 그런 다음 변환의 출력을 대상 구성 요소에 연결합니다. **AdventureWorks** 데이터베이스에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 실행하여 대상 테이블을 만들 수 있습니다.  
  
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
 이 예에서는 두 개의 출력을 사용하는 동기 변환 구성 요소를 보여 줍니다. 이 변환에서는 **AddressID** 열을 전달하고 **City** 열을 대문자로 변환합니다. 도시 이름이 Redmond이면 해당 행은 한 출력으로 전송되고 다른 모든 행은 다른 출력으로 전송됩니다.  
  
 이 예제 코드를 실행하려면 다음과 같이 패키지와 구성 요소를 구성해야 합니다.  
  
1.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 변환으로 구성합니다.  
  
2.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 원본 또는 다른 변환의 출력을 새 변환 구성 요소에 연결합니다. 이 출력은 **AdventureWorks** 샘플 데이터베이스에 있는 **Person.Address** 테이블의 데이터를 제공해야 하며, 이 데이터에는 적어도 **AddressID** 및 **City** 열이 포함됩니다.  
  
3.  **스크립트 변환 편집기**를 엽니다. **입력 열** 페이지에서 **AddressID** 및 **City** 열을 선택합니다. **City** 열을 읽기/쓰기로 표시합니다.  
  
4.  **입/출력** 페이지에서 두 번째 출력을 만듭니다. 새 출력을 추가한 후에는 해당 **SynchronousInputID**를 입력의 **ID**로 설정해야 합니다. 기본적으로 만들어진 첫 번째 출력에는 이 속성이 이미 설정되어 있습니다. 상호 배타적인 두 개의 출력 간에 입력 행을 분리하려면 각 출력에 대해 **ExclusionGroup** 속성을 0이 아닌 동일한 값으로 설정합니다. 출력에 출력 열을 추가할 필요는 없습니다.  
  
5.  입력 및 출력 이름을 **MyAddressInput**, **MyRedmondAddresses** 및 **MyOtherAddresses**와 같이 보다 알기 쉬운 이름으로 바꿉니다.  
  
6.  **스크립트** 페이지에서 **스크립트 편집**을 클릭하고 다음 스크립트를 입력합니다. 그런 다음 스크립트 개발 환경 및 **스크립트 변환 편집기**를 닫습니다.  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상, 플랫 파일 대상 또는 [스크립트 구성 요소를 사용하여 대상 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)에서 보여 준 예제 대상 구성 요소와 같이 **AddressID** 및 **City** 열을 필요로 하는 두 개의 대상 구성 요소를 만들고 구성합니다. 그런 다음 변환의 각 출력을 대상 구성 요소 중 하나에 연결합니다. **AdventureWorks** 데이터베이스에서 다음과 같이 고유한 테이블 이름으로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 실행하여 대상 테이블을 만들 수 있습니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [동기 및 비동기 변환 이해](~/integration-services/understanding-synchronous-and-asynchronous-transformations.md)  
 [스크립트 구성 요소를 사용하여 비동기 변환 만들기](~/integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
 [동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발](~/integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)
