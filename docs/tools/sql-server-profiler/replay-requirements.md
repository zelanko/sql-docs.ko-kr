---
title: Replay Requirements
titleSuffix: SQL Server Profiler
description: SQL Server Profiler 또는 Distributed Replay 유틸리티를 사용하여 추적 데이터를 재생할 수 있도록 추적에서 캡처할 이벤트 클래스 및 데이터 열에 대해 알아봅니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 0e01dfc7-84b9-47f6-8bf7-b0656df4fa7d
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: d5fa4964a2ffb0d62777c25aa0d0c6ef205ee94b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789929"
---
# <a name="replay-requirements"></a>Replay Requirements

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 나 Distributed Replay Utility를 사용하여 추적 데이터를 재생하려면 특정 이벤트 클래스 및 열 집합이 추적에 캡처되어야 합니다. **TSQL_Replay** 추적 템플릿을 사용하여 나중에 재생에 사용되도록 추적을 구성한 경우 이러한 설정이 기본적으로 사용됩니다. 이 항목에서는 이러한 설정 및 기타 재생 요구 사항에 대해 설명합니다.  
  
> [!NOTE]  
>  리소스를 많이 사용하는 OLTP 애플리케이션(활성 동시 연결 수가 많거나 처리량이 많음)을 재생하는 데는 Distributed Replay Utility를 사용하는 것이 좋습니다. Distributed Replay Utility는 여러 컴퓨터의 추적 데이터를 재생할 수 있으므로 중요한 작업을 효율적으로 시뮬레이션할 수 있습니다. 자세한 내용은 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)을 참조하세요.  
  
## <a name="event-classes-required-for-replay"></a>재생에 필요한 이벤트 클래스  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]가 데이터를 재생하려면 다음 이벤트 클래스 집합 및 모니터링하려는 기타 다른 이벤트 클래스가 추적에 캡처되어야 합니다.  
  
-   **CursorClose**(서버 쪽 커서를 재생할 때만 필요)  
  
-   **CursorExecute** (서버 쪽 커서를 재생할 때만 필요)  
  
-   **CursorOpen** (서버 쪽 커서를 재생할 때만 필요)  
  
-   **CursorPrepare** (서버 쪽 커서를 재생할 때만 필요)  
  
-   **CursorUnprepare** (서버 쪽 커서를 재생할 때만 필요)  
  
-   **Audit Login**  
  
-   **Audit Logout**  
  
-   **ExistingConnection**  
  
-   **RPC Output Parameter**  
  
-   **RPC:Completed**  
  
-   **RPC:Starting**  
  
-   **Exec Prepared SQL** (서버 쪽에서 준비한 SQL 문을 재생할 때만 필요)  
  
-   **Prepare SQL** (서버 쪽에서 준비한 SQL 문을 재생할 때만 필요)  
  
-   **SQL:BatchCompleted**  
  
-   **SQL:BatchStarting**  
  
## <a name="data-columns-required-for-replay"></a>재생에 필요한 데이터 열  
 추적을 재생하려면 캡처할 다른 데이터 열 외에도 다음 데이터 열을 추적에 캡처해야 합니다.  
  
-   **Event Class**  
  
-   **EventSequence**  
  
-   **TextData**  
  
-   **애플리케이션 이름**  
  
-   **LoginName**  
  
-   **DatabaseName**  
  
-   **데이터베이스 ID**  
  
-   **ClientProcessID**  
  
-   **HostName**  
  
-   **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**  
  
-   **Binary Data**  
  
-   **SPID**  
  
-   **Start Time**  
  
-   **EndTime**  
  
-   **IsSystem**  
  
-   **NTDomainName**  
  
-   **NTUserName**  
  
-   **오류**  
  
> [!NOTE]  
>  재생용 데이터를 캡처하는 추적에는 **TSQL_Replay** 추적 템플릿을 사용하세요.  
  
## <a name="other-replay-requirements"></a>기타 재생 요구 사항  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 재생할 때 필수 이벤트 및 열이 있는지 확인합니다. 이와 같이 변경된 기능은 재생의 정확도를 높이고 필수 데이터가 누락된 경우 재생 문제 해결 과정에서 추측을 통해 작업을 수행하지 않도록 도와 줍니다. 필수 데이터가 추적에 없을 경우 재생 시 오류가 반환되고 파일 재생이 중지됩니다.  
  
 원래 추적한 서버(원본)가 아니라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행되고 있는 서버(대상)에 대해 추적을 재생하려면 다음 조건이 충족되어야 합니다.  
  
-   추적에 포함된 모든 로그인 및 사용자가 대상 및 원본과 같은 데이터베이스에서 이미 만들어져 있어야 합니다.  
  
-   대상에 있는 모든 로그인 및 사용자는 원본에서 가진 권한과 같은 권한을 가져야 합니다.  
  
-   모든 로그인 암호는 재생을 실행하는 사용자의 로그인 암호와 같아야 합니다.  
  
-   대상에 있는 데이터베이스 ID가 원본에 있는 데이터베이스 ID와 같아야 합니다. 그러나 두 ID가 서로 다르다면 **DatabaseName** 이 추적에 있을 경우 이를 기준으로 일치시킬 수 있습니다.  
  
-   추적에 포함된 각 로그인의 기본 데이터베이스가 대상에서 로그인의 각 대상 데이터베이스로 설정되어야 합니다. 예를 들어 재생할 추적은 원본에 있는 **Fred_Db**데이터베이스의 **Fred** 라는 로그인에 대한 동작을 포함합니다. 그러므로 대상에서 **Fred**로그인에 대한 기본 데이터베이스는 **Fred_Db** 와 일치하는 데이터베이스로 설정되어야 합니다. 데이터베이스 이름이 다르더라도 마찬가지입니다. 로그인의 기본 데이터베이스를 설정하려면 **sp_defaultdb** 시스템 저장 프로시저를 사용합니다.  
  
 누락되거나 잘못된 로그인과 연관된 이벤트를 재생하면 재생 오류가 발생하지만 재생 작업은 계속됩니다.  
  
 추적 재생에 필요한 권한에 대한 자세한 내용은 [Permissions Required to Run SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [추적 테이블 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [추적 파일 재생&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [SQL Server 이벤트 클래스 참조](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_defaultdb&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
