---
title: 데이터베이스 관리자를 위한 진단 연결 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- server management [SQL Server], connections
- administrator connections [SQL Server]
- ports [SQL Server], DAC
- DAC
- network connections [SQL Server], dedicated administrator
- diagnostic connections [SQL Server]
- connections [SQL Server], dedicated administrator
- ports [SQL Server]
- dedicated administrator connections [SQL Server]
ms.assetid: 993e0820-17f2-4c43-880c-d38290bf7abc
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0d452ca155a5187136c910e81e8bd073e34cad56
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935374"
---
# <a name="diagnostic-connection-for-database-administrators"></a>데이터베이스 관리자를 위한 진단 연결
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 서버에 대한 표준 연결이 불가능할 때 관리자에게 특별 진단 연결을 제공합니다. 이 진단 연결을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 표준 연결 요청에 응답하지 않은 경우에도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 액세스하여 진단 쿼리를 실행하고 문제를 해결할 수 있습니다.  
  
 DAC(관리자 전용 연결)는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 암호화 및 다른 보안 기능을 지원합니다. DAC는 사용자 컨텍스트를 다른 관리자로 변경하는 작업만 허용합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 성공적으로 DAC가 연결되도록 모든 시도를 하지만 극단적인 경우 연결이 실패할 수도 있습니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] .|  
  
## <a name="connecting-with-dac"></a>DAC를 사용하여 연결  
 기본적으로 서버에서 실행되는 클라이언트에서만 연결이 허용됩니다. [remote admin connections 옵션](remote-admin-connections-server-configuration-option.md)이 사용된 sp_configure 저장 프로시저를 사용하여 구성하지 않은 경우에는 네트워크 연결이 허용되지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin 역할의 멤버만이 DAC를 사용하여 연결할 수 있습니다.  
  
 DAC는 **sqlcmd** 명령 프롬프트 유틸리티에 특수 관리자 스위치(**-A**)를 사용하여 이용 가능하며 지원됩니다. **sqlcmd**를 사용하는 방법은 [스크립팅 변수와 함께 sqlcmd 사용](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)을 참조하세요. `admin:` **Sqlcmd-sadmin:** _<instance_name>_ 형식으로 인스턴스 이름에 접두사를 연결할 수도 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 연결 하 여 쿼리 편집기에서 DAC를 시작할 수도 있습니다 `admin:` \<*instance_name*> .  
  
## <a name="restrictions"></a>제한  
 DAC는 드물게 발생하는 서버 문제 진단만을 위한 연결이므로 연결에 다음과 같은 제한이 있습니다.  
  
-   연결에 사용할 수 있는 리소스를 보장하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스당 하나의 DAC만 허용됩니다. DAC 연결이 이미 활성화된 경우 DAC를 통해 연결하려는 모든 새 요청은 17810 오류가 발생하면서 거부됩니다.  
  
-   리소스 절약을 위해 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 은 추적 플래그 7806을 사용하여 시작되지 않는 한 DAC 포트에서 수신하지 않습니다.  
  
