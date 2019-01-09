---
title: SQL 추적 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 83c6d1d9-19ce-43fe-be9a-45aaa31f20cb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a1dd2e117207f3737f54e2cd0269c51918a199f2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52823487"
---
# <a name="sql-trace"></a>SQL 추적
  SQL 추적에서는 이벤트가 추적 정의에 나열된 이벤트 클래스의 인스턴스인 경우 수집됩니다. 이러한 이벤트는 추적 외부로 필터링하고 대상에 대해 쿼리할 수 있습니다. 대상은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 관리하는 애플리케이션의 추적 정보를 사용할 수 있는 파일 또는 SMO( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]관리 개체)일 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 확장 이벤트를 대신 사용하세요.  
  
## <a name="benefits-of-sql-trace"></a>SQL 추적의 이점  
 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 인스턴스에 대한 추적을 만들 수 있는 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]시스템 저장 프로시저를 제공합니다. 이 시스템 저장 프로시저를 사용자의 애플리케이션에서 사용하면 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]를 사용하지 않고 추적을 수동으로 만들 수 있습니다. 따라서 각 사용자 조직의 필요에 따라 사용자 지정 애플리케이션을 쓸 수 있습니다.  
  
## <a name="sql-trace-architecture"></a>SQL 추적 아키텍처  
 이벤트 원본은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 일괄 처리 같은 추적 이벤트나 교착 상태 같은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이벤트를 생성하는 원본일 수 있습니다. 이벤트에 대한 자세한 내용은 [SQL Server Event Class Reference](../event-classes/sql-server-event-class-reference.md)를 참조하십시오. 이벤트가 발생한 후 해당 이벤트 클래스가 추적 정의에 포함되면 이벤트 정보가 추적에 의해 수집됩니다. 추적 정의의 이벤트 클래스에 필터가 정의되어 있으면 해당 필터가 적용되고 추적 이벤트 정보가 큐에 전달됩니다. 이 큐로부터 추적 정보가 파일에 기록되거나 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]같은 애플리케이션에서 SMO에 의해 사용될 수 있습니다. 다음 다이어그램에서는 추적 중 SQL 추적에서 이벤트를 수집하는 방법을 보여 줍니다.  
  
 ![데이터베이스 엔진 이벤트 추적 프로세스](../../database-engine/media/tracarch.gif "Database Engine event tracing process")  
  
## <a name="sql-trace-terminology"></a>SQL 추적 용어  
 다음은 SQL 추적의 주요 개념을 설명하는 용어입니다.  
  
 **이벤트**  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]인스턴스 내에서 동작이 발생했음을 의미합니다.  
  
 **데이터 열**  
 이벤트의 특성입니다.  
  
 **이벤트 클래스**  
 추적할 수 있는 이벤트의 유형입니다. 이벤트 클래스는 이벤트에서 보고할 수 있는 모든 데이터 열을 포함합니다.  
  
 **이벤트 범주**  
 관련된 이벤트 클래스들의 그룹입니다.  
  
 **추적** (명사)  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 반환한 이벤트 및 데이터의 모음입니다.  
  
 **추적** (동사)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스의 이벤트를 수집 및 모니터링하기 위한 동작입니다.  
  
 **Tracedefinition**  
 추적 중에 수집되는 이벤트의 유형을 식별하는 이벤트 클래스, 데이터 열 및 필터 모음입니다.  
  
 **Assert**  
 추적에서 수집되는 이벤트를 제한하는 조건입니다.  
  
 **추적 파일**  
 추적을 저장할 때 생성되는 파일입니다.  
  
 **템플릿**  
 추적에서 수집되는 이벤트 클래스 및 데이터 열을 정의하는 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]내의 파일입니다.  
  
 **추적 테이블**  
 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]에서 추적을 테이블에 저장할 때 생성되는 테이블입니다.  
  
## <a name="use-data-columns-to-describe-returned-events"></a>데이터 열을 사용하여 반환되는 이벤트 설명  
 SQL 추적은 추적 출력의 데이터 열을 통해 추적이 실행될 때 반환된 이벤트에 대한 정보를 제공합니다. 다음 표에서는 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 데이터 열에 대해 설명합니다. 이 데이터 열은 SQL 추적에서 사용하는 데이터 열과 동일하며 기본으로 선택된 열에 해당합니다.  
  
