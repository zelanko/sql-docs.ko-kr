---
title: 태스크 호스트 컨테이너 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.taskhostcontainer.f1
helpviewer_keywords:
- containers [Integration Services], Task Host
- Task Host container
ms.assetid: 7394a2c2-1b07-427d-b94a-9792e7783d35
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c934687c159d81ddaa20852844859801dc248405
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920980"
---
# <a name="task-host-container"></a>태스크 호스트 컨테이너

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  태스크 호스트 컨테이너는 단일 태스크를 캡슐화합니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 태스크 호스트는 별도로 구성되지 않고 캡슐화되는 태스크의 속성을 설정할 때 구성됩니다. 태스크 호스트 컨테이너에서 캡슐화하는 태스크에 대한 자세한 내용은 [Integration Services Tasks](../../integration-services/control-flow/integration-services-tasks.md)를 참조하십시오.  
  
 이 컨테이너는 변수 및 이벤트 처리기 사용을 태스크 수준에까지 확장합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 이벤트 처리기](../../integration-services/integration-services-ssis-event-handlers.md) 및 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md)를 참조하세요.  
  
## <a name="configuration-of-the-task-host"></a>태스크 호스트 구성  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 **속성** 창을 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 이러한 속성을 설정하는 방법에 대한 자세한 내용은 [태스크 또는 컨테이너의 속성 설정](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)을 참조하세요.  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법은 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [태스크 또는 컨테이너의 속성 설정](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 컨테이너](../../integration-services/control-flow/integration-services-containers.md)  
  
  
