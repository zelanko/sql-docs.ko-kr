---
title: SqlClient 문제 해결 가이드
description: 일반적으로 관찰되는 문제의 해결 방법을 제공하는 페이지입니다.
ms.date: 11/27/2020
dev_langs:
- csharp
- vb
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-jizho2
ms.openlocfilehash: 6cad6278eb6ac7b170ee108c1a3510db956ecb22
ms.sourcegitcommit: 0c0e4ab90655dde3e34ebc08487493e621f25dda
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96468092"
---
# <a name="sqlclient-troubleshooting-guide"></a>SqlClient 문제 해결 가이드

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

## <a name="exceptions-when-connecting-to-sql-server"></a>SQL Server에 연결할 때 발생하는 예외

다양한 이유로 연결 설정에 실패할 수 있습니다. 다음은 많은 문제를 분석하고 해결하는 지침으로 사용할 수 있는 몇 가지 문제 해결 팁입니다.

### <a name="unable-to-load-native-sni-server-name-indication-library"></a>네이티브 SNI(서버 이름 표시) 라이브러리를 로드할 수 없음

#### <a name="issues-in-net-framework-applications"></a>.NET Framework 애플리케이션의 문제

관찰된 StackTrace:

```log
TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.SNILoadHandle' threw an exception.
DllNotFoundException: Unable to load DLL 'Microsoft.Data.SqlClient.SNI.x64.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)
```

```log
TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.SNILoadHandle' threw an exception.
DllNotFoundException: Unable to load DLL 'Microsoft.Data.SqlClient.SNI.x86.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)
```

SNI는 Windows에서 실행될 때 다양한 네트워크 작업을 위해 SqlClient가 종속되는 C++ 네이티브 라이브러리입니다. MSBuild 프로젝트 SDK를 사용하여 빌드된 .NET Framework 애플리케이션에서 네이티브 DLL은 restore 명령을 사용하여 관리되지 않습니다. 따라서 필요한 "복사" 작업을 정의하는 "Microsoft.Data.SqlClient.SNI" NuGet 패키지에 ".targets" 파일이 포함됩니다.

"Microsoft.Data.SqlClient" 라이브러리에 직접 종속되는 경우 포함된 ".targets" 파일이 자동으로 참조됩니다. 전이적(간접) 참조가 수행되는 시나리오에서는 필요한 경우 "복사" 작업을 실행할 수 있도록 이 ".targets" 파일을 수동으로 참조해야 합니다.

**권장 해결 방법:** 애플리케이션의 “.csproj” 파일에서 ".targets" 파일이 참조되는지 확인하여 “복사” 작업이 실행되도록 합니다.

이러한 대상에는 Microsoft의 잘 알려지고 일반적으로 사용되는 대상만 포함됩니다. 외부 도구나 애플리케이션이 이진 파일을 복사할 사용자 지정 대상을 정의하는 경우, 도구 유지 관리자에서 새 대상을 정의하여 클라이언트 애플리케이션을 실행할 때 네이티브 SNI DLL이 Microsoft.Data.SqlClient.dll 바이너리와 함께 복사되고 사용 가능하도록 해야 합니다.

#### <a name="issues-in-net-core-applications"></a>.NET Core 애플리케이션 문제

관찰된 StackTrace:

```log
System.TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.TdsParser' threw an exception.
---> System.TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.SNILoadHandle' threw an exception.
---> System.DllNotFoundException: Unable to load shared library 'Microsoft.Data.SqlClient.SNI.dll' or one of its dependencies.
```

> [!NOTE]
> 이 오류는 Windows 애플리케이션에서만 발생할 수 있습니다. Unix 환경에서 발생하는 경우 Windows가 아닌 Unix 런타임을 적절하게 대상으로 지정하도록 애플리케이션을 빌드해야 합니다.

