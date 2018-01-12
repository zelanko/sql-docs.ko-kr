---
title: "구성 요소 그룹화 또는 그룹 해제 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- grouping containers
- tasks [Integration Services], grouping
- containers [Integration Services], grouping
- grouping tasks
ms.assetid: 34320838-c271-4f8c-90b3-1254690890bb
caps.latest.revision: "46"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8d2a7603080d7c4c5c479553933e9092e6f71bcf
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="group-or-ungroup-components"></a>구성 요소 그룹화 또는 그룹 해제
  **디자이너의**제어 흐름 **,**데이터 흐름 **및** 이벤트 처리기 [!INCLUDE[ssIS](../includes/ssis-md.md)] 탭에서는 축소 가능한 그룹화를 지원합니다. 패키지에 여러 구성 요소가 있는 경우 탭이 복잡해져서 모든 구성 요소를 한 번에 확인하기 어렵고 사용하려는 항목을 쉽게 찾기 어려울 수 있습니다. 축소 가능한 그룹화 기능을 사용하면 작업 공간을 절약하고 큰 패키지를 쉽게 사용할 수 있습니다.  
  
 그룹화하려는 구성 요소를 선택하여 그룹화한 다음 작업에 맞게 그룹을 확장하거나 축소합니다. 그룹을 확장하면 해당 그룹에 들어 있는 구성 요소의 속성을 사용할 수 있습니다. 태스크와 컨테이너를 연결하는 선행 제약 조건은 그룹에 자동으로 포함됩니다.  
  
 다음은 구성 요소를 그룹화할 때 고려할 사항입니다.  
  
-   구성 요소를 그룹화하려면 제어 흐름, 데이터 흐름 또는 이벤트 처리기에 두 개 이상의 구성 요소가 포함되어 있어야 합니다.  
  
-   또한 그룹을 중첩하여 그룹 내에 그룹을 만들 수 있습니다. 디자인 화면에서는 중첩되지 않은 여러 그룹을 구현할 수 있지만 그룹이 중첩되지 않은 경우 구성 요소는 하나의 그룹에만 속할 수 있습니다.  
  
-   패키지가 저장되면 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 그룹화 구성이 저장되지만 그룹화 구성은 패키지 실행에 영향을 주지 않습니다. 구성 요소를 그룹화하는 기능은 디자인 타임 기능이며 패키지의 런타임 동작에는 영향을 주지 않습니다.  
  
### <a name="to-group-components"></a>구성 요소를 그룹화하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름**, **데이터 흐름**또는 **이벤트 처리기** 탭을 클릭합니다.  
  
4.  탭의 디자인 화면에서 그룹화하려는 구성 요소를 선택하고 선택한 구성 요소를 마우스 오른쪽 단추로 클릭한 다음 **그룹화**를 클릭합니다.  
  
5.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
### <a name="to-ungroup-components"></a>구성 요소를 그룹 해제하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **제어 흐름**, **데이터 흐름**또는 **이벤트 처리기** 탭을 클릭합니다.  
  
4.  탭의 디자인 화면에서 그룹 해제하려는 구성 요소가 들어 있는 그룹을 선택하고 마우스 오른쪽 단추를 클릭한 다음 **그룹 해제**를 클릭합니다.  
  
5.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제](../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [기본 선행 제약 조건을 사용하여 태스크 및 컨테이너 연결](http://msdn.microsoft.com/library/8f31f15f-98ff-4c35-b41f-8b8cfd148d75)  
  
  
