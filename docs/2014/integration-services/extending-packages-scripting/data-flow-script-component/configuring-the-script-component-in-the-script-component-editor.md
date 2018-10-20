---
title: 스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script component
- Script Component Editor
- SSIS Script component, configuring
- Script component [Integration Services], configuring
ms.assetid: 586dd799-f383-4d6d-b1a1-f09233d14f0a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f2b36eef7c358fde58316bafc06697c992f3918b
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461034"
---
# <a name="configuring-the-script-component-in-the-script-component-editor"></a>스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성
  스크립트 구성 요소에서 사용자 지정 코드를 작성하려면, 먼저 만들려는 데이터 흐름 구성 요소의 유형(원본, 변환 또는 대상)을 선택한 다음, **스크립트 변환 편집기**에서 구성 요소의 메타데이터 및 속성을 구성해야 합니다.  
  
## <a name="selecting-the-type-of-component-to-create"></a>만들 구성 요소 유형 선택  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너의 데이터 흐름 창에 스크립트 구성 요소를 추가하면 **스크립트 구성 요소 유형 선택** 대화 상자가 표시됩니다. 이 대화 상자에서 구성 요소를 원본, 변환 또는 대상으로 미리 구성합니다. 이 초기 항목을 선택한 후에 **스크립트 변환 편집기**에서 구성 요소를 계속 구성할 수 있습니다.  
  
 스크립트 구성 요소에 대한 기본 스크립트 언어를 설정하려면 **옵션** 대화 상자의 **일반** 페이지에서 **스크립트 언어** 옵션을 사용합니다. 자세한 내용은 [General Page](../../general-page-of-integration-services-designers-options.md)을 참조하세요.  
  
## <a name="understanding-the-two-design-time-modes"></a>두 가지 디자인 타임 모드 이해  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 스크립트 구성 요소에는 메타데이터 디자인 모드와 코드 디자인 모드의 두 가지 모드가 있습니다.  
  
 **스크립트 변환 편집기**를 열면 구성 요소가 메타데이터 디자인 모드로 전환됩니다. 이 모드에서는 입력 열을 선택하고 출력 및 출력 열을 추가하거나 구성할 수 있지만 코드를 작성할 수는 없습니다. 구성 요소의 메타데이터를 구성한 후에 코드 디자인 모드로 전환하여 스크립트를 작성할 수 있습니다.  
  
 **스크립트 편집**을 클릭하여 코드 디자인 모드로 전환하면, 스크립트 구성 요소에서 추가로 변경하지 할 수 없도록 메타데이터를 잠근 다음 입력 및 출력의 메타데이터에서 기본 코드를 자동으로 생성합니다. 이 자동 생성 코드가 완성된 후 사용자 지정 코드를 입력할 수 있습니다. 코드에서는 자동으로 생성된 기본 클래스를 사용하여 입력 행을 처리하고, 버퍼와 버퍼의 열에 액세스하고, 패키지에서 연결 관리자와 변수를 모두 강력한 형식의 개체로 검색할 수 있습니다.  
  
 코드 디자인 모드에서 사용자 지정 코드를 입력한 후에는 메타데이터 디자인 모드로 다시 전환할 수 있습니다. 메타데이터 디자인 모드로 전환해도 입력한 코드는 삭제되지 않지만 메타데이터를 추가로 변경하면 기본 클래스가 다시 생성됩니다. 메타데이터 변경으로 인해 사용자 지정 코드에서 참조하는 개체가 더 이상 존재하지 않거나 수정된 경우에는 이후 구성 요소의 유효성 검사에 실패할 수 있습니다. 이 경우 다시 생성된 기본 클래스에 대해 성공적으로 컴파일할 수 있도록 코드를 수동으로 수정해야 합니다.  
  
## <a name="configuring-the-component-in-metadata-design-mode"></a>메타데이터 디자인 모드에서 구성 요소 구성  
 메타데이터 디자인 모드에서는 입력 열을 선택하고 출력과 출력 열을 추가 및 구성할 수 있지만 코드를 작성할 수는 없습니다. 구성 요소의 메타데이터를 구성한 후에 코드 디자인 모드로 전환하여 스크립트를 작성해야 합니다.  
  
 사용자 지정 편집기에서 구성해야 하는 속성은 스크립트 구성 요소의 사용 방식에 따라 달라집니다. 스크립트 구성 요소는 원본, 변환 또는 대상으로 구성될 수 있으며, 구성 요소의 사용 방법에 따라 입력이나 출력 또는 모두를 지원합니다. 작성하는 사용자 지정 코드에서는 입력 및 출력 행과 열을 처리합니다.  
  
