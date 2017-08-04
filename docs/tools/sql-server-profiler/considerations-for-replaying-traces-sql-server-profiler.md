---
title: "재생 추적 (SQL Server Profiler)에 대 한 고려 사항 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 73fa339f-b71a-4be4-97ca-d4ae84c8b90b
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 77934826a2ba364c4ec8b4e6a5295699d8469257
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="considerations-for-replaying-traces-sql-server-profiler"></a>추적 재생에 대한 고려 사항(SQL Server Profiler)
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]다음과 같은 종류의 추적을 재생할 수 없습니다.  
  
-   트랜잭션 복제 및 기타 트랜잭션 로그 동작이 들어 있는 추적. 이러한 이벤트는 건너뜁니다. 다른 종류의 복제는 트랜잭션 로그를 표시하지 않으므로 영향을 받지 않습니다.  
  
-   GUID(Globally Unique Identifier)가 관련된 작업을 포함한 추적. 이런 이벤트는 건너뜁니다.  
  
-   **bcp**유틸리티, BULK INSERT 문, READTEXT 문, WRITETEXT 문, UPDATETEXT 문 및 전체 텍스트 작업이 관련된 **text**, **ntext** 및 **image** 열에 대한 작업이 포함된 추적. 이러한 이벤트는 건너뜁니다.  
  
-   **sp_getbindtoken** 및 **sp_bindsession** 시스템 저장 프로시저 등의 세션 바인딩이 포함된 추적. 이러한 이벤트는 건너뜁니다.  
  
> [!NOTE]  
>  미리 구성된 재생 템플릿(**TSQL_Replay**)을 사용하지 않고 필요한 모든 데이터를 캡처하지 않으면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 추적을 재생하지 않습니다. 자세한 내용은 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)을 참조하세요.  
  
 추적 재생에 필요한 권한에 대한 자세한 내용은 [Permissions Required to Run SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [SQL Server 이벤트 클래스 참조](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_getbindtoken&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [sp_bindsession&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Readtext&#40; Transact SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [Writetext&#40; Transact SQL &#41;](../../t-sql/queries/writetext-transact-sql.md)   
 [Updatetext&#40; Transact SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
