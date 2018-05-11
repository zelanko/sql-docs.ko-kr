---
title: 스크립트 구성 요소 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.scriptcomponentdetails.f1
- sql13.dts.designer.scriptcomponent.f1
- sql13.dts.designer.scriptcomponent.connections.f1
- sql13.dts.designer.scriptcomponent.inputcolumn.f1
- sql13.dts.designer.scriptcomponent.columnproperties.f1
- sql13.dts.designer.scriptcomponent.script.f1
helpviewer_keywords:
- Script transformation
- scripts [Integration Services], transformations
- Script component [Integration Services], about Script component
- Script component [Integration Services]
ms.assetid: 131c2d0c-2e33-4785-94af-ada5c049821e
caps.latest.revision: 70
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 28b0e0036e6c85e6898c4d2f24007eb8915b3703
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="script-component"></a>스크립트 구성 요소
  스크립트 구성 요소는 스크립트를 호스팅하고 패키지에서 사용자 지정 스크립트 코드를 포함시키고 실행할 수 있도록 합니다. 패키지의 스크립트 구성 요소는 다음 용도로 사용할 수 있습니다.  
  
-   데이터 흐름에서 여러 변환을 사용하는 대신 데이터에 여러 변환을 적용합니다. 예를 들어 스크립트로 두 열에 값을 추가하고 합계의 평균을 계산할 수 있습니다.  
  
-   기존 .NET 어셈블리에 있는 비즈니스 규칙에 액세스합니다. 예를 들어 스크립트로 **Income** 열에서 유효한 값 범위를 지정하는 비즈니스 규칙을 적용할 수 있습니다.  
  
