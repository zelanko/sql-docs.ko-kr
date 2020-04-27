---
title: 예상 실행 계획 표시 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- zoom [SQL Server]
- estimated execution plan [SQL Server]
- displaying execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
- customizing execution plan display [SQL Server]
- modifying execution plan display
- custom zoom [SQL Server]
ms.assetid: e94aa576-4c0c-4c54-ad05-6c3432cc615b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 555ded0e34c0dc13ce794cc6f3119af7b2688910
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63150880"
---
# <a name="display-the-estimated-execution-plan"></a>예상 실행 계획 표시
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 그래픽 예상 실행 계획을 작성하는 방법에 대해 설명합니다. 예상 실행 계획이 작성되면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 또는 일괄 처리가 실행되지 않습니다. 대신 쿼리가 실제로 실행되었을 때 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 이 사용할 가능성이 가장 큰 쿼리 실행 계획이 실행 계획을 통해 표시됩니다.  
  
 이 기능을 사용하려면 사용자가 그래픽 실행 계획을 생성하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 실행하기 위한 적절한 권한을 갖고 있어야 하며 쿼리가 참조하는 모든 데이터베이스에 대한 SHOWPLAN 권한이 허용되어야 합니다.  
  
### <a name="to-display-the-estimated-execution-plan-for-a-query"></a>쿼리의 예상 실행 계획을 표시하려면  
  
1.  도구 모음에서 **데이터베이스 엔진 쿼리**를 클릭합니다. **파일 열기** 도구 모음 단추를 클릭하여 기존 쿼리를 열고 예상 실행 계획을 표시할 수도 있습니다.  
  
2.  예상 실행 계획을 표시할 쿼리를 입력합니다.  
  
3.  **쿼리** 메뉴에서 **예상 실행 계획 표시** 를 클릭하거나 **예상 실행 계획 표시** 도구 모음 단추를 클릭합니다. 예상 실행 계획은 결과 창의 **실행 계획** 탭에 표시됩니다. 추가 정보를 보려면 논리 및 물리 연산자 아이콘 위에 마우스를 올리고 잠시 대기하여 도구 설명을 표시하고 연산자에 대한 설명 및 속성을 확인합니다. 또는 속성 창에서 연산자 속성을 확인할 수 있습니다. 속성이 보이지 않으면 연산자를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 속성을 확인할 연산자를 선택합니다.  
  
4.  실행 계획의 표시를 변경 하려면 실행 계획을 마우스 오른쪽 단추로 클릭 하 고 **확대**, **축소**, **사용자 지정 확대/** 축소 또는 **크기에 맞게**를 선택 합니다. **축소** 및 **확대** 를 사용하면 실행 계획을 고정된 크기만큼 확대 또는 축소시킬 수 있습니다. **사용자 지정 확대/축소** 를 사용하면 사용자가 원하는 표시 배율을 정의할 수 있습니다(예: 80%로 축소). **크기에 맞게** 는 결과 창에 맞게 실행 계획을 확대합니다.  
  
  
