---
title: SqlClient에서 이벤트 추적 사용
description: 이벤트 수신기를 구현하여 SqlClient에서 이벤트 추적을 사용하도록 설정하는 방법과 이벤트 데이터에 액세스하는 방법을 설명합니다.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 4eac1ab519549ccace092cfc175c735dd4537269
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725744"
---
# <a name="enabling-event-tracing-in-sqlclient"></a>SqlClient에서 이벤트 추적 사용

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

## <a name="external-resources"></a>외부 리소스  
자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|설명|  
|--------------|-----------------|  
|[EventSource 클래스](/dotnet/api/system.diagnostics.tracing.eventsource)|ETW 이벤트를 만드는 기능을 제공합니다.| 
|[EventListener 클래스](/dotnet/api/system.diagnostics.tracing.eventlistener)|이벤트 원본에서 이벤트를 사용하거나 사용하지 않도록 설정하는 메서드를 제공합니다.|