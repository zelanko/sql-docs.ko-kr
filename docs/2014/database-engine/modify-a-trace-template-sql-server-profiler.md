---
title: 추적 템플릿 수정 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- templates [SQL Server], traces
- trace templates [SQL Server]
- modifying traces
ms.assetid: b81df2a1-e202-43d8-92b0-0beb145f0116
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 64c13b9fed062b73de7ab35ef5048ae4b68e5618
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089995"
---
# <a name="modify-a-trace-template-sql-server-profiler"></a>추적 템플릿 수정(SQL Server Profiler)
  이 항목에서는 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]를 사용하여 추적 템플릿을 수정하는 방법에 대해 설명합니다.  
  
### <a name="to-modify-a-trace-template"></a>추적 템플릿을 수정하려면  
  
1.  **파일** 메뉴에서 **템플릿**- **템플릿 편집**을 클릭합니다.  
  
2.  **추적 템플릿 속성** 대화 상자의 **일반** 탭에서 서버 유형과 템플릿 이름을 수정하거나 서버 유형에 맞는 기본 템플릿을 사용하도록 선택합니다.  
  
3.  **이벤트 선택**탭에서 표 형태 컨트롤을 사용 하 여 다음과 같이 추적 파일에서 이벤트와 데이터 열을 추가 하거나 제거 합니다.  
  
    -   이벤트를 추가하려면 **이벤트** 열의 해당 이벤트 범주를 확장한 다음 이벤트 이름을 선택합니다.  
  
    -   이벤트를 추가할 때는 관련된 모든 데이터 열이 기본적으로 포함됩니다. 추적에서 이벤트에 대한 데이터 열을 제거하려면 해당 이벤트에 대한 데이터 열의 확인란 선택을 취소합니다.  
  
    -   필터를 추가하려면 데이터 열 이름을 클릭하고 **필터 편집** 대화 상자에 필터 조건을 지정합니다. 또한 데이터 열 이름을 마우스 오른쪽 단추로 클릭하고 **열 필터 편집** 을 클릭하여 **필터 편집** 대화 상자를 실행할 수 있습니다. **확인** 을 클릭하여 필터를 추가합니다.  
  
4.  **저장**또는 **다른 이름으로 저장**을 클릭하여 추적 템플릿을 저장합니다.  
  
## <a name="see-also"></a>참고 항목  
 [추적 파일 &#40;SQL Server Profiler&#41;에 대 한 이벤트 및 데이터 열을 지정 합니다.](../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [실행 중인 추적에서 템플릿을 파생 SQL Server Profiler &#40;&#41;](../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [추적 파일 또는 추적 테이블에서 템플릿을 파생 SQL Server Profiler &#40;&#41;](../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [SQL Server Profiler 템플릿 및 권한](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