SNI는 Windows에서 실행될 때 다양한 네트워크 작업을 위해 SqlClient가 종속되는 C++ 네이티브 라이브러리입니다. Microsoft.Data.SqlClient는 .NET Core에서 이 라이브러리의 로드/언로드를 관리하지 않습니다.

**권장 해결 방법:** 네이티브 런타임 라이브러리가 .NET Core 프로세스에서 로드되는 파일 시스템에 대한 "실행" 권한이 부여되었는지 확인합니다. 이렇게 해도 문제가 해결되지 않으면 [dotnet/runtime](https://github.com/dotnet/runtime) 리포지토리에 문제를 제출하여 추가 지원을 받을 수 있습니다.

#### <a name="native-sni-pdb-not-found-errors"></a>네이티브 SNI(pdb 찾을 수 없음) 오류

관찰된 StackTrace:

```log
An assembly specified in the application dependencies manifest (sql2csv.deps.json) was not found:
  package: 'Microsoft.Data.SqlClient.SNI.runtime', version: '2.0.0'
  path: 'runtimes/win-x64/native/Microsoft.Data.SqlClient.SNI.pdb'
```

**권장 해결 방법:** 클라이언트 애플리케이션이 최소 [v2.1.0](https://www.nuget.org/packages/Microsoft.Data.SqlClient/2.1.0) 버전의 Microsoft.Data.SqlClient 패키지를 참조하는지 확인합니다. EF Core를 사용하는 경우 이 패키지 버전의 Microsoft.Data.SqlClient에 대한 참조를 직접 추가하여 종속성을 재정의하세요.

### <a name="hostname-resolution-errors"></a>호스트 이름 확인 오류

관찰된 StackTrace:

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible.
Verify that the instance name is correct and that SQL Server is configured to allow remote connections.
(provider: TCP Provider, error: 0 - No such host is known.)
```

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible.
Verify that the instance name is correct and that SQL Server is configured to allow remote connections.
(provider: TCP Provider, error: 35 - An internal exception was caught)
```

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible.
Verify that the instance name is correct and that SQL Server is configured to allow remote connections.
(provider: TCP Provider, error: 35 - An internal exception was caught)
 ---> System.Net.Internals.SocketExceptionFactory+ExtendedSocketException (00000005, 0xFFFDFFFF): Name does not resolve
```

#### <a name="possible-reasons"></a>가능한 이유

- SQL Server에서 TCP/명명된 파이프 프로토콜을 사용하도록 설정되어 있지 않음

  **권장 해결 방법:** SQL Server 구성 관리자 콘솔에서 SQL Server 인스턴스에 TCP/IP 파이프 프로토콜을 사용하도록 설정합니다.

- 호스트 이름 알 수 없음

  **권장 해결 방법:** 호스트 이름이 연결이 시작되는 클라이언트의 서버 IP 주소로 확인되는지 확인합니다.


### <a name="login-phase-errors"></a>로그인 단계 오류

관찰된 StackTrace:

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A connection was successfully established with the server, but then an error occurred during the pre-login handshake.
(provider: SSL Provider, error: 31 - Encryption(ssl/tls) handshake failed)
System.IO.EndOfStreamException: End of stream reached
```

```log
A connection was successfully established with the server, but then an error occurred during the login process.
(provider: SSL Provider, error: 0 - The target principal name is incorrect.)
```

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): Connection Timeout Expired. The timeout period elapsed during the post-login phase. The connection could have timed out while waiting for server to complete the login process and respond; Or it could have timed out while attempting to create multiple active connections.
The duration spent while attempting to connect to this server was - [Pre-Login] initialization=837; handshake=394; [Login] initialization=3; authentication=15; [Post-Login] complete=1027;
---> System.ComponentModel.Win32Exception (258): Unknown error 258
at Microsoft.Data.SqlClient.SqlInternalConnection.OnError(SqlException exception, Boolean breakConnection, Action1 wrapCloseInAction)
```

#### <a name="possible-reasons-and-solutions"></a>가능한 원인 및 해결 방법

- SQL Server는 TLS 1.2를 지원하지 않음

  일반적으로 이 오류는 TLS 1.2가 최소 지원 TLS 프로토콜인 docker 이미지 컨테이너, Unix 클라이언트 또는 Windows 클라이언트와 같은 클라이언트 환경에서 발생합니다.

  **권장 해결 방법:** 지원되는 버전의 SQL Server에<sup>1</sup> 최신 업데이트를 설치하고 서버에서 TLS 1.2 프로토콜을 사용하도록 설정했는지 확인합니다.

  _<sup>1</sup>_ 다양한 버전의 Microsoft.Data.SqlClient가 포함된 지원되는 SQL 서버 버전 목록은 [SqlClient 드라이버 지원 수명 주기](sqlclient-driver-support-lifecycle.md)를 참조하세요.

  **안전하지 않은 해결 방법:** docker 이미지/클라이언트 환경에서 TLS/SSL 설정을 구성하여 TLS 1.0에 연결합니다.

  ```docker
  MinProtocol = TLSv1
  CipherString = DEFAULT@SECLEVEL=1
  ```

  > [!NOTE]
  > Windows/Linux 환경에서 TLS 1.0 또는 TLS 1.1을 사용하여 Microsoft.Data.SqlClient v2.0 이상에 연결하는 경우 연결을 설정할 때 대상 SQL Server 및 클라이언트가 최소 TLS 버전 1.2을 협상할 수 없으면 보안 경고 메시지가 throw됩니다. `Security Warning: The negotiated <TLS1.0 | TLS1.1> is an insecure protocol and is supported for backward compatibility only. The recommended protocol version is TLS 1.2 and later.`

- SQL Server 적용 암호화

  대상 서버가 "암호화 강제 적용" 속성이 설정된 Azure SQL 인스턴스 또는 온-프레미스 SQL Server인 경우 암호화된 연결이 생성되며, 클라이언트는 이를 위해 서버와의 신뢰를 설정해야 합니다.

  **권장 해결 방법:** 이 문제를 해결하기 위해 다음과 같은 두 가지 옵션을 사용할 수 있습니다.

    1. 클라이언트 환경에 대상 SQL Server의 TLS/SSL 인증서를 설치합니다. 암호화가 필요한 경우 유효성 검사가 수행됩니다.
    2. 연결 문자열에서 "Trust Server Certificate = true" 속성을 설정합니다.

  **안전하지 않은 해결 방법:** SQL Server에서 "암호화 강제 적용" 설정을 사용하지 않도록 설정합니다.

- TLS/SSL 인증서가 SHA-256 이상으로 서명되지 않았습니다.

  **권장 해결 방법:** SHA-256 이상의 해시 알고리즘을 사용하여 해시가 서명된 새 서버 TLS/SSL 인증서를 생성합니다.

### <a name="connection-pool-exhaustion-errors"></a>연결 풀 고갈 오류

관찰된 StackTrace:

```log
System.InvalidOperationException: Timeout expired. The timeout period elapsed prior to obtaining a connection from the pool.
This may have occurred because all pooled connections were in use and max pool size was reached.
```

#### <a name="possible-reasons-and-solutions"></a>가능한 원인 및 해결 방법

특정 시간에 연결 풀이 활성 상태로 유지할 수 있는 것보다 많은 연결을 클라이언트 애플리케이션에서 열고 있습니다.

**권장 해결 방법:** "최대 풀 크기" 연결 속성을 더 큰 값으로 구성하고 사용하지 않는 연결을 제때 닫습니다.

## <a name="contact-support"></a>지원에 문의

이 가이드로 연결 문제가 해결되지 않는 경우 [dotnet/sqlclient](https://github.com/dotnet/SqlClient) 리포지토리에서 기존 문제를 확인하고 필요한 경우 새 문제를 열 수 있습니다.
