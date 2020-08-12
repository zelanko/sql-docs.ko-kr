---
title: SqlClient의 AppContext 스위치
description: SqlClient에서 제공되는 AppContext 스위치를 사용하는 방법을 설명합니다.
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
ms.openlocfilehash: 16d3ed6db478f12157333badf93682eb861c57f3
ms.sourcegitcommit: 8515bb2021cfbc7791318527b8554654203db4ad
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86091692"
---
# <a name="appcontext-switches-in-sqlclient"></a>SqlClient의 AppContext 스위치

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

AppContext 클래스를 통해 SqlClient는 이전 동작에 의존하는 호출자를 계속 지원하면서 새 기능을 제공할 수 있습니다. 사용자는 특정 AppContext 스위치를 설정하여 동작의 변경을 옵트아웃할 수 있습니다.

## <a name="enabling-decimal-truncation-behavior"></a>소수 잘림 동작 사용

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

Microsoft.Data.SqlClient 2.0부터는 10진 데이터가 SQL Server에서 수행하는 것처럼 기본적으로 반올림됩니다. 이전의 잘림 동작을 사용하도록 설정하려면 애플리케이션 시작 시 AppContext 스위치 **“Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal”** 을 `true`로 설정하면 됩니다.

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal", true);
```

## <a name="enabling-managed-networking-on-windows"></a>Windows에서 관리형 네트워킹 사용

[!INCLUDE [appliesto-xxxx-netcore-netst-md](../../includes/appliesto-xxxx-netcore-netst-md.md)]

Windows에서 SqlClient는 기본적으로 SNI 네트워크 인터페이스의 네이티브 구현을 사용합니다. 관리형 SNI 구현을 사용하려면 애플리케이션 시작 시 AppContext 스위치 **“Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows”** 를 `true`로 설정하면 됩니다.

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows", true);
```

이 스위치는 Windows의 .NET Core 2.1+ 프로젝트 및 .NET Standard 2.0+ 프로젝트에서 관리형 네트워킹 구현을 사용하도록 드라이버의 동작을 전환함으로써 Microsoft.Data.SqlClient 라이브러리의 네이티브 라이브러리 종속성을 모두 제거합니다. 테스트 및 디버깅을 위해서만 사용됩니다.

> [!NOTE]
> 네이티브 구현과 비교할 때 몇 가지 알려진 차이점이 있습니다. 예를 들어 관리형 구현은 비도메인 Windows 인증을 지원하지 않습니다.

## <a name="disabling-transparent-network-ip-resolution"></a>투명 네트워크 IP 확인 사용 안 함

[!INCLUDE [appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

TNIR(투명 네트워크 IP 확인)은 기존 MultiSubnetFailover 기능의 수정 버전입니다. TNIR은 호스트 이름의 첫 번째 확인된 IP가 응답하지 않고 호스트 이름과 연결된 여러 IP가 있는 경우 드라이버의 연결 시퀀스에 영향을 미칩니다. TNIR은 MultiSubnetFailover와 상호 작용하여 다음과 같은 세 가지 연결 시퀀스를 제공합니다.<br />
* 0: 하나의 IP가 시도된 후 모든 IP가 병렬로 실행됨
* 1: 모든 IP가 병렬로 시도됨
* 2: 모든 IP가 차례대로 하나씩 시도됨

|TransparentNetworkIPResolution|MultiSubnetFailover|동작|
|--------|--------|--------|
|True|True|1|
|참|거짓|0|
|False|True|1|
|False|False|2|

TransparentNetworkIPResolution은 기본적으로 사용하도록 설정되어 있습니다. MultiSubnetFailover은 기본적으로 사용하지 않도록 설정되어 있습니다. TNIR을 사용하지 않도록 설정하려면 애플리케이션 시작 시 AppContext 스위치 **“Switch.Microsoft.Data.SqlClient.DisableTNIRByDefaultInConnectionString”** 을 `true`로 설정하면 됩니다.

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.DisableTNIRByDefaultInConnectionString", true);
```

이러한 속성을 설정하는 방법에 대한 자세한 내용은 [SqlConnection.ConnectionString 속성](https://docs.microsoft.com/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring)을 참조하세요. 

## <a name="enable-a-minimum-timeout-during-login"></a>로그인 중 최소 시간 제한 사용

[!INCLUDE [appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

로그인 시도가 무기한 대기하지 않도록 하려면 애플리케이션 시작 시 AppContext 스위치 **Switch.Microsoft.Data.SqlClient.UseOneSecFloorInTimeoutCalculationDuringLogin**을 `true`로 설정하면 됩니다.

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.UseOneSecFloorInTimeoutCalculationDuringLogin", false);
```

## <a name="disable-blocking-behavior-of-readasync"></a>ReadAsync의 차단 동작 사용 안 함

[!INCLUDE [appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

기본적으로 ReadAsync는 동기적으로 실행되고 .NET Framework에서 호출 스레드를 차단합니다. 이 차단 동작을 사용하지 않도록 설정하려면 애플리케이션 시작 시 AppContext 스위치 **Switch.Microsoft.Data.SqlClient.MakeReadAsyncBlocking**을 `false`설정하면 됩니다.

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.MakeReadAsyncBlocking", false);
```

## <a name="see-also"></a>참고 항목

[AppContext 클래스](https://docs.microsoft.com/dotnet/api/system.appcontext?view=netcore-3.1)