-   DAC는 처음에 로그인과 관련된 기본 데이터베이스에 연결을 시도합니다. 성공적으로 연결되면 master 데이터베이스에 연결할 수 있습니다. 기본 데이터베이스가 오프라인이거나 사용할 수 없는 경우 연결은 4060 오류를 반환합니다. 그러나 다음 명령을 사용하면 기본 데이터베이스를 무시하고 master 데이터베이스에 연결할 수 있습니다.  
  
     **sqlcmd -A -d master**  
  
     [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 시작되면 master를 사용할 수 있으므로 DAC로 master 데이터베이스에 연결하는 것이 좋습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 DAC를 사용하여 병렬 쿼리 또는 명령을 실행할 수 없습니다. 예를 들어 DAC로 다음 문 중 하나를 실행하는 경우 3637 오류가 발생합니다.  
  
    -   RESTORE  
  
    -   BACKUP  
  
-   DAC에서는 제한된 리소스만 사용할 수 있습니다. DAC를 사용하여 많은 리소스가 필요한 쿼리(예: 큰 테이블의 복잡한 조인) 또는 차단될 수 있는 쿼리를 실행하지 마십시오. 그래야만 DAC가 기존 서버 문제를 더 악화시키는 것을 방지할 수 있습니다. 차단 가능성을 예방하려면 차단될 수 있는 쿼리를 실행해야 하는 경우에 가능하면 스냅샷 기반 격리 수준에서 해당 쿼리를 실행합니다. 또는 트랜잭션 격리 수준을 READ UNCOMMITTED로 설정하고 LOCK_TIMEOUT 값을 2000밀리초 등의 짧은 값으로 설정하거나 두 방법 모두를 사용합니다. 이렇게 하면 DAC 세션이 차단되지 않습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 상태에 따라 DAC 세션이 래치에서 차단될 수 있습니다. Ctrl+C를 사용하여 DAC 세션을 종료할 수도 있지만 보장할 수 없습니다. 이러한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작하는 것이 유일한 해결 방법입니다.  
  
-   DAC를 통한 연결과 문제 해결을 보장하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 DAC에서 실행된 명령을 처리하도록 제한된 리소스를 예약합니다. 일반적으로 이러한 리소스는 아래에 나열된 기능과 같은 간단한 진단 및 문제 해결 기능만을 수행할 수 있습니다.  
  
 이론상으로는 DAC에서 병렬로 실행하지 않아도 되는 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있지만 다음과 같은 진단 및 문제 해결 명령에만 사용하는 것이 좋습니다.  
  
-   기본 진단을 위해 잠금 상태에 대한 sys.dm_tran_locks, 캐시 상태를 확인하기 위한 sys.dm_os_memory_cache_counters, 활성 세션과 요청을 위한 sys.dm_exec_requests 및 sys.dm_exec_sessions 등 동적 관리 뷰를 쿼리합니다. 리소스를 많이 사용하는 동적 관리 뷰(예를 들어 sys.dm_tran_version_store는 전체 버전 저장소를 검색하므로 광범위한 I/O를 발생시킬 수 있음) 또는 복잡한 조인을 사용하는 동적 관리 뷰를 사용하지 마십시오. 성능에 미치는 영향에 대한 자세한 내용은 해당 [동적 관리 뷰](../../relational-databases/views/views.md)문서를 참조하십시오.  
  
-   카탈로그 뷰를 쿼리합니다.  
  
-   DBCC FREEPROCCACHE, DBCC FREESYSTEMCACHE, DBCC DROPCLEANBUFFERS`,` DBCC SQLPERF 등의 기본 DBCC 명령을 사용합니다. **Dbcc** CHECKDB, dbcc DBREINDEX 또는 dbcc SHRINKDATABASE와 같은 리소스를 많이 사용 하는 명령을 실행 하지 마십시오.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]KILL *\<spid>* 명령입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 상태에 따라 KILL 명령은 성공하지 않을 수도 있습니다. 이러한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작하는 것이 유일한 해결 방법입니다. 일반적인 지침은 다음과 같습니다.  
  
    -   `SELECT * FROM sys.dm_exec_sessions WHERE session_id = <spid>`쿼리를 실행하여 SPID가 실제로 중지되었는지 확인합니다. 행이 반환되지 않으면 세션이 중지된 것입니다.  
  
    -   세션이 아직 중지되지 않은 경우 `SELECT * FROM sys.dm_os_tasks WHERE session_id = <spid>`쿼리를 실행하여 이 세션에 할당된 태스크가 있는지 확인합니다. 할당된 태스크가 있는 경우 세션이 현재 중지되고 있을 가능성이 높습니다. 이러한 작업은 매우 많은 시간이 소요되며 실패할 수 있습니다.  
  
    -   이 세션과 연관된 sys.dm_os_tasks에 태스크가 없지만 KILL 명령을 실행한 후 sys.dm_exec_sessions에 세션이 그대로 남아 있는 경우 사용 가능한 작업자가 없음을 의미합니다. 현재 실행 중인 태스크( `sessions_id <> NULL`로 sys.dm_os_tasks 뷰에 나열된 작업) 중 하나를 선택하고 해당 작업과 연관된 세션을 중지하여 작업자를 확보합니다. 한 세션을 중지해도 해결되지 않으면 여러 세션을 중지해야 합니다.  
  
