---
title: 단일 이벤트를 한 번에 하나씩 재생(SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- events [SQL Server], replaying single event at a time
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 220fb192-9636-41a2-b15c-62af6cab8fff
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab6d5c64ab1f154e0b31cabfe89ba9aa095bf376
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47800012"
---
# <a name="replay-a-single-event-at-a-time-sql-server-profiler"></a>단일 이벤트를 한 번에 하나씩 재생(SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 재생 추적 파일이나 테이블에서 한 번에 하나씩 이벤트를 재생하는 방법에 대해 설명합니다.  
  
### <a name="to-replay-a-single-event-at-a-time"></a>한 번에 하나씩 단일 이벤트를 재생하려면  
  
1.  재생할 추적 파일이나 추적 테이블을 엽니다. 자세한 내용은 [추적 파일 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 또는 [추적 테이블 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)에서 제공되는 사전 정의된 튜닝 템플릿을 사용합니다.  
  
     열려는 추적 파일이나 추적 테이블에 재생에 필요한 이벤트 클래스가 포함되어 있는지 확인합니다. 자세한 내용은 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)을(를) 참조하세요.  
  
2.  **재생** 메뉴에서 **단계**를 클릭하고 추적을 재생하려는 서버 인스턴스에 연결합니다.  
  
3.  **재생 구성** 대화 상자에서 설정을 확인한 다음 **확인**을 클릭합니다. **재생 구성** 대화 상자에서 설정을 지정하는 방법은 [추적 파일 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md) 또는 [추적 테이블 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)을 참조하세요.  
  
4.  첫 번째 이벤트를 재생하려면 **재생 구성** 대화 상자에서 **확인** 을 클릭합니다.  
  
5.  다음 이벤트를 재생하려면 **재생** 메뉴에서 **단계**를 클릭하거나 F10 키를 누릅니다. **단계** 를 클릭하거나 F10 키를 누를 때마다 다음 이벤트가 순서대로 재생됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [추적 재생](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server 프로파일러](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
