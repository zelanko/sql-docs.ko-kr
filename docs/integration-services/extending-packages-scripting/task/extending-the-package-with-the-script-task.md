---
title: 스크립트 태스크를 사용하여 패키지 확장 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- scripts [Integration Services]
- SSIS Script task
- tasks [Integration Services], scripts
- Script task [Integration Services], about Script task
- scripts [Integration Services], about Script task with packages
- SSIS Script task, about Script task
ms.assetid: 911e6d26-a6fd-4fc3-a111-bf5f048e9bff
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 691fb53d772196e00c5ee35a02a2b62ee6dc8e2c
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58274906"
---
# <a name="extending-the-package-with-the-script-task"></a>스크립트 태스크를 사용하여 패키지 확장
  스크립트 태스크는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#으로 작성되고 패키지 런타임에 컴파일 및 실행되는 사용자 지정 코드를 사용하여 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 패키지의 런타임 기능을 확장합니다. 스크립트 태스크를 사용하면 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 제공하는 태스크가 개발자의 요구 사항을 완전히 만족시키지 못하는 경우 사용자 지정 런타임을 손쉽게 개발할 수 있습니다. 스크립트 태스크에서는 필요한 모든 인프라 코드를 자동으로 작성하므로 개발자는 사용자 지정 처리에 필요한 코드에만 집중하면 됩니다.  
  
 스크립트 태스크는 스크립팅 환경에서 제공되는 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> 클래스의 인스턴스인 전역 **Dts** 개체를 통해 포함된 패키지와 상호 작용합니다. 스크립트 태스크에서 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 변수에 저장된 값을 수정하는 코드를 작성할 수 있습니다. 그러면 나중에 패키지에서 업데이트된 이 값을 사용하여 패키지 워크플로의 경로를 확인할 수 있습니다. 또한 스크립트 태스크에서는 사용자 지정 기능을 구현하는 데 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 네임스페이스 및 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 클래스 라이브러리뿐 아니라 사용자 지정 어셈블리도 사용합니다.  
  
 스크립트 태스크 및 해당 구성 요소가 생성하는 인프라 코드를 사용하면 사용자 지정 태스크를 개발하는 과정이 훨씬 간단해집니다. 하지만 스크립트 태스크의 작동 방식을 이해하려면 [사용자 지정 태스크 개발](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md) 섹션을 통해 사용자 지정 태스크를 개발하는 데 필요한 단계를 파악하는 것이 좋습니다.  
  
 여러 패키지에서 재사용할 태스크를 만들 경우에는 스크립트 태스크를 사용하는 대신 사용자 지정 태스크를 개발하는 것이 좋습니다. 자세한 내용은 [스크립팅 솔루션과 사용자 지정 개체 비교](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)를 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 항목에서는 스크립트 태스크에 대해 자세히 설명합니다.  
  
 [스크립트 태스크 편집기에서 스크립트 태스크 구성](../../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)  
 **스크립트 태스크 편집기**에서 구성하는 속성이 스크립트 태스크 코드의 기능과 성능에 미치는 영향에 대해 설명합니다.  
  
 [스크립트 태스크 코딩 및 디버깅](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] VSTA([!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications)를 사용하여 스크립트 태스크에 포함되는 스크립트를 개발하는 방법에 대해 설명합니다.  
  
 [스크립트 태스크에서 변수 사용](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 속성을 통해 변수를 사용하는 방법에 대해 설명합니다.  
  
 [스크립트 태스크에서 데이터 원본에 연결](../../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> 속성을 통해 연결을 사용하는 방법에 대해 설명합니다.  
  
 [스크립트 태스크에서 이벤트 발생](../../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> 속성을 통해 이벤트를 발생시키는 방법에 대해 설명합니다.  
  
 [스크립트 태스크에서 로깅](../../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 메서드를 통해 정보를 로깅하는 방법에 대해 설명합니다.  
  
 [스크립트 태스크에서 결과 반환](../../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md)  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> 속성 및 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> 속성을 통해 결과를 반환하는 방법에 대해 설명합니다.  
  
 [스크립트 태스크 예제](../../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
 스크립트 태스크의 가능한 용도 몇 가지를 보여 주는 간단한 예를 제공합니다.  
  
## <a name="see-also"></a>참고 항목  
 [스크립트 태스크](../../../integration-services/control-flow/script-task.md)   
 [스크립트 태스크와 스크립트 구성 요소 비교](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  
