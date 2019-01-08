---
title: 재생 커서로 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- replaying cursors
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 89eadc41-4424-4a1c-ba61-0b52c851cdb1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7c4c4b9d2e2e07c53f850fe545d803fa411dbbc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52795825"
---
# <a name="replay-to-a-cursor-sql-server-profiler"></a>커서까지 재생(SQL Server Profiler)
  이 항목에서는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 커서에 도달했을 때 일시 중지된 추적 파일이나 테이블을 재생하는 방법에 대해 설명합니다. 커서에서 추적을 일시 중지하면 긴 추적 스크립트 재생을 증분 분석이 가능한 짧은 세그먼트로 나눌 수 있기 때문에 디버깅할 수 있습니다.  
  
### <a name="to-replay-to-the-cursor"></a>커서까지 재생하려면  
  
1.  재생할 추적 파일이나 추적 테이블을 엽니다. 자세한 내용은 [추적 파일 열기&#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) 또는 [추적 테이블 열기&#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)에서 제공되는 사전 정의된 튜닝 템플릿을 사용합니다.  
  
     열려는 추적 파일이나 추적 테이블에 재생에 필요한 이벤트 클래스가 포함되어 있는지 확인합니다. 자세한 내용은 [Replay Requirements](replay-requirements.md)을 참조하세요.  
  
2.  추적 창에서 이벤트를 클릭합니다.  
  
3.  **재생** 메뉴에서 **커서까지 실행**을 클릭한 다음 추적을 재생할 서버에 연결합니다.  
  
4.  **재생 구성** 대화 상자에서 설정을 확인한 다음 **확인**을 클릭합니다.  
  
     재생이 시작되며 첫 번째 커서에서 일시 중지됩니다.  
  
5.  추적을 다시 시작하려면 F5 키를 누릅니다.  
  
6.  추적이 끝날 때까지 5단계를 반복합니다.  
  
## <a name="see-also"></a>관련 항목  
 [중단점까지 재생&#40;SQL Server Profiler&#41;](replay-to-a-breakpoint-sql-server-profiler.md)   
 [추적 재생](replay-traces.md)   
 [SQL Server 프로파일러](sql-server-profiler.md)  
  
  