### <a name="inputs-columns-page-of-the-script-transformation-editor"></a>스크립트 변환 편집기의 입력 열 페이지  
 변환과 대상에 대해서는 **스크립트 변환 편집기**의 **입력 열** 페이지가 표시되지만, 원본에 대해서는 표시되지 않습니다. 이 페이지에서 사용자 지정 스크립트에서 사용할 사용 가능한 입력 열을 선택하고 해당 열에 대한 읽기 전용 또는 읽기/쓰기 권한을 지정합니다.  
  
 이 메타데이터를 기반으로 생성되는 코드 프로젝트에서 BufferWrapper 프로젝트 항목에는 각 입력에 대한 클래스가 포함되며 이 클래스에는 선택한 각 입력 열에 대한 형식화된 접근자 속성이 포함됩니다. 예를 들어 정수를 선택 하면 **CustomerID** 열과 문자열 **CustomerName** 라는 입력 열 `CustomerInput`, BufferWrapper 프로젝트 항목에 포함 될를 `CustomerInput` 클래스 파생 된 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>, 및 `CustomerInput` 클래스는 명명 된 정수 속성을 노출 **CustomerID** 이라는 문자열 속성 **CustomerName**합니다. 이 규칙을 통해 다음과 같이 형식 검사를 사용하는 코드를 작성할 수 있습니다.  
  
```vb  
Dim currentCustomerID as Integer = CustomerInput.CustomerID  
Dim currentCustomerName as String = CustomerInput.CustomerName  
```  
  
 특정 유형의 데이터 흐름 구성 요소에 대한 입력 열을 구성하는 방법에 대한 자세한 내용은 [특정 유형의 스크립트 구성 요소 개발](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)의 해당 예제를 참조하세요.  
  
### <a name="inputs-and-outputs-page-of-the-script-transformation-editor"></a>스크립트 변환 편집기의 입/출력 페이지  
 **스크립트 변환 편집기**의 **입/출력** 페이지는 원본, 변환 및 대상에 대해 표시됩니다. 이 페이지에서는 사용자 지정 스크립트에서 사용할 입력, 출력 및 출력 열을 추가하고 제거하고 구성할 수 있습니다. 단 다음과 같은 제한 사항이 있습니다.  
  
-   원본으로 사용되는 스크립트 구성 요소는 입력을 사용하지 않으며 여러 출력을 지원합니다.  
  
-   변환으로 사용되는 스크립트 구성 요소는 하나의 입력과 여러 출력을 지원합니다.  
  
-   대상으로 사용되는 스크립트 구성 요소는 하나의 입력을 지원하며 출력은 사용하지 않습니다.  
  
 이 메타데이터를 기반으로 생성되는 코드 프로젝트에서 BufferWrapper 프로젝트 항목에는 각 입력 및 출력에 대한 클래스가 포함됩니다. 예를 들어 명명 된 출력을 만들려면 `CustomerOutput`, BufferWrapper 프로젝트 항목에 포함 될를 `CustomerOutput` 에서 파생 된 클래스 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>, 및 `CustomerOutput` 클래스에는 만든 각 출력 열에 대 한 형식화 된 접근자 속성이 포함 됩니다.  
  
 **입/출력** 페이지에서만 출력 열을 구성할 수 있습니다. **입력 열** 페이지에서 변환 및 대상에 대한 입력 열을 선택할 수 있습니다. BufferWrapper 프로젝트 항목에 만들어진 형식화된 접근자 속성은 출력 열에 대한 쓰기 전용 속성이 됩니다. 입력 열의 접근자 속성은 **입력 열** 페이지에서 각 열에 대해 선택한 사용 유형에 따라 읽기 전용 또는 읽기/쓰기가 됩니다.  
  
 특정 유형의 데이터 흐름 구성 요소에 대한 입력 및 출력을 구성하는 방법에 대한 자세한 내용은 [특정 유형의 스크립트 구성 요소 개발](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)의 해당 예제를 참조하세요.  
  
