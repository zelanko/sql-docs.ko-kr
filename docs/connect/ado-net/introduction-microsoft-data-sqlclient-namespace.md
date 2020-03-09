---
title: Microsoft.Data.SqlClient 네임스페이스 소개
description: Microsoft.Data.SqlClient 네임스페이스의 소개 페이지입니다.
ms.date: 09/30/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: dbc76f1a2ee93faf642d923d3a543eee40d5348b
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78897125"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Microsoft.Data.SqlClient 네임스페이스 소개

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

## <a name="release-notes-for-microsoftdatasqlclient-110"></a>Microsoft.Data.SqlClient 1.1.0 릴리스 정보

릴리스 정보는 GitHub 리포지토리에서도 제공됩니다. [1.1 릴리스 정보](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1).

### <a name="new-features"></a>새로운 기능

#### <a name="always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted

Always Encrypted는 Microsoft SQL Server 2016부터 사용할 수 있습니다. 보안 enclave는 Microsoft SQL Server 2019부터 사용할 수 있습니다. Enclave 기능을 사용하려면 연결 문자열에 필수 증명 프로토콜 및 증명 URL이 포함되어야 합니다. 예제:

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

기본 원본이 기능을 지원하고 [데이터 민감도 및 분류](../../relational-databases/security/sql-data-discovery-and-classification.md)에 대한 메타데이터를 포함하는 경우 데이터 분류는 SqlDataReader를 통해 검색된 개체에 대하여 읽기 전용 데이터 민감도 및 분류 정보를 제공하는 새로운 API 집합을 제공합니다.

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

UTF-8 지원을 위해 애플리케이션 코드를 변경하지 않아도 됩니다. 이러한 SqlClient 변경은 서버에서 UTF-8을 지원하고 기본 열 데이터 정렬이 UTF-8인 경우 클라이언트와 서버 간의 통신을 간단히 최적화합니다. [SQL Server 2019 미리 보기의 새로운 기능](../../sql-server/what-s-new-in-sql-server-ver15.md)에서 UTF-8 섹션을 참조하세요.

### <a name="always-encrypted-with-enclaves"></a>Enclave를 사용한 상시 암호화

일반적으로 .NET Framework **및 기본 제공 열 마스터 키 저장소 공급자**에 System.Data.SqlClient를 사용하는 기존 설명서는 이제 .NET Core에서도 작동합니다.

 [.NET Framework 데이터 공급자와 Always Encrypted를 사용하여 개발](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted: Windows 인증서 저장소에 중요한 데이터를 보호하고 암호화 키 저장](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>인증

_인증_ 연결 문자열 옵션을 사용하여 다양한 인증 모드를 지정할 수 있습니다. 자세한 내용은 [SqlAuthenticationMethod 설명서](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2)를 참조하세요.

> [!NOTE]
> Azure Key Vault 공급자와 같은 사용자 지정 키 저장소 공급자는 Microsoft.Data.SqlClient를 지원하도록 업데이트해야 합니다. 마찬가지로 enclave 공급자도 Microsoft.Data.SqlClient를 지원하도록 업데이트해야 합니다.
> Always Encrypted는 .NET Framework 및 .NET Core 대상에 대해서만 지원됩니다. .NET Standard는 특정 암호화 종속성이 없기 때문에 .NET Standard에 대해서는 지원되지 않습니다.
