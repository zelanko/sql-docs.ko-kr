---
title: Microsoft.Data.SqlClient 네임스페이스 소개
description: Microsoft. SqlClient 네임 스페이스의 소개 페이지입니다.
ms.date: 09/30/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 4f4034c557c13054dcfb6ed425ca996b0c5363f6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452385"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Microsoft.Data.SqlClient 네임스페이스 소개

![Download-DownArrow-Circled](../../ssdt/media/download.png)[ADO.NET 다운로드](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

이 페이지에서는 Microsoft. SqlClient 네임 스페이스가 기존 System.web 네임 스페이스를 통해 추가 기능을 제공 하는 방법을 설명 합니다.
  
## <a name="release-notes"></a>릴리스 정보
모든 릴리스 정보는 [GitHub 리포지토리에서](https://github.com/dotnet/SqlClient/tree/master/release-notes)사용할 수 있습니다.

## <a name="new-features"></a>새 기능

### <a name="new-features-over-net-framework-472-systemdatasqlclient"></a>.NET Framework 4.7.2에 대 한 새로운 기능. SqlClient

데이터 분류-CTP 2.0 이후 Azure SQL Database 및 Microsoft SQL Server 2019에서 사용할 수 있습니다.

UTF-8 지원-CTP 2.3 이후의 Microsoft SQL Server SQL Server 2019에서 사용할 수 있습니다.

### <a name="new-features-over-net-core-22-systemdatasqlclient"></a>.NET Core 2.2를 통한 새로운 기능-데이터 SqlClient

데이터 분류-CTP 2.0 이후 Azure SQL Database 및 Microsoft SQL Server 2019에서 사용할 수 있습니다.

UTF-8 지원-CTP 2.3 이후의 Microsoft SQL Server SQL Server 2019에서 사용할 수 있습니다.

Enclaves를 사용 하는 Always Encrypted Always Encrypted Microsoft SQL Server 2016 이상에서 사용할 수 있습니다. Enclave 지원은 Microsoft Sql Server 2019 CTP 2.0에서 도입 되었습니다.

인증-Active Directory 암호 인증 모드입니다.

### <a name="data-classification"></a>데이터 분류

데이터 분류는 기본 원본이 기능을 지원 하 고 데이터 민감도에 대 한 메타 데이터를 포함 하는 경우 SqlDataReader를 통해 검색 된 개체에 대 한 읽기 전용 데이터 민감도 및 분류 정보를 제공 하는 새로운 Api 집합을 제공 합니다 [ 분류](../../relational-databases/security/sql-data-discovery-and-classification.md).

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

UTF-8 지원을 적용 하려면 응용 프로그램 코드를 변경 하지 않아도 됩니다. 이러한 SqlClient 변경은 서버에서 u t f-8을 지원 하 고 기본 열 데이터 정렬이 u t f-8 인 경우 클라이언트와 서버 간의 통신을 간단히 최적화 합니다. [SQL Server 2019 미리 보기의 새로운 기능](../../sql-server/what-s-new-in-sql-server-ver15.md)에서 utf-8 섹션을 참조 하세요.

### <a name="always-encrypted-with-enclaves"></a>Enclaves를 사용 하 여 상시 암호화

일반적으로 .NET Framework **및 기본 제공 열 마스터 키 저장소 공급자** 에 대 한 system.object를 사용 하는 기존 설명서는 이제 .net Core와 함께 작동 해야 합니다.

 [.NET Framework 데이터 공급자와 Always Encrypted를 사용하여 개발](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted: 중요 한 데이터 보호 및 Windows 인증서 저장소에 암호화 키 저장](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>인증

_인증_ 연결 문자열 옵션을 사용 하 여 서로 다른 인증 모드를 지정할 수 있습니다. 자세한 내용은 [SqlAuthenticationMethod에 대 한 설명서](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2)를 참조 하세요.

> [!NOTE]
> Azure Key Vault 공급자와 같은 사용자 지정 키 저장소 공급자는 Microsoft. SqlClient를 지원 하도록 업데이트 해야 합니다. 마찬가지로 enclave 공급자도 Microsoft. SqlClient를 지원 하도록 업데이트 해야 합니다.
> Always Encrypted은 .NET Framework 및 .NET Core 대상에 대해서만 지원 됩니다. .NET Standard에 특정 암호화 종속성이 없기 때문에 .NET Standard에 대해 지원 되지 않습니다.
