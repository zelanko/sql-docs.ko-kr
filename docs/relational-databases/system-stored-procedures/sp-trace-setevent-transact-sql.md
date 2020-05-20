---
title: sp_trace_setevent (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_setevent_TSQL
- sp_trace_setevent
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setevent
ms.assetid: 7662d1d9-6d0f-443a-b011-c901a8b77a44
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b8c58657eda708965821c4739f76b49c558c8e76
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832590"
---
# <a name="sp_trace_setevent-transact-sql"></a>sp_trace_setevent(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  추적에 이벤트 또는 이벤트 열을 추가하거나 제거합니다. **sp_trace_setevent** 는 중지 된 기존 추적 에서만 실행할 수 있습니다 (*상태* **0**). 존재 하지 않거나 *상태가* **0**이 아닌 추적에서이 저장 프로시저를 실행 하면 오류가 반환 됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 확장 이벤트를 대신 사용하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_trace_setevent [ @traceid = ] trace_id   
          , [ @eventid = ] event_id  
          , [ @columnid = ] column_id  
          , [ @on = ] on  
```  
  
## <a name="arguments"></a>인수  
`[ @traceid = ] trace_id`수정할 추적의 ID입니다. *trace_id* 는 **int**이며 기본값은 없습니다. 사용자는이 *trace_id* 값을 사용 하 여 추적을 식별, 수정 및 제어할 수 있습니다.  
  
`[ @eventid = ] event_id`설정할 이벤트의 ID입니다. *event_id* 는 **int**이며 기본값은 없습니다.  
  
 다음 표에서는 추적에서 추가 또는 제거될 수 있는 이벤트를 보여 줍니다.  
  
|이벤트 번호|이벤트 이름|설명|  
|------------------|----------------|-----------------|  
|0-9|Reserved|Reserved|  
|10|RPC:Completed|RPC(원격 프로시저 호출)가 완료되면 발생합니다.|  
|11|RPC:Starting|RPC가 시작되면 발생합니다.|  
|12|SQL:BatchCompleted|[!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리가 완료되면 발생합니다.|  
|13|SQL:BatchStarting|[!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리가 시작되면 발생합니다.|  
|14|로그인 감사|사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 성공적으로 로그인하면 발생합니다.|  
|15|로그아웃 감사|사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 로그아웃하면 발생합니다.|  
|16|Attention|클라이언트 인터럽트 요청이나 클라이언트 연결이 끊어지는 등 주의 이벤트가 일어나면 발생합니다.|  
|17|ExistingConnection|추적이 시작되기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결된 사용자의 모든 작업을 검색합니다.|  
|18|Audit Server Starts and Stops|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 상태가 수정되면 발생합니다.|  
|19|DTCTransaction|둘 이상의 데이터베이스 간에 일어나는 MS DTC([!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator) 통합 트랜잭션을 추적합니다.|  
|20|Audit Login Failed|클라이언트에서 시도한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 실패했음을 나타냅니다.|  
|21|EventLog|이벤트가 Windows 애플리케이션 로그에 기록되었음을 나타냅니다.|  
|22|ErrorLog|오류 이벤트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 기록되었음을 나타냅니다.|  
|23|Lock:Released|페이지 등 리소스 잠금이 해제되었음을 나타냅니다.|  
|24|Lock:Acquired|데이터 페이지 등 리소스 잠금이 획득되었음을 나타냅니다.|  
|25|Lock:Deadlock|다른 트랜잭션이 소유한 리소스에 대해 호환되지 않는 잠금을 가져오려고 시도하여 두 개의 동시 트랜잭션이 서로 교착 상태에 있음을 나타냅니다.|  
|26|Lock:Cancel|리소스 잠금 획득이 교착 상태 등에 의해 취소되었음을 나타냅니다.|  
|27|Lock:Timeout|필요한 리소스의 차단 잠금을 보유한 다른 트랜잭션으로 인해 페이지 등 리소스 잠금에 대한 요청 시간이 초과되었음을 나타냅니다. 제한 시간은 @ 함수에 의해 결정 @LOCK_TIMEOUT 되며 set LOCK_TIMEOUT 문으로 설정할 수 있습니다.|  
|28|Degree of Parallelism Event(7.0 Insert)|SELECT, INSERT 또는 UPDATE 문이 실행되기 전에 발생합니다.|  
|29-31|Reserved|이벤트 28을 대신 사용합니다.|  
|32|Reserved|Reserved|  
|33|예외|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 예외가 발생했음을 나타냅니다.|  
|34|SP:CacheMiss|저장 프로시저가 프로시저 캐시에서 발견되지 않는 때를 나타냅니다.|  
|35|SP:CacheInsert|항목이 프로시저 캐시에 삽입되는 때를 나타냅니다.|  
|36|SP:CacheRemove|항목이 프로시저 캐시에서 제거되는 때를 나타냅니다.|  
|37|SP:Recompile|저장 프로시저가 다시 컴파일되었음을 나타냅니다.|  
|38|SP:CacheHit|저장 프로시저가 프로시저 캐시에서 발견되는 때를 나타냅니다.|  
|39|사용되지 않음|사용되지 않음|  
|40|SQL:StmtStarting|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 시작되면 발생합니다.|  
|41|SQL:StmtCompleted|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 완료되면 발생합니다.|  
|42|SP:Starting|저장 프로시저가 시작된 때를 나타냅니다.|  
|43|SP:Completed|저장 프로시저가 완료된 때를 나타냅니다.|  
|44|SP:StmtStarting|저장 프로시저 내의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 실행을 시작했음을 나타냅니다.|  
|45|SP:StmtCompleted|저장 프로시저 내의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 실행을 완료했음을 나타냅니다.|  
|46|Object:Created|CREATE INDEX, CREATE TABLE 및 CREATE DATABASE 문 등을 위해 개체가 만들어졌음을 나타냅니다.|  
|47|Object:Deleted|DROP INDEX 및 DROP TABLE 문 등에서 개체가 삭제되었음을 나타냅니다.|  
|48|Reserved||  
|49|Reserved||  
|50|SQL Transaction|[!INCLUDE[tsql](../../includes/tsql-md.md)] BEGIN, COMMIT, SAVE 및 ROLLBACK TRANSACTION 문을 추적합니다.|  
|51|Scan:Started|테이블 또는 인덱스 검색이 시작된 때를 나타냅니다.|  
|52|Scan:Stopped|테이블 또는 인덱스 검색이 중지된 때를 나타냅니다.|  
|53|CursorOpen|커서가 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 ODBC, OLE DB 또는 DB-Library에 의해 열린 때를 나타냅니다.|  
|54|TransactionLog|트랜잭션이 트랜잭션 로그에 기록되는 시기를 추적합니다.|  
|55|Hash Warning|버퍼 파티션에서 처리되지 않는 해시 조인, 해시 집계, 해시 통합, 해시 중복 제외 등의 해시 작업이 대체 계획으로 되돌려졌음을 나타냅니다. 이는 재귀 깊이, 데이터 기울기, 추적 플래그 또는 비트 계산에 의해 발생할 수 있습니다.|  
|56-57|Reserved||  
|58|Auto Stats|인덱스 통계 자동 업데이트가 발생했음을 나타냅니다.|  
|59|Lock:Deadlock Chain|교착 상태로 끝난 각 이벤트에 대해 만들어집니다.|  
|60|Lock:Escalation|페이지 잠금이 TABLE 또는 HoBT 잠금으로 에스컬레이션 또는 변환되는 경우처럼 미세 잠금이 성긴 잠금으로 변환되었음을 나타냅니다.|  
|61|OLE DB Errors|OLE DB 오류가 발생하였음을 나타냅니다.|  
|62-66|Reserved||  
|67|Execution Warnings|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문이나 저장 프로시저 실행 중에 발생한 경고를 나타냅니다.|  
|68|Showplan Text (Unencoded)|실행된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 계획 트리를 표시합니다.|  
|69|Sort Warnings|정렬 작업이 메모리에 적합하지 않음을 나타냅니다. 인덱스 만들기와 연관된 정렬 작업은 포함하지 않으며 SELECT 문에 사용된 ORDER BY 절 등 쿼리 내의 정렬 작업만 포함합니다.|  
|70|CursorPrepare|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 커서를 ODBC, OLE DB 또는 DB-Library에서 사용할 수 있도록 준비된 때를 나타냅니다.|  
|71|Prepare SQL|ODBC, OLE DB 또는 DB-Library가 사용하기 위한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 준비했습니다.|  
|72|Exec Prepared SQL|ODBC, OLE DB 또는 DB-Library가 준비된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행했습니다.|  
|73|Unprepare SQL|ODBC, OLE DB 또는 DB-Library가 준비된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 준비 취소(삭제)했습니다.|  
|74|CursorExecute|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 ODBC, OLE DB 또는 DB-Library에 의해 이전에 준비된 커서를 실행했습니다.|  
|75|CursorRecompile|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 ODBC 또는 DB-Library에 의해 열린 커서를 직접 또는 스키마 변경에 따라 다시 컴파일했습니다.<br /><br /> ANSI 및 비-ANSI 커서에 대해 트리거됩니다.|  
|76|CursorImplicitConversion|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 커서를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 다른 유형으로 변환했습니다.<br /><br /> ANSI 및 비-ANSI 커서에 대해 트리거됩니다.|  
|77|CursorUnprepare|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 준비된 커서가 ODBC, OLE DB 또는 DB-Library에 의해 준비 취소(삭제)되었습니다.|  
|78|CursorClose|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 ODBC, OLE DB 또는 DB-Library에 의해 이전에 열린 커서가 닫혔습니다.|  
|79|Missing Column Statistics|최적화 프로그램에 사용하는 열 통계를 사용할 수 없습니다.|  
|80|Missing Join Predicate|조인 술어가 없는 쿼리가 실행 중입니다. 이 결과 실행 시간이 긴 쿼리가 나타날 수 있습니다.|  
|81|Server Memory Change|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 사용량이 1MB와 최대 서버 메모리의 5%에 해당하는 값 중 큰 값만큼 증가 또는 감소했습니다.|  
|82-91|User Configurable(0-9)|사용자가 정의한 이벤트 데이터입니다.|  
|92|Data File Auto Grow|데이터 파일이 서버에 의해 자동으로 확장되었음을 나타냅니다.|  
|93|Log File Auto Grow|로그 파일이 서버에 의해 자동으로 확장되었음을 나타냅니다.|  
|94|Data File Auto Shrink|데이터 파일이 서버에 의해 자동으로 축소되었음을 나타냅니다.|  
|95|Log File Auto Shrink|로그 파일이 서버에 의해 자동으로 축소되었음을 나타냅니다.|  
|96|Showplan Text|쿼리 최적화 프로그램에서 SQL 문의 쿼리 계획 트리를 표시합니다. **TextData** 열에는이 이벤트에 대 한 실행 계획이 포함 되지 않습니다.|  
|97|Showplan All|실행된 SQL 문의 전체 컴파일 시간 정보와 쿼리 계획을 표시합니다. **TextData** 열에는이 이벤트에 대 한 실행 계획이 포함 되지 않습니다.|  
|98|Showplan Statistics Profile|실행된 SQL 문의 전체 실행 시간 정보와 쿼리 계획을 표시합니다. **TextData** 열에는이 이벤트에 대 한 실행 계획이 포함 되지 않습니다.|  
|99|Reserved||  
|100|RPC Output Parameter|모든 RPC에 대한 매개 변수의 출력 값을 생성합니다.|  
|101|Reserved||  
|102|Audit Database Scope GDR|데이터베이스 사용 권한 부여와 같은 데이터베이스 전용 동작에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자가 문 사용 권한에 대한 GRANT, DENY 또는 REVOKE를 실행할 때마다 발생합니다.|  
|103|Audit Object GDR Event|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자가 개체 사용 권한에 대한 GRANT, DENY, REVOKE를 실행할 때마다 발생합니다.|  
|104|Audit Addlogin Event|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Sp_addlogin** 및 **sp_droplogin**에 대해 로그인이 추가 되거나 제거 될 때 발생 합니다.|  
|105|Audit Login GDR Event|Windows 로그인 권한이 추가 되거나 제거 될 때 발생 합니다. **sp_grantlogin**, **sp_revokelogin**및 **sp_denylogin**입니다.|  
|106|Audit Login Change Property Event|암호를 제외한 로그인 속성이 수정 되 면 발생 합니다. **sp_defaultdb** 및 **sp_defaultlanguage**.|  
|107|Audit Login Change Password Event|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 암호가 변경되면 발생합니다.<br /><br /> 암호가 기록되지 않았습니다.|  
|108|Audit Add Login to Server Role Event|고정 서버 역할에서 로그인이 추가 되거나 제거 될 때 발생 합니다. **sp_addsrvrolemember**및 **sp_dropsrvrolemember**.|  
|109|Audit Add DB User Event|데이터베이스 사용자 (Windows 또는)로 로그인을 추가 하거나 제거 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 발생 합니다. **sp_grantdbaccess**, **sp_revokedbaccess**, **sp_adduser**및 **sp_dropuser**에 대 한 것입니다.|  
|110|Audit Add Member to DB Role Event|데이터베이스에 대 한 데이터베이스 사용자 (고정 또는 사용자 정의)로 로그인이 추가 되거나 제거 될 때 발생 합니다. **sp_addrolemember**, **sp_droprolemember**및 **sp_changegroup**입니다.|  
|111|Audit Add Role Event|데이터베이스에 대 한 로그인이 데이터베이스 사용자로 추가 되거나 제거 될 때 발생 합니다. **sp_addrole** 및 **sp_droprole**.|  
|112|Audit App Role Change Password Event|애플리케이션 역할의 암호가 변경되면 발생합니다.|  
|113|Audit Statement Permission Event|CREATE TABLE 등 문 사용 권한이 사용되면 발생합니다.|  
|114|Audit Schema Object Access Event|SELECT 등 개체 사용 권한이 성공적으로 사용되거나 성공적으로 사용되지 않은 모든 경우에 발생합니다.|  
|115|Audit Backup/Restore Event|BACKUP 또는 RESTORE 명령을 실행하면 발생합니다.|  
|116|Audit DBCC Event|DBCC 명령을 실행하면 발생합니다.|  
|117|Audit Change Audit Event|감사 추적을 수정하면 발생합니다.|  
|118|Audit Object Derived Permission Event|CREATE, ALTER 및 DROP 개체 명령을 실행하면 발생합니다.|  
|119|OLEDB Call Event|분산 쿼리 및 원격 저장 프로시저에 대해 OLE DB Provider를 호출하면 발생합니다.|  
|120|OLEDB QueryInterface Event|분산 쿼리 및 원격 저장 프로시저에 대해 **QueryInterface** 호출이 수행 OLE DB 될 때 발생 합니다.|  
|121|OLEDB DataRead Event|OLE DB Provider에 대해 데이터 요청을 호출하면 발생합니다.|  
|122|Showplan XML|SQL 문을 실행하면 발생합니다. 실행 계획 연산자를 식별하는 이 이벤트를 포함합니다. 각 이벤트는 올바른 형식의 XML 문서에 저장됩니다. 이 이벤트의 **이진** 열에는 인코딩된 실행 계획이 포함 됩니다. SQL Server 프로파일러를 사용하여 추적을 열고 실행 계획을 확인할 수 있습니다.|  
|123|SQL:FullTextQuery|전체 텍스트 쿼리가 실행되면 발생합니다.|  
|124|Broker:Conversation|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화의 진행률을 보고합니다.|  
|125|Deprecation Announcement|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다음 버전에서 제거될 기능을 사용하면 발생합니다.|  
|126|Deprecation Final Support|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다음 버전에서 제거될 기능을 사용하면 발생합니다.|  
|127|Exchange Spill Event|병렬 쿼리 계획의 통신 버퍼가 **tempdb** 데이터베이스에 일시적으로 기록 될 때 발생 합니다.|  
|128|Audit Database Management Event|데이터베이스를 생성, 변경 또는 삭제하면 발생합니다.|  
|129|Audit Database Object Management Event|CREATE, ALTER 또는 DROP 문이 스키마 같은 데이터베이스 개체에서 실행되면 발생합니다.|  
|130|Audit Database Principal Management Event|사용자 같은 보안 주체가 데이터베이스에서 생성, 변경 또는 삭제되면 발생합니다.|  
|131|Audit Schema Object Management Event|서버 개체를 생성, 변경 또는 삭제하면 발생합니다.|  
|132|Audit Server Principal Impersonation Event|EXECUTE AS LOGIN처럼 서버 범위 내에 가장이 있으면 발생합니다.|  
|133|Audit Database Principal Impersonation Event|EXECUTE AS USER 또는 SETUSER처럼 데이터베이스 범위 내에서 가장이 수행되면 발생합니다.|  
|134|Audit Server Object Take Ownership Event|서버 범위의 개체에 대한 소유자가 변경되면 발생합니다.|  
|135|Audit Database Object Take Ownership Event|데이터베이스 범위 내에 있는 개체에 대한 소유자가 변경되면 발생합니다.|  
|136|Broker:Conversation Group|[!INCLUDE[ssSB](../../includes/sssb-md.md)]가 새 대화 그룹을 만들거나 기존 대화 그룹을 삭제하면 발생합니다.|  
|137|Blocked Process Report|지정된 기간 이상 동안 프로세스가 차단되면 발생합니다. 교착 상태를 감지할 수 없는 리소스에서 대기하는 시스템 프로세스 또는 프로세스를 포함하지 않습니다. **Sp_configure** 를 사용 하 여 보고서가 생성 되는 임계값과 빈도를 구성할 수 있습니다.|  
|138|Broker:Connection|[!INCLUDE[ssSB](../../includes/sssb-md.md)]가 관리하는 전송 연결의 상태를 보고합니다.|  
|139|Broker:Forwarded Message Sent|[!INCLUDE[ssSB](../../includes/sssb-md.md)]가 메시지를 전달하면 발생합니다.|  
|140|Broker:Forwarded Message Dropped|[!INCLUDE[ssSB](../../includes/sssb-md.md)]가 전달될 메시지를 삭제하면 발생합니다.|  
|141|Broker:Message Classify|[!INCLUDE[ssSB](../../includes/sssb-md.md)]가 메시지 라우팅을 지정하면 발생합니다.|  
|142|Broker:Transmission|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 전송 계층에서 오류가 발생했음을 나타냅니다. 오류 번호 및 상태 값이 오류의 원본을 나타냅니다.|  
|143|Broker:Queue Disabled|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 큐에서 다섯 번의 트랜잭션 롤백이 연속적으로 발생하여 포이즌 메시지가 감지되었음을 나타냅니다. 이벤트에 포이즌 메시지를 포함하는 큐의 큐 ID 및 데이터베이스 ID가 들어 있습니다.|  
|144-145|Reserved||  
|146|Showplan XML Statistics Profile|SQL 문을 실행하면 발생합니다. 실행 계획 연산자를 식별하고 컴파일 시간 데이터를 모두 표시합니다. 이 이벤트의 **이진** 열에는 인코딩된 실행 계획이 포함 됩니다. SQL Server 프로파일러를 사용하여 추적을 열고 실행 계획을 확인할 수 있습니다.|  
|148|Deadlock Graph|잠금 획득 시도가 교착 상태의 일부이고 교착 상태가 발생하여 해당 시도가 취소되면 발생합니다. 교착 상태에 대한 XML 설명을 제공합니다.|  
|149|Broker:Remote Message Acknowledgement|[!INCLUDE[ssSB](../../includes/sssb-md.md)]가 메시지 승인을 보내거나 받으면 발생합니다.|  
|150|Trace File Close|추적 파일 롤오버 중에 추적 파일이 닫히면 발생합니다.|  
|151|Reserved||  
|152|Audit Change Database Owner|ALTER AUTHORIZATION을 사용하여 데이터베이스의 소유자를 변경하고 이 작업을 수행하도록 사용 권한을 선택하면 발생합니다.|  
|153|Audit Schema Object Take Ownership Event|ALTER AUTHORIZATION을 사용하여 개체에 소유자를 할당하고 이 작업을 수행하도록 사용 권한을 선택하면 발생합니다.|  
|154|Reserved||  
|155|FT:Crawl Started|전체 텍스트 탐색(채우기)이 시작되면 발생합니다. 작업자 태스크로 탐색 요청이 선택되는지를 확인하는 데 사용합니다.|  
|156|FT:Crawl Stopped|전체 텍스트 탐색(채우기)이 중지되면 발생합니다. 탐색이 성공적으로 완료되거나 오류가 발생하는 경우에 중지됩니다.|  
|157|FT:Crawl Aborted|전체 텍스트 탐색 중에 예외가 생성되면 발생합니다. 일반적으로 전체 텍스트 탐색이 중지되도록 합니다.|  
|158|Audit Broker Conversation|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 대화 보안과 연관된 감사 메시지를 보고합니다.|  
|159|Audit Broker Login|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 전송 보안과 연관된 감사 메시지를 보고합니다.|  
|160|Broker:Message Undeliverable|[!INCLUDE[ssSB](../../includes/sssb-md.md)]가 받은 메시지를 유지할 수 없으면 발생합니다. 이 메시지는 서비스로 배달되어야 합니다.|  
|161|Broker:Corrupted Message|[!INCLUDE[ssSB](../../includes/sssb-md.md)]가 손상된 메시지를 받으면 발생합니다.|  
|162|User Error Message|오류 또는 예외가 발생하는 경우 사용자가 확인할 수 있는 오류 메시지를 표시합니다.|  
|163|Broker:Activation|큐 모니터가 활성화 저장 프로시저를 시작하고 QUEUE_ACTIVATION 알림을 보내거나 큐 모니터에서 시작한 활성화 저장 프로시저가 종료되면 발생합니다.|  
|164|Object:Altered|데이터베이스 개체가 변경되면 발생합니다.|  
|165|Performance statistics|컴파일된 쿼리 계획이 처음으로 캐시되었거나, 다시 컴파일되었거나, 계획 캐시에서 제거되면 발생합니다.|  
|166|SQL:StmtRecompile|문 수준 다시 컴파일이 수행되면 발생합니다.|  
|167|Database Mirroring State Change|미러된 데이터베이스의 상태가 변경되면 발생합니다.|  
|168|Showplan XML For Query Compile|SQL 문이 컴파일되면 발생합니다. 컴파일 시간 데이터를 모두 표시합니다. 이 이벤트의 **이진** 열에는 인코딩된 실행 계획이 포함 됩니다. SQL Server 프로파일러를 사용하여 추적을 열고 실행 계획을 확인할 수 있습니다.|  
|169|Showplan All For Query Compile|SQL 문이 컴파일되면 발생합니다. 컴파일 시간 데이터를 모두 표시합니다. 실행 계획 연산자를 식별하려면 사용합니다.|  
|170|Audit Server Scope GDR Event|로그인을 만드는 경우처럼 서버 범위에 있는 사용 권한에 대한 허용, 거부 또는 취소 이벤트가 발생되었음을 나타냅니다.|  
|171|Audit Server Object GDR Event|테이블 또는 함수 같은 스키마 개체에 대한 허용, 거부 또는 취소 이벤트가 발생했음을 나타냅니다.|  
|172|Audit Database Object GDR Event|어셈블리 및 스키마 같은 데이터베이스 개체에 대한 허용, 거부 또는 취소 이벤트가 발생했음을 나타냅니다.|  
|173|Audit Server Operation Event|설정, 리소스, 외부 액세스 또는 권한 부여 변경 등의 보안 감사 작업이 사용되면 발생합니다.|  
|175|Audit Server Alter Trace Event|문에서 ALTER TRACE 권한을 확인하면 발생합니다.|  
|176|Audit Server Object Management Event|서버 개체를 생성, 변경 또는 삭제하면 발생합니다.|  
|177|Audit Server Principal Management Event|서버 보안 주체를 생성, 변경 또는 삭제하면 발생합니다.|  
|178|Audit Database Operation Event|쿼리 알림 구독 또는 검사점 설정 같은 데이터베이스 작업이 수행되면 발생합니다.|  
|180|Audit Database Object Access Event|스키마 같은 데이터베이스 개체에 액세스하면 발생합니다.|  
|181|TM: Begin Tran starting|BEGIN TRANSACTION 요청이 시작되면 발생합니다.|  
|182|TM: Begin Tran completed|BEGIN TRANSACTION 요청이 완료되면 발생합니다.|  
|183|TM: Promote Tran starting|PROMOTE TRANSACTION 요청이 시작되면 발생합니다.|  
|184|TM: Promote Tran completed|PROMOTE TRANSACTION 요청이 완료되면 발생합니다.|  
|185|TM: Commit Tran starting|COMMIT TRANSACTION 요청이 시작되면 발생합니다.|  
|186|TM: Commit Tran completed|COMMIT TRANSACTION 요청이 완료되면 발생합니다.|  
|187|TM: Rollback Tran starting|ROLLBACK TRANSACTION 요청이 시작되면 발생합니다.|  
|188|TM: Rollback Tran completed|ROLLBACK TRANSACTION 요청이 완료되면 발생합니다.|  
|189|Lock: Timeout (timeout > 0)|페이지 같은 리소스에 대한 잠금 요청 시간이 초과되면 발생합니다.|  
|190|Progress Report: Online Index Operation|빌드 프로세스가 실행되는 동안 온라인 인덱스 작성 작업의 진행률을 보고합니다.|  
|191|TM: Save Tran starting|SAVE TRANSACTION 요청이 시작되면 발생합니다.|  
|192|TM: Save Tran completed|SAVE TRANSACTION 요청이 완료되면 발생합니다.|  
|193|Background Job Error|백그라운드 작업이 비정상적으로 종료되면 발생합니다.|  
|194|OLEDB Provider Information|분산 쿼리가 실행되어 공급자 연결에 해당하는 정보를 수집하면 발생합니다.|  
|195|Mount Tape|테이프 탑재 요청을 받으면 발생합니다.|  
|196|Assembly Load|CLR 어셈블리 로드 요청이 수행되면 발생합니다.|  
|197|Reserved||  
|198|XQuery Static Type|XQuery 식이 실행되면 발생합니다. 이 이벤트 클래스는 XQuery 식의 정적 유형을 제공합니다.|  
|199|QN: subscription|쿼리 등록을 구독할 수 없으면 발생합니다. **TextData** 열에는 이벤트에 대 한 정보가 포함 되어 있습니다.|  
|200|QN: parameter table|활성 구독에 대한 정보가 내부 매개 변수 테이블에 저장됩니다. 이 이벤트 클래스는 매개 변수 테이블을 만들거나 삭제하면 발생합니다. 일반적으로 이러한 테이블은 데이터베이스를 다시 시작할 때 생성되거나 삭제됩니다. **TextData** 열에는 이벤트에 대 한 정보가 포함 되어 있습니다.|  
|201|QN: template|쿼리 템플릿은 구독 쿼리의 클래스를 나타냅니다. 일반적으로 매개 변수 값을 제외하면 같은 클래스의 쿼리는 동일합니다. 이 이벤트 클래스는 새로운 구독 요청이 기존 클래스(Match), 새 클래스(Create), 활성 구독이 없는 쿼리 클래스에 대한 템플릿 정리를 나타내는 Drop 클래스에 있으면 발생합니다. **TextData** 열에는 이벤트에 대 한 정보가 포함 되어 있습니다.|  
|202|QN: dynamics|쿼리 알림의 내부 동작을 추적합니다. **TextData** 열에는 이벤트에 대 한 정보가 포함 되어 있습니다.|  
|212|Bitmap Warning|쿼리에서 비트맵 필터를 사용하지 않도록 설정한 시간을 나타냅니다.|  
|213|Database Suspect Data Page|**Msdb**의 **suspect_pages** 테이블에 페이지가 추가 되었음을 나타냅니다.|  
|214|CPU threshold exceeded|리소스 관리자가 CPU 임계값(REQUEST_MAX_CPU_TIME_SEC)을 초과하는 쿼리를 감지하는 시간을 나타냅니다.|  
|215|PreConnect:Starting|LOGON 트리거나 리소스 관리자 분류자 함수가 실행을 시작하는 시간을 나타냅니다.|  
|216|PreConnect:Completed|LOGON 트리거나 리소스 관리자 분류자 함수가 실행을 완료하는 시간을 나타냅니다.|  
|217|Plan Guide Successful|SQL Server에서 계획 지침이 포함된 쿼리 또는 일괄 처리에 대한 실행 계획을 성공적으로 생성했음을 나타냅니다.|  
|218|Plan Guide Unsuccessful|SQL Server에서 계획 지침이 포함된 쿼리 또는 일괄 처리에 대한 실행 계획을 생성하지 못했음을 나타냅니다. SQL Server에서 계획 지침을 적용하지 않고 이 쿼리 또는 일괄 처리의 실행 계획을 생성하려고 했습니다. 이러한 문제는 계획 지침이 잘못되어 발생할 수 있습니다. sys.fn_validate_plan_guide 시스템 함수를 사용하여 계획 지침의 유효성을 검사할 수 있습니다.|  
|235|Audit Fulltext||  
  
`[ @columnid = ] column_id`이벤트에 대해 추가할 열의 ID입니다. *column_id* 는 **int**이며 기본값은 없습니다.  
  
 다음 표에서는 이벤트에 추가될 수 있는 열을 나열합니다.  
  
|열 번호|열 이름|Description|  
|-------------------|-----------------|-----------------|  
|1|**TextData**|추적에서 캡처한 이벤트 클래스에 의존하는 텍스트 값입니다.|  
|2|**BinaryData**|추적에서 캡처된 이벤트 클래스에 의존하는 이진 값입니다.|  
|3|**DatabaseID**|USE *database* 문으로 지정한 데이터베이스 ID 이거나 지정 된 연결에 대해 use *database* 문을 실행 하지 않은 경우 기본 데이터베이스입니다.<br /><br /> 데이터베이스의 값은 DB_ID 함수로 확인할 수 있습니다.|  
|4|**TransactionID**|시스템이 할당한 트랜잭션의 ID입니다.|  
|5|**LineNumber**|오류를 포함하는 줄 번호를 나타냅니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] SP:StmtStarting **과 같은**문을 호출하는 이벤트의 경우 **LineNumber** 에 저장 프로시저 또는 일괄 처리에 있는 문의 줄 번호가 포함됩니다.|  
|6|**NTUserName**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자 이름입니다.|  
|7|**NTDomainName**|사용자가 속한 Windows 도메인입니다.|  
|8|**HostName**|요청을 처음에 시작한 클라이언트 컴퓨터의 이름입니다.|  
|9|**ClientProcessID**|클라이언트 애플리케이션이 실행 중인 프로세스에 클라이언트 컴퓨터가 할당한 ID입니다.|  
|10|**ApplicationName**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|  
|11|**LoginName**|클라이언트의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 이름입니다.|  
|12|**SPID**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|  
|13|**기간**|이벤트에 의해 사용된 경과 시간(마이크로초)입니다. 이 데이터 열은 Hash Warning 이벤트로 채워지지 않습니다.|  
|14|**StartTime**|사용 가능한 경우 이벤트가 시작된 시간입니다.|  
|15|**EndTime**|이벤트가 종료된 시간입니다. 이 열은 **SQL:BatchStarting** 또는 **SP:Starting**과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 또한 **해시 경고** 이벤트로 채워지지 않습니다.|  
|16|**나타납니다**|이벤트 대신 서버에서 수행한 논리적 디스크 읽기 수입니다. 이 열은 **Lock: Released** 이벤트로 채워지지 않습니다.|  
|17|**쓰므로**|이벤트 대신 서버에서 수행한 물리적 디스크 쓰기 수입니다.|  
|18|**CPU**|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|19|**권한**|보안 감사에 의해 사용된 사용 권한의 비트맵을 나타냅니다.|  
|20|**심각도**|예외적인 심각도입니다.|  
|21|**EventSubClass**|이벤트 하위 클래스의 유형입니다. 이 데이터 열은 모든 이벤트 클래스에 대해 채워지지는 않습니다.|  
|22|**ObjectID**|시스템이 할당한 개체의 ID입니다.|  
|23|**Success**|감사에 사용한 권한 사용 시도의 성공입니다.<br /><br /> **1** = 성공**0** = 실패|  
|24|**IndexID**|이벤트에 의해 영향 받는 개체의 인덱스 ID입니다. 개체의 인덱스 ID를 확인하려면 **sysindexes** 시스템 테이블의 **indid** 열을 사용하십시오.|  
|25|**IntegerData**|추적에서 캡처된 이벤트 클래스에 의존하는 정수 값입니다.|  
|26|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]추적 되 고 있는 인스턴스의 이름 ( *servername* 또는 *servername\instancename*)입니다.|  
|27|**EventClass**|기록되고 있는 이벤트 클래스의 유형입니다.|  
|28|**ObjectType**|개체 유형(테이블, 함수 또는 저장 프로시저 등)|  
|29|**NestLevel**|이 저장 프로시저가 실행하고 있는 중첩 수준입니다. [@ @NESTLEVEL &#40;transact-sql&#41;](../../t-sql/functions/nestlevel-transact-sql.md)을 참조 하세요.|  
|30|**State**|오류 발생 시의 서버 상태입니다.|  
|31|**오류**|오류 번호입니다.|  
|32|**모드**|획득된 잠금의 잠금 모드입니다. 이 열은 **Lock: Released** 이벤트로 채워지지 않습니다.|  
|33|**Handle**|이벤트에 참조된 개체의 핸들입니다.|  
|34|**ObjectName**|액세스된 개체의 이름입니다.|  
|35|**DatabaseName**|USE *database* 문에 지정 된 데이터베이스의 이름입니다.|  
|36|**FileName**|수정된 파일 이름의 논리적 이름입니다.|  
|37|**OwnerName**|참조된 개체의 소유자 이름입니다.|  
|38|**RoleName**|문의 대상이 되는 데이터베이스 또는 서버 차원 역할의 이름입니다.|  
|39|**TargetUserName**|일부 동작 대상의 사용자 이름입니다.|  
|40|**DBUserName**|클라이언트의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 사용자 이름입니다.|  
|41|**LoginSid**|로그인한 사용자의 SID(보안 ID)입니다.|  
|42|**TargetLoginName**|일부 동작 대상의 로그인 이름입니다.|  
|43|**TargetLoginSid**|일부 동작 대상의 로그인 SID입니다.|  
|44|**ColumnPermissions**|보안 감사에 사용된 열 수준 사용 권한 상태입니다.|  
|45|**LinkedServerName**|연결된 서버의 이름입니다.|  
|46|**ProviderName**|OLE DB Provider의 이름입니다.|  
|47|**MethodName**|OLE DB 메서드의 이름입니다.|  
|48|**RowCounts**|일괄 처리의 행 수입니다.|  
|49|**요청**|문을 포함하는 요청의 ID입니다.|  
|50|**XactSequence**|현재 트랜잭션을 설명하는 토큰입니다.|  
|51|**EventSequence**|이 이벤트의 시퀀스 번호입니다.|  
|52|**BigintData1**|**bigint** 값-추적에서 캡처된 이벤트 클래스에 따라 달라 집니다.|  
|53|**BigintData2**|**bigint** 값-추적에서 캡처된 이벤트 클래스에 따라 달라 집니다.|  
|54|**GUID**|추적에서 캡처된 이벤트 클래스에 따라 달라지는 GUID 값입니다.|  
|55|**IntegerData2**|추적에서 캡처된 이벤트 클래스에 따라 달라지는 정수 값입니다.|  
|56|**ObjectID2**|관련 개체 또는 엔터티의 ID입니다(사용 가능한 경우).|  
|57|**Type**|추적에서 캡처된 이벤트 클래스에 따라 달라지는 정수 값입니다.|  
|58|**OwnerID**|잠금을 소유하는 개체의 유형입니다. 잠금 이벤트 전용입니다.|  
|59|**ParentName**|개체가 포함된 스키마의 이름입니다.|  
|60|**IsSystem**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다.<br /><br /> **1** = 시스템<br /><br /> **0** = 사용자|  
|61|**이동**|저장 프로시저나 일괄 처리 내에 있는 문의 시작 오프셋입니다.|  
|62|**SourceDatabaseID**|개체의 원본이 있는 데이터베이스의 ID입니다.|  
|63|**Sqlhandle 대해**|임시 쿼리 또는 데이터베이스의 텍스트 및 SQL 개체의 개체 ID를 기반으로 하는 64비트 해시입니다. 이 값을 **sys. dm_exec_sql_text ()** 에 전달 하 여 연결 된 sql 텍스트를 검색할 수 있습니다.|  
|64|**SessionLoginName**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Login1 **을 사용하여** 에 연결하고 **Login2**로 문을 실행하는 경우 **SessionLoginName** 은 **Login1**을 표시하고 **LoginName** 은 **Login2**를 표시합니다. 이 데이터 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|  
  
 **[ @on =]** *on*  
 이벤트를 ON(1)으로 설정할지, 아니면 OFF(0)로 설정할지를 지정합니다. *on* 은 **bit**이며 기본값은 없습니다.  
  
 *On* 이 **1**로 설정 되 고 *COLUMN_ID* NULL 이면 이벤트는 on으로 설정 되 고 모든 열은 지워집니다. *Column_id* 가 null이 아니면 해당 이벤트에 대해 열이 ON으로 설정 됩니다.  
  
 *On* 이 **0**으로 설정 되 고 *column_id* NULL 이면 이벤트가 해제 되 고 모든 열이 지워집니다. *Column_id* 가 null이 아닌 경우에는 해당 열이 해제 됩니다.  
  
 다음 표에서는 및 ** \@ columnid**간의 ** \@ 상호 작용을 보여** 줍니다.  
  
|@on|@columnid|결과|  
|---------|---------------|------------|  
|ON(**1**)|NULL|이벤트를 ON으로 설정합니다.<br /><br /> 모든 열은 지워집니다.|  
||NOT NULL|지정한 이벤트에 대한 열을 ON으로 설정합니다.|  
|OFF(**0**)|NULL|이벤트를 OFF로 설정합니다.<br /><br /> 모든 열은 지워집니다.|  
||NOT NULL|지정한 이벤트에 대한 열을 OFF로 설정합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 아래 표에서는 저장 프로시저가 완료된 후 사용자가 얻을 수 있는 코드 값을 설명합니다.  
  
|반환 코드|설명|  
|-----------------|-----------------|  
|0|오류가 없습니다.|  
|1|알 수 없는 오류입니다.|  
|2|추적이 현재 실행 중입니다. 지금 추적을 변경하면 오류가 발생합니다.|  
|3|지정한 이벤트가 유효하지 않습니다. 이벤트가 존재하지 않거나 저장 프로시저에 적합하지 않습니다.|  
|4|지정한 열이 유효하지 않습니다.|  
|9|지정한 추적 핸들이 유효하지 않습니다.|  
|11|지정한 열이 내부적으로 사용되므로 제거할 수 없습니다.|  
|13|메모리가 부족합니다. 지정한 동작을 수행할 메모리가 충분하지 않으면 반환됩니다.|  
|16|함수가 이 추적에 유효하지 않습니다.|  
  
## <a name="remarks"></a>설명  
 **sp_trace_setevent** 는 이전 버전의에서 사용할 수 있는 확장 저장 프로시저에 의해 이전에 실행 된 많은 동작을 수행 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 다음 대신 **sp_trace_setevent** 를 사용 합니다.  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_eventclassrequired**  
  
-   **xp_trace_seteventclassrequired**  
  
 사용자는 각 이벤트에 대해 추가 된 각 열에 대해 **sp_trace_setevent** 를 실행 해야 합니다. 각 실행 중 ** \@ 에 on** 이 **1**로 설정 된 경우 **sp_trace_setevent** 는 지정 된 이벤트를 추적 이벤트 목록에 추가 합니다. ** \@ On** 이 **0**으로 설정 된 경우 **sp_trace_setevent** 는 목록에서 지정 된 이벤트를 제거 합니다.  
  
 모든 SQL 추적 저장 프로시저 (**sp_trace_xx**)의 매개 변수는 엄격 하 게 형식화 됩니다. 이러한 매개 변수가 정확한 입력 매개 변수 데이터 형식으로 호출되지 않으면 인수 설명에서 지정한 대로 저장 프로시저는 오류를 반환합니다.  
  
 추적 저장 프로시저 사용에 대한 예는 [추적 만들기&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 ALTER TRACE 권한이 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [fn_trace_geteventinfo &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [fn_trace_getinfo &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [Transact-sql&#41;sp_trace_generateevent &#40;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [SQL Server 이벤트 클래스 참조](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [SQL 추적](../../relational-databases/sql-trace/sql-trace.md)  
  
  
