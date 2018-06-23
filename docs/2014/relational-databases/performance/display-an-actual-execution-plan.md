---
title: 실제 실행 계획 표시 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- displaying execution plans
- actual execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 71c3239d474b6252ff36bc10fe33eb20024091b5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090205"
---
# <a name="display-an-actual-execution-plan"></a>실제 실행 계획 표시
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 실제 그래픽 실행 계획을 생성하는 방법에 대해 설명합니다. 실제 실행 계획을 생성하면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 또는 일괄 처리가 실행됩니다. 생성된 실행 계획은 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 이 쿼리를 실행할 때 사용하는 실제 쿼리 실행 계획을 표시합니다.  
  
 이 기능을 사용하려면 사용자가 그래픽 실행 계획이 생성되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 실행할 적절한 권한을 가져야 하며 쿼리가 참조하는 모든 데이터베이스에 대해서도 SHOWPLAN 권한이 필요합니다.  
  
### <a name="to-include-an-execution-plan-for-a-query-during-execution"></a>실행 중에 쿼리의 실행 계획을 포함하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 도구 모음에서 **데이터베이스 엔진 쿼리**를 클릭합니다. **파일 열기** 도구 모음 단추를 클릭하여 기존 쿼리를 열고 예상 실행 계획을 표시할 수도 있습니다.  
  
2.  실제 실행 계획을 표시할 쿼리를 입력합니다.  
  
3.  **쿼리** 메뉴에서 **실제 실행 계획 포함** 을 클릭하거나 **실제 실행 계획 포함** 도구 모음 단추를 클릭합니다.  
  
4.  **실행** 도구 모음 단추를 클릭하여 쿼리를 실행합니다. 쿼리 최적화 프로그램에서 사용하는 계획이 결과 창의 **실행 계획** 탭에 표시됩니다. 표시된 도구 설명에서 연산자의 설명과 속성을 보려면 논리/물리 연산자 위에 마우스를 놓고 기다립니다.  
  
     또는 속성 창에서 연산자 속성을 확인할 수 있습니다. 속성이 표시되지 않으면 연산자를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. 속성을 확인할 연산자를 선택합니다.  
  
5.  실행 계획을 마우스 오른쪽 단추로 클릭하고 **확대**, **축소**, **사용자 지정 확대/축소**또는 **크기에 맞게**를 선택하여 실행 계획의 보기를 변경할 수 있습니다. **확대** 및 **축소** 를 사용하면 실행 계획을 확대 또는 축소할 수 있으며 **사용자 지정 확대/축소** 를 사용하면 80% 축소와 같이 원하는 수준으로 확대 및 축소를 정의할 수 있습니다. **크기에 맞게** 는 결과 창에 맞게 실행 계획을 확대합니다.  
  
  