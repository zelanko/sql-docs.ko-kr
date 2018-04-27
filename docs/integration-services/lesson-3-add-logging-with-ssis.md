---
title: '3단원: SSIS를 사용하여 로깅 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 64cd24cc-ba8e-4bd7-b10b-6b80d8b04af6
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ade5618a5be46c4d8c4aed8fbbb6ed291d9a8729
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="lesson-3-add-logging-with-ssis"></a>3단원: SSIS를 사용하여 로깅 추가
[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에는 태스크 및 컨테이너 이벤트 추적을 제공하여 패키지 실행을 모니터링하고 문제를 해결할 수 있는 로깅 기능이 포함되어 있습니다. 로깅 기능은 융통성이 있으므로 패키지 수준 또는 패키지 내의 개별 태스크와 컨테이너에서 사용할 수 있습니다. 로깅하려는 이벤트를 선택하고 단일 패키지에 대해 여러 개의 로그를 만들 수 있습니다.  
  
로깅은 로그 공급자가 제공합니다. 각 로그 공급자는 다양한 형식과 대상 유형으로 로깅 정보를 작성할 수 있습니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 다음 로그 공급자를 제공합니다.  
  
-   텍스트 파일  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Windows 이벤트 로그  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   XML 파일  
  
이 단원에서는 [2단원: SSIS를 사용하여 루핑 추가](../integration-services/lesson-2-adding-looping-with-ssis.md)에서 만든 패키지의 복사본을 만든 다음 이 새 패키지 작업에서 패키지 실행 중에 특정 이벤트를 모니터링하도록 로깅을 추가하고 구성하는 방법에 대해 설명합니다. 이전 단원 중 완료한 단원이 없는 경우 완성된 상태로 포함된 2단원 패키지를 복사할 수도 있습니다.  
  
> [!IMPORTANT]  
> 이 자습서를 실행하려면 **AdventureWorksDW2012** 예제 데이터베이스가 필요합니다. **AdventureWorksDW2012**, [CodePlex의 Reporting Services 제품 샘플](http://go.microsoft.com/fwlink/p/?LinkID=526910)을 참조하세요.  
  
## <a name="lesson-tasks"></a>단원 태스크  
이 단원에서는 다음 태스크를 다룹니다.  
  
-   [1단계: 2단원 패키지 복사](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [2단계: 로깅 추가 및 구성](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
-   [3단계: 3단원 자습서 패키지 테스트](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
[1단계: 2단원 패키지 복사](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
  
  
