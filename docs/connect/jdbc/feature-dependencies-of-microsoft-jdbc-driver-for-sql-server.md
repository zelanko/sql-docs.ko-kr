---
title: SQL Server용 Microsoft JDBC Driver의 기능 종속성 | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c96a896e6d42172400b4a326abdc99824c6ac52
ms.sourcegitcommit: e2d65828faed6f4dfe625749a3b759af9caa7d91
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59670921"
---
# <a name="feature-dependencies-of-the-microsoft-jdbc-driver-for-sql-server"></a>SQL Server용 Microsoft JDBC Driver의 기능 종속성

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 문서에는 SQL Server용 Microsoft JDBC Driver가 종속된 라이브러리가 나열되어 있습니다. 프로젝트에는 다음과 같은 종속성이 있습니다.

## <a name="compile-time"></a>컴파일 시간

 - `com.microsoft.azure:azure-keyvault`: Always Encrypted Azure Key Vault 기능을 위한 Azure Key Vault 공급자(선택 사항)
 - `com.microsoft.azure:azure-keyvault-webkey`: Always Encrypted Azure Key Vault 기능을 위한 Azure Key Vault 공급자(선택 사항)
 - `com.microsoft.azure:adal4j` : Azure Active Directory 인증 기능 및 Azure Key Vault 기능을 위한 Java용 Azure Active Directory 라이브러리(선택 사항)
 - `com.microsoft.rest:client-runtime` : Azure Active Directory 인증 기능 및 Azure Key Vault 기능을 위한 Java용 Azure Active Directory 라이브러리(선택 사항)
- `org.osgi:org.osgi.core`: OSGi Framework 지원을 위한 OSGi Core 라이브러리
- `org.osgi:org.osgi.compendium`: OSGi Framework 지원을 위한 OSGi Compendium 라이브러리

## <a name="test-time"></a>테스트 시간

앞의 기능 중 하나가 필요한 특정 프로젝트에서는 해당 POM 파일에서 관련 종속성을 명시적으로 선언해야 합니다.

**예:** Azure Active Directory 인증 기능을 사용하는 경우프로젝트의 POM 파일에 `adal4j` 종속성을 다시 선언해야 합니다. 다음 코드 조각을 참조하세요.

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.2.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.3</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.5</version>
</dependency>
```

**예:** Azure Key Vault 기능을 사용하는 경우 프로젝트의 POM 파일에 `azure-keyvault` 종속성 및 `adal4j` 종속성을 다시 선언해야 합니다. 다음 코드 조각을 참조하세요.

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.2.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.3</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.5</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.2.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault-webkey</artifactId>
    <version>1.2.0</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>JDBC 드라이버 종속성 요구 사항

### <a name="working-with-the-azure-key-vault-provider"></a>Azure Key Vault 공급자 사용:

- JDBC Driver 버전 7.2.2 - 종속성 버전: Azure-keyvault(버전 1.2.0), Azure Keyvault Webkey(버전 1.2.0), Adal4j(1.6.3 버전), Client-Runtime-for-AutoRest(1.6.5) 및 해당 종속성([애플리케이션 예제](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- JDBC Driver 버전 7.0.0 - 종속성 버전: Azure-Keyvault(버전 1.0.0), Adal4j(버전 1.6.0) 및 해당 종속성([애플리케이션 예제](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- JDBC Driver 버전 6.4.0 - 종속성 버전: Azure-Keyvault(버전 1.0.0), Adal4j(버전 1.4.0) 및 해당 종속성([애플리케이션 예제](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC Driver 버전 6.2.2 - 종속성 버전: Azure-Keyvault(버전 1.0.0), Adal4j(버전 1.4.0) 및 해당 종속성([애플리케이션 예제](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- JDBC Driver 버전 6.0.0 - 종속성 버전: Azure-Keyvault(버전 0.9.7), Adal4j(버전 1.3.0) 및 해당 종속성([애플리케이션 예제](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> 6.2.2 및 6.4.0 드라이버 버전에서는 azure-keyvault-java 종속성 버전이 버전 1.0.0으로 업데이트되었습니다. 그러나 새 버전은 이전 버전(0.9.7)과 호환되지 않아 드라이버의 기존 구현이 중단됩니다. 드라이버의 새 구현을 사용하려면 API를 변경해야 하므로 Azure Key Vault 공급자를 사용하는 클라이언트 프로그램이 중단됩니다.
>
> 이 문제는 최신 드라이버 버전(7.0.0)에서 해결되었습니다. 인증 콜백 메커니즘을 사용한 제거된 생성자가 이전 버전과의 호환성을 위해 Azure Key Vault 공급자에 다시 추가되었습니다.

### <a name="working-with-azure-active-directory-authentication"></a>Azure Active Directory 인증 사용

- JDBC Driver 버전 7.2.2 - 종속성 버전: Adal4j(버전 1.6.3), Client-Runtime-for-AutoRest(1.6.5) 및 해당 종속성
- JDBC Driver 버전 7.0.0 - 종속성 버전: Adal4j(버전 1.6.0) 및 해당 종속성
- JDBC Driver 버전 6.4.0 - 종속성 버전: Adal4j(버전 1.4.0) 및 해당 종속성
- JDBC Driver 버전 6.2.2 - 종속성 버전: Adal4j(버전 1.4.0) 및 해당 종속성
- JDBC Driver 버전 6.0.0 - 종속성 버전: Adal4j(버전 1.3.0) 및 해당 종속성 이 버전의 드라이버에서는 Windows 운영 체제의 _ActiveDirectoryIntegrated_ 인증 모드만 사용하여 연결하고 sqljdbc_auth.dll 및 SQL Server용 Active Directory 인증 라이브러리(ADALSQL.DLL)를 사용하여 연결할 수 있습니다.

드라이버 버전 6.4.0부터는 애플리케이션에서 Windows 운영 체제의 ADALSQL.DLL을 사용하지 않아도 됩니다. ‘Windows가 아닌 운영 체제’의 경우 드라이버에서 ActiveDirectoryIntegrated 인증을 사용하려면 Kerberos 티켓이 필요합니다. Kerberos를 사용하여 Active Directory에 연결하는 방법에 대한 자세한 내용은 [Set Kerberos ticket on Windows, Linux, and Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)(Windows, Linux 및 Mac에서 Kerberos 티켓 설정)을 참조하세요.

‘Windows 운영 체제’의 경우 드라이버는 기본적으로 sqljdbc_auth.dll을 찾고 Kerberos 티켓 설정이나 Azure 라이브러리 종속성이 필요하지 않습니다. sqljdbc_auth.dll을 사용할 수 없으면 드라이버는 다른 운영 체제에서처럼 Active Directory에 인증하기 위해 Kerberos 티켓을 찾습니다.

이 기능을 사용하는 [애플리케이션 예제](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)를 다운로드할 수 있습니다.

## <a name="see-also"></a>관련 항목:

[JDBC Driver GitHub repository](https://github.com/microsoft/mssql-jdbc)(JDBC Driver GitHub 리포지토리)  
[JDBC 드라이버 API 참조](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
