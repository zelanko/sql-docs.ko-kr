---
title: 스크립트 태스크 편집기 (스크립트 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scripttask.script.f1
helpviewer_keywords:
- Script Task Editor
ms.assetid: 93da0e0d-83f5-406d-b144-4cce216571cb
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5ee7bb13e8a9fa4826297cd0c55b82881aee5296
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198083"
---
# <a name="script-task-editor-script-page"></a>스크립트 태스크 편집기(스크립트 페이지)
  **스크립트 태스크 편집기** 대화 상자의 **스크립트** 페이지를 사용하여 스크립트 속성을 설정하고 스크립트에서 액세스할 수 있는 변수를 지정할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssISversion10](../includes/ssisversion10-md.md)] 와 그 이후 버전에서는 모든 스크립트가 미리 컴파일됩니다. 그러나 이전 버전에서는 **PrecompileScriptIntoBinaryCode** 속성을 설정하여 스크립트가 미리 컴파일되었음을 지정해야 합니다.  
  
 스크립트 태스크에 대한 자세한 내용은 [Script Task](control-flow/script-task.md) 및 [스크립트 태스크 편집기에서 스크립트 태스크 구성](extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)을 참조하십시오. 스크립트 태스크 프로그래밍 방법은 [Extending the Package with the Script Task](extending-packages-scripting/task/extending-the-package-with-the-script-task.md)을 참조하십시오.  
  
## <a name="options"></a>변수  
 **ScriptLanguage**  
 태스크에 대한 스크립트 언어를 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C# 중에서 선택합니다.  
  
 태스크에 대한 스크립트를 작성한 후에는 **ScriptLanguage** 속성의 값을 변경할 수 없습니다.  
  
 스크립트 태스크에 대한 스크립트 언어를 설정하려면 **옵션** 대화 상자의 **일반** 페이지에서 **스크립트 언어** 옵션을 사용하십시오. 자세한 내용은 [General Page](general-page-of-integration-services-designers-options.md)을 참조하세요.  
  
 **EntryPoint**  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 런타임이 스크립트 태스크 코드에 대한 진입점으로 호출하는 메서드를 지정합니다. 지정된 메서드는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications) 프로젝트의 ScriptMain 클래스에 있어야 합니다. ScriptMain 클래스는 스크립트 템플릿에서 생성하는 기본 클래스입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [일반 페이지](general-page-of-integration-services-designers-options.md)   
 [스크립트 태스크 편집기 &#40;일반 페이지&#41;](../../2014/integration-services/script-task-editor-general-page.md)   
 [식 페이지](expressions/expressions-page.md)   
 [스크립트 태스크 예](extending-packages-scripting-task-examples/script-task-examples.md)   
 [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md)   
 [패키지에서 사용자 정의 변수의 범위 추가, 삭제, 변경](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
  