-   [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 식 문법에서 제공되는 함수와 연산자 외에 사용자 지정 수식과 함수를 사용합니다. 예를 들어 LUHN 수식을 사용하는 신용 카드 번호의 유효성을 검사합니다.  
  
-   열 데이터의 유효성을 검사하고 잘못된 데이터가 포함된 레코드는 건너 뜁니다. 예를 들어 스크립트로 적절한 우편 요금을 평가하여 금액이 너무 높거나 낮은 레코드를 건너뛸 수 있습니다.  
  
 스크립트 구성 요소를 사용하면 데이터 흐름에 사용자 지정 함수를 쉽고 빠르게 포함시킬 수 있습니다. 하지만 여러 패키지에서 스크립트 코드를 재사용하려는 경우에는 스크립트 구성 요소 대신 사용자 지정 구성 요소를 프로그래밍하는 방식을 고려하십시오. 자세한 내용은 [사용자 지정 데이터 흐름 구성 요소 개발](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)을 참조하세요.  
  
> [!NOTE]  
>  스크립트 구성 요소에 NULL인 열 값을 읽으려고 하는 스크립트가 포함되어 있는 경우 패키지를 실행할 때 스크립트 구성 요소가 실패합니다. 스크립트에서 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.IsNull%2A> 메서드를 사용하여 열 값을 읽기 전에 열이 NULL인지 여부를 확인하는 것이 좋습니다.  
  
 스크립트 구성 요소는 원본, 변환 또는 대상으로 사용될 수 있습니다. 이 구성 요소는 하나의 입력과 여러 출력을 지원합니다. 구성 요소의 사용 방법에 따라 입력이나 출력 또는 모두를 지원합니다. 스크립트는 입력 또는 출력의 모든 행에 의해 실행됩니다.  
  
-   원본으로 사용되는 스크립트 구성 요소는 여러 출력을 지원합니다.  
  
-   변환으로 사용되는 스크립트 구성 요소는 하나의 입력과 여러 출력을 지원합니다.  
  
-   대상으로 사용되는 스크립트 구성 요소는 하나의 입력을 지원합니다.  
  
 스크립트 구성 요소는 오류 출력을 지원하지 않습니다.  
  
 스크립트 구성 요소를 패키지에 적합한 선택 항목으로 결정한 후에는 입력과 출력을 구성하고 구성 요소에서 사용하는 스크립트를 개발하며 구성 요소 자체를 구성해야 합니다.  
  
## <a name="understanding-the-script-component-modes"></a>스크립트 구성 요소 모드 이해  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 스크립트 구성 요소에는 두 가지 모드인 메타데이터 디자인 모드와 코드 디자인 모드가 있습니다. 메타데이터 디자인 모드에서는 스크립트 구성 요소 입력 및 출력을 추가하고 수정할 수 있지만 코드를 작성할 수는 없습니다. 따라서 입력과 출력이 구성된 다음에는 스크립트를 작성하기 위해 코드 디자인 모드로 전환해야 합니다. 스크립트 구성 요소는 입력 및 출력의 메타데이터로부터 기본 코드를 자동으로 생성합니다. 스크립트 구성 요소가 기본 코드를 생성한 다음 메타데이터를 변경하면 업데이트된 기본 코드가 사용자의 코드와 호환되지 않기 때문에 사용자의 코드가 더 이상 컴파일되지 않을 수 있습니다.  
  
## <a name="writing-the-script-that-the-component-uses"></a>구성 요소에서 사용하는 스크립트 작성  
 스크립트 구성 요소는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) as the environment in which you write the scripts. VSTA는 **스크립트 변환 편집기**를 통해 액세스할 수 있습니다. 자세한 내용은 [스크립트 변환 편집기&#40;스크립트 페이지&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md)을 참조하세요.  
  
 스크립트 구성 요소는 구성 요소 메타데이터를 나타내는 ScriptMain이라는 자동 생성된 클래스가 포함된 VSTA 프로젝트를 제공합니다. 예를 들어 스크립트 구성 요소가 3개의 출력이 있는 변환으로 사용되는 경우 ScriptMain에는 각 출력에 대한 메서드가 포함됩니다. ScriptMain은 스크립트에 대한 진입점입니다.  
  
 VSTA에는 색 구분 기능이 포함된 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 편집기, IntelliSense, 개체 브라우저 등 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 환경의 모든 표준 기능이 포함됩니다. 스크립트 구성 요소에서 사용하는 스크립트는 패키지 정의에 저장됩니다. 패키지를 디자인할 때 스크립트 코드는 임시로 프로젝트 파일에 기록됩니다.  
  
 VSTA는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 및 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 프로그래밍 언어를 지원합니다.  
  
 스크립트 구성 요소를 프로그래밍하는 방법은 [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)을 참조하십시오. 스크립트 구성 요소를 원본, 변환 또는 대상으로 구성하는 방법에 대한 자세한 내용은 [Developing Specific Types of Script Components](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)을 참조하십시오. 스크립트 구성 요소 사용 방법을 보여 주는 ODBC 대상 등의 추가 예는 [Additional Script Component Examples](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)를 참조하십시오.  
  
> [!NOTE]  
>  스크립트가 미리 컴파일되었는지 여부를 지정할 수 있었던 이전 버전과는 달리 모든 스크립트가 [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 이상 버전에 미리 컴파일되어 있습니다. 스크립트가 미리 컴파일된 경우 런타임 시 언어 엔진이 로드되지 않으므로 패키지가 보다 신속하게 실행됩니다. 그러나 미리 컴파일된 이진 파일은 상당한 디스크 공간을 소비합니다.  
  
## <a name="configuring-the-script-component"></a>스크립트 구성 요소 구성  
 다음과 같은 방법으로 스크립트 구성 요소를 구성할 수 있습니다.  
  
-   참조할 입력 열을 선택합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용할 경우 입력을 한 개만 구성할 수 있습니다.  
  
-   구성 요소에서 실행할 스크립트를 제공합니다.  
  
-   스크립트 언어를 지정합니다.  
  
-   쉼표로 구분된 읽기 전용 및 읽기/쓰기 변수 목록을 제공합니다.  
  
-   출력을 추가하고 스크립트가 할당할 출력 열을 추가합니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
### <a name="configuring-the-script-component-in-the-designer"></a>디자이너에서 스크립트 구성 요소 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
### <a name="configuring-the-script-component-programmatically"></a>프로그래밍 방식으로 스크립트 구성 요소 구성  
 **속성** 창을 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="select-script-component-type"></a>스크립트 구성 요소 유형 선택
  **스크립트 구성 요소 유형 선택** 대화 상자를 사용하여 원본, 변환 또는 대상으로 사용하도록 미리 구성된 스크립트 변환 생성 여부를 지정할 수 있습니다.  
  
 스크립트 구성 요소에 대한 자세한 내용은 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)을 참조하세요. 스크립트 구성 요소 프로그래밍 방법은 [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)을 참조하십시오.  
  
### <a name="options"></a>변수  
 **원본**, **대상**또는 **변환** 에서 선택한 내용에 따라 스크립트 변환 편집기의 페이지와 스크립트 변환 구성이 달라집니다.  
  
## <a name="script-transformation-editor-connection-managers-page"></a>스크립트 변환 편집기(연결 관리자 페이지)
  **스크립트 변환 편집기** 의 **연결 관리자** 를 사용하여 스크립트에서 사용할 연결을 지정할 수 있습니다.  
  
 스크립트 구성 요소에 대한 자세한 내용은 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)을 참조하세요. 스크립트 구성 요소 프로그래밍 방법은 [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)을 참조하십시오.  
  
