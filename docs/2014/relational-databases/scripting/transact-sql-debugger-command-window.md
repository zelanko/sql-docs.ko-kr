---
title: 명령 창
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26306f8ad2adf01ebdcbf1b52169f1c2ec964920
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243077"
---
# <a name="command-window"></a>명령 창
  **Commandwindow** 를 사용 하 여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 쿼리 편집기 창에서 현재 디버깅 중인 코드에 디버그 및 편집 명령과 같은 명령을 실행 합니다. 
  **명령 창**을 사용하려면 디버그 모드여야 합니다. 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **명령** 창에서도 지원되는 많은 명령을 지원합니다. 자세한 내용은 [Visual Studio 명령 창](https://go.microsoft.com/fwlink/?LinkId=112007)을 참조하십시오.  
  
## <a name="task-list"></a>작업 목록  
 **명령 창에 액세스 하려면**  
  
-   
  **디버그** 메뉴에서 **디버깅 시작**을 클릭합니다.  
  
 **변수 값을 인쇄 하려면**  
  
-   
  **명령 창**에서 **Debug.Print \<VariableName>** 을 입력하고 Enter 키를 누릅니다.  
  
 **현재 스레드에 대 한 정보를 나열 하려면**  
  
-   **Commandwindow**에서를 입력 `Debug.ListThread`한 다음 enter 키를 누릅니다.  
  
 **간략 한 조사식 창에 변수를 추가 하려면**  
  
-   
  **명령 창**에서 **Debug.QuickWatch \<VariableName>** 을 입력하고 Enter 키를 누릅니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql 디버거](transact-sql-debugger.md)  
