---
title: '3단원: 로깅 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 64cd24cc-ba8e-4bd7-b10b-6b80d8b04af6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 088afb5cdd4640aab550552d4fc15c25f3a852e1
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53375285"
---
# <a name="lesson-3-adding-logging"></a>3단원: 로깅 추가
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에는 태스크 및 컨테이너 이벤트 추적을 제공하여 패키지 실행을 모니터링하고 문제를 해결할 수 있는 로깅 기능이 포함되어 있습니다. 로깅 기능은 융통성이 있으므로 패키지 수준 또는 패키지 내의 개별 태스크와 컨테이너에서 사용할 수 있습니다. 로깅하려는 이벤트를 선택하고 단일 패키지에 대해 여러 개의 로그를 만들 수 있습니다.  
  
 로깅은 로그 공급자가 제공합니다. 각 로그 공급자는 다양한 형식과 대상 유형으로 로깅 정보를 작성할 수 있습니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 다음 로그 공급자를 제공합니다.  
  
-   텍스트 파일  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Windows 이벤트 로그  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   XML 파일  
  
 이 단원에서 만든 패키지의 복사본을 만듭니다 [단원 2: 루핑 추가](lesson-2-adding-looping-with-ssis.md)합니다. 이 새 패키지 작업에서 패키지 실행 중에 특정 이벤트를 모니터링하도록 로깅을 추가하고 구성하는 방법에 대해 설명합니다. 이전 단원 중 완료한 단원이 없는 경우 완성된 상태로 포함된 2단원 패키지를 복사할 수도 있습니다.  
  
> [!IMPORTANT]  
>  이 자습서를 실행하려면 **AdventureWorksDW2012** 예제 데이터베이스가 필요합니다. **AdventureWorksDW2012**의 설치 및 배포 방법에 대한 자세한 내용은 [CodePlex의 Reporting Services 제품 샘플](https://go.microsoft.com/fwlink/p/?LinkID=52691)을 참조하십시오.  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 다룹니다.  
  
-   [1 단계: 2 단원 패키지 복사](lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [2단계: 로깅 추가 및 구성](lesson-3-2-adding-and-configuring-logging.md)  
  
-   [3 단계: 3 단원 자습서 패키지 테스트](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
 [1 단계: 2 단원 패키지 복사](lesson-3-1-copying-the-lesson-2-package.md)  
  
  
