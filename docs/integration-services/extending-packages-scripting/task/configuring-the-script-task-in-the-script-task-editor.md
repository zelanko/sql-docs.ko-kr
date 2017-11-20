---
title: "스크립트 태스크 편집기에서 스크립트 태스크 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], configuring
- Script Task Editor
- SSIS Script task, configuring
ms.assetid: 232de0c9-b24d-4c38-861d-6c1f4a75bdf3
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 182a7b8f04c2339a8f3d3b986c978a7998c8a9c3
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="configuring-the-script-task-in-the-script-task-editor"></a>스크립트 태스크 편집기에서 스크립트 태스크 구성
  세 페이지에서 주 속성을 구성 하는 스크립트 태스크의 사용자 지정 코드를 작성 하기 전에 **스크립트 태스크 편집기**합니다. 속성 창에서는 스크립트 태스크에 고유하지 않은 추가 태스크 속성을 구성할 수 있습니다.  
  
> [!NOTE]  
>  스크립트가 미리 컴파일되었는지 여부를 지정할 수 있었던 이전 버전과는 달리 [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 이상에서는 모든 스크립트가 미리 컴파일되어 있습니다.  
  
## <a name="general-page-of-the-script-task-editor"></a>스크립트 태스크 편집기의 일반 페이지  
 에 **일반** 의 페이지는 **스크립트 태스크 편집기**, 고유 이름 및 스크립트 태스크에 대 한 설명을 지정 합니다.  
  
## <a name="script-page-of-the-script-task-editor"></a>스크립트 태스크 편집기의 스크립트 페이지  
 **스크립트** 의 페이지는 **스크립트 태스크 편집기** 스크립트 태스크의 사용자 지정 속성을 표시 합니다.  
  
### <a name="scriptlanguage-property"></a>ScriptLanguage 속성  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] VSTA tools for Applications ()를 지원는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 프로그래밍 언어입니다. 스크립트 태스크의 스크립트를 만드는 값을 변경할 수 없습니다는 **u a g e** 속성입니다.  
  
 스크립트 태스크 및 스크립트 구성 요소에 대 한 기본 스크립트 언어를 설정 하려면는 **u a g e** 속성에는 **일반** 의 페이지는 **옵션** 대화 상자. 자세한 내용은 [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)을 참조하세요.  
  
### <a name="entrypoint-property"></a>EntryPoint 속성  
 **EntryPoint** 속성에서 메서드를 지정 된 **ScriptMain** VSTA에서 클래스를 프로젝트에 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 런타임이 스크립트 태스크 코드에 대 한 진입점으로 호출 합니다. **ScriptMain** 클래스는 스크립트 템플릿에서 생성 되는 기본 클래스입니다.  
  
 VSTA 프로젝트에서 메서드 이름을 변경한 경우 **EntryPoint** 속성의 값을 변경해야 합니다.  
  
### <a name="readonlyvariables-and-readwritevariables-properties"></a>ReadOnlyVariables 및 ReadWriteVariables 속성  
 쉼표로 구분된 기존 변수 목록을 이러한 속성의 값으로 입력하여 스크립트 태스크 코드 내에서 해당 변수를 읽기 전용 또는 읽기/쓰기 권한으로 액세스할 수 있게 할 수 있습니다. 두 유형의 변수를 통해 코드에 액세스 하는 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 속성은 **Dts** 개체입니다. 자세한 내용은 [Using Variables in the Script Task](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)을 참조하세요.  
  
> [!NOTE]  
>  변수 이름은 대소문자를 구분합니다.  
  
 변수를 선택 하려면 줄임표를 클릭 (**...** ) 속성 필드 옆에 있는 단추입니다. 자세한 내용은 참조 [변수 선택 페이지](../../../integration-services/control-flow/select-variables-page.md)합니다.  
  
### <a name="edit-script-button"></a>스크립트 편집 단추  
 **스크립트 편집** 단추 사용자 지정 스크립트를 작성할 수 있는 VSTA 개발 환경을 시작 합니다. 자세한 내용은 참조 [코딩 및 스크립트 태스크 디버깅](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)합니다.  
  
## <a name="expressions-page-of-the-script-task-editor"></a>스크립트 태스크 편집기의 식 페이지  
 에 **식** 의 페이지는 **스크립트 태스크 편집기**, 식을 사용 하 여 위에 나열 된 스크립트 태스크의 속성에 대 한 및 다른 여러 작업 속성에 값을 제공할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../../integration-services/expressions/integration-services-ssis-expressions.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [코딩 및 스크립트 태스크 디버깅](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
  
  

