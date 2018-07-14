---
title: 태스크 또는 컨테이너의 속성 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], properties
ms.assetid: 52d47ca4-fb8c-493d-8b2b-48bb269f859b
caps.latest.revision: 48
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4aa8b85c3b5c92b38f50bbfac850d4a69ed2d4c9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37264899"
---
# <a name="set-the-properties-of-a-task-or-container"></a>태스크 또는 컨테이너의 속성 설정
  **속성** 창을 사용하여 태스크 및 컨테이너의 속성을 대부분 설정할 수 있습니다. 태스크 컬렉션의 속성과 **속성** 창을 사용해서 설정하기에 너무 복잡한 속성은 예외입니다. 예를 들어 Foreach 루프 컨테이너에서 사용되는 열거자는 **속성** 창에서 구성할 수 없습니다. 이러한 복잡한 속성을 설정하려면 태스크 또는 컨테이너 편집기를 사용해야 합니다. 대부분의 태스크 및 컨테이너 편집기에는 여러 개의 노드가 포함되어 있으며, 각 노드에는 관련 속성이 들어 있습니다. 노드의 이름은 노드에 들어 있는 속성의 내용을 나타냅니다.  
  
 다음 절차에서는 **속성** 창이나 해당 태스크 또는 컨테이너 편집기를 사용하여 태스크 또는 컨테이너의 속성을 설정하는 방법에 대해 설명합니다.  
  
### <a name="to-set-the-properties-of-a-task-or-container-by-using-the-properties-window"></a>속성 창을 사용하여 태스크 또는 컨테이너의 속성을 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  **제어 흐름** 탭의 디자인 화면에서 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
5.  **속성** 창에서 속성 값을 업데이트합니다.  
  
    > [!NOTE]  
    >  대부분의 속성은 입력란에 직접 값을 입력하거나 목록에서 값을 선택하는 방법으로 설정할 수 있습니다. 그러나 일부 속성은 보다 복잡하므로 사용자 지정 속성 편집기를 사용해야 합니다. 이러한 속성을 설정하려면 입력란을 클릭하고 작성 **(…)** 단추를 클릭하여 사용자 지정 편집기를 엽니다.  
  
6.  선택적으로 속성 식을 만들어 태스크 또는 컨테이너의 속성을 동적으로 업데이트합니다. 자세한 내용은 [속성 식 추가 또는 변경](expressions/add-or-change-a-property-expression.md)을 참조하세요.  
  
7.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
### <a name="to-set-the-properties-of-a-task-or-container-by-using-a-task-or-container-editor"></a>태스크 또는 컨테이너 편집기를 사용하여 태스크 또는 컨테이너의 속성을 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  **제어 흐름** 탭의 디자인 화면에서 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **편집** 을 클릭하여 해당 태스크 또는 컨테이너 편집기를 엽니다.  
  
     For 루프 컨테이너를 구성하는 방법에 대한 자세한 내용은 [For 루프 컨테이너 구성](control-flow/for-loop-container.md)을 참조하세요.  
  
     Foreach 루프 컨테이너를 구성하는 방법에 대한 자세한 내용은 [Foreach 루프 컨테이너 구성](control-flow/foreach-loop-container.md)을 참조하세요.  
  
    > [!NOTE]  
    >  시퀀스 컨테이너에는 사용자 지정 편집기가 없습니다.  
  
5.  태스크 또는 컨테이너 편집기에 여러 개의 노드가 포함되어 있는 경우 설정하려는 속성이 들어 있는 노드를 클릭합니다.  
  
6.  선택적으로 **식** 페이지에서 **Expressions** 를 클릭하고 태스크 또는 컨테이너의 속성을 동적으로 업데이트하기 위한 속성 식을 만듭니다. 자세한 내용은 [속성 식 추가 또는 변경](expressions/add-or-change-a-property-expression.md)을 참조하세요.  
  
7.  속성 값을 업데이트합니다.  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 태스크](control-flow/integration-services-tasks.md)   
 [Integration Services 컨테이너](control-flow/integration-services-containers.md)  
  
  
