---
title: "스크립트 태스크 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.scripttask.f1
- sql13.dts.designer.scripttask.general.f1
- sql13.dts.designer.scripttask.script.f1
helpviewer_keywords:
- scripts [Integration Services], tasks
- Script task [Integration Services], about Script task
- Script task [Integration Services]
ms.assetid: f6cce7df-4bd6-4b75-9f89-6c37b4bb5558
caps.latest.revision: "67"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 83f4682136c01e29f034800656ee4bb27a8d62da
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="script-task"></a>스크립트 태스크
  스크립트 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 제공하는 기본 제공 태스크와 변환에서 사용할 수 없는 기능을 수행하는 코드를 제공합니다. 또한 여러 개의 태스크와 변환을 사용하는 대신 여러 기능을 하나의 스크립트에 결합할 수 있습니다. 스크립트 태스크는 데이터 행마다 한 번 수행하는 대신 패키지에서 한 번 또는 열거된 개체마다 한 번 수행해야 하는 작업에 사용합니다.  
  
 스크립트 태스크는 다음 용도로 사용할 수 있습니다.  
  
-   기본 제공 연결 형식에서 지원하지 않는 다른 기술을 사용하여 데이터에 액세스합니다. 예를 들어 스크립트는 ADSI(Active Directory Service Interface)를 사용하여 Active Directory에 액세스하고 사용자 이름을 추출할 수 있습니다.  
  
-   패키지 특정 성능 카운터를 만듭니다. 예를 들어 스크립트는 복잡하거나 성능이 저조한 태스크를 실행하는 동안 업데이트되는 성능 카운터를 만들 수 있습니다.  
  
-   지정된 파일이 비어 있는지 확인하고 그렇지 않은 경우 포함된 행 수를 확인한 다음 이러한 정보를 기반으로 패키지의 제어 흐름을 수정합니다. 예를 들어 파일에 포함된 행이 없는 경우 변수 값을 0으로 설정하고 이 값을 평가하는 선행 제약 조건으로 인해 파일 시스템 태스크가 파일을 복사할 수 없도록 합니다.  
  
 스크립트를 사용하여 한 집합에 있는 각 데이터 행에 대해 같은 작업을 수행해야 하는 경우에는 스크립트 태스크 대신 스크립트 구성 요소를 사용해야 합니다. 예를 들어 적절한 우표 금액을 평가하여 금액이 너무 높거나 낮은 데이터 행을 건너뛰려면 스크립트 구성 요소를 사용합니다. 자세한 내용은 [Script Component](../../integration-services/data-flow/transformations/script-component.md)를 참조하세요.  
  
 스크립트가 둘 이상의 패키지에 사용되는 경우 스크립트 태스크 대신 사용자 지정 태스크를 작성합니다. 자세한 내용은 [사용자 지정 태스크 개발](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)을 참조하세요.  
  
 스크립트 태스크를 패키지에 적합한 선택 항목으로 결정한 후에는 태스크에서 사용하는 스크립트를 개발하고 태스크 자체를 구성해야 합니다.  
  
## <a name="writing-and-running-the-script-that-the-task-uses"></a>태스크에서 사용하는 스크립트 작성 및 실행  
 스크립트 태스크는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 를 스크립트 작성 환경과 스크립트 실행 엔진으로 사용합니다.  
  
 VSTA는 색 구분 기능이 포함된 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 편집기, IntelliSense, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 개체 탐색기 **등**환경의 모든 표준 기능을 제공합니다. 또한 다른 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 개발 도구에서 사용하는 것과 동일한 디버거를 사용합니다. 스크립트 작업의 중단점이 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 태스크 및 컨테이너의 중단점과 문제 없이 작동합니다. VSTA는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 프로그래밍 언어를 지원합니다.  
  
 스크립트를 실행하려면 패키지가 실행되는 컴퓨터에 VSTA가 설치되어 있어야 합니다. 패키지를 실행하면 스크립트 태스크가 스크립트 엔진을 로드하고 스크립트를 실행합니다. 어셈블리에 대한 참조를 프로젝트에 추가하면 스크립트에서 외부 .NET 어셈블리에 액세스할 수 있습니다.  
  
> [!NOTE]  
>  스크립트가 미리 컴파일되었는지 여부를 지정할 수 있었던 이전 버전과는 달리 모든 스크립트가 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 이상 버전에 미리 컴파일되어 있습니다. 스크립트가 미리 컴파일된 경우 런타임 시 언어 엔진이 로드되지 않으므로 패키지가 보다 신속하게 실행됩니다. 그러나 미리 컴파일된 이진 파일은 상당한 디스크 공간을 소비합니다.  
  
## <a name="configuring-the-script-task"></a>스크립트 태스크 구성  
 다음과 같은 방법으로 스크립트 태스크를 구성할 수 있습니다.  
  
-   태스크에서 실행할 사용자 지정 스크립트를 제공합니다.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 런타임이 스크립트 태스크 코드에 대한 진입점으로 호출되는 VSTA 프로젝트의 메서드를 지정합니다.  
  
-   스크립트 언어를 지정합니다.  
  
