---
title: "스크립트 태스크를 사용 하 여 패키지를 확장 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b2e0b0a933568f8313cefd2f1d6dbdd02f5d3cbc
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="extending-the-package-with-the-script-task"></a>스크립트 태스크를 사용하여 패키지 확장
  스크립트 태스크의 런타임 기능을 확장 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 로 작성 된 사용자 지정 코드를 사용 하 여 패키지 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#으로 컴파일하여 패키지 실행 시 실행 합니다. 스크립트 태스크를 사용하면 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 제공하는 태스크가 개발자의 요구 사항을 완전히 만족시키지 못하는 경우 사용자 지정 런타임을 손쉽게 개발할 수 있습니다. 스크립트 태스크에서는 필요한 모든 인프라 코드를 자동으로 작성하므로 개발자는 사용자 지정 처리에 필요한 코드에만 집중하면 됩니다.  
  
 전역를 통해 포함 하는 패키지와 상호 작용 하는 스크립트 태스크 **Dts** 개체, 인스턴스는 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> 스크립팅 환경에서 제공 되는 클래스입니다. 스크립트 태스크에서 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 변수에 저장된 값을 수정하는 코드를 작성할 수 있습니다. 그러면 나중에 패키지에서 업데이트된 이 값을 사용하여 패키지 워크플로의 경로를 확인할 수 있습니다. 또한 스크립트 태스크에서는 사용자 지정 기능을 구현하는 데 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 네임스페이스 및 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 클래스 라이브러리뿐 아니라 사용자 지정 어셈블리도 사용합니다.  
  
 스크립트 태스크 및 해당 구성 요소가 생성하는 인프라 코드를 사용하면 사용자 지정 태스크를 개발하는 과정이 훨씬 간단해집니다. 그러나 스크립트 태스크의 작동 방식을 이해 하려면 유용할 수 있습니다이 섹션 [사용자 지정 태스크를 개발](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md) 사용자 지정 태스크를 개발 하는 단계를 이해할 수 있습니다.  
  
 여러 패키지에서 재사용할 태스크를 만들 경우에는 스크립트 태스크를 사용하는 대신 사용자 지정 태스크를 개발하는 것이 좋습니다. 자세한 내용은 참조 [스크립팅 솔루션 비교 및 사용자 지정 개체](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 항목에서는 스크립트 태스크에 대해 자세히 설명합니다.  
  
 [스크립트 태스크 편집기에서 스크립트 태스크 구성](../../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)  
 에 대해 설명 방법을 속성에서 구성 하는 **스크립트 태스크 편집기** 기능과 스크립트 태스크의 코드 성능에 영향을 줍니다.  
  
 [코딩 및 스크립트 태스크 디버깅](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
 사용 하는 방법에 설명 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] VSTA Tools for Applications ()는 스크립트 태스크에 포함 된 스크립트를 개발 합니다.  
  
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
  
 [스크립트 태스크 예](../../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
 스크립트 태스크의 가능한 용도 몇 가지를 보여 주는 간단한 예를 제공합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립트 태스크](../../../integration-services/control-flow/script-task.md)   
 [스크립트 태스크와 스크립트 구성 요소를 비교합니다.](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  