> [!NOTE]  
>  오류 행의 자동 처리를 위해 스크립트 구성 요소의 출력을 오류 출력으로 직접 구성할 수는 없지만 적절할 때 추가 출력을 만들고 스크립트를 사용하여 행을 이 출력으로 전송하는 방식으로 오류 출력의 기능을 재현할 수 있습니다. 자세한 내용은 [스크립트 구성 요소의 오류 출력 시뮬레이션](../../data-flow/transformations/script-component.md)을 참조하세요.  
  
#### <a name="exclusiongroup-and-synchronousinputid-properties-of-outputs"></a>출력의 ExclusionGroup 및 SynchronousInputID 속성  
 `ExclusionGroup` 속성 값은 동기 출력을 사용하는 변환에서만 0이 아니며, 이러한 변환에서 코드는 필터링 또는 분기를 수행하고 0이 아닌 동일한 `ExclusionGroup` 값을 공유하는 출력 중 하나로 각 행을 전송합니다. 예를 들어 변환에서는 행을 기본 출력이나 오류 출력 중 하나로 전송할 수 있습니다. 이 경우 추가 출력을 만들 때는 `SynchronousInputID` 속성의 값을 구성 요소의 입력에 대한 `ID`와 일치하는 정수로 설정해야 합니다.  
  
 `SynchronousInputID` 속성 값은 동기 출력을 사용하는 변환에서만 0이 아닙니다. 이 속성 값이 0이면 해당 출력이 비동기적임을 나타냅니다. 행이 선택한 출력으로 전달되며 이때 새 행이 추가되지는 않는 동기 출력의 경우 이 속성에는 구성 요소의 입력에 대한 `ID`가 들어 있어야 합니다.  
  
> [!NOTE]  
>  경우는 **스크립트 변환 편집기** 설정 첫 번째 출력을 만드는 `SynchronousInputID` 출력 속성은 `ID` 구성 요소의 입력 합니다. 그러나 이후 출력을 만들 때는 이러한 출력의 `SynchronousInputID` 속성을 0으로 설정합니다.  
>   
>  동기 출력을 사용하는 구성 요소를 만드는 경우 각 출력의 `SynchronousInputID` 속성은 구성 요소의 입력에 대한 `ID`로 설정되어야 합니다. 따라서 편집기에서 첫 번째 출력 이후에 만든 각 출력의 `SynchronousInputID` 값은 0에서 구성 요소의 입력에 대한 `ID`로 변경되어야 합니다.  
>   
>  비동기 출력을 사용하는 구성 요소를 만드는 경우 각 출력의 `SynchronousInputID` 속성은 0으로 설정되어야 합니다. 따라서 첫 번째 출력의 `SynchronousInputID` 값은 구성 요소의 입력에 대한 `ID`에서 0으로 변경되어야 합니다.  
  
 스크립트 구성 요소에서 두 개의 동기 출력 중 하나에 행을 보내는 예제는 [스크립트 구성 요소를 사용하여 동기 변환 만들기](../../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)를 참조하세요.  
  
### <a name="object-names-in-generated-script"></a>생성된 스크립트의 개체 이름  
 스크립트 구성 요소에서는 입력 및 출력의 이름을 구문 분석하고, 입력 및 출력의 열 이름을 구문 분석하며, 이러한 이름을 기반으로 BufferWrapper 프로젝트 항목에 클래스 및 속성을 생성합니다. 찾은 이름에 유니코드 범주 `UppercaseLetter`, `LowercaseLetter`, `TitlecaseLetter`, `ModifierLetter`, `OtherLetter` 또는 `DecimalDigitLetter`에 속하지 않는 문자가 포함된 경우 유효하지 않은 문자는 생성되는 이름에서 삭제됩니다. 예를 들어 공백은 삭제되므로 **FirstName** 및 [**First Name**] 이름의 두 입력 열이 모두 **FirstName**이라는 열 이름을 갖는 것으로 해석되며 예기치 않은 결과가 발생합니다. 이러한 문제가 발생하지 않도록 하려면 스크립트 구성 요소에서 사용하는 입력 및 출력의 이름과 입력 및 출력 열의 이름에는 이 섹션에 나열된 유니코드 범주의 문자만 사용해야 합니다.  
  