-   선택적으로 스크립트에서 사용할 읽기 전용 및 읽기/쓰기 변수 목록을 제공합니다.  
  
 이러한 속성은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 설정할 수 있습니다.  
  
### <a name="configuring-the-script-task-in-the-designer"></a>디자이너에서 스크립트 태스크 구성  
 다음 표에서는 스크립트 태스크용으로 로깅될 수 있는 **ScriptTaskLogEntry** 이벤트에 대해 설명합니다. **SSIS 로그 구성** 대화 상자의 **세부 정보** 탭에는 **ScriptTaskLogEntry** 이벤트가 로깅 대상으로 선택되어 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**ScriptTaskLogEntry**|스크립트에서 로깅을 구현한 결과를 보고합니다. 이 태스크는 **Log** 개체의 **Dts** 메서드를 호출할 때마다 로그 항목을 기록합니다. 이러한 항목은 코드가 실행될 때 기록됩니다. 자세한 내용은 [Logging in the Script Task](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)을 참조하세요.|  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [스크립트 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/script-task-editor-general-page.md)  
  
-   [스크립트 태스크 편집기&#40;스크립트 페이지&#41;](../../integration-services/control-flow/script-task-editor-script-page.md)  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법은 다음 항목을 참조하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
### <a name="configuring-the-script-task-programmatically"></a>프로그래밍 방식으로 스크립트 태스크 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법은 다음 항목을 참조하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask>  
  
## <a name="script-task-editor-general-page"></a>스크립트 태스크 편집기(일반 페이지)
  **스크립트 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 스크립트 태스크의 이름을 지정하고 설명할 수 있습니다.  
  
 스크립트 태스크에 대한 자세한 내용은 [Script Task](../../integration-services/control-flow/script-task.md) 및 [Configuring the Script Task in the Script Task Editor](../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)을 참조하십시오. 스크립트 태스크 프로그래밍 방법은 [Extending the Package with the Script Task](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)을 참조하십시오.  
  
### <a name="options"></a>옵션  
 **이름**  
 스크립트 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **Description**  
 스크립트 태스크에 대한 설명을 입력합니다.  
  
## <a name="script-task-editor-script-page"></a>스크립트 태스크 편집기(스크립트 페이지)
  **스크립트 태스크 편집기** 대화 상자의 **스크립트** 페이지를 사용하여 스크립트 속성을 설정하고 스크립트에서 액세스할 수 있는 변수를 지정할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 와 그 이후 버전에서는 모든 스크립트가 미리 컴파일됩니다. 그러나 이전 버전에서는 **PrecompileScriptIntoBinaryCode** 속성을 설정하여 스크립트가 미리 컴파일되었음을 지정해야 합니다.  
  
 스크립트 태스크에 대한 자세한 내용은 [Script Task](../../integration-services/control-flow/script-task.md) 및 [Configuring the Script Task in the Script Task Editor](../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)을 참조하십시오. 스크립트 태스크 프로그래밍 방법은 [Extending the Package with the Script Task](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)을 참조하십시오.  
  
### <a name="options"></a>옵션  
 **ScriptLanguage**  
 태스크에 대한 스크립트 언어를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 중에서 선택합니다.  
  
 태스크에 대한 스크립트를 작성한 후에는 **ScriptLanguage** 속성의 값을 변경할 수 없습니다.  
  
 스크립트 태스크에 대한 스크립트 언어를 설정하려면 **옵션** 대화 상자의 **일반** 페이지에서 **스크립트 언어** 옵션을 사용하십시오. 자세한 내용은 [General Page](../../integration-services/control-flow/script-task-editor-general-page.md)을 참조하세요.  
  
 **EntryPoint**  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 런타임이 스크립트 태스크 코드에 대한 진입점으로 호출하는 메서드를 지정합니다. 지정된 메서드는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) project The ScriptMain class is the default class generated by the script templates.  
  
 VSTA 프로젝트에서 메서드 이름을 변경한 경우 **EntryPoint** 속성의 값을 변경해야 합니다.  
  
 **ReadOnlyVariables**  
 스크립트에 사용할 수 있는 읽기 전용 변수 목록을 쉼표로 구분하여 입력하거나 줄임표 단추(**…**)를 클릭하고 **변수 선택** 대화 상자에서 변수를 선택합니다.  
  
> [!NOTE]  
>  변수 이름은 대/소문자를 구분합니다.  
  
 **ReadWriteVariables**  
 스크립트에 사용할 수 있는 읽기/쓰기 변수 목록을 쉼표로 구분하여 입력하거나 줄임표 단추(**…**)를 클릭하고 **변수 선택** 대화 상자에서 변수를 선택합니다.  
  
> [!NOTE]  
>  변수 이름은 대/소문자를 구분합니다.  
  
 **스크립트 편집**  
 스크립트를 작성하거나 수정할 수 있는 VSTA IDE가 열립니다.  
  
## <a name="related-content"></a>관련 내용  
  
-   shareourideas.com의 기술 문서 - [C#의 배달 알림으로 메일을 보내는 방법](http://go.microsoft.com/fwlink/?LinkId=237625)  
  
  
