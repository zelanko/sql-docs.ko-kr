---
title: '3단계: 플랫 파일 연결 관리자 수정 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 459e3995-2116-4f15-aaa2-32f26113869c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5f09ac0b6b7a1d0536205596a553eddb06765b93
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296025"
---
# <a name="lesson-2-3-modify-the-flat-file-connection-manager"></a>2-3단원: 플랫 파일 연결 관리자 수정

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



이 태스크에서는 1단원에서 플랫 파일 연결 관리자를 수정합니다. 해당 플랫 파일 연결 관리자는 단일 파일을 정적으로 로드하도록 구성됩니다. 플랫 파일 연결 관리자를 사용하여 반복적으로 파일을 로드하려면 런타임에 로드할 파일의 경로를 포함하는 사용자 정의 변수 `User::varFileName`을 사용하도록 연결 관리자의 ConnectionString 속성을 변경합니다.  
  
ConnectionString 속성을 변경하기 위해 사용자 정의 변수의 값을 사용하도록 연결 관리자를 수정하면 해당 연결 관리자가 다른 플랫에 연결합니다. 런타임에 Foreach 루프 컨테이너가 반복될 때마다 `User::varFileName` 변수가 업데이트됩니다. 따라서 변수를 업데이트하면 연결 관리자가 다른 플랫 파일에 연결하고 데이터 흐름 태스크가 다른 데이터 집합을 처리합니다.  
  
## <a name="configure-the-flat-file-connection-manager-to-use-a-variable"></a>변수를 사용하도록 플랫 파일 연결 관리자 구성  
  
1.  **연결 관리자** 창에서 **Sample Flat File Source Data**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  

2.  **속성** 창에서 **PackagePath**가 **\Package.Connections**로 시작되는지 확인합니다. 이와 같이 시작되지 않으면 **연결 관리자** 창에서 **Sample Flat File Source Data**를 마우스 오른쪽 단추로 클릭하고 **패키지 연결로 변환**을 선택합니다.
  
3.  **속성** 창에서 **식**의 빈 셀을 선택한 다음, 줄임표 단추 **(...)** 를 선택합니다.  
  
4.  **속성 식 편집기** 대화 상자의 **속성** 열에서 **ConnectionString**을 선택합니다.  
  
5.  **식** 열에서 줄임표 단추 **(...)** 를 선택하여 **식 작성기** 대화 상자를 엽니다.  
  
6.  **식 작성기** 대화 상자에서 **변수** 노드를 확장합니다.  
  
7.  **User::varFileName** 변수를 **식** 상자로 끌어 놓습니다.  
  
8.  **확인**을 선택하여 **식 작성기** 대화 상자를 닫습니다.  
  
9.  다시 **확인**을 선택하여 **속성 식 편집기** 대화 상자를 닫습니다.  
  
## <a name="go-to-next-task"></a>다음 작업으로 이동  
[4단계: 2단원 자습서 패키지 테스트](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
  
  
