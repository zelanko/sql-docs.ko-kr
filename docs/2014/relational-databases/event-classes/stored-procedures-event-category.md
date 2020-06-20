---
title: Stored Procedures 이벤트 범주 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Stored Procedures event category [SQL Server]
- SQL Server event classes, Stored Procedures event category
- event classes [SQL Server], Stored Procedures event category
ms.assetid: 71bebaa3-a05a-4695-b349-078cecd0949a
author: stevestein
ms.author: sstein
ms.openlocfilehash: df2e0d9a4c077ff16eba09bc5ebb6447d5d27595
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85051432"
---
# <a name="stored-procedures-event-category"></a>Stored Procedures 이벤트 범주
  **Stored Procedures** 이벤트 범주는 일반 저장 프로시저 이벤트를 포함합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[RPC:Completed 이벤트 클래스](rpc-completed-event-class.md)|RPC(원격 프로시저 호출)가 완료되었음을 나타냅니다.|  
|[PreConnect:Completed 이벤트 클래스](preconnect-completed-event-class.md)|리소스 관리자의 분류자 함수가 실행을 완료하는 때를 나타냅니다.|  
|[PreConnect:Starting 이벤트 클래스](preconnect-starting-event-class.md)|리소스 관리자의 분류자 함수가 실행을 시작하는 때를 나타냅니다.|  
|[RPC Output Parameter 이벤트 클래스](rpc-output-parameter-event-class.md)|실행 후 원격 프로시저 호출의 출력 매개 변수 값을 추적합니다.|  
|[RPC:Starting 이벤트 클래스](rpc-starting-event-class.md)|원격 프로시저 호출을 시작했음을 나타냅니다.|  
|[SP:CacheHit 이벤트 클래스](sp-cachehit-event-class.md)|저장 프로시저가 캐시에 있음을 나타냅니다.|  
|[SP:CacheInsert 이벤트 클래스](sp-cacheinsert-event-class.md)|저장 프로시저를 캐시로 가져왔음을 나타냅니다.|  
|[SP:CacheMiss 이벤트 클래스](sp-cachemiss-event-class.md)|저장 프로시저가 캐시에 없음을 나타냅니다.|  
|[SP:CacheRemove 이벤트 클래스](sp-cacheremove-event-class.md)|저장 프로시저가 캐시에서 제거되었음을 나타냅니다.|  
|[SP:Completed 이벤트 클래스](sp-completed-event-class.md)|저장 프로시저 실행이 완료되었음을 나타냅니다.|  
|[SP:Recompile 이벤트 클래스](sp-recompile-event-class.md)|저장 프로시저가 다시 컴파일되었음을 나타냅니다.|  
|[SP:Starting 이벤트 클래스](sp-starting-event-class.md)|저장 프로시저 실행을 시작했음을 나타냅니다.|  
|[SP:StmtCompleted 이벤트 클래스](sp-stmtcompleted-event-class.md)|저장 프로시저 내의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 완료했음을 나타냅니다.|  
|[SP:StmtStarting 이벤트 클래스](sp-stmtstarting-event-class.md)|저장 프로시저 내의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 시작했음을 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
