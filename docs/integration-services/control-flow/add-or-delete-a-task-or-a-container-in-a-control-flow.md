---
title: "태스크 또는 컨테이너는 제어 흐름에 추가 또는 삭제 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- containers [Integration Services], adding
- adding tasks
- adding containers
- tasks [Integration Services], adding
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c9c5a240223fb25e36a9ccd4591656fffbc8875a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="add-or-delete-a-task-or-a-container-in-a-control-flow"></a>제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제
  제어 흐름 디자이너에서 작업 중일 때 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 도구 상자에는 패키지의 제어 흐름을 작성하기 위해 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 제공하는 태스크가 나열됩니다. 도구 상자에 대한 자세한 내용은 [SSIS Toolbox](../../integration-services/ssis-toolbox.md)를 참조하십시오.  
  
 패키지에는 동일 태스크에 대한 여러 인스턴스가 포함될 수 있습니다. 태스크에 대한 각 인스턴스는 패키지에서 고유하게 식별되며 각 인스턴스를 서로 다르게 구성할 수 있습니다.  
  
 태스크를 삭제하면 이 태스크를 제어 흐름의 다른 태스크 및 컨테이너에 연결하는 선행 제약 조건도 삭제됩니다.  
  
 다음 절차에서는 패키지의 제어 흐름에서 태스크 또는 컨테이너를 추가하거나 삭제하는 방법에 대해 설명합니다.  
  
## <a name="add-a-task-or-a-container-to-a-control-flow"></a>제어 흐름에 태스크 또는 컨테이너 추가  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  **도구 상자**를 열려면 **보기** 메뉴에서 **도구 상자** 를 클릭합니다.  
  
5.  **제어 흐름 항목** 및 **유지 관리 계획 태스크**를 확장합니다.  
  
6.  **도구 상자** 에서 태스크 및 컨테이너를 **제어 흐름** 탭의 디자인 화면으로 끌어 옵니다.  
  
7.  패키지 제어 흐름 내의 태스크 또는 컨테이너에서 연결선을 제어 흐름 내의 다른 구성 요소로 끌어와서 서로 연결합니다.  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="delete-a-task-or-a-container-from-a-control-flow"></a>제어 흐름에서 태스크 또는 컨테이너를 삭제 합니다.  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다. 다음 중 하나를 수행합니다.  
  
    -   **제어 흐름** 탭을 클릭하고 제거하려는 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
    -   **패키지 탐색기**를 엽니다. **실행 파일** 폴더에서 제거하려는 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
3.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  

## <a name="set-the-properties-of-a-task-or-container"></a>태스크 또는 컨테이너의 속성 설정
**속성** 창을 사용하여 태스크 및 컨테이너의 속성을 대부분 설정할 수 있습니다. 태스크 컬렉션의 속성과 **속성** 창을 사용해서 설정하기에 너무 복잡한 속성은 예외입니다. 예를 들어 Foreach 루프 컨테이너에서 사용되는 열거자는 **속성** 창에서 구성할 수 없습니다. 이러한 복잡한 속성을 설정하려면 태스크 또는 컨테이너 편집기를 사용해야 합니다. 대부분의 태스크 및 컨테이너 편집기에는 여러 개의 노드가 포함되어 있으며, 각 노드에는 관련 속성이 들어 있습니다. 노드의 이름은 노드에 들어 있는 속성의 내용을 나타냅니다.  
  
 다음 절차에서는 **속성** 창이나 해당 태스크 또는 컨테이너 편집기를 사용하여 태스크 또는 컨테이너의 속성을 설정하는 방법에 대해 설명합니다.  
  
### <a name="set-the-properties-of-a-task-or-container-with-the-properties-window"></a>태스크 또는 속성 창 사용 하 여 컨테이너의 속성 설정  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  **제어 흐름** 탭의 디자인 화면에서 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
5.  **속성** 창에서 속성 값을 업데이트합니다.  
  
    > [!NOTE]  
    >  대부분의 속성은 입력란에 직접 값을 입력하거나 목록에서 값을 선택하는 방법으로 설정할 수 있습니다. 그러나 일부 속성은 보다 복잡하므로 사용자 지정 속성 편집기를 사용해야 합니다. 이러한 속성을 설정하려면 입력란을 클릭하고 작성 **(…)** 단추를 클릭하여 사용자 지정 편집기를 엽니다.  
  
6.  선택적으로 속성 식을 만들어 태스크 또는 컨테이너의 속성을 동적으로 업데이트합니다. 자세한 내용은 [속성 식 추가 또는 변경](../../integration-services/expressions/add-or-change-a-property-expression.md)을 참조하세요.  
  
7.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
### <a name="set-the-properties-of-a-task-or-container-with-the-task-or-container-editor"></a>태스크 또는 태스크 또는 컨테이너 편집기를 사용 하 여 컨테이너의 속성 설정  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  **제어 흐름** 탭의 디자인 화면에서 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **편집** 을 클릭하여 해당 태스크 또는 컨테이너 편집기를 엽니다.  
  
     For 루프 컨테이너를 구성하는 방법에 대한 자세한 내용은 [For 루프 컨테이너 구성](http://msdn.microsoft.com/library/b9cd7ea7-b198-4a35-8b16-6acf09611ca5)을 참조하세요.  
  
     Foreach 루프 컨테이너를 구성하는 방법에 대한 자세한 내용은 [Foreach 루프 컨테이너 구성](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)을 참조하세요.  
  
    > [!NOTE]  
    >  시퀀스 컨테이너에는 사용자 지정 편집기가 없습니다.  
  
5.  태스크 또는 컨테이너 편집기에 여러 개의 노드가 포함되어 있는 경우 설정하려는 속성이 들어 있는 노드를 클릭합니다.  
  
6.  선택적으로 **식** 페이지에서 **Expressions** 를 클릭하고 태스크 또는 컨테이너의 속성을 동적으로 업데이트하기 위한 속성 식을 만듭니다. 자세한 내용은 [속성 식 추가 또는 변경](../../integration-services/expressions/add-or-change-a-property-expression.md)을 참조하세요.  
  
7.  속성 값을 업데이트합니다.  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [Integration Services 컨테이너](../../integration-services/control-flow/integration-services-containers.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)  
  
  

