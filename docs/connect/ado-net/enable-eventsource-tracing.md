---
title: SqlClient에서 이벤트 추적 사용
description: 이벤트 수신기를 구현하여 SqlClient에서 이벤트 추적을 사용하도록 설정하는 방법과 이벤트 데이터에 액세스하는 방법을 설명합니다.
ms.date: 11/23/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: b45f6146f8b5e2f367281720b0fa1c3395d94256
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123955"
---
# <a name="enable-event-tracing-in-sqlclient"></a>SqlClient에서 이벤트 추적 사용

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

[ETW(Windows용 이벤트 추적)](/windows/win32/etw/event-tracing-portal)는 디버깅 및 테스트를 위해 드라이버에서 정의된 이벤트를 기록할 수 있는 효율적인 커널 수준 추적 기능입니다. SqlClient는 다양한 정보 수준에서 ETW 이벤트 캡처를 지원합니다. 클라이언트 애플리케이션은 이벤트 추적 캡처를 시작하기 위해 SqlClient의 EventSource 구현에서 이벤트를 수신 대기해야 합니다.

```
Microsoft.Data.SqlClient.EventSource
```

현재 구현에서는 다음과 같은 이벤트 키워드를 지원합니다.

| 키워드 이름 | 값 | Description |
| ------------ | ----- | ----------- |
| ExecutionTrace | 1 | 명령 실행 전후에 시작/중지 이벤트를 캡처하도록 설정합니다. |
| 추적 | 2 | 기본적인 애플리케이션 흐름 추적 이벤트를 캡처하도록 설정합니다. |
| 범위 | 4 | 진입 및 종료 이벤트를 캡처하도록 설정합니다. |
| NotificationTrace | 8 | `SqlNotification` 추적 이벤트를 캡처하도록 설정합니다. |
| NotificationScope | 16 | `SqlNotification` 범위 진입 및 종료 이벤트를 캡처하도록 설정합니다. |
| PoolerTrace | 32 | 연결 풀링 흐름 추적 이벤트를 캡처하도록 설정합니다. |
| PoolerScope | 64 | 연결 풀링 범위 추적 이벤트를 캡처하도록 설정합니다. |
| AdvancedTrace | 128 | 고급 흐름 추적 이벤트를 캡처하도록 설정합니다. |
| AdvancedTraceBin  | 256 | 추가 정보를 사용하여 고급 흐름 추적 이벤트를 캡처하도록 설정합니다. |
| CorrelationTrace | 512 | 상관 관계 흐름 추적 이벤트를 캡처하도록 설정합니다. |
| StateDump | 1024 | `SqlConnection`의 전체 상태 덤프를 캡처하도록 설정합니다. |
| SNITrace | 2048 | 관리형 네트워킹 구현에서 흐름 추적 이벤트를 캡처하도록 설정합니다(.NET Core에서만 적용). |
| SNIScope | 4096 | 관리형 네트워킹 구현에서 범위 이벤트를 캡처하도록 설정합니다(.NET Core에서만 적용). |
|||

## <a name="example"></a>예제
다음 예에서는 **AdventureWorks** 샘플 데이터베이스에서 데이터 작업에 대해 이벤트 추적을 사용하도록 설정하고 콘솔 창에 이벤트를 표시합니다.

