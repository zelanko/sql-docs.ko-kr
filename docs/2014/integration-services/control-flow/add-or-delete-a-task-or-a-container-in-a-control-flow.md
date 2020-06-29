---
title: 제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], adding
- adding tasks
- adding containers
- tasks [Integration Services], adding
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fde63d44a6434b1604a2f05ed1da777e7589a772
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85434140"
---
# <a name="add-or-delete-a-task-or-a-container-in-a-control-flow"></a>제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제
  제어 흐름 디자이너에서 작업 중일 때 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 도구 상자에는 패키지의 제어 흐름을 작성하기 위해 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 제공하는 태스크가 나열됩니다. 도구 상자에 대한 자세한 내용은 [SSIS Toolbox](../ssis-toolbox.md)를 참조하십시오.  
  
 패키지에는 동일 태스크에 대한 여러 인스턴스가 포함될 수 있습니다. 태스크에 대한 각 인스턴스는 패키지에서 고유하게 식별되며 각 인스턴스를 서로 다르게 구성할 수 있습니다.  
  
 태스크를 삭제하면 이 태스크를 제어 흐름의 다른 태스크 및 컨테이너에 연결하는 선행 제약 조건도 삭제됩니다.  
  
 다음 절차에서는 패키지의 제어 흐름에서 태스크 또는 컨테이너를 추가하거나 삭제하는 방법에 대해 설명합니다.  
  
### <a name="to-add-a-task-or-a-container-to-a-control-flow"></a>제어 흐름에 태스크 또는 컨테이너를 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  **도구 상자**를 열려면 **보기** 메뉴에서 **도구 상자** 를 클릭합니다.  
  
5.  **제어 흐름 항목** 및 **유지 관리 계획 태스크**를 확장합니다.  
  
6.  **도구 상자** 에서 태스크 및 컨테이너를 **제어 흐름** 탭의 디자인 화면으로 끌어 옵니다.  
  
7.  패키지 제어 흐름 내의 태스크 또는 컨테이너에서 연결선을 제어 흐름 내의 다른 구성 요소로 끌어와서 서로 연결합니다.  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
### <a name="to-delete-a-task-or-a-container-from-a-control-flow"></a>제어 흐름에서 태스크 또는 컨테이너를 삭제하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다. 다음 중 하나를 수행합니다.  
  
    -   **제어 흐름** 탭을 클릭하고 제거하려는 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
    -   **패키지 탐색기**를 엽니다. **실행 파일** 폴더에서 제거하려는 태스크 또는 컨테이너를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
3.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [작업 Integration Services](integration-services-tasks.md)   
 [Integration Services 컨테이너](integration-services-containers.md)   
 [제어 흐름](control-flow.md)  
  
  
