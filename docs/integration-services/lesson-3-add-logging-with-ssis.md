---
title: '3단원: SSIS를 사용하여 로깅 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 64cd24cc-ba8e-4bd7-b10b-6b80d8b04af6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f4d8fdf2a714f47e40e4c2afe12bb7357068fa9d
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65722076"
---
# <a name="lesson-3-add-logging-with-ssis"></a>3단원: SSIS를 사용하여 로깅 추가

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에는 태스크 및 컨테이너 이벤트 추적을 제공하여 패키지 실행을 모니터링하고 문제를 해결할 수 있는 로깅 기능이 포함되어 있습니다. 로깅 기능은 유연합니다. 패키지 수준이나 패키지 내의 개별 태스크 또는 컨테이너에서 로깅을 사용할 수 있습니다. 로그할 이벤트를 선택하고 단일 패키지에 대해 여러 개의 로그를 만듭니다.  
  
로그 공급자는 로그를 만듭니다. 각 로그 공급자는 다양한 형식과 대상 유형으로 로깅 정보를 작성할 수 있습니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 다음 로그 공급자를 제공합니다.  
  
-   텍스트 파일  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Windows 이벤트 로그  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   XML 파일  
  
이 단원에서는 [2단원: SSIS를 사용하여 루핑 추가](../integration-services/lesson-2-adding-looping-with-ssis.md)에서 만든 패키지의 복사본을 만듭니다. 이 새 패키지로 작업한 다음, 패키지 실행 중에 특정 이벤트를 모니터링하도록 로깅을 추가하고 구성합니다. 이전 단원 중 하나를 완료하지 않은 경우 자습서에 포함된 2단원 패키지를 복사할 수도 있습니다.  

> [!NOTE]
> 아직 준비가 안되었다면 [1단원 필수 구성 요소](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)를 참조하세요.

## <a name="lesson-tasks"></a>단원 태스크  
이 단원에서는 다음 태스크를 다룹니다.  
  
-   [1단계: 2단원 패키지 복사](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [2단계: 로깅 추가 및 구성](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
-   [3단계: 3단원 패키지 테스트](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
[1단계: 2단원 패키지 복사](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
