---
title: 추적에 표시된 열 구성(SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: profiler
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- organizing trace columns displayed [SQL Server]
- arranging trace columns displayed
- traces [SQL Server], data columns
ms.assetid: 6b923f94-0eb1-467e-82f6-ceed43f77017
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 38a7e0a75dc850b5f4ef883d44c6ceb4d426b651
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37980965"
---
# <a name="organize-columns-displayed-in-a-trace-sql-server-profiler"></a>표시된 열 추적으로 구성(SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  추적 테이블이나 **추적 파일 속성** 대화 상자에서 **열 구성** 을 선택하는 방법으로 또는 추적을 정의할 때 추적에서 데이터 열을 그룹화할 수 있습니다. 데이터 열을 그룹화하면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 추적 출력을 더 정확히 분석할 수 있습니다. 자세한 내용은 [SQL Server Profiler를 사용하여 추적 보기 및 분석](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)을 참조하세요.  
  
 **열 구성** 을 사용하여 선택한 데이터 열을 기준으로 추적 이벤트를 그룹화하거나 그룹화한 후 집계할 수 있습니다.  
  
-   그룹 추적 이벤트로만 그룹화하도록 다중 데이터 열을 선택합니다. 그룹화할 다중 데이터 열을 선택하면 추적 창에 그룹화하도록 선택한 데이터 열의 값을 기준으로 그룹화된 이벤트가 표시됩니다. 다음 예에서는 그룹화하도록 **Duration** 및 **StartTime** 데이터 열을 선택한 경우 추적 창 표 형태가 나타나는 방법을 보여 줍니다. **Duration** 열 값이 오름차순으로 표시된 다음 **StartTime** 값이 표시됩니다.  
  
|Duration|StartTime|EventClass|ClientProcessID|  
|--------------|---------------|----------------|---------------------|  
||12/12/2006 3:16:43 PM|SQL:StmtStarting|2124|  
|0|12/12/2006 5:39:23 PM|Audit Login|648|  
|@shouldalert|12/12/2006 5:24:44 PM|SQL:StmtStarting|2124|  
|25|12/12/2006 5:24:44 PM|SQL:StmtCompleted|648|  
  
-   그룹화하려는 열을 하나만 선택하여 추적 이벤트를 그룹화하고 집계합니다. 그룹화할 데이터 열을 하나만 선택하는 경우 추적 창에는 데이터 열의 값을 기준으로 그룹화된 이벤트가 표시되고 그 아래에서 모든 이벤트가 축소됩니다. 그룹화를 위해 선택한 데이터 열에서 이벤트의 왼쪽에 더하기 기호(**+**)가 나타나고 그 아래에 축소된 이벤트 수가 괄호로 묶여 이벤트의 오른쪽에 나타납니다. 그룹화를 위해 **EventClass** 데이터 열을 선택한 경우 추적 창 표 형태가 나타나는 방법을 보여 줍니다. 모든 이벤트는 **EventClass** 데이터 열 아래에 구성됩니다. 이벤트를 모두 보려면 더하기 기호를 클릭하여 확장하고 해당 유형의 모든 이벤트 클래스를 표시합니다.  
  
|EventClass|StartTime|Duration|ClientProcessID|  
|----------------|---------------|--------------|---------------------|  
|+ ExistingConnection(6)||||  
|+ SQL:BatchStarting(25)||||  
|+ SQL:StmtCompleted(11)||||  
|+ SQL:SmtStarting(21)||||  
  
### <a name="to-group-data-columns-displayed-in-a-trace"></a>추적에 표시된 데이터 열을 그룹화하려면  
  
1.  기존 추적 파일이나 테이블을 엽니다.  
  
2.  **파일** 메뉴에서 **속성**을 클릭합니다.  
  
3.  **추적 파일 속성** 또는 **추적 테이블 속성** 대화 상자에서 **이벤트 선택** 탭을 클릭합니다.  
  
4.  **이벤트 선택** 탭에서 **열 구성**을 클릭합니다.  
  
5.  **열 구성** 대화 상자에서 그룹으로 표시하려는 열을 선택하고 **위로** 를 클릭하여 **그룹**아래로 열을 이동합니다. **그룹**아래로 이동하려는 모든 열을 옮긴 후에는 **위로** 및 **아래로** 단추를 사용하여 순서를 다시 정렬할 수 있습니다.  
  
     **그룹** 목록으로 데이터 열 이름을 옮기면 표시된 추적은 **그룹** 목록에 나타나는 최상위 데이터 열의 값을 기준으로 먼저 구성된 다음 **그룹** 목록의 두 번째 데이터 열을 기준으로 구성됩니다.  
  
6.  **열 구성** 대화 상자에서 **확인** 을 클릭한 다음 **추적 테이블 속성** 또는 **추적 파일 속성** 대화 상자에서 **확인** 을 클릭합니다.  
  
     **추적 테이블 속성** 또는 **추적 파일 속성** 대화 상자에서 **확인** 을 클릭하면 표시된 추적에서 데이터 열이 재구성됩니다. **그룹** 목록에서 최상위 위치로 옮긴 데이터 열은 왼쪽에서 오른쪽으로 표 형태를 읽어 나갈 때 추적 표시에 제일 먼저 나타납니다. 추적의 행은 **그룹** 목록에 포함된 데이터 열의 값을 기준으로 하여 오름차순으로 구성됩니다. 그룹화를 위해 선택한 열은 표시에 고정된 상태로 있지만 오른쪽 또는 왼쪽으로 스크롤하여 다른 열을 볼 수 있습니다.  
  
7.  표시된 추적 데이터의 그룹화를 해제하려면 **보기** 메뉴에서 **그룹화 보기** 를 클릭하여 선택을 취소합니다. 그룹화 보기로 되돌리려면 **보기** 메뉴에서 **그룹화 보기** 를 다시 클릭하여 다시 선택합니다.  
  
### <a name="to-group-and-aggregate-data-columns-in-a-trace"></a>추적의 데이터 열을 그룹화하고 집계하려면  
  
1.  기존 추적 파일이나 테이블을 엽니다.  
  
2.  **파일** 메뉴에서 **속성**을 클릭합니다.  
  
3.  **추적 파일 속성** 또는 **추적 테이블 속성** 대화 상자에서 **이벤트 선택** 탭을 클릭합니다.  
  
4.  **이벤트 선택** 탭에서 **열 구성**을 클릭합니다.  
  
5.  **열 구성** 대화 상자에서 표시된 추적 이벤트를 그룹화하고 집계하는 기준으로 삼을 열을 하나 선택합니다. **그룹** 아래로 열 이름을 이동하려면 **위로**를 클릭합니다. 필요한 경우 **위로** 및 **아래로** 단추를 사용하여 **열** 아래에 남은 열을 다시 정렬할 수 있습니다.  
  
6.  **열 구성** 대화 상자에서 **확인** 을 클릭한 다음 **추적 테이블 속성** 또는 **추적 파일 속성** 대화 상자에서 **확인** 을 클릭합니다.  
  
     **추적 테이블 속성** 또는 **추적 파일 속성** 대화 상자에서 **확인** 을 클릭하면 표시된 추적에서 데이터 열이 재구성됩니다. 기타 모든 데이터 열 이벤트가 **그룹** 목록으로 옮긴 데이터 열 아래에서 집계됩니다. 집계에 대해 선택한 데이터 열에서 이벤트의 왼쪽에 있는 더하기 기호(**+**)를 클릭하여 확장하고 해당 유형의 이벤트를 모두 볼 수 있습니다. 집계를 위해 선택한 열은 표시에 고정된 상태로 있지만 오른쪽 또는 왼쪽으로 스크롤하여 다른 열을 볼 수 있습니다.  
  
7.  추적 데이터의 일반 보기로 되돌리려면 **보기** 메뉴에서 **집계 보기** 를 클릭하여 선택을 취소합니다. 집계 보기로 되돌리려면 **보기** 메뉴에서 **집계 보기** 를 다시 클릭하여 다시 선택합니다. **보기** 메뉴에서 **그룹화 보기** 를 클릭해도 그룹화된 추적 이벤트를 축소하지 않고 표시할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [추적 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)   
 [추적 테이블 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [추적 파일 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
  
