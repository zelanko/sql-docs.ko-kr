---
title: "SQL Server R Services의 확장 이벤트 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4e90e057-aacb-4adc-8da6-64861f4e87df
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 814dacf2dbc7f3be05ad163c8c7162acf53fe404
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="extended-events-for-sql-server-r-services"></a>SQL Server R Services의 확장 이벤트
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 은(는) [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 에 보내는 R 작업 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]관련 문제 해결 작업에 사용할 확장 이벤트를 제공합니다.  
  
 SQL Server 관련 이벤트 목록을 보려면, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 다음 쿼리를 실행합니다.  
  
```  
select o.name as event_name, o.description  
  from sys.dm_xe_objects o  
  join sys.dm_xe_packages p  
    on o.package_guid = p.guid  
 where o.object_type = 'event'  
   and p.name = 'SQLSatellite';  
```  
  
 하지만, [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 의 일부 추가적인 확장 이벤트는 R 런타임을 시작하는 위성 프로세스, [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], BXLServer와 같은 외부 프로세스를 통해서만 실행됩니다. 이러한 이벤트를 캡처하는 방법에 대한 자세한 내용은 [Collecting Events from External Processes](#bkmk_externalevents)을(를) 참조하십시오.  
  
 확장 이벤트 사용에 대한 일반 정보는 [SQL Server Extended Events Sessions](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)을(를) 참조하십시오.  

  
##  <a name="bkmk_xeventtable"></a> 확장 이벤트 테이블  
  
|이벤트|설명|이후|  
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
|satellite_data_send_start|데이터 전송이 시작된 경우에 실행됩니다(첫 번째 데이터 청크를 보내기 직전에).||  
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
  
###  <a name="bkmk_externalevents"></a> Collecting Events from External Processes  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 은(는) SQL Server 프로세스 외부에서 실행되는 일부 서비스를 시작합니다. 외부 프로세스 관련 이벤트를 캡처하려면 이벤트 추적 구성 파일을 만들고 프로세스의 실행 파일과 동일한 디렉터리에 파일을 배치해야 합니다.  
  
-   **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
     실행 패드 관련 이벤트를 캡처하려면, SQL Server 인스턴스의 Binn 디렉터리에 *.config* 파일을 배치합니다.  기본 설치 시 디렉터리는 `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`입니다.  
  
-   **BXLServer**는 R 및 다른 외부 스크립트 언어를 사용하여 SQL 확장성을 지원하는 위성 프로세스입니다.  
  
     BXLServer 관련 이벤트를 캡처하려면, R 설치 디렉터리에 *.config* 파일을 배치합니다.  기본 설치 시 디렉터리는 `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`입니다.  
  
> [!IMPORTANT]
>   구성 파일은 “[name].xevents.xml” 형식을 사용하여 실행 파일과 같은 이름을 지정해야 합니다. 즉, 파일 이름을 다음과 같이 지정해야 합니다.  
>   
> - Launchpad.xevents.xml  
> - bxlserver.xevents.xml  
  
 구성 파일 자체의 형식은 다음과 같습니다.  
  
```  
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
  
 **참고:**  
  
-   추적을 구성하려면 *session name* 자리 표시자, 파일 이름(`[SessionName].xel`)의 자리 표시자, 캡처할 이벤트의 이름(예: `[XEvent Name 1]`, `[XEvent Name 1]`)을 편집합니다.  
  
-   사용할 수 있는 `event package` 태그의 수에는 제한이 없으며, name 특성이 올바르기만 하면 수집됩니다.  
  
### <a name="example-capturing-launchpad-events"></a>예: 실행 패드 이벤트 캡처  
 다음 예는 실행 패드 서비스 이벤트 추적에 대한 정의를 보여줍니다.  
  
```  
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
  
 **참고:**  
  
-   SQL Server 인스턴스의 Binn 디렉터리에 *.config* 파일을 배치합니다.  
  
-   파일의 이름을 *Launchpad.xevents.xml*로 지정해야 합니다.  
  
### <a name="example-capturing-bxlserver-events"></a>예: BXLServer 이벤트 캡처  
 다음 예는 BXLServer 실행 파일 이벤트 추적에 대한 정의를 보여줍니다.  
  
```  
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
  
 **참고:**  
  
-   BXLServer 실행 파일과 같은 디렉터리에 *.config* 파일을 배치합니다.  
  
-   파일의 이름을 *bxlserver.xevents.xml*로 지정해야 합니다.  
  
## <a name="see-also"></a>참고 항목
[R Services에 대한 사용자 지정 Management Studio 보고서](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [R 솔루션 관리 및 모니터링](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
  
  