### <a name="script-page-of-the-script-transformation-editor"></a>스크립트 변환 편집기의 스크립트 페이지  
 **스크립트 태스크 편집기**의 **스크립트** 페이지에서는 스크립트 태스크에 대한 고유한 이름과 설명을 지정합니다. 다음 속성의 값을 지정할 수도 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 와 그 이후 버전에서는 모든 스크립트가 미리 컴파일됩니다. 이전 버전에서는 개발자가 태스크의 `Precompile` 속성을 설정하여 스크립트가 미리 컴파일되었는지 여부를 지정했습니다.  
  
#### <a name="validateexternalmetadata-property"></a>ValidateExternalMetadata 속성  
 `ValidateExternalMetadata` 속성의 부울 값은 구성 요소에서 디자인 타임에 외부 데이터 원본에 대한 유효성 검사를 수행해야 하는지 아니면 런타임까지 유효성 검사를 연기해야 하는지를 지정합니다. 기본적으로 이 속성의 값은 `True`입니다. 즉, 디자인 타임과 런타임 모두에 외부 메타데이터의 유효성이 검사됩니다. 디자인 타임에 외부 데이터 원본을 사용할 수 없는 경우 이 속성의 값을 `False`로 설정할 수 있습니다. 예를 들어 패키지가 원본을 다운로드하거나 런타임에만 대상을 만드는 경우가 이러한 경우에 해당합니다.  
  
#### <a name="readonlyvariables-and-readwritevariables-properties"></a>ReadOnlyVariables 및 ReadWriteVariables 속성  
 쉼표로 구분된 기존 변수 목록을 이러한 속성의 값으로 입력하여 스크립트 구성 요소 코드 내에서 해당 변수를 읽기 전용 또는 읽기/쓰기 권한으로 액세스할 수 있게 할 수 있습니다. 변수는 코드에서 자동으로 생성된 기본 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> 속성을 통해 액세스할 수 있습니다. 자세한 내용은 [스크립트 구성 요소에서 변수 사용](using-variables-in-the-script-component.md)을 참조하세요.  
  
> [!NOTE]  
>  변수 이름은 대소문자를 구분합니다.  
  
#### <a name="scriptlanguage"></a>ScriptLanguage  
 스크립트 구성 요소에 대한 프로그래밍 언어로 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#을 선택할 수 있습니다.  
  
#### <a name="edit-script-button"></a>스크립트 편집 단추  
 **스크립트 편집** 단추를 클릭하면 사용자 지정 스크립트를 작성할 수 있는 VSTA([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications) IDE가 열립니다. 자세한 내용은 [스크립트 구성 요소 코딩 및 디버깅](coding-and-debugging-the-script-component.md)을 참조하세요.  
  
### <a name="connection-managers-page-of-the-script-transformation-editor"></a>스크립트 변환 편집기의 연결 관리자 페이지  
 **스크립트 변환 편집기**의 **연결 관리자** 페이지에서는 사용자 지정 스크립트에 사용할 연결 관리자를 추가하거나 제거합니다. 일반적으로 원본 또는 대상 구성 요소를 만들 때는 연결 관리자를 참조해야 합니다.  
  
 이 메타데이터를 기반으로 생성되는 코드 프로젝트에서 `ComponentWrapper` 프로젝트 항목에는 선택된 각 연결 관리자에 대한 형식화된 접근자 속성이 있는 `Connections` 컬렉션 클래스가 포함됩니다. 형식화된 각 접근자 속성은 연결 관리자와 동일한 이름을 가지며 연결 관리자에 대한 참조를 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100>의 인스턴스로 반환합니다. 예를 들어 편집기의 **연결 관리자** 페이지에서 `MyADONETConnection`이라는 연결 관리자를 추가한 경우 다음 코드를 사용하여 스크립트에서 해당 연결 관리자에 대한 참조를 가져올 수 있습니다.  
  
```vb  
Dim myADONETConnectionManager As IDTSConnectionManager100 = _  
    Me.Connections.MyADONETConnection  
```  
  
 자세한 내용은 [스크립트 구성 요소에서 데이터 원본에 연결](connecting-to-data-sources-in-the-script-component.md)을 참조하세요.  
  
![Integration Services 아이콘 (작은)](../../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [스크립트 구성 요소 코딩 및 디버깅](coding-and-debugging-the-script-component.md)  
  
  
