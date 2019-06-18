---
title: 추적 재생에 대한 고려 사항(SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 73fa339f-b71a-4be4-97ca-d4ae84c8b90b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c76f57d548ed0531920c968c30028083980777d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63033805"
---
# <a name="considerations-for-replaying-traces-sql-server-profiler"></a>추적 재생에 대한 고려 사항(SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 다음과 같은 종류의 추적을 재생할 수 없습니다.  
  
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
 [sp_getbindtoken&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [sp_bindsession&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [READTEXT&#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [WRITETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)   
 [UPDATETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
