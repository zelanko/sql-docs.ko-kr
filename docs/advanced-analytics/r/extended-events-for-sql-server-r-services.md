---
title: SQL Server 컴퓨터 학습 서비스에 대 한 확장 이벤트 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 43fbd32cf1bead610e4cdae9b59983fe5ad1b15e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202685"
---
# <a name="extended-events-for-sql-server-machine-learning-services"></a>SQL Server 컴퓨터 학습 서비스에 대 한 확장된 이벤트
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 문제 해결 관련 된 작업에 사용할 확장된 이벤트를 집합이 제공 된 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], Python 또는 R 작업에 전송 하는 것은 물론 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스

## <a name="sql-server-events-for-machine-learning"></a>기계 학습에 대 한 SQL Server 이벤트

SQL Server 관련 이벤트 목록을 보려면, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 다음 쿼리를 실행합니다.

```SQL
SELECT o.name AS event_name, o.description
FROM sys.dm_xe_objects o
JOIN sys.dm_xe_packages p
ON o.package_guid = p.guid
WHERE o.object_type = 'event'
AND p.name = 'SQLSatellite';
```

확장된 이벤트 사용에 대 한 일반 정보를 참조 하십시오. [확장 이벤트 도구](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)합니다.

> [!TIP]
> SQL Server에서 생성 하는 확장된 이벤트에 대 한 새 시도 [SSMS의 XEvent 프로파일러](https://docs.microsoft.com/sql/relational-databases/extended-events/use-the-ssms-xe-profiler)합니다. Management Studio의이 새로운 기능, 확장된 이벤트에 대 한 라이브 뷰어를 표시 및 유사한 프로파일러 추적을 보다 SQL Server 개입 수준이 낮습니다.

## <a name="additional-events-specific-to-machine-learning-components"></a>특정 컴퓨터 학습 구성 요소에 추가 이벤트

와 관련 된 및와 같은 SQL Server 컴퓨터 학습 서비스에서 사용 되는 구성 요소에 대해 사용할 수 있는 추가 확장된 이벤트는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], bxlserver, R 런타임을 시작 하는 위성 프로세스입니다. 이러한 추가적인 확장 이벤트는 외부 프로세스에서 발생 하 고 따라서 캡처되어야 외부 유틸리티를 사용 하 합니다.

