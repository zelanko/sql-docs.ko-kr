---
title: 태스크 호스트 컨테이너 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.taskhostcontainer.f1
helpviewer_keywords:
- containers [Integration Services], Task Host
- Task Host container
ms.assetid: 7394a2c2-1b07-427d-b94a-9792e7783d35
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2067223b4c26f1581a522ebe9fa19690bf76fb56
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089609"
---
# <a name="task-host-container"></a>태스크 호스트 컨테이너
  태스크 호스트 컨테이너는 단일 태스크를 캡슐화합니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 태스크 호스트는 별도로 구성되지 않고 캡슐화되는 태스크의 속성을 설정할 때 구성됩니다. 태스크 호스트 컨테이너에서 캡슐화하는 태스크에 대한 자세한 내용은 [Integration Services Tasks](integration-services-tasks.md)를 참조하십시오.  
  
 이 컨테이너는 변수 및 이벤트 처리기 사용을 태스크 수준에까지 확장합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 이벤트 처리기](../integration-services-ssis-event-handlers.md) 및 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md)를 참조하세요.  
  
## <a name="configuration-of-the-task-host"></a>태스크 호스트 구성  
 **의** 속성 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 창을 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 이러한 속성을 설정하는 방법에 대한 자세한 내용은 [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)을 참조하세요.  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>를 참조하십시오.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 컨테이너](integration-services-containers.md)  
  
  