### <a name="options"></a>변수  
 **Connection managers**  
 스크립트에 사용할 수 있는 연결 목록을 표시합니다.  
  
 **이름**  
 연결에 대한 설명이 포함된 고유 이름을 입력합니다.  
  
 **연결 관리자**  
 사용 가능한 연결 관리자 목록에서 선택하거나 **\<새 연결>** 을 선택하여 **SSIS 연결 관리자 추가** 대화 상자를 엽니다.  
  
 **설명**  
 연결에 대한 설명을 입력합니다.  
  
 **추가**  
 **연결 관리자** 목록에 다른 연결을 추가합니다.  
  
 **제거**  
 선택한 연결을 **연결 관리자** 목록에서 제거합니다.  
  
## <a name="script-transformation-editor-input-columns-page"></a>스크립트 변환 편집기(입력 열 페이지)
  **스크립트 변환 편집기** 대화 상자의 **입력 열** 페이지를 사용하여 입력 열의 속성을 설정할 수 있습니다.  
  
> [!NOTE]  
>  **입력 열** 페이지는 출력은 있지만 입력은 없는 원본 구성 요소에 대해서는 표시되지 않습니다.  
  
 스크립트 구성 요소에 대한 자세한 내용은 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)을 참조하세요. 스크립트 구성 요소 프로그래밍 방법은 [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)을 참조하십시오.  
  
### <a name="options"></a>변수  
 **입력 이름**  
 사용 가능한 입력 목록에서 선택합니다.  
  
 **사용 가능한 입력 열**  
 확인란을 사용하여 스크립트 변환에서 사용할 열을 지정합니다.  
  
 **입력 열**  
 각 행에 대해 사용 가능한 입력 열 목록에서 선택합니다. 선택 내용에 따라 **사용 가능한 입력 열**테이블의 확인란이 달라집니다.  
  
 **출력 별칭**  
 각 출력 열의 별칭을 입력합니다. 기본값은 입력 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
 **사용 유형**  
 스크립트 변환에서 각 열을 **ReadOnly** 로 처리할지, 아니면 **ReadWrite**로 처리할지를 지정합니다.  
  
## <a name="script-transformation-editor-inputs-and-outputs-page"></a>스크립트 변환 편집기(입/출력 페이지)
  **스크립트 변환 편집기** 대화 상자의 **입/출력** 페이지를 사용하여 스크립트 변환에 대한 입력 및 출력을 추가, 제거 및 구성할 수 있습니다.  
  
