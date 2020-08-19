---
description: 스크립트 태스크 편집기에서 스크립트 태스크 구성
title: 스크립트 태스크 편집기에서 스크립트 태스크 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], configuring
- Script Task Editor
- SSIS Script task, configuring
ms.assetid: 232de0c9-b24d-4c38-861d-6c1f4a75bdf3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8b4a052ea59e3c72adda887c3084bca278059f0b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430255"
---
# <a name="configuring-the-script-task-in-the-script-task-editor"></a>스크립트 태스크 편집기에서 스크립트 태스크 구성

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  스크립트 태스크에서 사용자 지정 코드를 작성하려면 먼저 **스크립트 태스크 편집기**의 세 페이지에서 주 속성을 구성해야 합니다. 속성 창에서는 스크립트 태스크에 고유하지 않은 추가 태스크 속성을 구성할 수 있습니다.  
  
> [!NOTE]  
>  스크립트가 미리 컴파일되었는지 여부를 지정할 수 있었던 이전 버전과는 달리 [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 이상에서는 모든 스크립트가 미리 컴파일되어 있습니다.  
  
## <a name="general-page-of-the-script-task-editor"></a>스크립트 태스크 편집기의 일반 페이지  
 **스크립트 태스크 편집기**의 **일반** 페이지에서는 스크립트 태스크의 고유한 이름과 설명을 지정합니다.  
  
## <a name="script-page-of-the-script-task-editor"></a>스크립트 태스크 편집기의 스크립트 페이지  
 **스크립트 태스크 편집기**의 **스크립트** 페이지에는 스크립트 태스크의 사용자 지정 속성이 표시됩니다.  
  
### <a name="scriptlanguage-property"></a>ScriptLanguage 속성  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] VSTA([!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications)는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 프로그래밍 언어를 지원합니다. 스크립트 태스크에서 스크립트를 만든 후에는 **ScriptLanguage** 속성의 값을 변경할 수 없습니다.  
  
 스크립트 태스크 및 스크립트 구성 요소에 대한 기본 스크립트 언어를 설정하려면 **옵션** 대화 상자의 **일반** 페이지에 있는 **ScriptLanguage** 속성을 사용합니다. 자세한 내용은 [General Page](../../general-page-of-integration-services-designers-options.md)을 참조하세요.  
  
### <a name="entrypoint-property"></a>EntryPoint 속성  
 **EntryPoint** 속성은 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 런타임이 VSTA 프로젝트의 **ScriptMain** 클래스에서 스크립트 태스크 코드에 대한 진입점으로 호출하는 메서드를 지정합니다. **ScriptMain** 클래스는 스크립트 템플릿이 생성하는 기본 클래스입니다.  
  
 VSTA 프로젝트에서 메서드 이름을 변경한 경우 **EntryPoint** 속성의 값을 변경해야 합니다.  
  
### <a name="readonlyvariables-and-readwritevariables-properties"></a>ReadOnlyVariables 및 ReadWriteVariables 속성  
 쉼표로 구분된 기존 변수 목록을 이러한 속성의 값으로 입력하여 스크립트 태스크 코드 내에서 해당 변수를 읽기 전용 또는 읽기/쓰기 권한으로 액세스할 수 있게 할 수 있습니다. 두 유형의 변수 모두 코드에서 **Dts** 개체의 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 속성을 통해 액세스할 수 있습니다. 자세한 내용은 [Using Variables in the Script Task](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)을 참조하세요.  
  
> [!NOTE]  
>  변수 이름은 대소문자를 구분합니다.  
  
 변수를 선택하려면 속성 필드 옆의 줄임표( **...** ) 단추를 클릭합니다. 자세한 내용은 [변수 선택 페이지](../../../integration-services/control-flow/select-variables-page.md)를 참조하세요.  
  
### <a name="edit-script-button"></a>스크립트 편집 단추  
 **스크립트 편집** 단추를 클릭하면 사용자 지정 스크립트를 작성할 수 있는 VSTA 개발 환경이 시작됩니다. 자세한 내용은 [스크립트 태스크 코딩 및 디버깅](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)을 참조하십시오.  
  
## <a name="expressions-page-of-the-script-task-editor"></a>스크립트 태스크 편집기의 식 페이지  
 **스크립트 태스크 편집기**의 **식**에서 식을 사용하여 위에 나열된 스크립트 태스크의 속성과 그 밖의 여러 태스크 속성에 대한 값을 제공할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../../integration-services/expressions/integration-services-ssis-expressions.md)가 될 때까지 워크플로를 반복합니다.  
  
## <a name="see-also"></a>참고 항목  
 [스크립트 태스크 코딩 및 디버깅](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
  
  
