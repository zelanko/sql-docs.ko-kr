---
title: "4단원: SSIS를 사용하여 오류 흐름 리디렉션 추가 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 0c8dbda2-75e3-4278-9b4e-dcd220c92522
caps.latest.revision: "24"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 71522bf83637a5f783f14c0a13c2e129b5a0afdd
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="lesson-4-add-error-flow-redirection-with-ssis"></a>4단원: SSIS를 사용하여 오류 흐름 리디렉션 추가
변환 프로세스에서 발생할 수 있는 오류를 처리하기 위해 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서는 변환할 수 없는 데이터를 처리하는 방법을 구성 요소 단위 및 열 단위로 결정할 수 있습니다. 특정 열의 오류를 무시하거나 오류가 발생한 전체 행을 리디렉션하거나 또는 구성 요소 작동이 실패하도록 선택할 수 있습니다. 기본적으로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 의 모든 구성 요소는 오류 발생 시 작동이 실패하도록 구성되어 있습니다. 구성 요소 작동이 실패하면 이에 따라 패키지 실행이 실패하고 모든 후속 처리가 중지됩니다.  
  
변환 중에 처리 오류가 발생할 수 있으므로 오류로 인해 패키지 실행이 중지되지 않도록 발생 가능한 처리 오류를 구성하고 해결하는 것이 좋습니다. 패키지가 성공적으로 실행되도록 오류를 무시할 수 있지만 대부분의 경우 데이터와 오류를 유지하여 나중에 조사하고 재처리할 수 있는 다른 처리 경로로 오류가 발생한 행을 리디렉션하는 것이 좋습니다.  
  
이 단원에서는 [3단원: SSIS를 사용하여 로깅 추가](../integration-services/lesson-3-add-logging-with-ssis.md)에서 생성한 패키지의 복사본을 만드는 방법을 설명합니다. 이 새 패키지에 대한 작업에서는 예제 데이터 파일 중 하나를 손상된 버전으로 만듭니다. 손상된 파일이 있으면 패키지를 실행할 때 처리 오류가 발생합니다.  
  
오류 데이터를 처리하려면 Lookup Currency Key 변환에서 조회 값을 찾지 못하는 모든 행을 파일에 기록하는 플랫 파일 대상을 추가하고 구성합니다.  
  
파일에 오류 데이터가 기록되기 전에 스크립트를 사용하여 오류 설명을 가져오는 스크립트 구성 요소를 포함합니다. 그런 다음 처리하지 못한 모든 데이터를 스크립트 변환으로 리디렉션하도록 Lookup Currency Key 변환을 다시 구성합니다.  
  
> [!IMPORTANT]  
> 이 자습서를 실행하려면 **AdventureWorksDW2012** 예제 데이터베이스가 필요합니다. **AdventureWorksDW2012**, [CodePlex의 Reporting Services 제품 샘플](http://go.microsoft.com/fwlink/p/?LinkID=526910)을 참조하세요.  
  
## <a name="tasks-in-lesson"></a>단원의 태스크  
이 단원에서는 다음 태스크를 다룹니다.  
  
-   [1단계: 3단원 패키지 복사](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
-   [2단계: 손상된 파일 만들기](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
-   [3단계: 오류 흐름 리디렉션 추가](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
-   [4단계: 플랫 파일 대상 추가](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
-   [5단계: 4단원 자습서 패키지 테스트](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
[1단계: 3단원 패키지 복사](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
  
  
