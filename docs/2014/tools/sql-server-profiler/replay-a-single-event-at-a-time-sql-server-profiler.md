---
title: 단일 이벤트를 한 번에 하나씩 재생(SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- events [SQL Server], replaying single event at a time
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 220fb192-9636-41a2-b15c-62af6cab8fff
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5424a91d2672710a593555c937157a4501469e4a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299353"
---
# <a name="replay-a-single-event-at-a-time-sql-server-profiler"></a>단일 이벤트를 한 번에 하나씩 재생(SQL Server Profiler)
  이 항목에서는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 재생 추적 파일이나 테이블에서 한 번에 하나씩 이벤트를 재생하는 방법에 대해 설명합니다.  
  
### <a name="to-replay-a-single-event-at-a-time"></a>한 번에 하나씩 단일 이벤트를 재생하려면  
  
1.  재생할 추적 파일이나 추적 테이블을 엽니다. 자세한 내용은 [추적 파일 열기&#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) 또는 [추적 테이블 열기&#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)를 참조하세요.  
  
     열려는 추적 파일이나 추적 테이블에 재생에 필요한 이벤트 클래스가 포함되어 있는지 확인합니다. 자세한 내용은 [Replay Requirements](replay-requirements.md)을(를) 참조하세요.  
  
2.  **재생** 메뉴에서 **단계**를 클릭하고 추적을 재생하려는 서버 인스턴스에 연결합니다.  
  
3.  **재생 구성** 대화 상자에서 설정을 확인한 다음 **확인**을 클릭합니다. **재생 구성** 대화 상자에서 설정을 지정하는 방법은 [추적 파일 재생&#40;SQL Server Profiler&#41;](replay-a-trace-file-sql-server-profiler.md) 또는 [추적 테이블 재생&#40;SQL Server Profiler&#41;](replay-a-trace-table-sql-server-profiler.md)을 참조하세요.  
  
4.  첫 번째 이벤트를 재생하려면 **재생 구성** 대화 상자에서 **확인** 을 클릭합니다.  
  
5.  다음 이벤트를 재생하려면 **재생** 메뉴에서 **단계**를 클릭하거나 F10 키를 누릅니다. **단계** 를 클릭하거나 F10 키를 누를 때마다 다음 이벤트가 순서대로 재생됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [추적 재생](replay-traces.md)   
 [SQL Server 프로파일러](sql-server-profiler.md)  
  
  
