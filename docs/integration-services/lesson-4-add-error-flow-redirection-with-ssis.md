---
description: '4단원: SSIS를 사용하여 오류 흐름 리디렉션 추가'
title: '4단원: SSIS를 사용하여 오류 흐름 리디렉션 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0c8dbda2-75e3-4278-9b4e-dcd220c92522
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d7ef0a6862e334221fd497a5adc44ffd0ab7990d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466592"
---
# <a name="lesson-4-add-error-flow-redirection-with-ssis"></a>4단원: SSIS를 사용하여 오류 흐름 리디렉션 추가

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



변환 프로세스에서 발생할 수 있는 오류를 처리하기 위해 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]를 사용하면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 변환할 수 없는 데이터를 처리하는 방법을 구성 요소 단위 및 열 단위로 결정할 수 있습니다. 특정 열의 오류를 무시하거나 오류가 발생한 전체 행을 리디렉션하거나 구성 요소를 실패하도록 선택할 수 있습니다. 기본적으로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]의 구성 요소는 오류 발생 시 작동이 실패하도록 구성되어 있습니다. 실패한 구성 요소는 차례로 패키지 실행이 실패하고 처리가 중지됩니다.  
  
실패로 인해 패키지 실행이 중지되지 않도록 잠재적인 처리 오류가 발생할 때 구성하고 처리할 수 있습니다. 한 가지 옵션은 실패를 모두 무시하여 패키지가 항상 성공적으로 실행되도록 하는 것입니다. 실행한 행을 다른 처리 경로로 리디렉션할 수도 있습니다. 여기서 데이터 및 오류를 유지, 검사 또는 다시 처리할 수 있습니다.  
  
이 단원에서는 [ 3단원에서 개발한 패키지의 복사본을 만듭니다. SSIS를 사용하여 로깅 추가](../integration-services/lesson-3-add-logging-with-ssis.md). 이 새 패키지에 대한 작업에서는 예제 데이터 파일 중 하나를 손상된 버전으로 만듭니다. 손상된 파일로 인해 패키지를 실행할 때 처리 오류가 발생합니다.  
  
오류 데이터를 처리하려면 실패한 행을 오류 파일에 기록하는 플랫 파일 대상을 추가하고 구성합니다. 
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서 오류 데이터를 파일에 작성하기 전에 오류 설명을 가져오는 스크립트 구성 요소를 포함시킵니다. 그런 다음, 처리하지 못한 모든 데이터를 스크립트 변환으로 리디렉션하도록 Lookup Currency Key 변환을 다시 구성합니다.  
  
## <a name="prerequisites"></a>전제 조건

> [!NOTE]
> 아직 준비가 되지 않았다면 [1단원 필수 구성 요소](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)를 참조하세요.
 
## <a name="lesson-task"></a>단원 태스크
이 단원에서는 다음 태스크를 다룹니다.  
  
-   [1단계: 3단원 패키지 복사](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
-   [2단계: 손상된 파일 만들기](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
-   [3단계: 오류 흐름 리디렉션 추가](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
-   [4단계: 플랫 파일 대상 추가](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
-   [5단계: 4단원 자습서 패키지 테스트](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
[1단계: 3단원 패키지 복사](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
  
  
