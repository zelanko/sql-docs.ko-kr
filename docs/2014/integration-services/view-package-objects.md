---
title: 패키지 개체 보기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- Package Explorer window [Integration Services]
- packages [Integration Services], properties
- explorer view [Integration Services]
- SSIS packages, properties
- viewing package objects
- SQL Server Integration Services packages, properties
ms.assetid: a85c0245-0a68-4eb0-83b1-9b11df80bd10
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 78a9b551ae44348de1c007533be3606b33c974cd
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58390091"
---
# <a name="view-package-objects"></a>패키지 개체 보기
  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 **패키지 탐색기** 탭은 패키지에 대한 탐색기 뷰를 제공합니다. 이 뷰에는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 아키텍처의 컨테이너 계층이 표시됩니다. 패키지 컨테이너는 최상위 계층에 있으며, 패키지를 확장하면 패키지에 있는 연결, 실행 개체, 이벤트 처리기, 로그 공급자, 선행 제약 조건 및 변수를 볼 수 있습니다.  
  
 패키지의 컨테이너 및 태스크인 실행 개체에는 이벤트 처리기, 선행 제약 조건 및 변수가 포함될 수 있습니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 컨테이너가 중첩된 계층을 지원하며, For 루프, Foreach 루프 및 시퀀스 컨테이너에는 다른 실행 개체가 포함될 수 있습니다  
  
 패키지에 데이터 흐름이 포함된 경우 **패키지 탐색기** 에는 데이터 흐름 태스크가 나열되며 데이터 흐름 구성 요소가 나열된 **구성 요소** 폴더가 포함됩니다.  
  
 **패키지 탐색기** 탭에서는 패키지의 개체를 삭제하고 **속성** 창을 사용하여 개체 속성을 볼 수 있습니다.  
  
 다음 다이어그램에서는 예제 패키지의 트리 뷰를 보여 줍니다.  
  
 ![패키지 탐색기 탭의 스크린샷](media/packageexplorer.gif "패키지 탐색기 탭의 스크린샷")  
  
### <a name="to-view-package-content"></a>패키지 내용을 보려면  
  
-   [패키지 탐색기에서 패키지 개체 보기](../../2014/integration-services/view-package-objects-in-package-explorer.md)  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 태스크](control-flow/integration-services-tasks.md)   
 [Integration Services 컨테이너](control-flow/integration-services-containers.md)   
 [선행 제약 조건](control-flow/precedence-constraints.md)   
 [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md)   
 [Integration Services&#40;SSIS&#41; 이벤트 처리기](integration-services-ssis-event-handlers.md)   
 [Integration Services&#40;SSIS&#41; 로깅](performance/integration-services-ssis-logging.md)  
  
  