## <a name="dac-port"></a>DAC 포트  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 TCP 포트 1434(사용 가능한 경우) 또는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 시작 시 동적으로 할당된 TCP 포트에서 DAC를 수신합니다. 오류 로그에는 DAC를 수신 대기 중인 포트 번호가 포함되어 있습니다. 기본적으로 DAC 수신기는 로컬 포트에서만 연결을 허용합니다. 원격 관리 연결을 활성화하는 코드 샘플은 [remote admin connections 서버 구성 옵션](remote-admin-connections-server-configuration-option.md)을 참조하세요.  
  
 원격 관리 연결이 구성된 후에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작하지 않고도 DAC 수신기를 사용할 수 있고 클라이언트가 DAC에 원격으로 연결할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 응답하지 않더라도 먼저 DAC를 로컬로 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결한 다음 sp_configure 저장 프로시저를 실행하여 원격 연결을 허용하면 DAC 수신기가 원격 연결을 허용하도록 할 수 있습니다.  
  
 클러스터 구성에서 DAC는 기본적으로 해제되어 있습니다. 사용자는 sp_configure의 remote admin connection 옵션을 실행하여 DAC 수신기가 원격 연결에 액세스하도록 할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 응답하지 않고 DAC 수신기를 사용할 수 없는 경우 DAC에 연결하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작해야 합니다. 그러므로 클러스터형 시스템에서는 remote admin connections 구성 옵션을 설정하는 것이 좋습니다.  
  
 시작할 때 DAC 포트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 의해 동적으로 할당됩니다. 기본 인스턴스에 연결할 때 DAC는 SQL Server Browser 서비스에 대한 SSRP( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol) 요청을 사용하지 않습니다. 먼저 TCP 포트 1434를 통해 연결합니다. 연결이 실패할 경우 SSRP 호출을 실행하여 포트를 설정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser가 SSRP 요청을 수신하지 않을 경우 연결 요청이 오류를 반환합니다. 오류 로그를 참조하여 DAC를 수신 대기 중인 포트 번호를 찾으십시오. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 원격 관리 연결을 허용하도록 구성되어 있는 경우 DAC를 명시적 포트 번호로 시작해야 합니다.  
  
 **sqlcmd-Stcp:** _ \<server> , \<port> _  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그는 DAC의 포트 번호를 표시합니다. 포트 번호는 기본적으로 1434입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 로컬 DAC 연결만 허용하도록 구성된 경우 다음 명령을 사용하여 루프백 어댑터를 통해 연결하십시오.  
  
 **sqlcmd-s 127.0.0.1**,`1434`  
  
## <a name="example"></a>예제  
 이 예에서 관리자는 `URAN123` 서버가 응답하지 않음을 확인하고 문제를 진단하려고 합니다. 이 작업을 수행하려면 사용자는 `sqlcmd` 명령 프롬프트 유틸리티를 활성화하고 DAC를 나타내는 `URAN123` 를 사용하여 `-A` 서버에 연결해야 합니다.  
  
 `sqlcmd -S URAN123 -U sa -P <xxx> -A`  
  
 이제 관리자가 쿼리를 실행하여 문제를 진단하고 응답하지 않는 세션을 종료할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
## <a name="related-content"></a>관련 내용  
 [스크립팅 변수와 함께 sqlcmd 사용](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)  
  
 [SELECT&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)  
  
 [sp_who&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql)  
  
 [sp_lock&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-lock-transact-sql)  
  
 [KILL&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/kill-transact-sql)  
  
 [DBCC CHECKALLOC&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkalloc-transact-sql)  
  
 [DBCC CHECKDB&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
 [DBCC OPENTRAN&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-opentran-transact-sql)  
  
 [DBCC INPUTBUFFER&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-inputbuffer-transact-sql)  
  
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
 [트랜잭션 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql)  
  
 [추적 플래그&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)  
  
  
