---
title: 스크립트 구성 요소 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scriptcomponentdetails.f1
helpviewer_keywords:
- Script transformation
- scripts [Integration Services], transformations
- Script component [Integration Services], about Script component
- Script component [Integration Services]
ms.assetid: 131c2d0c-2e33-4785-94af-ada5c049821e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d9a601a710531aa6905f35a2fe5ca7f02a9177f1
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58394561"
---
# <a name="script-component"></a>스크립트 구성 요소
  스크립트 구성 요소는 스크립트를 호스팅하고 패키지에서 사용자 지정 스크립트 코드를 포함시키고 실행할 수 있도록 합니다. 패키지의 스크립트 구성 요소는 다음 용도로 사용할 수 있습니다.  
  
-   데이터 흐름에서 여러 변환을 사용하는 대신 데이터에 여러 변환을 적용합니다. 예를 들어 스크립트로 두 열에 값을 추가하고 합계의 평균을 계산할 수 있습니다.  
  
-   기존 .NET 어셈블리에 있는 비즈니스 규칙에 액세스합니다. 예를 들어 스크립트로 `Income` 열에서 유효한 값 범위를 지정하는 비즈니스 규칙을 적용할 수 있습니다.  
  
-   [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 식 문법에서 제공되는 함수와 연산자 외에 사용자 지정 수식과 함수를 사용합니다. 예를 들어 LUHN 수식을 사용하는 신용 카드 번호의 유효성을 검사합니다.  
  
-   열 데이터의 유효성을 검사하고 잘못된 데이터가 포함된 레코드는 건너 뜁니다. 예를 들어 스크립트로 적절한 우편 요금을 평가하여 금액이 너무 높거나 낮은 레코드를 건너뛸 수 있습니다.  
  
 스크립트 구성 요소를 사용하면 데이터 흐름에 사용자 지정 함수를 쉽고 빠르게 포함시킬 수 있습니다. 하지만 여러 패키지에서 스크립트 코드를 재사용하려는 경우에는 스크립트 구성 요소 대신 사용자 지정 구성 요소를 프로그래밍하는 방식을 고려하십시오. 자세한 내용은 [사용자 지정 데이터 흐름 구성 요소 개발](../../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)을 참조하세요.  
  
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
 스크립트 구성 요소는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) as the environment in which you write the scripts. VSTA는 **스크립트 변환 편집기**를 통해 액세스할 수 있습니다. 자세한 내용은 [스크립트 변환 편집기&#40;스크립트 페이지&#41;](../../script-transformation-editor-script-page.md)을 참조하세요.  
  
 스크립트 구성 요소는 구성 요소 메타데이터를 나타내는 ScriptMain이라는 자동 생성된 클래스가 포함된 VSTA 프로젝트를 제공합니다. 예를 들어 스크립트 구성 요소가 3개의 출력이 있는 변환으로 사용되는 경우 ScriptMain에는 각 출력에 대한 메서드가 포함됩니다. ScriptMain은 스크립트에 대한 진입점입니다.  
  
 VSTA에는 색 구분 기능이 포함된 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 편집기, IntelliSense, 개체 브라우저 등 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 환경의 모든 표준 기능이 포함됩니다. 스크립트 구성 요소에서 사용하는 스크립트는 패키지 정의에 저장됩니다. 패키지를 디자인할 때 스크립트 코드는 임시로 프로젝트 파일에 기록됩니다.  
  
 VSTA는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 및 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 프로그래밍 언어를 지원합니다.  
  
 스크립트 구성 요소를 프로그래밍하는 방법은 [스크립트 구성 요소를 사용하여 데이터 흐름 확장](script-component.md)을 참조하십시오. 스크립트 구성 요소를 원본, 변환 또는 대상으로 구성하는 방법에 대한 자세한 내용은 [Developing Specific Types of Script Components](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)을 참조하십시오. 스크립트 구성 요소 사용 방법을 보여 주는 ODBC 대상 등의 추가 예는 [Additional Script Component Examples](../../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)를 참조하십시오.  
  
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
 **스크립트 변환 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [스크립트 변환 편집기&#40;입력 열 페이지&#41;](../../script-transformation-editor-input-columns-page.md)  
  
-   [스크립트 변환 편집기&#40;입/출력 페이지&#41;](../../script-transformation-editor-inputs-and-outputs-page.md)  
  
-   [스크립트 변환 편집기&#40;스크립트 페이지&#41;](../../script-transformation-editor-script-page.md)  
  
-   [스크립트 변환 편집기&#40;연결 관리자 페이지&#41;](../../script-transformation-editor-connection-managers-page.md)  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)  
  
### <a name="configuring-the-script-component-programmatically"></a>프로그래밍 방식으로 스크립트 구성 요소 구성  
 **속성** 창을 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [Common Properties](../../common-properties.md)  
  
-   [변환 사용자 지정 속성](transformation-custom-properties.md)  
  
 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>관련 내용  
 [Integration Services 변환](integration-services-transformations.md)  
  
 [스크립트 구성 요소를 사용하여 데이터 흐름 확장](script-component.md)  
  
  