이 작업을 수행 하는 방법에 대 한 자세한 내용은 섹션을 참조 [외부 프로세스에서 이벤트 수집](#bkmk_externalevents)합니다.

##  <a name="bkmk_xeventtable"></a> 확장된 이벤트 테이블

|이벤트|Description|참고|  
|-----------|-----------------|---------|  
|connection_accept|새 연결이 허용될 때 발생합니다. 이 이벤트는 모든 연결 시도를 기록합니다.||  
|failed_launching|시작하지 못했습니다.|오류를 나타냅니다.|  
|satellite_abort_connection|연결 기록을 중단합니다.||  
|satellite_abort_received|위성 연결을 통해 중단 메시지를 수신하는 경우 실행됩니다.||  
|satellite_abort_sent|위성 연결을 통해 중단 메시지가 전송되는 경우 실행됩니다.||  
|satellite_authentication_completion|TCP 또는 Namedpipe를 통해 연결 인증이 완료되면 실행됩니다.||  
|satellite_authorization_completion|TCP 또는 Namedpipe를 통해 연결 권한 부여가 완료되면 실행됩니다.||  
|satellite_cleanup|위성 호출을 정리할 때 실행됩니다.|외부 프로세스를 통해서만 실행됩니다. 외부 프로세스 이벤트 수집에 대한 지침을 참조하십시오.|  
|satellite_data_chunk_sent|위성 연결이 단일 데이터 청크 보내기를 마칠 때 실행됩니다.|이 이벤트는 전송된 행 수, 열 수, 사용된 SNI 패킷 수, 청크를 전송하는 동안 경과된 시간(밀리초)을 보고합니다. 이 정보는 각 유형의 데이터를 전달하는 데 소비된 시간 및 사용된 패킷 수를 파악하는 데 도움이 됩니다.|  
|satellite_data_receive_completion|위성 연결을 통해 쿼리에 필요한 모든 데이터를 수신한 경우에 실행됩니다.|외부 프로세스를 통해서만 실행됩니다. 외부 프로세스 이벤트 수집에 대한 지침을 참조하십시오.|  
|satellite_data_send_completion|위성 연결을 통해 세션에 필요한 모든 데이터를 보낸 경우에 실행됩니다.||  
|satellite_data_send_start|데이터 전송을 시작 될 때 발생 합니다.| 데이터 전송에 첫 번째 데이터 청크를 보내기 전에 바로 시작 됩니다.|  
|satellite_error|SQL 위성 오류를 추적하는 데 사용됩니다.||  
|satellite_invalid_sized_message|메시지의 크기가 유효하지 않습니다.||  
|satellite_message_coalesced|네트워킹 계층의 메시지 결합을 추적하는 데 사용됩니다.||  
|satellite_message_ring_buffer_record|메시지 링 버퍼 레코드||  
|satellite_message_summary|메시징에 대한 요약 정보||  
|satellite_message_version_mismatch|메시지 버전 필드가 일치하지 않습니다.||  
|satellite_messaging|메시징 이벤트(바인딩, 언바인딩 등)을 추적하는 데 사용됩니다.||  
|satellite_partial_message|네트워킹 계층의 부분적인 메시지를 추적하는 데 사용됩니다.||  
|satellite_schema_received|SQL에서 스키마 메시지를 수신하고 읽었을 때 실행됩니다.||  
|satellite_schema_sent|위성에서 스키마 메시지를 보냈을 때 실행됩니다.|외부 프로세스를 통해서만 실행됩니다. 외부 프로세스 이벤트 수집에 대한 지침을 참조하십시오.|  
|satellite_service_start_posted|서비스 시작 메시지가 실행 패드에 게시되면 실행됩니다.|실행 패드가 외부 프로세스를 시작하도록 알려주며 새 세션의 ID를 포함합니다.|  
|satellite_unexpected_message_received|예상치 않은 메시지를 수신하면 실행됩니다.|오류를 나타냅니다.|  
|stack_trace|프로세스의 메모리 덤프가 요청될 때 발생합니다.|오류를 나타냅니다.|  
|trace_event|추적 목적으로 사용됩니다.|이 이벤트는 SQL Server, 실행 패드, 외부 프로세스 추적 메시지를 포함할 수 있습니다. 여기에는 R의 stdout 및 stderr에 대한 출력이 포함됩니다.|  
|launchpad_launch_start|실행 패드가 위성 실행을 시작하면 실행됩니다.|실행 패드에서만 실행됩니다. launchpad.exe 이벤트 수집에 대한 지침을 참조하십시오.|  
|launchpad_resume_sent|실행 패드가 위성을 실행하고 SQL Server에 재개 메시지를 보내면 실행됩니다.|실행 패드에서만 실행됩니다. launchpad.exe 이벤트 수집에 대한 지침을 참조하십시오.|  
|satellite_data_chunk_sent|위성 연결이 단일 데이터 청크 보내기를 마칠 때 실행됩니다.|열의 수, 행의 수, 패킷 수, 청크를 보내면서 경과한 시간에 대한 정보를 포함합니다.|  
|satellite_sessionId_mismatch|메시지의 세션 ID가 예상한 것과 다릅니다.||  
  
###  <a name="bkmk_externalevents"></a> 외부 프로세스에서 이벤트 수집

SQL Server 컴퓨터 학습 서비스는 SQL Server 프로세스 외부에서 실행 되는 일부 서비스를 시작 합니다. 외부 프로세스와 관련 된 이벤트를 캡처하려면 이벤트 추적 구성 파일을 만들고 프로세스의 실행 파일과 동일한 디렉터리에 파일을 배치 합니다.  
  
+ **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
    실행 패드 관련 이벤트를 캡처하려면, SQL Server 인스턴스의 Binn 디렉터리에 *.config* 파일을 배치합니다.  기본 설치에서이 합니다.

    `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`을 참조하세요.  
  
+ **BXLServer** 는 Python 또는 R 등의 외부 스크립트 언어로 SQL 확장성을 지 원하는 위성 프로세스입니다. 외부 언어 인스턴스마다 BxlServer의 개별 인스턴스가 시작 됩니다.
  
    BXLServer 관련 이벤트를 캡처하려면, 배치는 *.config* Python 또는 R 설치 디렉터리에 파일입니다.  기본 설치에서이 합니다.
     
    **R:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`합니다.  

    **Python:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\PYTHON_SERVICES\library\RevoScaleR\rxLibs\x64`합니다.

구성 파일은 “[name].xevents.xml” 형식을 사용하여 실행 파일과 같은 이름을 지정해야 합니다. 즉, 파일 이름을 다음과 같이 지정해야 합니다.

+ `Launchpad.xevents.xml`
+ `bxlserver.xevents.xml`

구성 파일 자체의 형식은 다음과 같습니다.

```xml
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="[session name]" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="you">Xevent for launchpad or bxl server.</description>  
    <event package="SQLSatellite" name="[XEvent Name 1]" />  
    <event package="SQLSatellite" name="[XEvent Name 2]" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="[SessionName].xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ 추적을 구성 하려면 편집는 *세션 이름* 자리 표시자, 파일 이름에 대 한 자리 표시자 (`[SessionName].xel`), 이벤트를 캡처하려면, 예를 들어의 이름과 `[XEvent Name 1]`, `[XEvent Name 1]`).  
+ 이벤트 패키지 태그 개수에 관계 없이 지정할 수 있으며 name 특성이으로 수집 됩니다.

### <a name="example-capturing-launchpad-events"></a>예: 실행 패드 이벤트 캡처

다음 예제에서는 실행 패드 서비스에 대 한 이벤트 추적의 정의 보여 줍니다.

```xml
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="launchpad_launch_start" />  
    <event package="SQLSatellite" name="launchpad_resume_sent" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="launchpad_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ SQL Server 인스턴스의 Binn 디렉터리에 *.config* 파일을 배치합니다.
+ 이 파일 이름을 지정 해야 `Launchpad.xevents.xml`합니다.

### <a name="example-capturing-bxlserver-events"></a>예: BXLServer 이벤트 캡처  

다음 예는 BXLServer 실행 파일 이벤트 추적에 대한 정의를 보여줍니다.
  
```xml
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
 <event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="satellite_abort_received" />  
    <event package="SQLSatellite" name="satellite_authentication_completion" />  
    <event package="SQLSatellite" name="satellite_cleanup" />  
    <event package="SQLSatellite" name="satellite_data_receive_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_start" />  
    <event package="SQLSatellite" name="satellite_schema_sent" />   
    <event package="SQLSatellite" name="satellite_unexpected_message_received" />    
    <event package="SQLSatellite" name="satellite_data_chunk_sent" />   
    <target package="package0" name="event_file">  
      <parameter name="filename" value="satellite_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ BXLServer 실행 파일과 같은 디렉터리에 *.config* 파일을 배치합니다.
+ 이 파일 이름을 지정 해야 `bxlserver.xevents.xml`합니다.

## <a name="see-also"></a>참고 항목

[컴퓨터 학습 서비스에 대 한 사용자 지정 관리 Studio 보고서](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)
