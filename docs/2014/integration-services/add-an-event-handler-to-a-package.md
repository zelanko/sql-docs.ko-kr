---
title: 패키지에 이벤트 처리기를 추가 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- event handlers [Integration Services], creating
ms.assetid: 5e56885d-8658-480a-bed9-3f2f8003fd78
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 589d90b52647241b22929473efc9c6e54eb3b75f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062024"
---
# <a name="add-an-event-handler-to-a-package"></a>패키지에 이벤트 처리기 추가
  컨테이너와 태스크는 런타임에 이벤트를 발생시킵니다. 이벤트가 발생할 때 워크플로를 실행하여 이벤트에 응답하는 사용자 지정 이벤트 처리기를 만들 수 있습니다. 예를 들어 태스크가 실패하면 전자 메일 메시지를 보내는 이벤트 처리기를 만들 수 있습니다.  
  
 이벤트 처리기는 패키지와 비슷합니다. 패키지와 같이 이벤트 처리기에서는 변수에 대한 범위를 제공할 수 있으며 제어 흐름과 선택적 데이터 흐름이 포함됩니다. 패키지, Foreach 루프 컨테이너, For 루프 컨테이너, 시퀀스 컨테이너 및 모든 태스크에 대해 이벤트 처리기를 만들 수 있습니다.  
  
 **디자이너에서** 이벤트 처리기 [!INCLUDE[ssIS](../includes/ssis-md.md)] 탭의 디자인 화면을 사용하여 이벤트 처리기를 만들 수 있습니다.  
  
 **이벤트 처리기** 탭이 활성화되면 **디자이너의 도구 상자에 있는** 제어 흐름 항목 **및** 유지 관리 계획 태스크 [!INCLUDE[ssIS](../includes/ssis-md.md)] 노드에 이벤트 처리기의 제어 흐름을 작성하기 위한 태스크와 컨테이너가 포함됩니다. **데이터 흐름 원본**, **변환**및 **데이터 흐름 대상** 노드에는 이벤트 처리기의 데이터 흐름을 작성하기 위한 데이터 원본, 변환 및 대상이 포함됩니다. 자세한 내용은 [Control Flow](control-flow/control-flow.md) 및 [Data Flow](data-flow/data-flow.md)를 참조하세요.  
  
 **이벤트 처리기** 탭에는 또한 이벤트 처리기에서 서버 및 데이터 원본에 연결하는 데 사용하는 연결 관리자를 만들고 수정할 수 있는 **연결 관리자** 영역이 포함됩니다. 자세한 내용은 [연결 관리자 만들기](../../2014/integration-services/create-connection-managers.md)를 참조하세요.  
  
### <a name="to-create-an-event-handler"></a>이벤트 처리기를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **이벤트 처리기** 탭을 클릭합니다.  
  
     ![이벤트 처리기가 있는 디자인 화면의 스크린샷](media/eventhandlers.gif "이벤트 처리기가 있는 디자인 화면의 스크린샷")  
  
     이벤트 처리기에서 제어 흐름과 데이터 흐름을 만드는 방법은 패키지에서 제어 흐름과 데이터 흐름을 만드는 방법과 비슷합니다. 자세한 내용은 [Control Flow](control-flow/control-flow.md) 및 [Data Flow](data-flow/data-flow.md)를 참조하세요.  
  
4.  **실행 파일** 목록에서 이벤트 처리기를 만들 실행 파일을 선택합니다.  
  
5.  **이벤트 처리기** 목록에서 만들 이벤트 처리기를 선택합니다.  
  
6.  **이벤트 처리기** 탭의 디자인 화면에서 링크를 클릭합니다.  
  
7.  이벤트 처리기에 제어 흐름 항목을 추가하고 제어 흐름 항목 간에 제약 조건을 끌어서 선행 제약 조건을 사용하는 항목을 연결합니다. 자세한 내용은 [Control Flow](control-flow/control-flow.md)을 참조하세요.  
  
8.  필요에 따라 **데이터 흐름** 탭의 디자인 화면에 데이터 흐름 태스크를 추가하고 이벤트 처리기의 데이터 흐름을 만들 수도 있습니다. 자세한 내용은 [Data Flow](data-flow/data-flow.md)을 참조하세요.  
  
9. **파일** 메뉴에서 **선택한 항목 저장** 을 클릭하여 패키지를 저장합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Integration Services](../../2014/integration-services/sql-server-integration-services.md)   
 [Integration Services&#40;SSIS&#41; 로깅](performance/integration-services-ssis-logging.md)  
  
  