> [!NOTE]  
>  원본 구성 요소는 출력이 있고 입력이 없지만 대상 구성 요소는 입력이 있고 출력이 없습니다. 변환은 입력과 출력이 모두 있습니다.  
  
 스크립트 구성 요소에 대한 자세한 내용은 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)을 참조하세요. 스크립트 구성 요소 프로그래밍 방법은 [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)을 참조하십시오.  
  
### <a name="options"></a>변수  
 **Inputs and outputs**  
 왼쪽에서 입력 또는 출력을 선택하여 오른쪽에 있는 테이블에서 해당 속성을 확인합니다. 편집할 수 있는 속성은 선택하는 입력 또는 출력에 따라 다릅니다. 표시된 속성 중 다수는 읽기 전용입니다. 개별 속성에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
 [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
 [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 **출력 추가**  
 목록에 출력을 추가합니다.  
  
 **열 추가**  
 새 출력 열을 추가할 폴더를 선택한 다음 **열 추가**를 클릭하여 열을 추가합니다.  
  
 **출력 제거**  
 출력을 선택한 다음 **출력 제거**를 클릭하여 제거합니다.  
  
 **열 제거**  
 열을 선택한 다음 **열 제거**를 클릭하여 제거합니다.  
  
## <a name="script-transformation-editor-script-page"></a>스크립트 변환 편집기(스크립트 페이지)
  **스크립트 변환 편집기** 대화 상자의 **스크립트** 탭을 사용하여 스크립트 및 관련 속성을 지정할 수 있습니다.  
  
 스크립트 구성 요소에 대한 자세한 내용은 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)을 참조하세요. 스크립트 구성 요소 프로그래밍 방법은 [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)을 참조하십시오.  
  
### <a name="options"></a>변수  
 **Properties**  
 스크립트 변환 속성을 보고 수정합니다. 표시된 속성 중 다수는 읽기 전용입니다. 다음 속성을 수정할 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**설명**|스크립트 변환의 목적을 기준으로 스크립트 변환을 설명합니다.|  
|**LocaleID**|정렬과 날짜 및 시간 변환에 사용할 지역별 정보를 제공하는 로캘을 지정합니다.|  
|**이름**|구성 요소에 대한 설명이 포함된 이름을 입력합니다.|  
|**ValidateExternalMetadata**|스크립트 변환이 디자인 타임에서 외부 데이터 원본에 대해 열 메타데이터의 유효성을 검사할 것인지 여부를 나타냅니다. 값 **false** 는 실행 시간까지 유효성 검사를 지연합니다.|  
|**ReadOnlyVariables**|스크립트 변환을 통해 읽기 전용으로 액세스할 변수 목록을 쉼표로 구분하여 입력합니다.<br /><br /> 참고: 변수 이름은 대/소문자를 구분합니다.|  
|**ReadWriteVariables**|스크립트 변환을 통해 읽기/쓰기로 액세스할 변수 목록을 쉼표로 구분하여 입력합니다.<br /><br /> 참고: 변수 이름은 대/소문자를 구분합니다.|  
|**ScriptLanguage**|스크립트 구성 요소에 사용될 스크립트 언어를 선택합니다.<br /><br /> 스크립트 구성 요소 및 스크립트 태스크에 대한 기본 스크립트 언어를 설정하려면 **옵션** 대화 상자의 **일반** 페이지에서 **스크립트 언어** 옵션을 사용합니다.|  
|**UserComponentTypeName**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인프라를 지원하는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost> 클래스 및 **Microsoft.SqlServer.TxScript** 어셈블리를 지정합니다.|  
  
 **스크립트 편집**  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications)를 사용하여 스크립트를 작성하거나 수정할 수 있습니다.  
  
## <a name="related-content"></a>관련 내용  
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
 [Extending the Data Flow with the Script Component](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)  
  
  
