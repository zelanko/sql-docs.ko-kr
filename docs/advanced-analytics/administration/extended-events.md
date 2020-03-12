---
title: 확장 이벤트를 사용하여 스크립트 모니터링
description: 확장 이벤트를 사용하여 SQL Server Machine Learning Services, SQL Server 실행 패드, Python 또는 R 작업 외부 스크립트와 관련된 작업을 모니터링하고 문제를 해결하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/04/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cf0253788e19061fe54b8e2b0b8dfd3142856472
ms.sourcegitcommit: 85b26bc1abbd8d8e2795ab96532ac7a7e01a954f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78335735"
---
# <a name="monitor-python-and-r-scripts-with-extended-events-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에서 확장 이벤트를 사용하여 Python 및 R 스크립트 모니터링
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

확장 이벤트를 사용하여 SQL Server Machine Learning Services, SQL Server 실행 패드, Python 또는 R 작업 외부 스크립트와 관련된 작업을 모니터링하고 문제를 해결하는 방법에 대해 알아봅니다.

## <a name="extended-events-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services용 확장 이벤트

SQL Server Machine Learning Services와 관련된 이벤트 목록을 보려면 Azure Data Studio 또는 SQL Server Management Studio에서 다음 쿼리를 실행합니다.

```sql
SELECT o.name AS event_name, o.description
FROM sys.dm_xe_objects o
JOIN sys.dm_xe_packages p
ON o.package_guid = p.guid
WHERE o.object_type = 'event'
AND p.name = 'SQLSatellite';
```

확장 이벤트를 사용하는 방법에 대한 자세한 내용은 [확장 이벤트 도구](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)를 참조하세요.

## <a name="additional-events-specific-to-machine-learning-services"></a>Machine Learning Services 관련 추가 이벤트

추가 확장 이벤트는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], BXLServer와 같은 SQL Server Machine Learning Services와 관련되고 사용되는 구성 요소 및 Python 또는 R 런타임을 시작하는 위성 프로세스에 사용할 수 있습니다. 이러한 추가 확장 이벤트는 외부 프로세스에서 발생합니다. 따라서 외부 유틸리티를 사용하여 캡처해야 합니다.

이를 수행하는 방법에 대한 자세한 내용은 [외부 프로세스에서 이벤트 수집](#bkmk_externalevents) 섹션을 참조하세요.

<a name="bkmk_xeventtable"></a> 

## <a name="table-of-extended-events"></a>확장 이벤트 테이블

|행사|Description|메모|  
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
|satellite_data_send_start|데이터 전송이 시작될 때 발생합니다.| 첫 번째 데이터 청크가 전송되지 직전에 데이터 전송이 시작됩니다.|  
|satellite_error|SQL 위성 오류를 추적하는 데 사용됩니다.||  
|satellite_invalid_sized_message|메시지의 크기가 유효하지 않습니다.||  
|satellite_message_coalesced|네트워킹 계층의 메시지 결합을 추적하는 데 사용됩니다.||  
|satellite_message_ring_buffer_record|메시지 링 버퍼 레코드||  
|satellite_message_summary|메시징에 대한 요약 정보||  
|satellite_message_version_mismatch|메시지 버전 필드가 일치하지 않습니다.||  
|satellite_messaging|메시징 이벤트(바인딩, 바인딩 해제 등)을 추적하는 데 사용됩니다.||  
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

<a name="bkmk_externalevents"></a>

### <a name="collecting-events-from-external-processes"></a>외부 프로세스에서 이벤트 수집

SQL Server Machine Learning Services는 SQL Server 프로세스 외부에서 실행되는 일부 서비스를 시작합니다. 외부 프로세스 관련 이벤트를 캡처하려면 이벤트 추적 구성 파일을 만들고 프로세스의 실행 파일과 동일한 디렉터리에 파일을 배치해야 합니다.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!IMPORTANT]
> SQL Server 2019부터 격리 메커니즘이 변경되었습니다. 따라서 이벤트 추적 구성 파일이 저장되는 디렉터리에 적절한 권한을 부여해야 합니다. 이러한 권한을 설정하는 방법에 대한 자세한 내용은 [Windows의 SQL Server 2019: Machine Learning Services에 대한 격리 변경 내용의 파일 사용 권한 섹션](../install/sql-server-machine-learning-services-2019.md#file-permissions)을 참조하세요.
::: moniker-end

+ **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
    실행 패드 관련 이벤트를 캡처하려면 SQL Server 인스턴스의 Binn 디렉터리에 *.xml* 파일을 배치합니다. 기본 설치의 경우 다음과 같습니다.

    `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`입니다.  
  
+ **BXLServer**는 R 또는 Python과 같은 외부 스크립트 언어를 사용하여 SQL 확장성을 지원하는 위성 프로세스입니다. 각 외부 언어 인스턴스에 대해 별도의 BxlServer 인스턴스가 실행됩니다.
  
    BXLServer 관련 이벤트를 캡처하려면 R 또는 Python 설치 디렉터리에 *.xml* 파일을 배치합니다. 기본 설치의 경우 다음과 같습니다.
     
    **R:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`.  

    **Python:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\PYTHON_SERVICES\library\RevoScaleR\rxLibs\x64`.

구성 파일은 "[name].xevents.xml" 형식을 사용하여 실행 파일과 같은 이름을 지정해야 합니다. 즉, 파일 이름을 다음과 같이 지정해야 합니다.

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

+ 추적을 구성하려면 *세션 이름* 자리 표시자, 파일 이름(`[SessionName].xel`)의 자리 표시자, 캡처할 이벤트의 이름(예: `[XEvent Name 1]`, `[XEvent Name 1]`)을 편집합니다.  
+ 사용할 수 있는 이벤트 패키지 태그의 수에는 제한이 없으며, name 특성이 올바르기만 하면 수집됩니다.

### <a name="example-capturing-launchpad-events"></a>예제: 실행 패드 이벤트 캡처

다음 예제는 실행 패드 서비스 이벤트 추적에 대한 정의를 보여줍니다.

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

+ SQL Server 인스턴스의 Binn 디렉터리에 *.xml* 파일을 배치합니다.
+ 이 파일의 이름은 `Launchpad.xevents.xml`이어야 합니다.

### <a name="example-capturing-bxlserver-events"></a>예제: BXLServer 이벤트 캡처  

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

+ BXLServer 실행 파일과 동일한 디렉터리에 *.xml* 파일을 배치합니다.
+ 이 파일의 이름은 `bxlserver.xevents.xml`이어야 합니다.

## <a name="next-steps"></a>다음 단계

- [SQL Server Management Studio에서 사용자 지정 보고서를 사용하여 Python 및 R 스크립트 실행 모니터링](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md)
- [DMV(동적 관리 뷰)를 사용하여 SQL Server Machine Learning Services 모니터링](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)