[!code-csharp [SqlClientEventSource#1](~/../sqlclient/doc/samples/SqlClientEventSource.cs#1)]

## <a name="event-tracing-support-in-native-sni"></a>네이티브 SNI에서 이벤트 추적 지원

**Microsoft.Data.SqlClient** v2.1.0은 **Microsoft.Data.SqlClient.SNI** 및 **Microsoft.Data.SqlClient.SNI.runtime** 에서 이벤트 추적 지원을 확장합니다. EventCommand를 `SqlClientEventSource`에 보내면 [Xperf](https://docs.microsoft.com/windows-hardware/test/wpt/) 및 [PerfView](https://github.com/microsoft/perfview) 도구를 사용하여 네이티브 SNI.dll의 이벤트를 수집할 수 있습니다. 유효한 EventCommand 값은 다음과 같습니다.

```cs
// Enables trace events:
EventSource.SendCommand(eventSource, (EventCommand)8192, null);

// Enables flow events:
EventSource.SendCommand(eventSource, (EventCommand)16384, null);

// Enables both trace and flow events:
EventSource.SendCommand(eventSource, (EventCommand)(8192 | 16384), null);
```

다음 예제에서는 애플리케이션이 .NET Framework를 대상으로 할 때 네이티브 SNI.dll에서 이벤트 추적을 활성화합니다. 

```cs
// Native SNI tracing example
// .NET Framework application
using System;
using System.Diagnostics.Tracing;
using Microsoft.Data.SqlClient;

public class SqlClientListener : EventListener
{
    protected override void OnEventSourceCreated(EventSource eventSource)
    {
        if (eventSource.Name.Equals("Microsoft.Data.SqlClient.EventSource"))
        {
            // Enables both trace and flow events
            EventSource.SendCommand(eventSource, (EventCommand)(8192 | 16384), null);
        }
    }
}

class Program
{
    static string connectionString = @"Data Source = localhost; Initial Catalog = AdventureWorks;Integrated Security=true;";

    static void Main(string[] args)
    {
        using (SqlClientListener listener = new SqlClientListener())
        using (SqlConnection connection = new SqlConnection(connectionString))
        {
            connection.Open();
        }        
    }
}
```

### <a name="use-xperf-to-collect-trace-log"></a>Xperf를 사용하여 추적 로그 수집

1. 다음 명령줄을 사용하여 추적을 시작합니다.

   ```
   xperf -start trace -f myTrace.etl -on *Microsoft.Data.SqlClient.EventSource
   ```
   
2. 네이티브 SNI 추적 예제를 실행하여 SQL Server에 연결합니다.

3. 다음 명령줄을 사용하여 추적을 중지합니다.

   ```
   xperf -stop trace
   ```
   
4. PerfView를 사용하여 1단계에서 지정한 myTrace.etl 파일을 엽니다. SNI 추적 로그는 `Microsoft.Data.SqlClient.EventSource/SNIScope` 및 `Microsoft.Data.SqlClient.EventSource/SNITrace` 이벤트 이름으로 찾을 수 있습니다. 

   ![PerfView를 사용하여 SNI 추적 파일보기](media/view-event-trace-native-sni.png)


### <a name="use-perfview-to-collect-trace-log"></a>PerfView를 사용하여 추적 로그 수집

1. PerfView를 시작하고 메뉴 표시 줄에서 `Collect > Collect`를 실행하세요.

2. 추적 파일 이름, 출력 경로 및 공급자 이름을 구성합니다.

   ![수집 전 Prefview 구성](media/collect-event-trace-native-sni.png)
   
3. 수집을 시작합니다.

4. 네이티브 SNI 추적 예제를 실행하여 SQL Server에 연결합니다.

5. PerfView에서 수집을 중지합니다. 2단계의 구성에 따라 PerfViewData.etl 파일을 생성하는 데 시간이 걸립니다.

6. PerfView에서 etl 파일을 엽니다. SNI 추적 로그는 `Microsoft.Data.SqlClient.EventSource/SNIScope` 및 `Microsoft.Data.SqlClient.EventSource/SNITrace` 이벤트 이름으로 찾을 수 있습니다. 


## <a name="external-resources"></a>외부 리소스  
자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|설명|  
|--------------|-----------------|  
|[EventSource 클래스](/dotnet/api/system.diagnostics.tracing.eventsource)|ETW 이벤트를 만드는 기능을 제공합니다.| 
|[EventListener 클래스](/dotnet/api/system.diagnostics.tracing.eventlistener)|이벤트 원본에서 이벤트를 사용하거나 사용하지 않도록 설정하는 메서드를 제공합니다.|
