---
title: Microsoft.Data.SqlClient 네임스페이스 소개
description: Microsoft.Data.SqlClient 네임스페이스의 소개 페이지입니다.
ms.date: 06/23/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 3a4f0611d3708aba9557deb81ab702f29e7a7462
ms.sourcegitcommit: 22f687e9e8b4f37b877b2d19c5090dade8fa26d0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85334587"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Microsoft.Data.SqlClient 네임스페이스 소개

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

## <a name="release-notes-for-microsoftdatasqlclient-20"></a>Microsoft.Data.SqlClient 2.0 릴리스 정보

릴리스 정보는 GitHub 리포지토리에서도 제공됩니다. [2.0 릴리스 정보](https://github.com/dotnet/SqlClient/tree/master/release-notes/2.0).

### <a name="breaking-changes"></a>주요 변경 내용

- Enclave 공급자 인터페이스 `SqlColumnEncryptionEnclaveProvider`의 액세스 한정자가 `public`에서 `internal`로 변경되었습니다.

- `SqlClientMetaDataCollectionNames` 클래스의 상수가 SQL Server 변경 내용을 반영하도록 업데이트되었습니다.

- 이제 드라이버는 대상 SQL Server에서 TLS 암호화를 적용할 때 서버 인증서 유효성 검사를 수행하며, 이 동작은 Azure 연결을 위한 기본값입니다.

- 이제 `SqlDataReader.GetSchemaTable()`이 `null` 대신 빈 `DataTable`을 반환합니다.

- 이제 드라이버가 SQL Server 동작과 일치하도록 10진 소수 자릿수 반올림을 수행합니다. 이전 버전과의 호환성을 위해 AppContext 스위치를 사용하여 이전의 잘림 동작을 사용하도록 설정할 수 있습니다.

- **Microsoft.Data.SqlClient**를 사용하는 .NET Framework 애플리케이션의 경우 이전에 `bin\x64` 및 `bin\x86` 폴더에 다운로드되던 SNI.dll 파일이 `bin` 디렉터리에 다운로드되며 파일 이름이 `Microsoft.Data.SqlClient.SNI.x64.dll` 및 ` Microsoft.Data.SqlClient.SNI.x86.dll`로 지정됩니다.

- 일관성을 위해 `SqlConnectionStringBuilder`에서 연결 문자열을 가져올 때 새 연결 문자열 속성 동의어가 이전 속성을 대체합니다. [자세히 알아보기](#new-connection-string-property-synonyms)

### <a name="new-features"></a>새로운 기능

#### <a name="dns-failure-resiliency"></a>DNS 오류 복원력

이제 드라이버는 이 기능을 지원하는 SQL Server 엔드포인트에 성공적으로 연결될 때마다 연결의 IP 주소를 캐시합니다. 연결 시도 중에 DNS 확인 오류가 발생하면 드라이버는 해당 서버의 캐시된 IP 주소(있는 경우)를 사용하여 연결을 설정하려고 시도합니다. 

#### <a name="eventsource-tracing"></a>EventSource 추적

이 릴리스에는 애플리케이션 디버깅을 위해 이벤트 추적 로그 캡처 지원이 도입되었습니다. 이러한 이벤트를 캡처하려면 클라이언트 애플리케이션은 SqlClient의 EventSource 구현에서 이벤트를 수신 대기해야 합니다.

```
Microsoft.Data.SqlClient.EventSource
```

자세한 내용은 [SqlClient에서 이벤트 추적을 사용](enable-eventsource-tracing.md)하는 방법을 확인합니다.

#### <a name="enabling-managed-networking-on-windows"></a>Windows에서 관리형 네트워킹 사용

새로운 AppContext 스위치 **“Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows”** 를 사용하면 테스트 및 디버깅을 위해 Windows에서 관리형 SNI 구현을 사용할 수 있습니다. 이 스위치는 Windows에서 .NET Core 2.1+ 프로젝트 및 .NET Standard 2.0+ 프로젝트에서 관리형 SNI를 사용하도록 드라이버의 동작을 전환함으로써 Microsoft.Data.SqlClient 라이브러리의 네이티브 라이브러리 종속성을 모두 제거합니다.

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows", true);
```

드라이버에서 사용할 수 있는 스위치의 전체 목록은 [SqlClient의 AppContext 스위치](appcontext-switches.md)를 참조하세요.

#### <a name="enabling-decimal-truncation-behavior"></a>소수 잘림 동작 사용 

10진 데이터 소수 자릿수가 SQL Server에서 수행하는 것처럼 기본적으로 드라이버에서 반올림됩니다. 이전 버전과의 호환성을 위해 AppContext 스위치 **“Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal”** 을 **true**로 설정할 수 있습니다.

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal", true);
```

#### <a name="new-connection-string-property-synonyms"></a>새 연결 문자열 속성 동의어

두 단어 이상이 포함된 속성에서 간격 혼동을 방지하기 위해 다음과 같은 기존 연결 문자열 속성의 새 동의어가 추가되었습니다. 이전 버전과의 호환성을 위해 이전 속성 이름이 계속 지원되지만, 이제 [SqlConnectionStringBuilder](https://docs.microsoft.com/dotnet/api/microsoft.data.sqlclient.sqlconnectionstringbuilder)에서 연결 문자열을 가져올 때 새 연결 문자열 속성이 포함됩니다.

|기존 연결 문자열 속성|새 동의어|
|-----------------------------------|-----------|
| 애플리케이션 의도 | 애플리케이션 의도 |
| ConnectRetryCount | 연결 다시 시도 횟수 |
| ConnectRetryInterval | 연결 다시 시도 간격 |
| PoolBlockingPeriod | 풀 차단 기간 |
| MultipleActiveResultSets | Multiple Active Result Set |
| MultiSubnetFailover | 다중 서브넷 장애 조치(failover) |
| TransparentNetworkIPResolution | 투명 네트워크 IP 확인 |
| TrustServerCertificate | 서버 인증서 신뢰 |

#### <a name="sqlbulkcopy-rowscopied-property"></a>SqlBulkCopy RowsCopied 속성

RowsCopied 속성은 진행 중인 대량 복사 작업에서 처리된 행의 수에 대한 읽기 전용 액세스를 제공합니다. 이 값은 대상 테이블에 추가된 마지막 행 수와 다를 수도 있습니다. 

#### <a name="connection-open-overrides"></a>연결 열기 재정의

SqlConnection.Open()의 기본 동작을 재정의하여 임시 오류에 의해 트리거되는 10초 지연 및 자동 연결 재시도를 사용하지 않도록 설정할 수 있습니다.

```csharp
using SqlConnection sqlConnection = new SqlConnection("Data Source=(local);Integrated Security=true;Initial Catalog=AdventureWorks;");
sqlConnection.Open(SqlConnectionOverrides.OpenWithoutRetry);
```

> [!NOTE]
> 이 재정의는 SqlConnection.Open()에만 적용할 수 있으며 SqlConnection.OpenAsync()에는 적용할 수 없습니다.

#### <a name="username-support-for-active-directory-interactive-mode"></a>Active Directory 대화형 모드를 위한 사용자 이름 지원

.NET Framework와 .NET Core에 Azure Active Directory 대화형 인증 모드를 사용할 때 연결 문자열에 사용자 이름을 지정할 수 있습니다.

**사용자 ID** 또는 **UID** 연결 문자열 속성을 사용하여 사용자 이름을 설정합니다.

```
"Server=<server name>; Database=<db name>; Authentication=Active Directory Interactive; User Id=<username>;"
```

#### <a name="order-hints-for-sqlbulkcopy"></a>SqlBulkCopy의 정렬 힌트

클러스터형 인덱스가 있는 테이블에 대한 대량 복사 작업의 성능을 향상하기 위해 정렬 힌트를 제공할 수 있습니다. 자세한 내용은 [대량 복사 작업](sql/bulk-copy-order-hints.md) 섹션을 참조하세요.

#### <a name="sni-dependency-changes"></a>SNI 종속성 변경 내용

Windows의 Microsoft.Data.SqlClient(.NET Core 및 .NET Standard)는 이제 **Microsoft.Data.SqlClient.SNI.runtime**에 의존합니다. 이로써 이전의 **runtime.native.System.Data.SqlClient.SNI** 종속성이 대체되었습니다. 이 새 종속성은 기존에 지원되는 플랫폼인 Windows의 ARM64, x64, x86과 함께 ARM 플랫폼에 대한 지원을 추가합니다.

## <a name="release-notes-for-microsoftdatasqlclient-110"></a>Microsoft.Data.SqlClient 1.1.0 릴리스 정보

릴리스 정보는 GitHub 리포지토리에서도 제공됩니다. [1.1 릴리스 정보](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1).

### <a name="new-features"></a>새로운 기능

#### <a name="always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted

Always Encrypted는 Microsoft SQL Server 2016부터 사용할 수 있습니다. 보안 enclave는 Microsoft SQL Server 2019부터 사용할 수 있습니다. Enclave 기능을 사용하려면 연결 문자열에 필수 증명 프로토콜 및 증명 URL이 포함되어야 합니다. 예를 들면 다음과 같습니다.

```
Attestation Protocol=HGS;Enclave Attestation Url=<attestation_url_for_HGS>
```

자세한 내용은 다음을 참조하세요.

- [Always Encrypted에 대한 SqlClient 지원](sql/sqlclient-support-always-encrypted.md)
- [자습서: 보안 enclave를 사용한 Always Encrypted를 이용하여 .NET 애플리케이션 개발](sql/tutorial-always-encrypted-enclaves-develop-net-apps.md)을 참조하세요.

## <a name="release-notes-for-microsoftdatasqlclient-10"></a>Microsoft.Data.SqlClient 1.0 릴리스 정보

Microsoft.Data.SqlClient 네임스페이스의 초기 릴리스는 기존 System.Data.SqlClient 네임스페이스에 대한 추가 기능을 제공합니다.
릴리스 정보는 GitHub 리포지토리에서도 제공됩니다. [1.0 릴리스 정보](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.0).

### <a name="new-features"></a>새로운 기능

#### <a name="new-features-over-net-framework-472-systemdatasqlclient"></a>.NET Framework 4.7.2에 대한 새로운 기능 System.Data.SqlClient

- **데이터 분류** - Azure SQL Database 및 Microsoft SQL Server 2019에서 사용할 수 있습니다.

- **UTF-8 지원** - Microsoft SQL Server 2019에서 사용할 수 있습니다.

#### <a name="new-features-over-net-core-22-systemdatasqlclient"></a>.NET Core 2.2에 대한 새로운 기능 System.Data.SqlClient

- **데이터 분류** - Azure SQL Database 및 Microsoft SQL Server 2019에서 사용할 수 있습니다.

- **UTF-8 지원** - Microsoft SQL Server 2019에서 사용할 수 있습니다.

- **인증** - Active Directory 암호 인증 모드입니다.

### <a name="data-classification"></a>데이터 분류

기본 원본이 기능을 지원하고 [데이터 민감도 및 분류](../../relational-databases/security/sql-data-discovery-and-classification.md)에 대한 메타데이터를 포함하는 경우 데이터 분류는 SqlDataReader를 통해 검색된 개체에 대하여 읽기 전용 데이터 민감도 및 분류 정보를 제공하는 새로운 API 집합을 제공합니다. [SqlClient의 데이터 검색 및 분류](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1)에서 애플리케이션 예제를 참조하세요.

```csharp
public class SqlDataReader
{
    public Microsoft.Data.SqlClient.DataClassification.SensitivityClassification SensitivityClassification
}

namespace Microsoft.Data.SqlClient.DataClassification
{
    public class ColumnSensitivity
    {
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.SensitivityProperty> SensitivityProperties
    }
    public class InformationType
    {
        public string Id
        public string Name
    }
    public class Label
    {
        public string Id
        public string Name
    }
    public class SensitivityClassification
    {
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.ColumnSensitivity> ColumnSensitivities
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.InformationType> InformationTypes
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.Label> Labels
    }
    public class SensitivityProperty
    {
        public Microsoft.Data.SqlClient.DataClassification.InformationType InformationType
        public Microsoft.Data.SqlClient.DataClassification.Label Label
    }
}
```

### <a name="utf-8-support"></a>UTF-8 지원

UTF-8 지원을 위해 애플리케이션 코드를 변경하지 않아도 됩니다. 이러한 SqlClient 변경에 따라, 서버에서 UTF-8을 지원하고 기본 열 데이터 정렬이 UTF-8인 경우 클라이언트-서버 통신이 최적화됩니다. [SQL Server 2019 미리 보기의 새로운 기능](../../sql-server/what-s-new-in-sql-server-ver15.md)에서 UTF-8 섹션을 참조하세요.

### <a name="always-encrypted-with-enclaves"></a>Enclave를 사용한 상시 암호화

일반적으로 .NET Framework **및 기본 제공 열 마스터 키 저장소 공급자**에 System.Data.SqlClient를 사용하는 기존 설명서는 이제 .NET Core에서도 작동합니다.

 [.NET Framework 데이터 공급자와 Always Encrypted를 사용하여 개발](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted: Windows 인증서 저장소에 중요한 데이터를 보호하고 암호화 키 저장](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>인증

_인증_ 연결 문자열 옵션을 사용하여 다양한 인증 모드를 지정할 수 있습니다. 자세한 내용은 [SqlAuthenticationMethod 설명서](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2)를 참조하세요.

> [!NOTE]
> Azure Key Vault 공급자와 같은 사용자 지정 키 저장소 공급자는 Microsoft.Data.SqlClient를 지원하도록 업데이트해야 합니다. 마찬가지로 enclave 공급자도 Microsoft.Data.SqlClient를 지원하도록 업데이트해야 합니다.
> Always Encrypted는 .NET Framework 및 .NET Core 대상에 대해서만 지원됩니다. .NET Standard는 특정 암호화 종속성이 없기 때문에 .NET Standard에 대해서는 지원되지 않습니다.