|데이터 열|열 번호|Description|  
|-----------------|-------------------|-----------------|  
|**ApplicationName** <sup>1</sup>|10|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|  
|**BigintData1**|52|추적에 지정된 이벤트 클래스에 따라 달라지는 값(`bigint` 데이터 형식)입니다.|  
|**BigintData2**|53|추적에 지정된 이벤트 클래스에 따라 달라지는 값(`bigint` 데이터 형식)입니다.|  
|**Binary Data**|2|추적에서 캡처된 이벤트 클래스에 따라 달라지는 이진 값입니다.|  
|**ClientProcessID** <sup>1</sup>|9|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|  
|**ColumnPermissions**|44|열 사용 권한이 설정되어 있는지 나타냅니다. 문 텍스트를 구문 분석하여 어떤 권한이 어떤 열에 적용되었는지 알 수 있습니다.|  
|**CPU**|18|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|**데이터베이스 ID** <sup>1</sup>|3|USE *database_name* 문으로 지정한 데이터베이스 ID이거나 지정한 인스턴스에 대해 실행된 USE *database_name*문이 없는 경우 기본 데이터베이스 ID입니다. [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|  
|**DatabaseName**|35|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|**DBUserName** <sup>1</sup>|40|클라이언트의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 사용자 이름입니다.|  
|**기간**|13|이벤트의 기간(마이크로초)입니다.<br /><br /> 서버는 이벤트 기간을 마이크로초(1초의 1/1000000, 즉 10<sup>-6</sup>) 단위로 보고하고 이벤트에 사용되는 CPU 시간량을 밀리초(1초의 1/1000, 즉 10<sup>-3</sup>) 단위로 보고합니다. [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 그래픽 사용자 인터페이스는 기본적으로 **Duration** 열을 밀리초 단위로 표시하지만 추적을 파일이나 데이터베이스 테이블에 저장하면 **Duration** 열 값이 마이크로초 단위로 기록됩니다.|  
|**EndTime**|15|이벤트가 종료된 시간입니다. 이 열은 **SQL:BatchStarting** 또는 **SP:Starting**등의 시작하는 이벤트를 참조하는 이벤트 클래스에 대해 채워지지 않습니다.|  
|**오류**|31|지정된 이벤트의 오류 번호입니다. 종종 **sysmessages**테이블에 저장된 오류 번호를 나타냅니다.|  
|**EventClass** <sup>1</sup>|27|캡처된 이벤트 클래스 유형입니다.|  
|**EventSequence**|51|이 이벤트의 시퀀스 번호입니다.|  
|**EventSubClass** <sup>1</sup>|21|각 이벤트 클래스에 대한 추가 정보를 제공하는 이벤트 하위 클래스 유형입니다. 예를 들어 **Execution Warning** 이벤트 클래스에 대한 이벤트 하위 클래스 값은 실행 경고 유형을 나타냅니다.<br /><br /> **1** = 쿼리 대기 쿼리는 실행하기 전에 리소스(예: 메모리)를 기다려야 합니다.<br /><br /> **2** = 쿼리 제한 시간 실행을 위해 리소스를 기다리는 동안 제한 시간을 초과한 쿼리입니다. 이 데이터 열은 모든 이벤트 클래스에 대해 채워지지는 않습니다.|  
|**GUID**|54|추적에 지정된 이벤트 클래스에 따라 달라지는 GUID 값입니다.|  
|**FileName**|36|수정한 파일의 논리적 이름입니다.|  
|**Handle**|33|ODBC, OLE DB, DB-Library가 서버와의 공동 실행을 위해 사용하는 정수입니다.|  
|**호스트 이름** <sup>1</sup>|8|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|  
|**IndexID**|24|이벤트에 의해 영향 받는 개체의 인덱스 ID입니다. 개체의 인덱스 ID를 확인하려면 **sysindexes** 시스템 테이블의 **indid** 열을 사용하십시오.|  
|**IntegerData**|25|추적에서 캡처된 이벤트 클래스에 따라 달라지는 정수 값입니다.|  
|**IntegerData2**|55|추적에서 캡처된 이벤트 클래스에 따라 달라지는 정수 값입니다.|  
|**IsSystem**|60|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다.<br /><br /> **1** = 시스템<br /><br /> **0** = 사용자|  
|**LineNumber**|5|오류를 포함하는 줄 번호를 나타냅니다. [!INCLUDE[tsql](../../../includes/tsql-md.md)] SP:StmtStarting **과 같은**문을 호출하는 이벤트의 경우 **LineNumber** 에 저장 프로시저 또는 일괄 처리에 있는 문의 줄 번호가 포함됩니다.|  
|**LinkedServerName**|45|연결된 서버의 이름입니다.|  
|**LoginName**|11|사용자 로그인 이름(DOMAIN\Username 형식의 Microsoft Windows 로그인 자격 증명 또는 SQL Server 보안 로그인)입니다|  
|**LoginSid** <sup>1</sup>|41|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **master** 데이터베이스의 **sys.server_principals** 뷰에 있습니다. 서버로의 각 로그인에는 고유 ID가 있습니다.|  
|**MethodName**|47|OLEDB 메서드 이름입니다.|  
|**모드**|32|여러 가지 이벤트에서 이벤트의 요청 또는 수신 상태를 설명할 때 사용하는 정수입니다.|  
|**NestLevel**|29|@@NESTLEVEL에서 반환한 데이터를 나타내는 정수입니다.|  
|**NTDomainName** <sup>1</sup>|7|사용자가 속한 Microsoft Windows 도메인입니다.|  
|**NTUserName** <sup>1</sup>|6|Windows 사용자 이름입니다.|  
|**Exchange Spill**|22|시스템이 할당한 개체의 ID입니다.|  
|**ObjectID2**|56|관련 개체 또는 엔터티의 ID입니다(사용 가능한 경우).|  
|**ObjectName**|34|참조되는 개체의 이름입니다.|  
|**ObjectType** <sup>2</sup>|28|이벤트와 관련된 개체 유형을 나타내는 값입니다, 이 값은 **sysobjects** 의 **유형**열과 일치합니다.|  
|**Offset**|61|저장 프로시저나 일괄 처리 내에 있는 문의 시작 오프셋입니다.|  
|**OwnerID**|58|잠금 이벤트 전용입니다. 잠금을 소유한 개체의 유형을 나타냅니다.|  
|**OwnerName**|37|개체 소유자의 데이터베이스 사용자 이름입니다.|  
|**ParentName**|59|개체가 속해 있는 스키마의 이름입니다.|  
|**사용 권한**|19|확인한 사용 권한의 유형을 나타내는 정수 값입니다. 값은 다음과 같습니다.<br /><br /> **1** = SELECT ALL<br /><br /> **2** = UPDATE ALL<br /><br /> **4** = REFERENCES ALL<br /><br /> **8** = INSERT<br /><br /> **16** = DELETE<br /><br /> **32** = EXECUTE(프로시저에만 해당)<br /><br /> **4096** = SELECT ANY(하나 이상의 열)<br /><br /> **8192** = UPDATE ANY<br /><br /> **16384** = REFERENCES ANY|  
|**ProviderName**|46|OLE DB 공급자 이름입니다.|  
|**Reads**|16|이벤트에 대해 서버에서 수행한 논리적 디스크 읽기 작업의 수입니다. 이 읽기 작업에는 해당 문 실행 중의 모든 테이블 및 버퍼 읽기가 포함됩니다.|  
|**RequestID**|49|문을 포함하는 요청의 ID입니다.|  
|**RoleName**|38|활성화된 애플리케이션 역할의 이름입니다.|  
|**RowCounts**|48|일괄 처리에 있는 행 수입니다.|  
|**ServerName** <sup>1</sup>|26|추적되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|  
|**SessionLoginName**|64|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 사용자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Login1 **을 사용하여** 에 연결하고 **Login2**로 문을 실행하는 경우 **SessionLoginName** 은 **Login1**을 표시하고 **LoginName** 은 **Login2**를 표시합니다. 이 데이터 열은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|  
|**Severity**|20|예외 이벤트의 심각도 수준입니다.|  
|**SourceDatabaseID**|62|개체 원본이 있는 데이터베이스의 ID입니다.|  
|**SPID**|12|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가 클라이언트와 연결된 프로세스에 할당한 SPID(서버 프로세스 ID)입니다.|  
|**SqlHandle**|63|임시 쿼리 또는 데이터베이스의 텍스트 및 SQL 개체의 개체 ID를 기반으로 하는 64비트 해시입니다. 이 값은 **sys.dm_exec_sql_text()** 에 전달되어 연관된 SQL 텍스트를 검색할 수 있습니다.|  
|**StartTime** <sup>1</sup>|14|이벤트가 시작된 시간입니다(사용 가능한 경우).|  
|**State**|30|오류 상태 코드입니다.|  
|**성공**|23|이벤트가 성공적이었는지를 나타냅니다. 다음과 같은 값이 올 수 있습니다.<br /><br /> **1** = 성공,<br /><br /> **0** = 실패.<br /><br /> 예를 들어 **1** 은 권한 확인에 성공했음을 의미하며 **0** 은 확인에 실패했음을 의미합니다.|  
|**TargetLoginName**|42|로그인을 대상으로 하는 동작(예: 새 로그인 추가)의 경우 대상 로그인의 이름입니다.|  
|**TargetLoginSid**|43|로그인을 대상으로 하는 동작(예: 새 로그인 추가)의 경우 대상 로그인의 SID입니다.|  
|**TargetUserName**|39|데이터베이스 사용자를 대상으로 하는 동작(예: 사용자에게 권한 부여)의 경우 해당 사용자의 이름입니다.|  
|**TextData**|1|추적에서 캡처된 이벤트 클래스에 따라 달라지는 텍스트 값입니다. 그렇지만 매개 변수가 있는 쿼리를 추적하면 변수는 **TextData** 열에 데이터 값으로 표시되지 않습니다.|  
|**Transaction ID**|4|시스템이 할당한 트랜잭션 ID입니다.|  
|**형식**|57|추적에서 캡처된 이벤트 클래스에 따라 달라지는 정수 값입니다.|  
|**Writes**|17|이벤트에 대해 서버에서 수행한 물리적 디스크 쓰기 작업의 수입니다.|  
|**XactSequence**|50|현재 트랜잭션을 설명하는 토큰입니다.|  
  
 <sup>1</sup> 이러한 데이터 열은 기본적으로 모든 이벤트에 대해 채워집니다.  
  
 <sup>2</sup> 에 대 한 자세한 내용은 합니다 **ObjectType** 데이터 열을 참조 하세요 [ObjectType 추적 이벤트 열](../event-classes/objecttype-trace-event-column.md)합니다.  
  
## <a name="sql-trace-tasks"></a>SQL 추적 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|TRANSACT-SQL 저장 프로시저를 사용하여 추적을 만들고 실행하는 방법을 설명합니다.|[Transact-SQL 저장 프로시저를 사용하여 추적 만들기 및 실행](../sql-trace/create-and-run-traces-using-transact-sql-stored-procedures.md)|  
|[!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]인스턴스에서 저장 프로시저를 사용하여 수동 추적을 만드는 방법을 설명합니다.|[저장 프로시저를 사용하여 수동 추적 만들기](../sql-trace/create-manual-traces-using-stored-procedures.md)|  
|추적 결과가 기록되는 파일에 추적 결과를 저장하는 방법을 설명합니다.|[파일에 추적 결과 저장](../sql-trace/save-trace-results-to-a-file.md)|  
|**temp** 디렉터리의 공간을 사용하여 추적 데이터에 대한 액세스를 개선하는 방법을 설명합니다.|[추적 데이터에 대한 액세스 향상](../sql-trace/improve-access-to-trace-data.md)|  
|저장 프로시저를 사용하여 추적을 만드는 방법을 설명합니다.|[추적 만들기&#40;Transact-SQL&#41;](../sql-trace/create-a-trace-transact-sql.md)|  
|저장 프로시저를 사용하여 추적 중인 이벤트에 필요한 정보만 검색하는 필터를 만드는 방법을 설명합니다.|[추적 필터 설정&#40;Transact-SQL&#41;](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)|  
|저장 프로시저를 사용하여 기존 추적을 수정하는 방법을 설명합니다.|[기존 추적 수정&#40;Transact-SQL&#41;](../sql-trace/modify-an-existing-trace-transact-sql.md)|  
|기본 제공 함수를 사용하여 저장된 추적을 보는 방법을 설명합니다.|[저장된 추적 보기&#40;Transact-SQL&#41;](../sql-trace/view-a-saved-trace-transact-sql.md)|  
|기본 제공 함수를 사용하여 추적 필터 정보를 보는 방법을 설명합니다.|[필터 정보 보기&#40;Transact-SQL&#41;](../sql-trace/view-filter-information-transact-sql.md)|  
|저장 프로시저를 사용하여 추적을 삭제하는 방법을 설명합니다.|[추적 삭제&#40;Transact-SQL&#41;](../sql-trace/delete-a-trace-transact-sql.md)|  
|추적에서 발생하는 성능 비용을 최소화하는 방법을 설명합니다.|[SQL 추적 최적화](../sql-trace/sql-trace.md)|  
|추적을 필터링하여 추적 중에 발생하는 오버헤드를 최소화하는 방법을 설명합니다.|[추적 필터링](../sql-trace/filter-a-trace.md)|  
|추적에서 수집하는 데이터의 양을 최소화하는 방법을 설명합니다.|[추적 파일 및 테이블 크기 제한](../sql-trace/limit-trace-file-and-table-sizes.md)|  
|Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 추적을 예약하는 두 가지 방법을 설명합니다.|[예약된 추적](../sql-trace/schedule-traces.md)|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Profiler 템플릿 및 권한](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SMO&#40;SQL Server 관리 개체&#41; 프로그래밍 가이드](../server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
